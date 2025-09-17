# Documentació, Sistemes de Control de Versions i d'Integració Contínua

## 1. Eines col·laboratives per a la generació de documentació
La documentació és essencial per garantir el manteniment, l’evolució i la transmissió del coneixement sobre una aplicació o projecte.

**Eines habituals:**
- Editors en línia col·laboratius com Google Docs, OnlyOffice, Etherpad.
- Sistemes de wikis com Confluence, MediaWiki o DokuWiki.
- Generadors de documentació estàtica com MkDocs o Docusaurus.

**Instal·lació i configuració:**
- Desplegar un servidor propi (Wiki, OnlyOffice, etc.) o utilitzar serveis al núvol.
- Configurar usuaris, permisos i rols d’edició.
- Establir estructures de carpetes, plantilles bàsiques i normes d’estil de redacció.

**Ús:**
- Redactar manuals tècnics, guies d’instal·lació i tutorials.
- Incorporar captures, diagrames i codis d’exemple.
- Gestionar versions i revisions dels documents.

---

## 2. Creació i utilització de plantilles
Les plantilles garanteixen coherència, estalvien temps i faciliten l’actualització de la documentació.

**Exemples de plantilles habituals:**
- Guia d’instal·lació de software.
- Document d’arquitectura tècnica.
- Manual d’usuari.
- Fitxa d’incidències o canvis (change log).

**Bones pràctiques:**
- Incloure camps obligatoris (data, autor, versió, revisió).
- Definir un estil visual coherent (títols, llistes, taules…).
- Emmagatzemar les plantilles en un repositori centralitzat.

---

## 3. Instal·lació, configuració i ús de sistemes de control de versions
Els sistemes de control de versions (VCS) permeten registrar els canvis realitzats als fitxers d’un projecte i coordinar el treball entre diversos desenvolupadors.

**Exemples populars:** Git (el més utilitzat), Subversion (SVN), Mercurial.

**Instal·lació:**
- Instal·lar el programari (`git`, `svn`, etc.) al sistema local.
- Configurar el nom i correu d’usuari.
- Crear un repositori local i/o clonar un repositori remot.

**Ús bàsic:**
- `add` → afegir canvis a l’índex
- `commit` → confirmar canvis al repositori
- `push` → enviar canvis al servidor remot
- `pull` → descarregar canvis del remot
- `branch` → crear o canviar de branca

**Integració amb plataformes remotes:** GitHub, GitLab, Bitbucket, etc.

---

### 3.1 Git
**Git** és un sistema de control de versions distribuït que guarda un historial complet de canvis en cada còpia del repositori.  
És extremadament ràpid, flexible i escalable.

**Conceptes clau:**
- **Repositori local i remot:** cada usuari té una còpia completa de l’historial.
- **Commits:** punts de control que registren els canvis realitzats.
- **Branches (branques):** línies paral·leles de desenvolupament.
- **Merge i rebase:** combinació de canvis entre branques.
- **Staging area (índex):** zona intermèdia on es preparen els canvis abans de confirmar-los.

**Flux de treball bàsic:**
1. `git clone <url>` → clona un repositori remot.
2. `git status` → comprova l’estat del repositori local.
3. `git add <fitxers>` → afegeix canvis a l’índex.
4. `git commit -m "Missatge"` → crea un nou commit.
5. `git push` → envia els commits al repositori remot.
6. `git pull` → baixa els canvis nous del remot i els integra.

**Bones pràctiques amb Git:**
- Fer commits freqüents i amb missatges clars i descriptius.
- Treballar en branques de funcionalitat i integrar-les a `main` o `develop` amb merge requests.
- Resoldre conflictes immediatament i amb cura.
- Utilitzar `.gitignore` per evitar pujar fitxers innecessaris.
- Revisar el codi amb *pull/merge requests* abans d’integrar canvis.

---

## 4. Operacions avançades
A mesura que el projecte creix, cal dominar operacions més avançades per gestionar el codi de forma eficient:

- Gestió de **branques** i estratègies de flux de treball (Git Flow, Trunk Based Development).
- **Merge** i **rebase** per combinar canvis entre branques.
- Resolució de **conflictes** en fitxers modificats per diverses persones.
- **Etiquetes (tags)** per marcar versions estables.
- **Hooks** per automatitzar accions (tests, format, desplegaments).

---

## 5. Seguretat dels sistemes de control de versions
La seguretat és clau per evitar pèrdua de dades i accessos no autoritzats.

**Bones pràctiques:**
- Limitar els permisos d’accés als repositoris (lectura/escriptura).
- Utilitzar connexions segures (SSH, HTTPS).
- Fer còpies de seguretat periòdiques dels repositoris.
- Revisar el codi abans de fer merges a branques principals.
- Evitar pujar informació sensible (claus API, contrasenyes, certificats…).

**Eines útils:**
- `.gitignore` per evitar pujar fitxers confidencials.
- Escanejadors de secrets i vulnerabilitats (TruffleHog, GitGuardian…).

---

## 6. Instal·lació, configuració i ús de sistemes d'integració contínua del codi
La integració contínua (CI) és el procés d’automatitzar la construcció, proves i validació del codi cada vegada que es fan canvis.

**Eines habituals:** Jenkins, GitLab CI/CD, GitHub Actions, Travis CI.

**Instal·lació i configuració:**
- Instal·lar el servidor de CI (o usar-lo com a servei al núvol).
- Configurar un fitxer de pipeline (`.gitlab-ci.yml`, `.github/workflows/...`).
- Definir etapes: compilació, tests, anàlisi de codi, desplegament automàtic.
- Configurar notificacions d’errors i resultats.

**Avantatges:**
- Detectar errors ràpidament.
- Reduir el temps de desplegament.
- Augmentar la qualitat i coherència del codi.

---

## 7. Monitorització contínua de les mètriques de qualitat de l'aplicació
Per garantir que l’aplicació manté un nivell de qualitat adequat, cal monitoritzar-ne aspectes clau de manera contínua.

**Tipus de mètriques:**
- Cobertura de tests automàtics.
- Nombre d’errors o vulnerabilitats detectades.
- Compliment d’estàndards de codi i estil.
- Rendiment (temps de resposta, ús de memòria/CPU).

**Eines comunes:**
- SonarQube, CodeClimate, Coveralls, Lighthouse.

**Bones pràctiques:**
- Integrar les mètriques dins del pipeline de CI.
- Definir objectius mínims (per exemple, 80% de cobertura de tests).
- Generar informes periòdics i revisar-los en reunions d’equip.
