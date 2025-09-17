# Administració de Servidors d'Aplicacions

## 1. Arquitectura i configuració bàsica del servidor d'aplicacions
Un servidor d’aplicacions és un programari que proporciona un entorn d’execució per a aplicacions web, gestionant la lògica de negoci, l’accés a dades i la comunicació entre clients i altres serveis.

**Característiques principals:**
- Gestió del cicle de vida de les aplicacions.
- Suport a diversos llenguatges i frameworks (Java, .NET, PHP...).
- Connexió amb bases de dades i serveis externs.
- Capacitat d’escalabilitat i alta disponibilitat.

**Configuració bàsica:**
- Definició de ports i protocols de comunicació (HTTP/HTTPS).
- Configuració de recursos (pools de connexions, memòria, llindars de CPU).
- Rutes de desplegament i directoris d’aplicacions.
- Fitxers de configuració (per exemple: `server.xml`, `domain.xml`).

---

## 2. Administrar aplicacions web
Tasques habituals d’administració d’aplicacions web en el servidor d’aplicacions:

- Desplegar (pujar i activar) aplicacions empaquetades (`.war`, `.ear`, `.jar`).
- Actualitzar versions existents sense perdre dades ni configuracions.
- Monitoritzar l’estat i rendiment de les aplicacions.
- Aturar, reiniciar o eliminar aplicacions de manera segura.
- Gestionar dependències i biblioteques compartides.

---

## 3. Autenticació d'usuaris i dominis de seguretat
Els servidors d’aplicacions ofereixen mecanismes per validar i autoritzar usuaris:

- Autenticació bàsica (usuari/contrasenya), digest i formularis.
- Integració amb serveis d’identitat (LDAP, Active Directory).
- Definició de dominis o “realms” de seguretat per agrupar usuaris i rols.
- Assignació de permisos i rols per a recursos específics.

---

## 4. Administració de sessions
La sessió representa l’estat de la interacció d’un usuari amb l’aplicació:

- Configurar el temps de vida d’una sessió.
- Almacenar dades de sessió en memòria o en bases de dades.
- Replicar sessions en entorns amb equilibradors de càrrega (cluster).
- Bona pràctica: minimitzar l’ús de sessió i evitar informació sensible.

---

## 5. Cooperació amb servidors web
El servidor d’aplicacions pot treballar conjuntament amb un servidor web que actua com a frontal:

- Configurar el servidor web com a proxy invers (per ex. Nginx o Apache).
- Redirigir les peticions dinàmiques al servidor d’aplicacions.
- Servir contingut estàtic des del servidor web per millorar el rendiment.
- Compartir certificats SSL i gestionar el xifrat de connexions.

---

## 6. Desplegament d'aplicacions en el servidor d'aplicacions
Fases del desplegament:

1. Preparar el paquet d’aplicació (`.war`, `.ear`, `.jar`).
2. Pujar-lo al servidor via consola d’administració, CLI o scripts.
3. Assignar els recursos necessaris (connexions a BD, variables d’entorn...).
4. Verificar que el desplegament ha sigut correcte i l’aplicació respon.

**Bones pràctiques:**
- Fer còpies de seguretat abans de desplegar.
- Utilitzar entorns de proves (staging) abans de producció.
- Automatitzar els desplegaments amb scripts o eines d’integració contínua.

---

## 7. Seguretat en el servidor d'aplicacions
Mesures essencials de seguretat:

- Actualitzar i aplicar pegats de seguretat del servidor.
- Configurar correctament rols, permisos i accés als recursos.
- Xifrar les comunicacions amb TLS/SSL.
- Auditar els logs d’accés i error regularment.
- Deshabilitar serveis o ports no utilitzats.
- Limitar els intents d’autenticació fallits.

---

## 8. Documentació
És fonamental documentar tot el procés d’instal·lació, configuració i administració:

- Versions de programari utilitzades.
- Configuracions aplicades i raons de les decisions.
- Procediments de desplegament i manteniment.
- Incidències trobades i com s’han resolt.
- Ubicació dels fitxers de configuració i logs.

---

## 9. Desplegament de servidors d'aplicacions mitjançant virtualització, núvol i contenidors
Hi ha diverses formes d’allotjar servidors d’aplicacions:

### Virtualització tradicional
- Crear màquines virtuals amb hipervisors (VMware, VirtualBox, Proxmox).
- Cada màquina té el seu propi sistema operatiu.

### Contenidors
- Crear imatges lleugeres amb Docker o Podman.
- Llançar contenidors aïllats amb el servidor d’aplicacions.
- Avantatges: rapidesa, escalabilitat i portabilitat.

### Núvol
- Plataformes com AWS, Azure o Google Cloud permeten desplegar servidors d’aplicacions gestionats.
- Integració amb balancejadors de càrrega, escalabilitat automàtica i alta disponibilitat.

**Bones pràctiques:**
- Automatitzar el desplegament amb fitxers de configuració (Dockerfile, docker-compose, Helm Charts...).
- Utilitzar plantilles i imatges base segures i actualitzades.
- Definir entorns separats (desenvolupament, proves, producció).
