# CV-lab1
# Server Virtual
Realizare lucrarii de laborator nr.1 unde ne familiarizam cu virtualizarea sistemelor de operare si configurarea unui server HTTP virtual.

Realizat de: Bozian Ana-Maria, I2301 
Data: 13.02.2025

# Scopul Lucrarii
Descarcarea distributivului Debian pentru servere cu arhitectura x64 si a sistemului de virtualizare QEMU.

# Realizarea lucrarii
1. Descarcam Debian de pe site-ul oficial. Dupa descarcare, il adaugam in directorul dvd cu numele debian.iso
2. Descarcam si instalam QEMU.
3. Deschidem consola si introducem comanda: qemu-img create -f qcow2 debian.qcow2 8G pentru a crea imaginea discului pentru masina virtuala de dimensiunea 8 GB si formagt qcow2.
4. Instalam debian so pe masina virtuala folosind comanda: qemu-system-x86_64 -hda debian.qcow2 -cdrom dvd/debian.iso -boot d -m 2G
5. Alegem optiunea de Install si citim cu atentie urmatorii pasi pentru finisarea instalarii. Folosim urmatorii parametrii:
nume calculator: debian;
nume domeniu: debian.localhost;
nume utilizator: user;
parola utilizator: password.
![photo_5285496809155849133_y](https://github.com/user-attachments/assets/eb885f58-3569-4e43-b059-338e2b9eecb4)
![photo_5285496809155849116_y](https://github.com/user-attachments/assets/a8ade105-5077-4db9-8698-a60ce9db0779)
Aici selectam ultimele 2 optiuni.
![Screenshot 2025-02-09 184301](https://github.com/user-attachments/assets/f08629d7-780f-49aa-9dd7-e66cdddcbb3a)
7. dupa instalare, repornim masina virtuala folosind comanda:
qemu-system-x86_64 -hda debian.qcow2 -m 2G -smp 2 -device e1000,netdev=net0 -netdev user,id=net0,hostfwd=tcp::1080-:80,hostfwd=tcp::1022-:22
8. Instalam LAMP in masina virtuala. pentru a face asta folosim comanda su ca sa avem drepturi de superutilizator si dupa comenzile:
apt update -y
apt install -y apache2 php libapache2-mod-php php-mysql mariadb-server mariadb-client unzip
![Screenshot 2025-02-11 142311](https://github.com/user-attachments/assets/55f2c9d7-c635-4cbd-afbd-b54012f9a2b7)
Destinatia pachetelor instalate este in /etc pentru configurari. exemplu: /etc/apache2/, /etc/php/, /etc/mysql/. aceste locatii sunt standard in utilizeazarea managerul de pachete apt.
9. Descarcarea SGBD phpmyadmin si CMS drupal cu ajutorul la wget + link.
![Screenshot 2025-02-11 144229](https://github.com/user-attachments/assets/0e9589bf-a26b-47f3-a0b0-93824939d186)
10. dezarhivam fisierele descarcate follosind conditiile din lucrare.
11. Cream baza de date drupal. ![Screenshot 2025-02-13 112312](https://github.com/user-attachments/assets/e8e0a1ed-214b-4b69-8ca8-6f1df16b62d5)
12. pentru phpmyadmin si drupal creem fisiere de configurare unde sunt introduse date despre host-uri virtuale. si activam configuratia utilizand comenzile:
/usr/sbin/a2ensite 01-phpmyadmin
/usr/sbin/a2ensite 02-drupal
13. facem un reload la apache2 si dupa adaugam adesele IP in /etc/hosts.
![Screenshot 2025-02-13 131508](https://github.com/user-attachments/assets/4b86e601-ac84-401a-a3a7-99b111fc10d3)
![Screenshot 2025-02-13 131002](https://github.com/user-attachments/assets/796fb202-0f56-419e-aac4-c0766aabb6c8)

# Pornire si testare
1. uname -a va afisa:
![Screenshot 2025-02-13 122604](https://github.com/user-attachments/assets/cc266809-96ad-4936-a1e0-357ee1b8d314)
2. apache2 se poate reporni folosind comanda: systemctl restart apache2
3. Verificam disponibilitatea site-urilor ![Screenshot 2025-02-13 124441](https://github.com/user-attachments/assets/21b29924-efbd-4a23-b10b-2c36f35f1965)
![Screenshot 2025-02-13 124428](https://github.com/user-attachments/assets/2396ad19-6029-4138-b6ca-9b7fc2afa3a4)

# Raspuns la intrebari
1. pentru a descarca un fisier cu wget se poate adauga in consola comanda: wget + link URL
2. este important sa avem baze de date diferite pentru site-urile nostare, deoarece acest lucru afecteaza securitatea, performanta aplicatiei. atunci cand datele sunt separate, utilizatorii sunt izolate astfel datele nu vor fi impartite intru aplicatii si exista posibilitatea de a crea diferite permisiuni pentru utilizatori. cand vine vorba de performanta, bazele de date separate pot oferi un spatiu de lucru mai eficient pentru utilizatori.
3. pentru a schimba portul trebuie sa editam fisierul de configurare si sa modificam portul in 1234. dupa facem restart pentru a vedea modificarile.
4. avantajele virtualizarii sunt: consolidare buna a serverului, izolarea datelor si flexibilitate.
5. este necesara stabilirea orei sau a zonei de timp pe server pentru o sincronizare optima a datelor, sau stabilirea unor programe automate care se bazeaza pe timp.
6. so are dimensiunea de 2 G.
7. 

# Bibliografie
https://www.sitepoint.com/does-site-need-database/
https://stackoverflow.com/questions/45237991/how-to-change-mysql-mariadb-10-xx-default-port
https://barrazacarlos.com/advantages-and-disadvantages-of-virtualization/

# Toate drepturile imi apartin MIE, nu dati lui Denis.
