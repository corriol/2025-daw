# Implantació d'Arquitectures Web

## 1. Aspectes generals d'arquitectures web
Una arquitectura web és l’estructura que defineix com s’organitzen i interactuen els components d’una aplicació web. Estableix com el client (navegador) i el servidor intercanvien informació, i com es gestionen les dades i serveis.

- Components bàsics: client web, servidor web, servidor d’aplicacions, base de dades i xarxa de comunicacions.
- Objectius: millorar el rendiment, la seguretat, la mantenibilitat i l’escalabilitat de les aplicacions.
- Tipus de comunicació: peticions HTTP/HTTPS, serveis web REST o SOAP, i protocols de xarxa.

---

## 2. Escalabilitat, portabilitat i componentització
### Escalabilitat
Capacitat del sistema per suportar un augment de la càrrega de treball sense perdre rendiment.
- Escalabilitat horitzontal: afegir més màquines (servidors).
- Escalabilitat vertical: augmentar els recursos d’un servidor (CPU, RAM).

### Portabilitat
Facilitat per executar una aplicació en diferents entorns (sistemes operatius, maquinari, núvols).
- S’aconsegueix utilitzant tecnologies multiplataforma i contenidors.

### Componentització
Divisió de l’aplicació en mòduls independents i reutilitzables.
- Millora la mantenibilitat i permet el treball paral·lel de diversos equips.
- Ús de patrons de disseny com MVC, MVVM, microserveis, etc.

---

## 3. Arquitectures web: models
### Arquitectura de 2 capes
- Client i servidor comparteixen la lògica d’aplicació.
- El client fa peticions directes a la base de dades.
- Exemple: aplicacions antigues de client pesat.

### Arquitectura de 3 capes
- Presentació (client)
- Lògica de negoci (servidor d’aplicacions)
- Dades (servidor de base de dades)
- Millora l’escalabilitat i la seguretat.

### Arquitectures orientades a serveis (SOA) i microserveis
- Divisió en serveis independents que s’intercomuniquen.
- Cada servei pot estar desenvolupat i desplegat de forma autònoma.
- Faciliten la reutilització i l’escalabilitat.

---

## 4. Plataformes web lliures i propietàries
### Plataformes lliures
- Apache HTTP Server: servidor web molt utilitzat, altament configurable.
- Nginx: lleuger, alt rendiment, ideal per servir contingut estàtic i com a proxy invers.
- Tomcat: servidor d’aplicacions Java.
- WildFly: plataforma Java EE amb suport complet d’aplicacions empresarials.

### Plataformes propietàries
- Microsoft IIS: integrat amb Windows Server, fàcil de gestionar.
- Oracle WebLogic: plataforma empresarial Java.
- Adobe ColdFusion: per aplicacions web ràpides basades en CFML.

---

## 5. Servidors web i d'aplicacions
- Servidor web: processa peticions HTTP i serveix contingut estàtic (HTML, CSS, JS, imatges).
- Servidor d’aplicacions: executa lògica de negoci i genera contingut dinàmic (Java, .NET, PHP…).

### Instal·lació bàsica
- Escollir el servidor adequat (Apache, Nginx, IIS…).
- Instal·lar paquets i dependències.
- Configurar ports, arxius de configuració i permisos.
- Comprovar el funcionament amb una pàgina de prova.

---

## 6. Tecnologies de virtualització i contenidors
### Virtualització
- Utilitza un hipervisor per executar diverses màquines virtuals sobre un mateix host.
- Exemples: VMware, VirtualBox, Proxmox.
- Avantatges: aïllament complet, flexibilitat i seguretat.
- Inconvenients: més consum de recursos.

### Contenidors
- Comparteixen el mateix nucli del sistema operatiu.
- Lleugers i ràpids d’iniciar.
- Exemples: Docker, Podman, LXC.
- Avantatges: portabilitat i eficiència.
- Inconvenients: menys aïllament que les màquines virtuals.

---

## 7. Estructura i recursos d’una aplicació web
- Client (frontend): HTML, CSS, JavaScript, imatges, fitxers multimèdia.
- Servidor (backend): lògica de negoci, APIs, gestió de dades i seguretat.
- Base de dades: sistema gestor (SQL o NoSQL) i els esquemes de dades.
- Arxius de configuració: `.env`, `config.yml`, etc.
- Descriptor de desplegament: defineix com s’ha d’executar l’aplicació (`web.xml`, `application.yml`, `Dockerfile`, etc.).

---

## 8. Programari lliure vs. programari propietari
| Aspecte               | Programari lliure                  | Programari propietari           |
|------------------------|-----------------------------------|--------------------------------|
| Llicència               | Oberta (GPL, MIT, Apache...)       | Tancada                         |
| Cost                    | Normalment gratuït                 | Sol licència de pagament        |
| Accés al codi font      | Sí                                 | No                              |
| Suport tècnic            | Comunitari                         | Oficial de l’empresa            |
| Personalització         | Alta                                | Limitada                         |

**Criteris de selecció:** pressupost, necessitat de suport, grau de personalització i seguretat requerida.

---

## 9. Instal·lació de servidors web lliures i propietaris
### Fases comunes
1. Preparar el sistema operatiu i actualitzar els paquets.
2. Instal·lar el programari (via repositoris o instal·ladors oficials).
3. Configurar fitxers principals (`httpd.conf`, `nginx.conf`, `web.config`…).
4. Obrir i comprovar els ports necessaris al tallafoc.
5. Crear un lloc web de prova i comprovar que respon.

### Exemples
- Apache/Nginx en Ubuntu.
- IIS en Windows Server.

---

## 10. Documentació dels processos realitzats
- Redactar un manual amb:
  - Objectiu i entorn utilitzat.
  - Passos d’instal·lació i configuració amb comandes i captures.
  - Proves realitzades i resultats.
  - Problemes trobats i solucions aplicades.
- Utilitzar eines de control de versions (Git) per registrar els canvis i millores.
- Guardar la documentació en formats reutilitzables (`.md`, `.pdf`) i compartir-la amb l’equip.
