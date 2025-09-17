# Serveis de Xarxa Implicats en el Desplegament d'una Aplicació Web

## 1. Resolutors de noms i procés de resolució d'un nom de domini
Els resolutors de noms (DNS resolvers) són serveis que tradueixen noms de domini (com `www.exemple.com`) en adreces IP comprensibles per les màquines.

**Procés bàsic de resolució:**
1. L’usuari escriu un nom de domini en el navegador.
2. El client consulta el resolutor DNS configurat al sistema.
3. Si el resolutor no coneix la resposta, fa consultes recursives a:
   - Servidors arrel (root)
   - Servidors TLD (Top Level Domain, com `.com`, `.org`, `.es`)
   - Servidors autoritaris del domini
4. El resolutor retorna la IP corresponent al client i la guarda temporalment a la memòria cau (cache).

**Funcions clau del DNS en el desplegament web:**
- Permet que els usuaris accedisquen a l’aplicació web a través d’un nom fàcil de recordar.
- Gestiona l’assignació d’IPs públiques a noms de domini i subdominis.

---

## 2. Paràmetres de configuració i registres del servidor de noms afectats en el desplegament
Un **servidor de noms** manté els registres DNS d’un domini. Aquests registres són essencials per redirigir el trànsit cap al servidor on està desplegada l’aplicació web.

**Registres DNS més habituals:**
- `A`: associa un nom de domini a una adreça IPv4.
- `AAAA`: associa un nom a una adreça IPv6.
- `CNAME`: crea un àlies cap a un altre nom de domini.
- `MX`: indica els servidors de correu del domini.
- `TXT`: permet afegir informació addicional (validació SPF, DKIM…).
- `NS`: defineix els servidors de noms autoritaris del domini.

**Paràmetres importants:**
- TTL (Time To Live): quant de temps es guarda un registre a la cache.
- Serial i valors SOA (Start of Authority): identifiquen l’estat del domini.

**Bones pràctiques:**
- Configurar correctament els registres `A` o `CNAME` per apuntar al servidor web.
- Reduir el TTL temporalment durant canvis de DNS per accelerar la propagació.
- Validar la configuració amb eines com `dig`, `nslookup` o `host`.

---

## 3. Servei de directoris: característiques i funcionalitat
Un **servei de directoris** és una base de dades jeràrquica i centralitzada que emmagatzema informació sobre usuaris, equips, aplicacions i altres recursos d’una xarxa.

**Característiques principals:**
- Organització jeràrquica en forma d’arbre (unitats organitzatives, dominis…).
- Accés mitjançant protocols estàndard com LDAP.
- Permet gestionar i autenticar usuaris de manera centralitzada.
- Facilita l’aplicació de polítiques comunes a tots els usuaris.

**Exemples de serveis de directoris:**
- OpenLDAP (lliure)
- Microsoft Active Directory (propietari)
- 389 Directory Server

---

## 4. Fitxers bàsics de configuració
Els serveis de directoris utilitzen fitxers de configuració per establir el seu funcionament:

- Fitxers de configuració principal (`slapd.conf`, `ldap.conf`, `krb5.conf`…).
- Fitxers d’esquemes que defineixen els tipus d’objectes i atributs disponibles.
- Fitxers de dades inicials per importar usuaris, grups i unitats organitzatives.

**Aspectes clau a definir:**
- Port i interfícies d’escolta.
- Domini base (base DN) de la jerarquia.
- Mètodes d’autenticació acceptats.
- Logs i ubicació de la base de dades.

---

## 5. Autenticació d'usuaris en el servei de directoris
El servei de directoris s’utilitza sovint com a font central d’autenticació d’usuaris en aplicacions web:

- Les aplicacions consulten el servei de directoris (via LDAP) per verificar credencials.
- Cada usuari té una entrada (DN) amb els seus atributs: nom, correu, contrasenya, grups…
- Es poden definir **grups o rols** per controlar permisos dins de l’aplicació.
- L’autenticació es pot combinar amb protocols segurs (TLS/SSL) per evitar robatoris de credencials.

**Avantatges:**
- Centralització de la gestió d’usuaris.
- Coherència i seguretat en l’accés a recursos.
- Menor càrrega administrativa.

---

## 6. Adaptació de la configuració del servidor de directoris per al desplegament de l'aplicació
Quan es desplega una aplicació web que empra el servei de directoris per autenticar usuaris, cal adaptar-ne la configuració:

- Crear unitats organitzatives específiques per a l’aplicació.
- Donar d’alta els usuaris i grups necessaris.
- Configurar el **binding** (connexió) de l’aplicació al servidor de directoris amb un compte de servei.
- Establir permisos de lectura adequats per a les aplicacions (evitant exposar dades sensibles).
- Testar la connexió amb eines com `ldapsearch`.

---

## 7. Documentació
És fonamental documentar tota la infraestructura de noms i directoris utilitzada:

- Configuració actual dels registres DNS del domini i subdominis.
- Configuració del servidor de noms (fitxers `zone`, valors SOA…).
- Estructura del directori LDAP (unitats, grups, usuaris).
- Fitxers de configuració clau i la seua ubicació.
- Procediments d’alta i baixa d’usuaris i grups.
- Històric de canvis i incidències resoltes.

**Consell:** guardar la documentació en un repositori de control de versions (Git).

---

## 8. Desplegament de servidors de directoris mitjançant virtualització, núvol i contenidors
Segons els requisits del projecte, es pot escollir entre diferents formes de desplegar un servidor de directoris:

### Virtualització tradicional
- Crear màquines virtuals amb hipervisors com VMware, VirtualBox o Proxmox.
- Instal·lar-hi el servei de directoris i configurar-lo com si fos un servidor físic.
- Fer snapshots per poder recuperar ràpidament en cas d’error.

### Contenidors
- Crear imatges Docker amb OpenLDAP o altres serveis preconfigurats.
- Llançar contenidors per a proves, entorns temporals o microserveis.
- Ràpid de desplegar i fàcil d’automatitzar.

### Núvol
- Utilitzar serveis gestionats com AWS Directory Service, Azure AD Domain Services o Google Cloud Directory.
- Permeten integrar fàcilment aplicacions sense haver de mantenir infraestructura pròpia.
- Escalabilitat automàtica i alta disponibilitat.

**Bones pràctiques:**
- Utilitzar TLS per protegir les connexions LDAP.
- Mantenir còpies de seguretat de la base de dades del directori.
- Segregar entorns (desenvolupament, proves, producció) per evitar errors.

