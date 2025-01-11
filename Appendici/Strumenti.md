# Strumenti utili al test

## Testing Generale del Web

### Proxy Web

- [ZAP](https://www.zaproxy.org)
    - Il Zed Attack Proxy (ZAP) è uno strumento integrato di penetration testing facile da usare per trovare vulnerabilità nelle applicazioni web. È progettato per essere utilizzato da persone con una vasta gamma di esperienze di sicurezza ed è ideale per sviluppatori e tester funzionali che sono nuovi al penetration testing.
    - ZAP fornisce scanner automatici e una serie di strumenti che consentono di trovare vulnerabilità di sicurezza manualmente.
- [Burp Suite Community Edition](https://portswigger.net/burp/communitydownload)
    - Burp Suite è un proxy di intercettazione per il testing di sicurezza. Permette di intercettare e modificare tutto il traffico HTTP(S) in entrambe le direzioni, può lavorare con certificati TLS personalizzati e client non a conoscenza dei proxy.
- [Telerik Fiddler](https://www.telerik.com/fiddler)
    - Fiddler è un proxy web di intercettazione principalmente rivolto agli sviluppatori piuttosto che ai tester di penetrazione, ma fornisce comunque funzionalità utili. Si integra direttamente con le API HTTP di Windows, consentendo di intercettare il traffico di alcuni software che non permettono di impostare proxy personalizzati.

### Estensioni per Firefox

- [Firefox HTTP Header Live](https://addons.mozilla.org/en-US/firefox/addon/http-header-live)
    - Visualizza le intestazioni HTTP di una pagina durante la navigazione.
- [Firefox Multi-Account Containers](https://addons.mozilla.org/en-GB/firefox/addon/multi-account-containers/)
    - Crea più contenitori, ognuno con i propri cookie e sessioni isolati. Utile per testare il controllo degli accessi tra diversi utenti.
- [Firefox Tamper Data](https://addons.mozilla.org/en-US/firefox/addon/tamper-data-for-ff-quantum/)
    - Usa Tamper Data per visualizzare e modificare le intestazioni HTTP/HTTPS e i parametri POST.
- [Firefox Web Developer](https://addons.mozilla.org/en-US/firefox/addon/web-developer/)
    - L'estensione Web Developer aggiunge vari strumenti per sviluppatori web al browser.

### Estensioni per Chrome

- [Chrome Web Developer](https://chrome.google.com/webstore/detail/bfbameneiokkgbdmiekhjnmfkcnldhhm)
    - L'estensione Web Developer aggiunge un pulsante nella barra degli strumenti del browser con vari strumenti per sviluppatori web. Questa è la versione ufficiale dell'estensione Web Developer per Chrome.
- [HTTP Request Maker](https://chrome.google.com/webstore/detail/kajfghlhfkcocafkcjlajldicbikpgnp?hl=en-US)
    - Request Maker è uno strumento per il penetration testing. Con esso puoi facilmente catturare le richieste effettuate dalle pagine web, modificare l'URL, le intestazioni e i dati POST e, naturalmente, effettuare nuove richieste.
- [Cookie Editor](https://chrome.google.com/webstore/detail/fngmhnnpilhplaeedifhccceomclgfbg?hl=en-US)
    - Edit This Cookie è un gestore di cookie. Puoi aggiungere, eliminare, modificare, cercare, proteggere e bloccare i cookie.

### Testing per Vulnerabilità Specifiche

#### Testing per SQL Injection

- [sqlmap](http://sqlmap.org)

#### Testing TLS

- [OWASP O-Saft](https://owasp.org/www-project-o-saft/)
- [sslyze](https://github.com/nabla-c0d3/sslyze)
- [testssl.sh](https://github.com/drwetter/testssl.sh)
- [SSLScan](https://github.com/rbsec/sslscan)
- [SSLLabs](https://www.ssllabs.com/ssltest/)

#### Testing per Attacchi di Forza Bruta

##### Cracker di Hash

- [John the Ripper](https://github.com/openwall/john)
- [hashcat](https://hashcat.net/hashcat/)

##### Forza Bruta Remota

- [ZAP](https://www.zaproxy.org)
- [Patator](https://github.com/lanjelot/patator)
- [THC Hydra](https://github.com/vanhauser-thc/thc-hydra)
- [Burp Suite Community Edition (Intruder)](https://portswigger.net/burp/communitydownload)

#### Fuzzers

- [Ffuf](https://github.com/ffuf/ffuf)
- [Wfuzz](https://github.com/xmendez/wfuzz)
- [Jdam](https://gitlab.com/michenriksen/jdam)

#### Google Hacking

- [Google Hacking database](https://www.exploit-db.com/google-hacking-database/)

#### Slow HTTP

- [Slowloris](https://github.com/gkbrk/slowloris)
- [slowhttptest](https://github.com/shekyan/slowhttptest)

### Mirroring del Sito

- [wget](https://www.gnu.org/software/wget/)
- [wget per Windows](http://gnuwin32.sourceforge.net/packages/wget.htm)
- [curl](https://curl.haxx.se)

### Scoperta dei Contenuti

- [Gobuster](https://github.com/OJ/gobuster)

### Scoperta di Porte e Servizi

- [Nmap](https://nmap.org/)

## Scanner di Vulnerabilità

- [ZAP](https://www.zaproxy.org)
- [Nikto](https://cirt.net/Nikto2)
- [Nuclei](https://nuclei.projectdiscovery.io/)
- [SecOps Solution](https://secopsolution.com)

## Framework di Sfruttamento

- [Metasploit](https://github.com/rapid7/metasploit-framework)
- [BeEF](https://github.com/beefproject/beef/)

## Distribuzioni Linux

- [Kali](https://www.kali.org)
- [Parrot](https://www.parrotsec.org)
- [Samurai](https://github.com/SamuraiWTF/samuraiwtf)
- [Santoku](https://sourceforge.net/projects/santoku/)
- [BlackArch](https://blackarch.org/downloads.html)

## Analizzatori di Codice Sorgente

- [Spotbugs](https://spotbugs.github.io)
- [Find Security Bugs](https://find-sec-bugs.github.io)
- [phpcs-security-audit](https://github.com/squizlabs/PHP_CodeSniffer)
- [PMD](https://pmd.github.io)
- [Analizzatori .NET di Microsoft](https://docs.microsoft.com/en-us/visualstudio/code-quality/install-net-analyzers)
- [SonarQube Community Edition](https://www.sonarqube.org)

## Strumenti di Automazione del Browser

Gli strumenti di automazione del browser sono utilizzati per convalidare la funzionalità delle applicazioni web. Alcuni seguono un approccio scriptato e tipicamente utilizzano un framework di unit testing per costruire suite di test e casi di test. La maggior parte, se non tutti, possono essere adattati per eseguire test specifici di sicurezza oltre ai test funzionali.

### Strumenti Open Source

- [HtmlUnit](http://htmlunit.sourceforge.net)
    - Un framework basato su Java e JUnit che utilizza Apache HttpClient come trasporto.
    - Molto robusto e configurabile e viene utilizzato come motore per numerosi altri strumenti di testing.
- [Selenium](https://www.selenium.dev)
    - Un framework di testing basato su JavaScript, multipiattaforma e che fornisce un'interfaccia grafica per la creazione di test.


<br>


### OLTRE A QUESTI STRUMENTI ELENCATI NEL FILE DI OWASP CI SONO ALTRI STRUMENTI CHE CREDO ESSERE UTILI
---

<br>

##### [OWASP Benchmark Project](https://owasp.org/www-project-benchmark/)
È una suite di test progettata per valutare la velocità, la copertura e l'accuratezza degli strumenti e dei servizi automatizzati di rilevamento delle vulnerabilità del software. In poche parole è un tester che controlla la completezza di strumenti automatizzati di test.

<br>

##### [mod_headers di Apache](https://httpd.apache.org/docs/current/mod/mod_headers.html)
Inviando richieste ad un server si possono ottenere informazioni da esso scritte negli header di risposta:

1. **Tipo di contenuto**
   Indica il formato dei dati restituiti (es. `Content-Type: text/html` per HTML, `application/json` per JSON).

2. **Dimensione del contenuto**
   La dimensione del corpo della risposta, specificata con `Content-Length`.

3. **Codifica**
   Informazioni sulla codifica del contenuto, come `Content-Encoding` (es. gzip).

4. **Cache**
   Direttive relative alla cache, come `Cache-Control`, che indicano se e come la risposta può essere memorizzata.

5. **Autenticazione**
   Intestazioni relative alla sicurezza, come `WWW-Authenticate` e `Authorization`.

6. **Informazioni sul server**
   Dettagli sul software del server web, forniti con l'intestazione `Server`.

7. **Data e ora**
   Data e ora in cui la risposta è stata generata, tramite l'intestazione `Date`.

8. **Reindirizzamenti**
   Informazioni su eventuali reindirizzamenti tramite intestazioni come `Location`.

9. **Politiche di sicurezza**
   Intestazioni come `Content-Security-Policy` e `Strict-Transport-Security` che indicano politiche di sicurezza applicate.

Queste informazioni possono essere utilizzate per il debug, ma se viste da un attaccante possono essere dannose. [mod_headers di Apache](https://httpd.apache.org/docs/current/mod/mod_headers.html) fa si che si possano nascondere ad un intercettatore alcune di queste specifiche.


##### [OWASP Attack Surface Detector](https://github.com/secdec/attack-surface-detector-cli/releases) 
Permette di trovare tutti gli endpoint di un sito (anche non raggiungibili dagli spider). Sono disponibili come plugin di ZAP e Burp Suite. 
