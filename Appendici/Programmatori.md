# Buone pratiche che i programmatori dovrebbero seguire
*In questo file metterò le pratiche migliori che ci sono nel file OWASP, che i programmatori dovrebbero seguire. Non scriverò i perché, se una persona è interessata può guardare sul file esteso (metterò il nome del pararafo per ritrovarlo meglio).*

<br>

È dato per scontato in questo file che la parte **2 - Introduzione** e **3 - Il framework di testing di OWASP** del [file completo](http://10.10.10.2:8888/documents/owasp/-/blob/dev/README.md?ref_type=heads) sia già stata letta dato che dà informazioni di base su come approcciare la scrittura di un nuovo programma partendo dall'ideazione dell'architettura. 


## Cosa fare

### 4.1 - Raccolta di informazioni

#### 4.1.2 - Fingerprinting del server web e 4.1.3 - Esaminare i meta-file dei server web per la fuga di informazioni
* Fai attenzione alla compilazione del file 'robots.txt' in modo che i motori di ricerca sappiano cosa indicizzare o meno 

#### 4.1.5 - Esaminare il contenuto delle pagine web per verificare la presenza di perdite di informazioni
* Non scrivere dati sensibili come username o password o altri metadati nei commenti del codice sorgente

#### 4.1.8 - Framework di fingerprinting per applicazioni web
* Usare strumenti come [mod_headers di Apache](https://httpd.apache.org/docs/current/mod/mod_headers.html) per nascondere parti dell'header di risposta che potrebbero mostrare all'attccante come è costruito il tuo backend: è consigliato nascondere la voce `Server`, `X-Powered-By` e ualsiasi informazionee dettagliata dui messaggi di errore.

### 4.2 - Test sulla gestione della configurazione dell'implementazione

#### 4.2.2 - Test sulla configurazione della piattaforma di un'applicazione
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

#### 4.2.3 - Test sulle estensini di file che potrebbero contenere informazioni sensibili
* Controlla i file resi noti al pubblico in cerca di informazioni sensibili (come per esempio tutti i file di testo come `.docx pdf .zip`)

#### 4.2.6 - Test dei metodi HTTP
* Configura il server per consentire solo i metodi HTTP necessari (non lasciare per esempio PUT se non serve)

#### 4.2.7 - Controllare la funzionalità HTTP Strict transport Security 
* Utilizza sempre le connessioni HTTPS e non HTTP

#### 4.2.9 - Test per il Takeover di Sottodomini
* Assicurarsi di rimuovere DNS che puntano a risorse non più attive o necessarie
* Utilizzare servizi di monitoraggio che avvisano quando un dominio o un sottodominio scade o viene modificato

#### 4.2.11 - Testing for Content Security Policy
* Configura una forte content security policy che riduca la superficie di attacco dell'applicazione. Gli sviluppatori possono verificare la robustezza della content security policy utilizzando strumenti online come il [Google CSP Evaluator](https://csp-evaluator.withgoogle.com/).

#### 4.2.12 - Test path confusion
* Evitare di classificare/gestire la cache in base all'estensione del file (.html, .css, .js) o al percorso (/images/, /api/), bensì in base al contenuto: conviene sempre scrivere nell'header il "Content-Type" che indica il tipo di dati restituiti.
* Implementare una gestione degli errori `File not found` conforme all'RFC (Request for comment) e i reindirizzamenti.

### 4.3 - Test di gestione dell'identità

#### 4.3.4 - Test per l'enumerazione degli account
* Assicurarsi che i messaggi di errore per credenziali errate siano identici, indipendentemente dal fatto che il nome utente o la password sia errato. Ad esempio, un messaggio come "Credenziali non valide" è preferibile a "Nome utente non trovato" o "Password errata".
* Implementare un sistema di limitazione dei tentativi di accesso per prevenire attacchi di forza bruta. Dopo un numero definito di tentativi falliti, bloccare temporaneamente l’account o richiedere un CAPTCHA.
* Introduzione di un ritardo crescente tra i tentativi di accesso.
* Assicurarsi che i tempi di risposta siano simili, indipendentemente dalla validità delle credenziali fornite.

### 4.4 - Test di autenticazione

#### 4.4.3 - Test per il bypass dello schema di autenticazione
* Non implementare il controllo degli accessi solo sulla pagina di login dato che potrebbe essere bypassato con un proxy. Implementalo sempre in backend.
* Fai si che l'ID di sessione generato non sia prevedibile ma che invece sia il più casuale possibile con librerie di sicurezza o mischiando valori casuali e una variabile temporale secondo qualche formula.

#### 4.4.4 - Testare la vulnerabilità di 'Ricorda password'
* Controllare che le credenzali non vengano mai salvate nell'applicazione client ma solamente sul lato server e che queste vengano poi sostituite con un token di sessione. 
* Assicurarsi anche che la sessione sia gestita correttamente, che sia sicura e che il timeout sia impostato ad una durata adeguata.

#### 4.4.5 - Testare debolezze della cache del browser
* L'applicazione deve istruire bene la cache del browser a non memorizzare i dati sensibili dell'utente..
In una pagina che gestisce informazioni sensibili, istruisci la cache del browser così:

        Cache-Control: no-store, no-cache, must-revalidate
        Pragma: no-cache
        Expires: 0

#### 4.4.6 - Test sulla politica di 'Password non sicura'
* Imporre all'utente ad utilizzare un minimo numero di caratteri e che i caratteri non siano di almeno tre tipi (lettere, numeri e speciali) o implementare un sistema di autenticazione a due fattori (la prima è migliore in un ambiente aperto al pubblico)

#### 4.4.7 - Test pe le domande di sicurezza per il recupero password deboli
* In generale evitare di usare domande di sicurezza per il recuper o della password perché le risposte a molte di queste sono facilmente indovinabili, ma se proprio si vogliono usare impostale come 'Qual è il nome della strada in cui hai vissuto il tuo terzo anno di scuola elementare?' oppure 'Qual era il soprannome del tuo migliore amico d'infanzia?': cose non reperibili facilmente su internet.

#### 4.4.8 - Test delle funzionalità di cambio o ripristino password
* Utilizzare metodi di verifica a più fattori (MFA) per confermare l'identità dell'utente prima di procedere con il ripristino della password.
* Implementare rate limiting per prevenire attacchi di brute force o di enumerazione degli utenti. Ad esempio, limitare il numero di richieste di ripristino password da un singolo indirizzo IP in un determinato intervallo di tempo.

#### 4.4.9 - Testare che non ci siano canali di autenticazione più deboli di altri
* Controlla che non ci siano canali di autenticazioni più debli di altri.

### 4.5 - Test di autorizzazione

#### 4.5.1 - Testing dell'inclusione di file in directory incrociate
* Assicurati che il tuo server web abbia accesso solo alle directory e ai file necessari. Riduci i privilegi degli utenti del server.
* RICORDA DI FARE IL SANITIZE() O DI IMPLEMENTARE UNA WHITELIST DI INPUT ACCETTATI DALL'ESTERNO, NON USARLI COSÌ COME SONO INSERITI DALL'UTENTE FINALE: questo consiglio tornerà spessissimo nella guida ed è una delle cause principali di bercce nella sicurezza informatica.

#### 4.5.2 - Test per il bypassing dello schema di autorizzazione
* Applicare i principi di minimo privilegio sugli utenti, ruoli e risorse per garantire che non si verifichino accessi non autorizzati.

#### 4.5.3 - Test per l'escalation dei privilegi
* Definisci chiaramente i ruoli e i privilegi. Ogni azione deve essere associata a un controllo che verifichi se l'utente ha i diritti necessari.

#### 4.5.5, 4.5.6, 4.5.7
Se viene usato OAuth consiglio di leggere i 3 capitoli perché non capisco di cosa parlino.

### 4.6 - Test sulla gestione della sessione

#### 4.6.1 - Test per lo schema di gestione della sessione
* Assicurati che l'applicazione utilizzi sempre HTTPS. I cookie critici dovrebbero avere il flag Secure impostato, in modo che vengano trasmessi solo su connessioni sicure.
* Utilizza il flag `HttpOnly` per i cookie che non devono essere accessibili tramite JavaScript. Questo aiuta a prevenire attacchi di tipo Cross-Site Scripting (XSS).

        res.cookie('sessionId', 'abc123', { httpOnly: true });

* Definisci un periodo di scadenza ragionevole per i cookie persistenti. I cookie di sessione dovrebbero scadere al termine della sessione (es. chiusura del browser).
* Utilizza algoritmi crittografici robusti per generare ID di sessione. Assicurati che siano lunghi e casuali, evitando schemi prevedibili.
* Implementa controlli di validazione lato server per garantire che i dati contenuti nei cookie non possano essere facilmente manomessi. Ad esempio, utilizza firme digitali o hash per verificare l'integrità.
* Limita il numero di tentativi di accesso e implementa misure di rate limiting per proteggere gli ID di sessione da attacchi di forza bruta.
* Utilizza il flag SameSite per limitare l'invio dei cookie alle richieste di origine. Questo riduce il rischio di attacchi Cross-Site Request Forgery (CSRF).

#### 4.6.2 - Test per gli attributi dei cookies
* Assicurati di utilizzare gli attributi e i prefissi corretti per i cookies in base alle esigenze (al capitolo corrispondente c'è la lista di ognuno di essi con spiegazione sul loro funzionamento)

#### 4.6.3 - Test per la Session Fixation
* Assicurati di cambiare l'ID di sessione prima e dopo l'autenticazione o utilizza i prefissi _Host e _Secure

#### 4.6.4 - Test per variabili di sessione esposte
* Assicurati che nel passaggio dal backend al frontend i cookies siano crittografati in maniera corretta altrimenti un attaccnte con un proxy potrebbe facilmente impossessarsene.
* Per trasferire questo tipo di informazini sensibili utilizza sempre POST e mai GET

#### 4.6.5 - Test per il cross site forgery
* Generare un token univoco per ogni sessione utente e includerlo in ogni modulo o richiesta che modifica lo stato dell'applicazione. Questo token deve essere validato dal server al momento della ricezione della richiesta.
* Utilizzare il flag SameSite per i cookie, che limita l'invio dei cookie solo a richieste provenienti dallo stesso sito, riducendo la possibilità che vengano inviati in contesti cross-origin.

#### 4.6.6 - Test per le funzionalità di logout
* Controlla che il bottone di logout sia sempre visibile sullo schermo dell'utente

#### 4.6.7 - Test per il timeout della sessione
* Imposta un tempo di scadenza della sessione adeguato al tipo di utilizzo che deve esserne fatto: nè troppo lungo nè troppo breve e imposta un modo per il refresh del timer in modo che questo si avvii solamente in caso di inutilizzo della pagina (per non cacciare fuori dalla pagina un utente nel mezzo di un'operazione)

#### 4.6.8 - Test per il puzzling delle sessioni
* Le variabili di sessione dovrebbero essere utilizzate solo per un unico scopo.

#### 4.6.9 - Test per il session hijacking
* Utilizza l'attributo `Secure` anche quando utilizzo connessioni HTTPS
* HSTS completo dovrebbe essere attivato sul dominio apex (dominio principale senza alcun sottodominio) per prevenire questo attacco.

#### 4.6.10 - Test per i JSON web token
* Utilizza librerie sicure
* Assicurati che la firma sia valida e usi l'algoritmo previsto
* Usa una chiave HMAC robusta o una chiave privata unica per firmarli
* Assicurati che non ci siano informazioni sensibili esposte nel payload (o in caso, criptarle)

#### 4.6.11 - Test per le sessioni concorrenti
* Fai si che l'applicazione monitori e limiti il numero di sessioni attive per un singolo utente. Se il numero limite viene superato, devono invalidarsi le prime sessioni.
* Monitora gli indirizzi IP degli utenti che accedono ad un account  e segnala eventuli attività sospette, come accessi multipli da località diverse

### 4.7 - Test della valutazione degli input

#### 4.7.1 - Testare per il Cross Site Scripting Riflesso e 4.7.2 - Test per il cross site scripting persistente
* Sanifica l'input prima di inserirlo nelle variabili corrispondenti o nel database (anche tramite l'utilizzo di whitelist)
* Codificare l'output per garantire che i caratteri speciali vengano visualizzati come testo normale. Ad esempio, utilizzare `&lt;` per <, `&gt;` per > e così via, per prevenire l'inserimento di codice javascript all'interno del proprio codice.
* Abilitare l'intestazione X-XSS-Protection nel server per attivare i filtri XSS dei browser.

#### 4.7.3 - Testing per l'iniezione SQL e 4.7.4 - Testing per MySQL
* Utilizzare query parametrizzate. Invece di costruire le query SQL concatenando le stringhe, usa le query parametrizzate o le procedure memorizzate. Questo assicura che i dati dell'input vengano trattati come dati e non come codice SQL.
* Utilizzare ORM (Object-Relational Mapping): Framework ORM come Hibernate, Entity Framework, e Sequelize gestiscono automaticamente le query SQL in modo sicuro, riducendo il rischio di iniezioni.
* Sanitizza sempre l'
* Limita l'accesso al database

#### 4.7.5 - Test per iniezioni XML
* Configura il parser XML in modo da disabilitare le entità esterne
* Scegliere parser XML che offrono opzioni di sicurezza integrate (come `javax.xml.parsers.DocumentBuilderFactory` in Java)
* Validare i dati in ingresso per assicurarsi che siano conformi a uno schema definito (ad esempio, XSD). Questo può aiutare a identificare e rimuovere contenuti pericolosi.
* Se possibile, limitare l'accesso alle risorse di sistema e alle risorse di rete che il parser XML può utilizzare.

#### 4.7.6 - Test per l'iniezione di SSI (Server Side Includes) e 4.7.7 - Test per Xpath Injection e 4.7.8 - Test per le iniezioni IMAP/SMTP e 4.7.9 - Test per l'iiezione di codice e 4.7.10 - Test per l'iniezione di comandi di sistema e 4.7.11 - Test per l'iniezione di stringhe di formato e 4.7.12 - Test per le vulnerabilità incubate e 4.7.13 - Test per HTTP splitting e smuggling
* È fondamentale filtrare e sanificare tutti gli input dell'utente. Utilizzare librerie di sanitizzazione per rimuovere caratteri speciali che potrebbero essere usati per iniezioni.
* Proprio come con SQL, l'uso di dichiarazioni preparate (o parametrizzate) aiuta a separare i dati dall'istruzione. In XPath, questo può essere implementato attraverso l'uso di variabili o binding di parametri.
* Utilizza funzioni di formattazine sicure
* Utilizzare ORM (Object Relational Mapping)

#### 4.7.15 - Test per l'iniezione dell'intestazione Host
* Validazione dell'intestazione Host. Consentire solo gli host attesi e noti, rifiutando tutte le richieste che contengono un valore non valido.
* Configurare correttamente il server web per limitare l'elaborazione delle richieste agli host definiti nella configurazione del server stesso, disabilitando eventuali host virtuali non utilizzati.
* Non fidarsi mai delle intestazioni come `X-Forwarded-Host`, `X-Real-IP`, o simili senza una validazione appropriata, poiché possono essere facilmente manipolate da un attaccante. Se necessario utilizzare queste intestazioni, validarle in modo simile all'intestazione Host.
* Implementare correttamente le intestazioni di controllo della cache (ad esempio, Cache-Control, Pragma) per evitare che contenuti sensibili o potenzialmente malevoli vengano memorizzati e serviti da un proxy o CDN.
* Generare i link di reimpostazione della password utilizzando l’URL corretto del dominio dell'applicazione, invece di fare affidamento sull'intestazione Host. Includere l'URL di reimpostazione direttamente nel server, evitando di costruirlo basandosi su input dell'utente.


#### 4.7.16 - Test per l'iniezione di Template lato server
* Sanitizza l'input

#### 4.7.17 - Test per la falsificazione delle rchieste lato server
* Limita gli URL o i percorsi che l'applicazione può accettare. Utilizza whitelist per consentire solo richieste a servizi interni specifici. Assicurati che gli input seguano un formato atteso e specifico (ad esempio, URL validi) e scarta input sospetti.
* Implementa controlli per rifiutare richieste verso localhost, 127.0.0.1 e altre interfacce di rete interne. Limita le richieste a intervalli di indirizzi IP noti e considerati sicuri, come quelli delle reti private (RFC 1918).
* Se non necessario, disabilita le funzionalità che permettono al server di caricare contenuti da URL esterni. Configura un firewall per bloccare richieste sospette o non autorizzate a servizi interni.

L'SSRF è noto per essere uno degli attacchi più difficili da sconfiggere senza l'uso di liste di autorizzazione che richiedono specifici IP e URL. Per ulteriori informazioni sulla prevenzione dell'SSRF, leggi la `Server Side Request Forgery Prevention Cheatsheet`.

#### 4.7.18 - Test per assegnamenti di massa
* Utilizza le funzionalità integrate, fornite dai framework, per definire campi assegnabili e non assegnabili. Un approccio basato su campi consentiti (assegnabili), in cui vengono definiti esplicitamente solo le proprietà che dovrebbero essere aggiornate dall'utente, è preferibile. Un approccio architetturale per prevenire il problema è utilizzare il pattern Data Transfer Object (DTO) per evitare il binding diretto. Il DTO dovrebbe includere solo i campi che devono essere modificabili dall'utente.

### 4.8 - Test sulla gestione dell'errore
#### 4.8.1 - Test per la gestione errata dell'errore
* Fornire messaggi di errore generali agli utenti finali, evitando dettagli tecnici o informazioni sensibili che potrebbero essere sfruttate da un attaccante.
* Registrare dettagli degli errori in log sicuri per l’analisi da parte degli sviluppatori. È importante non includere dati sensibili nei log, ma mantenere informazioni utili per il debugging.

Per i rimedi consultare il [Proactive Controls C10](https://owasp.org/www-project-proactive-controls/v3/en/c10-errors-exceptions) e l'[Error Handling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html).

### 4.9 - Test per una crittografia debole
#### 4.9.1 - Test per una sicurezza inadeguata nel TLS (Transport Layer Security)
* Assicurarsi di non supportare SSLv2, SSLv3 e TLS 1.0, poiché sono vulnerabili. Utilizzare solo cifrari considerati sicuri e aggiornati, evitando quelli deprecati o vulnerabili come RC4 o 3DES.
* Configurare HSTS per forzare l'uso di HTTPS e prevenire attacchi di downgrade.

#### 4.9.2 - Testing per Padding Oracle
* Utilizzare modalità di cifratura che integrano l'autenticazione, come GCM (Galois/Counter Mode) o CCM (Counter with CBC-MAC). Queste modalità garantiscono che i dati siano sia crittografati che autenticati, riducendo il rischio di errori di padding.
* Implementare una gestione degli errori che fornisca risposte uniformi per tutti i tipi di errore, senza rivelare dettagli specifici sull'errore di padding. Ad esempio, restituire sempre un messaggio generico come "Errore di decrittazione" senza indicare se il problema è legato al padding o a un'altra causa.
* Utilizzare un codice di autenticazione del messaggio (HMAC) per garantire che i dati non siano stati manomessi. Prima di decrittare, verificare l'HMAC del messaggio per assicurarsi che sia autentico.

#### 4.9.3 - Test per informazioni sensibili inviate in canali non criptati
* Utilizza HTTPS per tutto il sito e reindirizza le richieste HTTP in HTTPS.

#### 4.9.4 - Test per crittografia debole
* Crittografia Simmetrica: Utilizzare AES (128 o 256 bit) con modalità sicure come GCM o CBC con un IV casuale e unico per ogni operazione.
* Crittografia Asimmetrica: Preferire ECC (Curve25519) per la crittografia asimmetrica. Se non è possibile, usare RSA con una lunghezza di chiave minima di 2048 bit e padding OAEP.
* Non utilizzare algoritmi di hashing o crittografia considerati obsoleti o vulnerabili come MD5, SHA1, DES, Blowfish, o RC4.
* Assicurarsi di non utilizzare la modalità ECB per gli algoritmi simmetrici.
* Utilizzare librerie sicure come java.security.SecureRandom per generare chiavi e IV, assicurandosi che siano sempre casuali e unici per ogni sessione di crittografia.
* Utilizzare metodi di hashing sicuri come PBKDF2, bcrypt o scrypt, con un numero di iterazioni superiore a 10.000.

### 4.10 - Test della logica aziendale
#### 4.10.1 - Introduzione alla logica aziendale e 4.10.2 - Test di validazione della logica aziendale e 4.10.3 - Testare l'abilità nel forgiare richieste e 4.10.7 - Test per l'elusione dei flussi di lavoro
* Assicurarsi di avere una buona logica nel programam e che io devo compiere degli step in fila: prima 1 poi 2 e poi 3 non sia possibile cambiare questa sequenza in alcun modo

#### 4.10.4 - Controlli di integrità dei test
* Assicurarsi che tutti gli endpoint siano protetti da controlli di accesso basati sui ruoli. Utilizzare framework di autenticazione robusti (ad es. OAuth, JWT) per gestire le sessioni utente.
* Verificare sempre le autorizzazioni lato server per ogni richiesta, indipendentemente dai controlli effettuati sul client.

#### 4.10.5 - Test per il timing dei processi
* Sviluppare applicazioni tenendo presente il tempo di elaborazione. Se gli attaccanti possono ottenere qualche tipo di vantaggio conoscendo i diversi tempi di elaborazione e risultati, aggiungere passaggi extra o elaborazione in modo che, indipendentemente dai risultati, vengano forniti nello stesso intervallo di tempo.
* L'applicazione/sistema deve avere meccanismi in atto per non consentire agli attaccanti di estendere le transazioni oltre un periodo di tempo "accettabile". Ciò può essere fatto annullando o reimpostando le transazioni dopo un determinato periodo di tempo.

#### 4.10.6 - Limiti del numero di volte che una funzione può essere utilizzata
* L'applicazione dovrebbe impostare controlli rigidi per prevenire l'abuso dei limiti. Ciò può essere realizzato impostando un coupon come non più valido a livello di database, impostando un limite di conteggio per utente a livello di backend o database, poiché tutti gli utenti devono essere identificati tramite una sessione, a seconda di ciò che è meglio per il requisito aziendale.

#### 4.10.8 - Caricamento di tipi di file inaspettati
* Le applicazioni dovrebbero essere sviluppate con meccanismi per accettare e manipolare solo file "accettabili" che le altre funzionalità dell'applicazione sono pronte a gestire e si aspettano. Alcuni esempi specifici includono: liste di rifiuto o di approvazione delle estensioni dei file, utilizzo di "Content-Type" dall'intestazione, o utilizzo di un riconoscitore di tipo file, il tutto per consentire solo tipi di file specificati nel sistema.

#### 4.10.9 - Test per l'upload di dati maligni
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

#### 4.10.10 - Test per le funzionalità di pagamento
* Evitare di inviare, memorizzare o elaborare i dettagli delle carte ovunque possibile
* Esaminare la documentazione del gateway di pagamento e utilizzare tutte le funzionalità di sicurezza disponibili
* Gestire tutte le informazioni relaive ai prezzi sul lato server
* Implementare una valida input validation e vincoli di logica di business (come controllare numeri o valori di articolo negativi).
* Assicurarsi che il flusso di pagamento dell'applicazione sia robusto e che i passaggi non possano essere eseguiti in modo non sequenziale.

### 4.11 - Test lato client
#### 4.11.1 - Test per il Cross Site basato su DOM 
* Assicurati di sanificare e validare tutti i dati in ingresso prima di utilizzarli nel DOM. Utilizza librerie di sanitizzazione per rimuovere caratteri speciali e potenzialmente pericolosi.
* Evita di usare document.write() per inserire contenuti nel DOM, poiché può facilmente portare a vulnerabilità XSS. Utilizza invece metodi più sicuri come element.innerHTML, element.textContent, o element.appendChild().
* Quando inserisci testo nel DOM, preferisci textContent a innerHTML, poiché il primo non esegue alcun codice HTML o script e quindi riduce il rischio di XSS.
* Imposta intestazioni di sicurezza come Content Security Policy (CSP) per limitare le origini da cui il contenuto può essere caricato e per vietare l'esecuzione di script non autorizzati.

#### 4.11.2 - Test per l'esecuzione di Javascript
* Utilizzare eval() per eseguire codice JavaScript dinamicamente è rischioso. È meglio evitare completamente il suo uso e trovare metodi alternativi per elaborare i dati.
* Assicurarsi che qualsiasi dato proveniente da location.hash o da qualsiasi altra fonte esterna sia correttamente validato e sanitizzato. Questo significa filtrare e rimuovere qualsiasi carattere o stringa potenzialmente pericolosa.
* Se si devono utilizzare dati JSON, si potrebbe considerare di usare JSON.parse() al posto di eval(), poiché JSON.parse() è più sicuro e non esegue codice arbitrario.

#### 4.11.4 - Test per il Redirect URL lato client
* Implementare una robusta validazione dell'input per garantire che gli URL forniti dall'utente siano sicuri e autorizzati. Ad esempio, è possibile utilizzare una lista bianca di domini consentiti a cui gli utenti possono essere reindirizzati. Se possibile, evitare di utilizzare input utente per generare reindirizzamenti. Utilizzare invece percorsi predefiniti o identificatori unici per le pagine di destinazione.
* Sanificare l'input dell'utente per rimuovere qualsiasi contenuto pericoloso. Utilizzare funzioni di escaping per codificare caratteri speciali e prevenire l'iniezione di JavaScript.

#### 4.11.5 - Test per le iniezioni CSS
* Sanitizzazione e validazione
* Evitare di utilizzare input degli utenti direttamente nei contesti CSS. Utilizzare classi CSS predefinite e assegnarle in base a input validati, piuttosto che inserire direttamente stili.
* Implementare una CSP rigorosa per limitare le origini delle risorse, riducendo la possibilità che codice malevolo venga eseguito nel contesto del browser.

#### 4.11.6 - Test per la manipolazione delle risorse client side
* Fare sanitizzazione e validazione dell'input
* Configurare correttamente le intestazioni CORS per consentire solo le richieste da domini specifici e attendibili. Evitare di utilizzare wildcard (*) per `Access-Control-Allow-Origin`, se non necessario.
* Non utilizzare direttamente location.hash per costruire URL o altre risorse. Invece, considerare l'uso di metodi di navigazione più sicuri o di un meccanismo di routing più controllato.

#### 4.11.7 - Test per il Cross Origin Resource Sharing (CORS)
* Non utilizzare `Access-Control-Allow-Origin: *` se la risposta contiene dati sensibili. Specificare esplicitamente i domini autorizzati.
*  Implementare una whitelist delle origini da cui è consentito l'accesso. Questo può essere fatto controllando se l'Origin della richiesta è in una lista predefinita di domini consentiti.
* Utilizzare `Access-Control-Allow-Methods` per specificare solo i metodi HTTP necessari (ad esempio, GET, POST) e limitare ulteriormente quelli consentiti.
* Utilizzare `Access-Control-Allow-Headers` per specificare solo le intestazioni che sono necessarie.

#### 4.11.8 - Test per il Cross Site Flashing
* Sempre convalidare e filtrare i dati ricevuti tramite FlashVars o URL per evitare l’inserimento di dati malevoli.
* Evitare di utilizzare variabili FlashVars non controllate. Se necessario, limitare le FlashVars a valori specifici o predeterminati.
* Quando si devono gestire URL, preferire l'uso di URL relativi anziché assoluti, per ridurre il rischio di reindirizzamento verso domini malevoli.
* Limitare l’uso di ExternalInterface.call, assicurandosi che solo funzioni sicure e necessarie siano esposte e che i parametri passati siano validati.
* Non utilizzare metodi come loadMovie(), getURL(), o loadVariables() con input non filtrati. Considerare alternative più sicure o implementare logiche di controllo.

#### 4.11.9 - Test per i clickjacking
* Utilizzare l'intestazione `X-FRAME-OPTIONS`: questa intestazione impedisce che la pagina venga caricata all'interno di un iframe su domini non autorizzati.
* Implementare una Content Security Policy che utilizzi la direttiva frame-ancestors per specificare quali domini possono incorporare la pagina. Tipo : `Content-Security-Policy: frame-ancestors 'self';`
* Se è necessario utilizzare iframe, l'attributo sandbox può limitare le azioni che il contenuto caricato può eseguire. Questo può ridurre il rischio di attacchi di clickjacking, specialmente se combinato con altre misure.

Per indicazioni sicure, leggere il [Clickjacking Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html).
Per laboratori interattivi guarda il [Port Swigger](https://portswigger.net/web-security/clickjacking). 

#### 4.11.10 - Test sulle WebSockets
* Implementare controlli rigorosi sull'intestazione Origin durante l'handshake WebSocket. Solo le origini autorizzate dovrebbero essere consentite a stabilire una connessione.
* Assicurarsi che tutte le comunicazioni WebSocket avvengano su wss:// per garantire la crittografia dei dati in transito. Ciò protegge le informazioni sensibili da attacchi di tipo "man-in-the-middle".
* Implementare meccanismi di autenticazione robusti prima di aprire una connessione WebSocket. Utilizzare token JWT o sessioni per garantire che solo gli utenti autorizzati possano accedere alle risorse. 

#### 4.11.11 - Testing Web Messaging
* Assicurarsi di controllare l'origine dei messaggi in modo specifico e preciso. Ad esempio, invece di utilizzare controlli basati su stringhe parziali o wildcard, controllare esattamente l'origin per evitare bypass: `if (e.origin === "https://trusted.domain.com") do smt...`
* Per prevenire attacchi XSS, evitare di usare `innerHTML`, che interpreta il codice HTML, e utilizzare `innerText` o `textContent`

#### 4.11.12 - Testare la memoria del browser
* Le applicazioni dovrebbero memorizzare i dati sensibili lato server e non lato client, in modo sicuro seguendo le migliori pratiche.

#### 4.11.13 - Test per l'inclusione di Cross Site Scripting
* Evitare di memorizzare informazioni sensibili in variabili globali JavaScript. Utilizzare scope più ristretti come funzioni o moduli.
* Sebbene non sia una soluzione definitiva, offuscare i dati può rendere più difficile per un attaccante capire e sfruttare i dati esposti. Utilizza tecniche di minificazione o librerie di offuscamento. (Per esempio chimare una variabile importante `a` invce che `secretKey`)
* Assicurarsi che gli endpoint che forniscono dati sensibili siano accessibili solo a utenti autenticati e autorizzati.

#### 4.11.14 - Test per il reverse tabnabbing
* Utilizzare `rel="noopener noreferrer"`: Assicurati di aggiungere questo attributo a tutti i link che aprono una nuova scheda con `target="_blank"`. Questo impedisce alla nuova pagina di accedere alla finestra originale tramite `window.opener`.
* Rimuovere `target="_blank"` quando non necessario

### 4.12 - API Testing
#### 4.12.3 - Testare GraphQL
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

