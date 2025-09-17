# Instal·lació i Administració de Servidors de Transferència d'Arxius

## 1. Configuració del servei de transferència d'arxius
Un servidor de transferència d’arxius permet enviar i rebre fitxers entre ordinadors a través d’una xarxa utilitzant protocols específics. És un element essencial per publicar contingut web, compartir fitxers amb usuaris o fer còpies de seguretat remotes.

**Protocols habituals:**
- **FTP (File Transfer Protocol):** protocol antic però encara molt utilitzat; no xifra dades per defecte.
- **FTPS (FTP Secure):** versió de FTP amb capa de xifrat SSL/TLS.
- **SFTP (SSH File Transfer Protocol):** utilitza el canal segur d’SSH; més segur i modern que FTP.

**Configuració bàsica:**
- Instal·lar el programari del servidor (ex: vsftpd, ProFTPD, FileZilla Server…).
- Definir el port de connexió (21 per FTP, 22 per SFTP).
- Establir el directori arrel o “home” per als usuaris.
- Activar i configurar el xifrat (TLS/SSL o SSH).
- Configurar els fitxers principals (`vsftpd.conf`, `proftpd.conf`…).

---

## 2. Permisos i quotes
La correcta gestió de permisos i quotes garanteix la seguretat i l’ús eficient dels recursos del servidor.

- Assignar permisos de **lectura (r)**, **escriptura (w)** i **execució (x)** segons cada usuari o grup.
- Utilitzar propietaris i grups de fitxers adequats per evitar accessos indeguts.
- Definir **quotes de disc** per limitar l’espai assignat a cada usuari, evitant saturacions.
- Bloquejar els usuaris dins del seu directori (xarxa tancada o “chroot jail”).
- Monitoritzar els logs per detectar intents d’accés no autoritzats o saturacions.

---

## 3. Tipus d'usuaris i accessos al servei
Els servidors FTP/SFTP poden treballar amb diferents tipus d’usuaris segons el nivell d’accés requerit:

- **Usuaris locals:** creats al sistema operatiu. Fan servir les credencials del sistema i poden tindre accés a més recursos.
- **Usuaris virtuals:** gestionats només pel servidor FTP. No existeixen com a usuaris del sistema. Es guarden en fitxers de base de dades o arxius de text.
- **Accés anònim:** permet connectar-se sense credencials. Normalment només ofereix accés de lectura a un directori públic.

**Bones pràctiques:**
- Evitar l’accés anònim tret que siga estrictament necessari.
- Donar només els permisos mínims imprescindibles a cada usuari.
- Emprar contrasenyes robustes i polítiques de caducitat de contrasenya.

---

## 4. Modes de connexió del client
El protocol FTP utilitza dos canals: un de **comandaments** i un altre de **dades**. Açò provoca dues formes de connexió:

- **Mode actiu:** el client envia el port on escoltarà i el servidor inicia la connexió de dades cap al client. Pot donar problemes amb tallafocs.
- **Mode passiu:** el servidor indica un port i el client inicia la connexió de dades. És el mode més utilitzat actualment per compatibilitat amb NAT i tallafocs.

**Consell:** configurar correctament el rang de ports passius i obrir-los al tallafocs del servidor.

---

## 5. Protocol segur de transferència d'arxius
El trànsit FTP tradicional no està xifrat, cosa que permetria interceptar credencials o fitxers. Per això cal utilitzar protocols segurs:

- **FTPS:** implementa TLS/SSL sobre FTP. Pot funcionar en mode explícit o implícit. Compatible amb clients FTP tradicionals.
- **SFTP:** funciona sobre SSH. És més senzill de configurar i més segur, ja que tot el canal està xifrat.
- **Avantatges dels protocols segurs:**
  - Protecció de les dades i les credencials.
  - Eviten atacs de tipus “man-in-the-middle”.
  - Autenticació robusta i possibilitat d’ús de claus públiques.

**Bones pràctiques:**
- Deshabilitar FTP sense xifrat.
- Obligar l’ús de FTPS o SFTP.
- Configurar certificats vàlids i actualitzats.

---

## 6. Utilització de comandes i d'eines gràfiques
### Eines en línia de comandes
- `ftp` (bàsic), `sftp` (segur), `lftp` (avançat), `scp` (transferència ràpida via SSH).
- Comandes bàsiques:
  - `ls` (llistar fitxers)
  - `cd` (canviar de directori)
  - `get` / `mget` (baixar fitxers)
  - `put` / `mput` (pujar fitxers)
  - `bye` (tancar connexió)

### Eines gràfiques
- Clients amb interfície gràfica com FileZilla, WinSCP o Cyberduck.
- Permeten arrossegar i deixar fitxers, gestionar permisos i emmagatzemar credencials.
- Útils per a usuaris no tècnics o per transferències puntuals.

---

## 7. Utilització del servei de transferència d'arxius en el procés de desplegament de l'aplicació web
El servei FTP/SFTP és molt habitual per pujar aplicacions web a un servidor de producció:

- Transferir els fitxers HTML, CSS, JS i altres recursos al servidor web.
- Actualitzar versions noves de l’aplicació sense interrompre el servei.
- Automatitzar la pujada amb scripts (bash, PowerShell) o eines de CI/CD.
- Ajustar permisos i propietaris dels fitxers després de cada desplegament.
- Fer còpies de seguretat prèvies abans de substituir fitxers antics.

**Avantatge:** facilita un desplegament ràpid i directe, sense necessitat de coneixements avançats de DevOps.

---

## 8. Documentació
És essencial mantindre un registre clar i actualitzat del servei:

- Llistat d’usuaris amb els seus permisos i directoris assignats.
- Configuració actual del servidor (ports, directoris, seguretat, quotes…).
- Fitxers de configuració i les seues ubicacions.
- Procediments de connexió i transferència per als usuaris finals.
- Historial d’incidències i solucions aplicades.
- Ubicació i rotació dels fitxers de log.

**Consell:** guardar la documentació en un repositori Git per controlar versions i canvis.

---

## 9. Desplegament de servidors de transferència d'arxius mitjançant virtualització, núvol i contenidors
Segons les necessitats, el servidor de transferència es pot desplegar en diferents entorns:

### Virtualització tradicional
- Crear màquines virtuals a hipervisors com VMware, VirtualBox o Proxmox.
- Instal·lar-hi el servidor FTP/SFTP i configurar-lo com si fos un servidor físic.
- Permet aïllar entorns i realitzar snapshots per recuperar l’estat ràpidament.

### Contenidors
- Crear imatges lleugeres amb Docker o Podman que incloguen el servidor FTP/SFTP configurat.
- Llançar contenidors per a cada entorn (proves, producció).
- Avantatges: rapidesa de desplegament, consum mínim de recursos, portabilitat.

### Núvol
- Utilitzar serveis gestionats de transferència d’arxius (AWS Transfer Family, Azure Blob amb SFTP…).
- No cal administrar infraestructura pròpia.
- Escalabilitat automàtica, alta disponibilitat i còpies de seguretat integrades.

**Bones pràctiques generals:**
- Mantindre els sistemes actualitzats i amb pegats de seguretat.
- Segregar els entorns (desenvolupament, proves, producció).
- Automatitzar la creació i configuració amb scripts d’infraestructura com a codi (Terraform, Ansible…).
