---
TOCTitle: 'Guida alla pianificazione dell''accesso protetto mediante smart card - Capitolo 4 - Utilizzo di smart card per la protezione degli account di accesso remoto'
Title: 'Guida alla pianificazione dell''accesso protetto mediante smart card - Capitolo 4 - Utilizzo di smart card per la protezione degli account di accesso remoto'
ms:assetid: '7ce4f10a-fb5d-42c4-ab77-e5cc8fd201d2'
ms:contentKeyID: 20200797
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Dd536197(v=TechNet.10)'
---

Guida alla pianificazione dell'accesso protetto mediante smart card
===================================================================

### Capitolo 4 - Utilizzo di smart card per la protezione degli account di accesso remoto

La maggior parte delle organizzazioni deve garantire accesso remoto alle risorse di rete mediante connessioni remote o VPN (Virtual Private Network). Le modifiche continue nelle modalità di lavoro delle aziende, ad esempio la necessità di fornire il supporto agli utenti remoti o ai rappresentanti commerciali sul campo, contribuisce ad accelerare ulteriormente questa tendenza. Sebbene l'accesso remoto offra numerosi vantaggi a un'organizzazione, un accesso esterno espone sempre la rete dell'azienda a potenziali rischi per la protezione. L'autenticazione basata su due fattori è un ulteriore requisito per le reti che supportano l'accesso remoto.

##### In questa pagina

[](#eeaa)[Protezione dell'accesso remoto con le smart card](#eeaa)
[](#edaa)[Problemi e requisiti](#edaa)
[](#ecaa)[Progettazione della soluzione](#ecaa)
[](#ebaa)[Riepilogo](#ebaa)

### Protezione dell'accesso remoto con le smart card

L'accesso remoto deve consentire a tutti i dipendenti autorizzati l'accesso alle risorse della rete Intranet di un'organizzazione. Per semplificare l'accesso remoto sulla rete VPN, è necessario aprire le porte dei firewall esterni. Questa maggiore accessibilità crea un passaggio che gli utenti malintenzionati potrebbero utilizzare per penetrare nella rete.

Nel capitolo 1, "Introduzione", viene sottolineato che il processo di autenticazione degli account mediante nomi utente e password fonda la protezione del controllo degli accessi sull'utilizzo delle password. Le password sono facilmente individuabili e le credenziali di un account compromesso che può effettuare l'accesso remoto a una rete aziendale potrebbero essere molto interessanti per le organizzazioni criminali.

Sebbene sia possibile configurare criteri di blocco delle password di dominio per gli account utente, tali criteri di blocco sono vulnerabili agli attacchi di tipo Denial of Service (DoS) e possono bloccare continuamente l'account dell'utente remoto. Anche se un attacco di questo tipo non compromette le informazioni sulla rete, è comunque motivo di frustrazione per l'utente bloccato.

Un sistema di autenticazione utente restrittivo che utilizza i certificati digitali incorporati in una smart card garantisce un approccio affidabile e flessibile per la protezione del connessioni di accesso remoto.

#### Requisiti del client

L'utilizzo delle smart card per controllare l'accesso remoto dipende dai componenti in esecuzione sul client remoto. È necessario conoscere bene le caratteristiche di questi componenti e, in particolare, di Connection Manager e Connection Manager Administration Kit (CMAK). Connection Manager centralizza e automatizza le operazioni per stabilire e gestire le connessioni di rete. Connection Manager supporta le seguenti aree principali per la configurazione dell'accesso mediante smart card:

-   EAP-TLS (Extensible Authentication Protocol - Transport Layer Security) per le connessioni VPN e di accesso remoto

-   I controlli di protezione a livello di applicazione per gestire automaticamente le configurazioni dei computer client

-   I controlli e le convalide per la protezione dei computer che fanno parte della procedura di accesso

Per ulteriori informazioni su Connection Manager e CMAK, consultare il sito Web di Connection Manager Administration Kit all'indirizzo <http://technet.microsoft.com/en-us/library/cc739464.aspx>.

##### Connection Manager per il client

Per implementare una soluzione di accesso remoto gestibile, è necessario creare e distribuire le impostazioni di Connection Manager su più client. Per distribuire Connection Manager su più client, è necessario creare i profili di Connection Manager.

I profili di Connection Manager sono pacchetti dialer client di Connection Manager personalizzati che è possibile creare con CMAK e distribuire sui computer client in un file eseguibile autoestraente. Per distribuire i profili è possibile utilizzare qualsiasi meccanismo di distribuzione software, ad esempio Criteri di gruppo, Microsoft® Systems Management Server 2003, CD o chiavi USB.

Il file eseguibile installa il profilo sul computer insieme ai numeri di telefono o agli indirizzi degli host appropriati per connettersi ai server di accesso remoto. Quando un utente avvia una connessione mediante il profilo di Connection Manager, questo controlla automaticamente la presenza di una smart card e richiede il PIN all'utente. Se l'utente fornisce il PIN corretto, Connection Manager stabilisce le connessioni remote e VPN appropriate e autentica le credenziali dell'utente.

Connection Manager semplifica inoltre il processo di connessione per l'utente. Limita ad esempio il numero di opzioni di configurazione che un utente può modificare e garantisce che le connessioni abbiano sempre esito positivo. Le organizzazioni possono personalizzare Connection Manager per definire:

-   **I numeri di telefono disponibili**. Elenco di numeri di telefono che l'utente ha a disposizione nella propria sede.

-   **Il contenuto personalizzato**. La connessione può includere grafica, icone, messaggi e contenuto della guida personalizzati.

-   **Le connessioni pre-tunnel**. Connessioni remote a Internet che avvengono automaticamente prima del tentativo di connessione VPN.

-   **Le azioni pre-connessione e post-connessione**. Esempi di azioni pre-connessione e post-connessione includono il ripristino del profilo del dialer e la configurazione di Windows Firewall per ignorare le eccezioni alle regole di filtro dei pacchetti.

##### Requisiti del sistema operativo

La soluzione di accesso remoto mediante smart card funziona solo con Microsoft Windows® XP Professional. Microsoft consiglia Windows XP Professional con SP2 o versioni successive. Nei computer client devono essere installati tutti gli aggiornamenti per la protezione.

#### Requisiti dei server

I requisiti dei server per l'accesso mediante smart card sono relativamente semplici. I server di accesso remoto devono eseguire Windows 2000 Server o versioni successive e devono supportare il protocollo EAP-TLS.

**Nota:** a differenza delle smart card destinate agli scenari di amministrazione, le smart card per l'accesso remoto non richiedono obbligatoriamente Microsoft Windows Server™ 2003, anche se si consiglia vivamente di aggiornare l'infrastruttura PKI a Windows Server 2003 con Service Pack 1 (SP1) o versioni successive.

##### Considerazioni sulle connessioni remote e VPN

La soluzione che utilizza le smart card per la protezione dell'accesso remoto supporta le connessioni remote ISDN (Integrated Services Digital Network) o PSTN (Public Switched Telephone Network), ma è possibile che gli utenti debbano aspettare a lungo per effettuare l'accesso.

Le connessioni remote che utilizzano le reti VPN aumentano il carico di lavoro del processore del server di accesso remoto. L'accesso protetto mediante smart card non aumenta notevolmente il carico di lavoro ma può allungare i tempi di accesso. I server di accesso remoto VPN con volumi elevati di connessioni in ingresso richiedono processori veloci, preferibilmente inseriti in una configurazione multiprocessore. Le organizzazioni che utilizzano le connessioni VPN protette con IPsec possono implementare schede di rete che gestiscono l'elaborazione della crittografia IPsec su un processore distinto sulla scheda di rete.

##### Supporto del protocollo EAP (Extensible Authentication Protocol)

EAP-TLS è un protocollo di autenticazione reciproca sviluppato per l'utilizzo con i metodi di autenticazione e i dispositivi di protezione quali smart card e token hardware. EAP-TLS supporta le connessioni PPP (Point-to-Point Protocol) e VPN e attiva lo scambio delle chiavi segrete condivise per MPPE (Microsoft Point-to-Point Encryption).

I vantaggi principali offerti dal protocollo EAP-TLS sono la resistenza agli attacchi a forza bruta e il supporto per l'autenticazione reciproca. Con l'autenticazione reciproca, sia il client che il server sono tenuti a dimostrare la propria identità. Se il client o il server non invia un certificato per la convalida dell'identità, la connessione viene interrotta.

Windows Server 2003 supporta EAP-TLS per le connessioni remote e VPN, il che consente l'utilizzo delle smart card per gli utenti remoti. Per ulteriori informazioni su EAP-TLS, consultare l'articolo su Extensible Authentication Protocol (in inglese) all'indirizzo <http://technet.microsoft.com/en-us/network/bb643147.aspx>

Per ulteriori informazioni sui requisiti dei certificati EAP, consultare l'articolo Certificare i requisiti quando si utilizza EAP-TLS o PEAP con EAP-TLS all'indirizzo <http://support.microsoft.com/default.aspx?scid=kb;en-us;814394>

#### Individuazione dei requisiti dei server di autenticazione

Gli utenti remoti che desiderano accedere a una rete devono presentare le credenziali a un servizio di autenticazione. Windows fornisce due servizi di autenticazione per gli utenti remoti:

-   Server IAS (Internet Authentication Services)

-   Servizio Active Directory

Se l'organizzazione decide di utilizzare il provider di autenticazione RADIUS (Remote Authentication Dial-In User Service), è necessario includere i server IAS nella propria configurazione. IAS è l'implementazione Microsoft di RADIUS e viene eseguito come servizio in Windows 2000 Server o versioni successive.

L'implementazione di IAS per l'autenticazione RADIUS mediante smart card offre alle organizzazioni numerosi vantaggi, fra i quali:

-   Autorizzazione e autenticazione centralizzata degli utenti

-   Meccanismi di gestione e accounting separati

-   Ampia gamma di opzioni di autorizzazione e autenticazione

Il server IAS gestisce il processo di autenticazione. IAS consegna la richiesta di autenticazione dell'utente e le informazioni del certificato di accesso ad Active Directory che, a sua volta, confronta il certificato di accesso con le informazioni dei certificati memorizzati per quell'utente remoto. Se le informazioni dei certificati corrispondono, Active Directory autentica l'utente.

Per ulteriori informazioni sulla progettazione di una soluzione che utilizza IAS, consultare la sezione "Progettazione della soluzione" più avanti in questo capitolo.

#### Distribuzione e registrazione delle smart card per l'accesso remoto

La distribuzione e la registrazione delle smart card per l'accesso remoto viene eseguita secondo un processo simile a quello utilizzato per la soluzione degli account amministratore, come descritto nel capitolo 3 "Utilizzo di smart card per la protezione degli account amministratore". Le differenze principali sono rappresentate dal numero maggiore di utenti e dall'eventualità che il processo avvenga in più Paesi/aree geografiche.

La verifica dell'identità dell'utente remoto ha un ruolo importante nel processo. Tuttavia, poiché gli utenti remoti non hanno gli stessi diritti degli amministratori, l'identificazione tramite la fotografia del passaporto o della patente di guida dovrebbe rivelarsi adeguata. Un manager che richiede l'accesso remoto deve fornire una giustificazione valida all'amministratore incaricato di concederlo.

Le stazioni di registrazione devono trovarsi in luoghi adeguati, ad esempio nell'ufficio del personale o nel reparto di protezione e gli utenti devono recarsi in tali sedi per ricevere le smart card. Se un utente non può recarsi in una stazione di registrazione, è possibile utilizzare gli strumenti di connessione remota per sbloccare e registrare l'utente e per attivare la smart card.

La procedura di registrazione richiede che un agente di registrazione generi la richiesta dei certificati per conto dell'utente e installi il certificato ottenuto sulla smart card. L'agente di registrazione invia la smart card bloccata all'utente utilizzando un metodo protetto. L'utente contatta poi il reparto help desk, dichiara la propria identità e sblocca le smart card, come descritto nella sezione relativa al server Web di attivazione del capitolo 2 "Tecnologie delle smart card".

#### Ulteriori considerazioni

L'introduzione della protezione dell'accesso remoto in un'organizzazione causa spesso un aumento del numero di utenti che desiderano utilizzare il servizio. Le organizzazioni devono esaminare l'infrastruttura di rete attuale e, se necessario, fornire risorse aggiuntive. Di seguito sono elencate le aree che è necessario valutare:

-   Elenchi di certificati revocati (CRL)

-   Disponibilità e larghezza di banda elevate

-   Distribuzione degli aggiornamenti software

##### Elenchi di certificati revocati (CRL)

L'implementazione dei certificati per gli utenti remoti comporta la modifica della modalità con cui i client possono individuare un elenco di certificati revocati (CRL) per controllare la validità di un certificato. Il CRL dell'URL (Uniform Resource Locator) per Windows Server 2003 rimanda a una posizione della rete Intranet, ad esempio URL=http://Certification\_Root\_Server\_DNS\_Name/CertEnroll/
Certification\_Authority\_Name.crl.

Per gli utenti remoti, questo URL deve rimandare a una posizione accessibile da Internet. Questo requisito riguarda tutti i certificati emessi e include gli URL delle reti Intranet ed Extranet per l'elenco CRL.

**Nota:** i computer remoti potrebbero avere problemi di timeout se scaricano l'elenco CRL con una connessione lenta.

##### Distribuzione degli aggiornamenti software

L'implementazione di un meccanismo per la distribuzione degli aggiornamenti software è un passaggio importante nel processo di fornitura delle smart card per consentire l'accesso agli utenti. Gli aggiornamenti software includono i profili di Connection Manager aggiornati e le nuove versioni degli strumenti delle smart card.

È possibile distribuire gli aggiornamenti software contenuti in:

-   Server Web accessibili esternamente che contengono gli aggiornamenti.

-   CD o chiavi USB.

-   Soluzioni di gestione software come SMS (Systems Management Server) 2003.

-   Messaggi di posta elettronica che contengono aggiornamenti con firma del codice.

Se si implementa una connessione VPN in quarantena, è possibile distribuire gli aggiornamenti dei profili di Connection Manager con lo stesso metodo utilizzato per fornire gli aggiornamenti per la protezione e il software antivirus. Per ulteriori informazioni sulla quarantena VPN, consultare la Guida alla pianificazione dell'implementazione di servizi di quarantena con la rete privata virtuale Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=41307](http://www.microsoft.com/italy/technet/security/prodtech/windowsserver2003/quarantineservices/default.mspx).

La possibilità di ottenere gli aggiornamenti di Connection Manager e delle smart card attraverso server Web accessibili dall'esterno consente agli utenti di scaricare gli aggiornamenti prima di connettersi alla rete dell'organizzazione. Lo svantaggio associato a questa soluzione è l'eventualità che non sia possibile utilizzare la smart card per eseguire l'autenticazione con il server Web esterno. In questo caso, gli utenti possono basarsi sulle combinazioni di nomi utente e password per connettersi e scaricare gli aggiornamenti. Questo metodo può sembrare poco coerente con l'utilizzo di un'autenticazione basata su due fattori ma, dato che questo server Web fornisce solo le risorse aggiornate, questo tipo di rischio può essere accettabile.

L'utilizzo dei CD per distribuire gli aggiornamenti è un metodo utile per i rollout iniziali di grandi dimensioni, perché il costo di ogni CD si riduce se viene prodotto in quantità notevoli. Le chiavi USB sono invece la soluzione ideale per la distribuzione degli aggiornamenti su base individuale.

L'utilizzo dei sistemi di gestione software come Systems Management Server 2003 per distribuire gli aggiornamenti software richiede la connessione dei computer alla rete. Questo meccanismo può essere adatto per gli utenti mobili e remoti che si connettono alla rete LAN con cadenza regolare e che utilizzano i computer appartenenti al dominio dell'organizzazione. I meccanismi di aggiornamento software come Systems Management Server non sono però adeguati per gli utenti remoti che utilizzano i propri computer da casa.

In situazioni particolari è possibile inviare gli aggiornamenti per posta elettronica. Per implementare questo metodo di distribuzione software, è necessario fornire gli aggiornamenti con firma del codice e istruire gli utenti affinché controllino l'autenticità del certificato con firma del codice.

In questa sezione sono stati presentati i componenti in grado di fornire l'autenticazione delle smart card per gli account di accesso remoto. Nella sezione successiva, intitolata "Problemi e requisiti", vengono illustrati i problemi che Woodgrove National Bank dovrà affrontare durante l'implementazione delle smart card.

[](#mainsection)[Inizio pagina](#mainsection)

### Problemi e requisiti

Durante la pianificazione e la progettazione della soluzione di accesso remoto mediante smart card, il reparto IT di Woodgrove ha riscontrato numerosi problemi di carattere aziendale, tecnico e di protezione. In questa sezione vengono descritti tali problemi.

#### Informazioni generali sullo scenario di Woodgrove National Bank

L'accesso remoto alla rete aziendale di Woodgrove National Bank è garantito agli addetti alle vendite, agli addetti al supporto IT e ai dirigenti. La soluzione di accesso remoto attuale utilizza connessioni remote attraverso linee private a server di accesso remoto dedicati, dotati di modem o schede ISDN (Integrated Services Digital Network). Queste connessioni sono lente e costose, se paragonate alle connessioni a banda larga, in particolare per gli utenti remoti che viaggiano in tutto il mondo.

La maggiore disponibilità dell'accesso a Internet a banda larga consente alle organizzazioni di utilizzare le connessioni VPN per l'accesso remoto. Questo approccio riduce i costi grazie all'eliminazione delle connessioni remote e garantisce all'utente un'esperienza migliore, anche se aumenta la vulnerabilità della banca agli attacchi dannosi.

##### Conformità con i requisiti legali

In quanto istituzione finanziaria, Woodgrove National Bank è anche tenuta al rispetto di severi requisiti legali nei diversi Paesi/aree geografiche in cui esercita. La banca deve conservare la fiducia dei clienti proteggendo i beni dell'azienda e dei clienti. Woodgrove National Bank ha implementato un'iniziativa per la protezione dei computer e ha impostato severi criteri di protezione su tutti i computer che accedono alla rete aziendale, indipendentemente dal fatto che questi computer si connettano alla rete LAN (Local Area Network) in locale o in remoto.

##### Verifica degli utenti

L'attuale soluzione di accesso remoto di Woodgrove National Bank non è in grado di affrontare in modo adeguato gli "attacchi di rappresentazione", in cui un pirata informatico tenta di individuare il nome utente e la password di un utente legittimo. Gli "attacchi di rappresentazione" causano il blocco degli account di accesso remoto, impedendo così la connessione dell'utente legittimo. Questa vulnerabilità aumenta i rischi per la rete aziendale e ha obbligato Woodgrove National Bank a limitare le opzioni di connettività per i propri dipendenti.

#### Problemi aziendali

Molti dirigenti utilizzano l'accesso remoto. Sebbene la protezione sia un fattore essenziale durante l'implementazione di una soluzione basata su smart card, la produttività dei dipendenti che lavorano in remoto è altrettanto importante. La soluzione utilizzata deve essere in grado di bilanciare in modo opportuno queste esigenze.

##### Gestione della produttività

I dipendenti nutrono spesso poca fiducia nelle soluzioni basate sulla protezione che influiscono sulla produttività. Gli utenti, infatti, affrontano spesso con un certo disagio i problemi di accesso alle risorse di rete che si verificano durante e subito dopo la distribuzione di una soluzione. Il reparto IT di Woodgrove deve fornire metodi di accesso alternativi che consentano di superare questo disagio. Gli strumenti elencati di seguito forniscono metodi di accesso alla rete alternativi:

-   **Outlook Web Access** Fornisce agli utenti l'accesso protetto alla posta elettronica mediante un browser Web.

-   **Desktop remoto e Servizi terminal** I dipendenti possono utilizzare Desktop remoto e Servizi terminal per accedere alle applicazioni line-of-business e ai file del desktop.

##### Supporto dell'help desk

L'accettazione dell'utente e l'integrità di una soluzione di accesso remoto dipendono spesso dal livello di supporto disponibile. I dirigenti non accettano volentieri attese prolungate per ottenere il supporto. Le organizzazioni devono investire nella formazione degli utenti finali e del personale di supporto.

#### Problemi tecnici

Woodgrove National Bank ha individuato diversi problemi tecnici che devono essere valutati attentamente prima di implementare le smart card per l'accesso remoto. Questi problemi includono la distribuzione delle smart card e dei lettori di smart card, l'integrazione della soluzione nella rete attuale con interruzioni minime del funzionamento e l'integrazione nell'infrastruttura di gestione IT attuale.

-   **Lettori di smart card supportati**. È possibile che gli utenti remoti lavorino da casa utilizzando computer con sistemi operativi diversi. Il reparto IT di Woodgrove ha stabilito che l'unica configurazione supportata è Windows XP Professional con SP2 o versioni successive. Gli utenti remoti che utilizzano Windows 2000 Professional non hanno alcuna garanzia che i lettori di smart card funzionano anche sui loro computer.

-   **Latenza di rete**. Il tempo impiegato dai pacchetti per raggiungere e tornare da un server di accesso remoto potrebbe causare la perdita delle connessioni protette con VPN. Ciò è particolarmente problematico per le connessioni a banda larga via satellite. Woodgrove National Bank ha deciso di non supportare le connessioni remote il cui periodo di latenza supera i 300 millisecondi.

-   **Distribuzione delle smart card**. Poiché Woodgrove National Bank opera in diversi Paesi/aree geografiche del mondo, la distribuzione delle smart card pone un problema di carattere tecnico e di protezione. Gli agenti di registrazione devono essere in grado di contattare il server Web di attivazione indipendentemente dal Paese/area geografica in cui si trovano. In alternativa, gli utenti potrebbero dover sbloccare le smart card con un sistema Challenge/Response. L'implementazione del sistema Challenge/Response potrebbe richiedere strumenti software specifici da sviluppare con il Software Development Kit (SDK) del produttore di smart card.

#### Problemi relativi alla protezione

La strategia di implementazione studiata da Woodgrove National Bank per proteggere l'accesso remoto utilizzando le smart card presenta i seguenti problemi:

-   **Identificazione degli utenti con accesso remoto**. Il reparto IT di Woodgrove National Bank deve convalidare l'identità degli utenti con accesso remoto durante il processo di distribuzione e attivazione delle smart card.

-   **Eccezioni di connessione per la soluzione Woodgrove**. Poiché le smart card possono essere perse, rubate o semplicemente dimenticate, il reparto IT di Woodgrove deve garantire che la soluzione preveda un metodo rapido per distribuire in modo sicuro le smart card sostitutive e anche un metodo che consenta di gestire le eccezioni durante il periodo in cui le smart card vengono consegnate.

#### Requisiti delle soluzioni

La soluzione per la protezione degli account di accesso remoto mediante smart card deve includere i seguenti componenti:

-   **Servizio di autenticazione Internet (IAS)** I server IAS attuali richiedono l'aggiornamento a Windows Server 2003 con Service Pack 1 o versioni successive per agevolare i filtri IP migliorati e l'accettazione degli attributi specifici dei produttori. Inoltre, il reparto IT di Woodgrove deve abilitare il supporto per EAP-TLS sui server di accesso remoto.

-   **Modelli di utente di smart card**. Woodgrove National Bank deve personalizzare i modelli di certificato e impostare le autorizzazioni corrette nei modelli. I modelli di agente di registrazione dei certificati e di accesso alle smart card richiedono le autorizzazioni adeguate.

    **Nota:** è possibile limitare l'accesso remoto ai certificati delle smart card impostando criteri di accesso remoto che accettino solo un certificato con un identificatore oggetto specifico. Per ulteriori informazioni sui modelli di certificato e gli identificatori oggetto, consultare il white paper relativo all'implementazione e alla gestione dei modelli di certificato in Windows Server 2003 all'indirizzo <http://www.microsoft.com/technet/prodtechnol/windowsserver2003/technologies/security/ws03crtm.mspx>.

-   **Strumenti di gestione dei PIN**. Gli utenti devono avere un'utilità software per gestire i PIN. La maggior parte dei produttori di smart card fornisce strumenti di base per la gestione dei PIN. Il reparto IT di Woodgrove ha deciso di personalizzare lo strumento di gestione dei PIN integrandolo con un'utilità di sblocco dei PIN in remoto.

-   **Oggetti Criteri di gruppo**.** **Il reparto IT di Woodgrove deve creare oggetti Criteri di gruppo (GPO) appropriati per la struttura dell'unità organizzativa. Questi oggetti Criteri di gruppo devono includere le impostazioni necessarie per supportare eccezioni quali, ad esempio, un utente che perde o dimentica la smart card o il PIN.

-   **Profili di Connection Manager**. Il reparto IT di Woodgrove deve creare i profili di Connection Manager e configurarli in modo che contengano le impostazioni appropriate per la connessione remota o VPN per i server di accesso remoto di Woodgrove. Il reparto IT di Woodgrove deve anche personalizzare il testo dell'interfaccia utente dei profili di Connection Manager per aiutare gli utenti a capire meglio il processo di connessione e per indicare loro come procedere quando riscontrano problemi. Il reparto IT di Woodgrove ha creato diversi profili di Connection Manager per vari utenti, come dirigenti e utenti comuni, ma un solo profilo per il personale amministrativo. A ciascun profilo sono state assegnate priorità diverse durante l'impostazione della connessione. Gli amministratori possono connettersi da una postazione remota indipendentemente dai livelli di traffico della rete.

-   **Windows XP Professional con Service Pack 2**. Woodgrove National Bank deve aggiornare tutti i computer di accesso remoto a Windows XP Professional con SP2 o versioni successive. Windows XP Professional con SP2 offre funzionalità di protezione avanzate come Windows Firewall e un migliore supporto per gli aggiornamenti automatici che aumentano la protezione della soluzione di accesso remoto. Windows XP Home con SP2 fornisce questi vantaggi di protezione ma non è in grado di unirsi a un dominio e utilizzare i criteri di gruppo. Windows 2000 Professional con SP4 non è dotato dei miglioramenti alla protezione che vanta Windows XP Professional con SP2.

-   **Fornitura delle smart card e dei lettori di smart card**. Sebbene Woodgrove National Bank disponga di un'infrastruttura PKI avanzata, la banca potrebbe godere di ben pochi vantaggi se installasse il sistema operativo Windows for Smart Cards su smart card vuote. La maggior parte dei produttori offre smart card su cui è già stato installato il sistema operativo. Scegliendo le smart card e i lettori di smart card di un unico produttore si potrà godere del vantaggio di avere un solo punto di riferimento per qualsiasi problema di supporto.

-   **Lettori di smart card USB o PC Card**.** **La creazione di una base standard per la distribuzione riduce il costo di installazione di una soluzione basata su smart card. Woodgrove National Bank ha implementato un criterio aziendale secondo cui tutti i nuovi computer portatili devono avere lettori di smart card incorporati. Woodgrove National Bank ha anche stabilito uno standard comune per la fornitura dei lettori di smart card USB. La banca fornisce lettori di smart card USB ai dipendenti che utilizzano i propri computer per lavorare da casa. Woodgrove si è assicurata la continuità nel tempo grazie a un contratto stipulato con il produttore di lettori di schede che prevede la fornitura dello stesso modello di lettori di smart card per due anni.

-   **Relazioni di trust**. Per l'implementazione delle smart card, Woodgrove National Bank ha utilizzato le relazioni di trust attuali tra insiemi di strutture diverse e relazioni di trust unidirezionali, come quelle che esistono tra i piccoli insiemi di strutture dei gruppi di sviluppo e l'insieme di strutture principale dell'azienda. Questo tipo di impostazione non ha richiesto alcuna modifica ai modelli di certificato.

-   **Infrastruttura a chiave pubblica (Public Key Infrastructure, PKI) di Windows Server 2003**. I servizi certificati di Windows Server 2003 sono in grado di assegnare le autorizzazioni necessarie agli elementi di un modello predefinito di certificato delle smart card e di personalizzare i modelli. L'accresciuta flessibilità delle autorizzazioni dei modelli è un elemento chiave che consente al personale IT di Woodgrove di delegare in modo sicuro l'emissione dei certificati in base al modello di emissione definito. Il reparto IT di Woodgrove utilizza le funzionalità avanzate dell'infrastruttura PKI di Windows Server 2003 per impostare le regole per il rinnovo automatico dei certificati. Il reparto IT utilizza le funzionalità di autorizzazione dei modelli di certificato per richiedere agli addetti alla protezione di Woodgrove National Bank di creare manualmente tutte le nuove registrazioni dei certificati di smart card. L'utente può però rinnovare automaticamente tutti i certificati delle smart card attuali.

Woodgrove National Bank aveva già implementato un'infrastruttura PKI di Windows 2000 Server quando l'organizzazione ha deciso di implementare le smart card. Per il progetto pilota iniziale, il reparto IT di Woodgrove National Bank aveva deciso di utilizzare la propria infrastruttura di protezione basata su Windows 2000 per creare e gestire i certificati delle smart card, invece di ricorrere a servizi di terze parti. Tuttavia, la soluzione per la protezione delle smart card di Woodgrove richiedeva che i certificati scadessero dopo un anno. Questo requisito avrebbe comportato costi di supporto eccessivi perché prevedeva il rinnovo manuale di decine di migliaia di certificati utente ogni anno. L'aumento del carico di lavoro amministrativo spinse il gruppo IT di Woodgrove National Bank ad aggiornare la propria PKI a Windows Server 2003.

Se Woodgrove National Bank avesse utilizzato l'infrastruttura PKI di Windows 2000 Server per il rinnovo automatico dei certificati, le opzioni di rinnovo dei certificati avrebbero consentito esclusivamente il rinnovo automatico di tutti i certificati oppure il rinnovo manuale di tutti i certificati. Il rinnovo automatico di tutti i certificati avrebbe però eliminato la flessibilità delle opzioni di rinnovo.

[](#mainsection)[Inizio pagina](#mainsection)

### Progettazione della soluzione

In questa sezione vengono descritte le scelte di progettazione effettuate dal reparto IT di Woodgrove National Bank per utilizzare le smart card per la protezione dell'accesso remoto. Vengono illustrati inoltre il concetto, i prerequisiti e l'architettura della soluzione.

#### Concetto della soluzione

La soluzione utilizza una combinazione di impostazioni di Criteri di gruppo, criteri di accesso remoto, profili di Connection Manager, certificati utente X.509 versione 3 installati sulle smart card e lettori di smart card. Questo concetto prevede che un utente con accesso remoto avvii un profilo di Connection Manager personalizzato che richiede all'utente di inserire una smart card nel lettore collegato. Il sistema operativo richiede poi all'utente di inserire un PIN. Se il PIN è corretto, il lettore estrae il certificato della smart card e le informazioni sull'account. Connection Manager stabilisce poi una connessione al server di accesso remoto aziendale e presenta le credenziali della smart card. Active Directory autentica queste credenziali e il server di accesso remoto concede all'utente l'accesso alla rete aziendale.

#### Prerequisiti della soluzione

I requisiti per l'utilizzo delle smart card per proteggere gli account di accesso remoto sono simili a quelli che proteggono gli account amministratore. È necessario:

-   Consultare gli utenti e i gruppi

-   Reclutare il team del progetto

-   Definire le aspettative degli utenti

-   Aggiornare l'hardware e il software

-   Distribuire e attivare le smart card in modo sicuro

##### Consultare gli utenti e i gruppi

Pianificare un ciclo di valutazione di tutte le soluzioni di accesso remoto attuali e consultarne i rispettivi utenti. Woodgrove National Bank opera in diversi Paesi/aree geografiche in cui sono presenti gli utenti con accesso remoto. Il team iniziale ha raccolto i commenti degli attuali utenti con accesso remoto e dei team di supporto per individuare possibili utenti, gruppi e personale di supporto da includere nei progetti pilota.

##### Reclutare il team del progetto

Prima di implementare un progetto di questo tipo, è necessario accertarsi di disporre del personale e delle competenze adeguati. È probabile che il team del progetto necessiti del contributo delle seguenti figure rappresentative:

-   Program manager

-   Architetto di sistemi informativi

-   Analista o integratore di sistemi

-   Tecnici di sistema

-   Product release manager

-   Testing manager

-   Responsabile help desk o responsabile supporto tecnico

-   Specialisti del supporto tecnico per gli utenti

-   Responsabili della protezione

Per ulteriori informazioni sulle mansioni dei rappresentanti e sulle associazioni ai ruoli in Microsoft Operations Framework (MOF), consultare l'articolo relativo alla tassonomia delle occupazioni IT nei white paper aggiuntivi di Microsoft Solutions Framework (in inglese) all'indirizzo [http://www.microsoft.com/downloads/details.aspx?FamilyID=839058c3-d998-4700-b958-3bedfee2c053](http://www.microsoft.com/downloads/details.aspx?familyid=839058c3-d998-4700-b958-3bedfee2c053)

Se l'azienda non dispone di personale con competenze specifiche al suo interno, deve provvedere ad assumere personale aggiuntivo. Dal momento che di norma il progetto non richiede la partecipazione dell'intero organico in ogni fase, è necessario determinare il livello di disponibilità che ciascuno deve assicurare per tutta la durata del progetto.

##### Definire le aspettative degli utenti

Il problema principale relativo alle aspettative degli utenti che utilizzano le smart card per l'accesso remoto è il rallentamento dei tempi di accesso. Gli utenti devono essere consapevoli che i tempi di accesso aumentano di alcuni secondi con l'autenticazione delle smart card.

##### Aggiornare l'hardware e il software

La soluzione di accesso remoto mediante smart card richiede i sistemi operativi e i service pack più recenti di Microsoft. Questo requisito consente a tale soluzione di sfruttare al meglio gli ultimi aggiornamenti e le funzionalità di protezione di Windows XP Professional con SP2 e Windows Server 2003 con SP1, quali Windows Firewall, Data Execution Prevention (DEP), la procedura guidata Security Configuration e VPN Quarantine.

Gli aggiornamenti software potrebbero richiedere l'aggiornamento dell'hardware del client o del server. Un programma pilota può stabilire se le apparecchiature obsolete possono eseguire i sistemi operativi più recenti. Per controllare se le apparecchiature sono certificate per Windows XP o Windows Server 2003, consultare l'argomento sul catalogo di Windows e HCL nell'articolo relativo ai prodotti progettati per Microsoft Windows all'indirizzo <http://www.microsoft.com/whdc/hcl/default.mspx>.

##### Distribuire e attivare le smart card in modo sicuro

L'implementazione delle smart card per l'accesso remoto richiede un metodo sicuro per proteggere e attivare le smart card. Solitamente questo processo di distribuzione richiede agli utenti remoti di rivolgersi ai rispettivi uffici amministrativi locali in modo che l'agente di registrazione possa verificarne l'identità, emettere la smart card ed eseguire la procedura di attivazione. Nella sezione Modello di emissione delegata, più avanti in questo capitolo, viene descritto come Woodgrove National Bank ha distribuito e attivato le smart card per gli utenti remoti.

#### Architettura della soluzione

L'implementazione della soluzione di accesso remoto mediante smart card di Woodgrove National Bank richiede i seguenti componenti:

-   Active Directory

-   IAS installato su un server Windows Server 2003

-   Windows Server 2003 con SP1 dotato di routing e accesso remoto

-   Criteri di gruppo

-   Computer client che eseguono Windows XP Professional con SP2 o versioni successive

-   Lettori di smart card

-   Smart card con almeno 32 KB di memoria

-   Profili di Connection Manager creati con CMAK

-   Script lato client per il profilo di Connection Manager

Il reparto IT di Woodgrove aveva inizialmente pensato di fornire il supporto per tutte le versioni di Windows distribuite. Tuttavia, la maggiore consapevolezza delle minacce cui sono soggetti i computer connessi a Internet ha convinto il personale IT a scegliere Windows XP Professional con SP2 e versioni successive come opzione standard.

Gli account utente e l'appartenenza ai gruppi memorizzati in Active Directory regolano la connettività remota e l'accesso alle risorse aziendali di Woodgrove National Bank. Il reparto IT di Woodgrove utilizza anche i Criteri di gruppo per configurare i computer client affinché soddisfino i criteri di protezione della rete aziendale.

#### Procedura di funzionamento della soluzione

In questa sezione vengono forniti i dettagli tecnici riguardanti la soluzione di Woodgrove National Bank. Viene illustrata la modalità con cui Active Directory autentica l'utente e tiene traccia del percorso di autenticazione per le credenziali delle smart card.

La procedura descritta di seguito attiva l'accesso remoto con le smart card:

1.  Un utente remoto si connette a un computer dotato di accesso a Internet e lettore di smart card. L'utente avvia il profilo di Connection Manager personalizzato facendo doppio clic sulla connessione denominata **Woodgrove IT Connection Manager for smart cards**.

2.  Il profilo di Connection Manager verifica la presenza di una smart card nel lettore di smart card. Viene visualizzata una finestra di dialogo in cui viene chiesto all'utente di inserire il PIN. Connection Manager utilizza il PIN per eseguire le operazioni principali sulla scheda come servizio di sistema perché non è in grado di chiedere e mostrare l'interfaccia utente sul desktop. Se l'utente inserisce il PIN corretto, la scheda si sblocca e consente il proseguimento del processo di accesso remoto.

3.  L'autorità di protezione locale (LSA) è il componente del sistema operativo attendibile che esegue tutte le autenticazioni. SChannel, il codice che implementa SSL, viene eseguito parzialmente nell'autorità di protezione locale e avvia la sequenza di mapping.

4.  Il profilo di Connection Manager stabilisce un collegamento ai server IAS di Woodgrove National Bank utilizzando una connessione remota o VPN. Il server IAS esegue un controllo delle revoche sul certificato del client. Con il mapping dei certificati per il nome principale utente (UPN), la CA di emissione deve trovarsi nell'archivio NTAuth. È anche possibile impostare il mapping esplicito per l'account utente di Active Directory.

5.  L'autorità di protezione locale (LSA) presenta le informazioni dell'utente al server IAS. Il codice SChannel che viene eseguito sul server IAS invia un messaggio al codice SChannel che risiede sul controller di dominio e passa a questo le informazioni UPN del certificato.

6.  Il codice SChannel che viene eseguito sul server IAS convalida il certificato ed esegue poi una ricerca degli utenti in Active Directory sul controller di dominio. Il controller di dominio genera un PAC (Privilege Access Certificate) che contiene l'identificatore da 128 bit e l'appartenenza al gruppo dell'utente. Le comunicazioni successive che partono da questo punto utilizzano il protocollo Kerberos versione 5.

7.  Il controller di dominio trasmette una chiave di sessione avanzata generata casualmente che include il ticket di concessione ticket (TGT, Ticket Granting Ticket) di Kerberos nel computer client. La ricezione di questa chiave autentica il server di accesso remoto sul client. Ora entrambi i computer sono stati autenticati reciprocamente.

8.  Il computer client decifra la chiave della sessione di accesso e presenta il TGT di Kerberos versione 5 al servizio di concessione. Una volta completato questo processo, tutte le altre comunicazioni del protocollo Kerberos versione 5 utilizzano la crittografia simmetrica.

9.  Se l'utente si è connesso utilizzando una connessione remota, viene visualizzata una finestra in cui si richiede il nome utente e la password. Dopo aver immesso le credenziali, l'utente può accedere a tutte le risorse di rete di Woodgrove Bank. Gli utenti che si sono connessi utilizzando una connessione VPN non devono eseguire questo passaggio.   

Nella figura seguente sono mostrati i passaggi che devono essere eseguiti per utilizzare una smart card per l'autenticazione dell'accesso remoto.

[![](images/Dd536197.pgfg0401(it-it,TechNet.10).gif "Figura 4.1 Accesso remoto e processo di autenticazione con una smart card")](https://technet.microsoft.com/it-it/dd536197.pgfg0401_big(it-it,technet.10).gif)

**Figura 4.1 Accesso remoto e processo di autenticazione con una smart card**

I cicli aggiuntivi del processore necessari per elaborare le informazioni della smart card allungano il processo di autenticazione iniziale di circa 20-25 secondi. Al termine dell'autenticazione, le prestazioni non subiscono alcun cambiamento.

#### Considerazioni aggiuntive sulla progettazione

Nella sezione successiva vengono fornite altre informazioni dettagliate sulla distribuzione delle smart card, compreso il meccanismo di distribuzione delle smart card utilizzato da Woodgrove National Bank.

##### Modello di emissione delegata

Il reparto IT di Woodgrove National Bank ha sviluppato un modello di emissione delegata per le smart card. Questo modello offre un supporto tempestivo che consente di assicurare il più alto livello di protezione delle smart card ai dipendenti sparsi in tutto il mondo.

Il reparto IT di Woodgrove National Bank ha utilizzato il modello di emissione delegata per distribuire le smart card all'esterno dell'ufficio IT principale dell'azienda situato a Londra. Il reparto IT di Woodgrove National Bank ha inviato i propri tecnici nelle varie sedi internazionali per formare i responsabili incaricati dell'emissione (DIO, Delegated Issuance Officer). I tecnici hanno insegnato al personale DIO come distribuire le smart card e come utilizzare gli strumenti delle smart card. Dopo la visita iniziale, gli incaricati DIO hanno partecipato alle conferenze telefoniche settimanali con il team IT centrale di Woodgrove National Bank per discutere di problemi eventualmente emersi.

Nella figura successiva sono mostrati i passaggi che costituiscono il modello di emissione delegata per l'approvazione delle richieste di certificati.

[![](images/Dd536197.pgfg0402(it-it,TechNet.10).gif "Figura 4.2 Processo di delega utilizzato per emettere le smart card per l'accesso remoto")](https://technet.microsoft.com/it-it/dd536197.pgfg0401_big(it-it,technet.10).gif)

**Figura 4.2 Processo di delega utilizzato per emettere le smart card per l'accesso remoto**

I passaggi eseguiti in conformità con questo diagramma di flusso sono i seguenti:

1.  L'utente richiede una smart card all'incaricato DIO.

2.  L'incaricato DIO convalida l'identità dell'utente in base a un documento di identificazione accettabile, ad esempio un passaporto o una patente di guida, e verifica l'identità dell'utente con il responsabile del reparto. Dopo aver l'identità dell'utente, l'incaricato DIO inoltra una richiesta di certificato al responsabile della protezione a Londra.

3.  Per convalidare la richiesta, il responsabile della protezione controlla l'esistenza di eventuali certificati precedenti emessi a nome dell'utente. Il responsabile della protezione determina inoltre se l'utente ha già presentato altre richieste di smart card. Se non esistono obiezioni all'emissione della smart card, il responsabile della protezione concede l'approvazione. Se il responsabile della protezione riscontra un problema, il processo deve essere sottoposto a un controllo, come descritto nel passaggio cinque.

4.  L'incaricato DIO riceve l'approvazione e utilizza l'account dell'agente di registrazione per emettere il certificato. Questo certificato è associato a una nuova smart card consegnata all'utente dall'incaricato DIO. Il processo di emissione delegata è terminato.

5.  Se dovessero sorgere dubbi riguardo la validità della richiesta, il responsabile della protezione avvia un controllo della richiesta per determinare se concedere l'approvazione all'utente. Al termine del controllo, l'utente deve presentare una nuova richiesta.

6.  Il processo di emissione delegata è terminato.

Woodgrove National Bank ha potuto implementare il modello di emissione delegata solo dopo che il reparto IT di Woodgrove ha eseguito la migrazione delle autorità di certificazione aziendali a Windows Server 2003. L'infrastruttura PKI di Windows Server 2003 è in grado di applicare autorizzazioni dettagliate a sezioni dei modelli di certificato, attivando così il ruolo dell'incaricato DIO all'interno del modello di emissione delegata. All'interno di tale modello, Woodgrove ha sviluppato le procedure per emettere nuovamente in modo sicuro le smart card perse o rubate.  

##### Configurare l'accounting RADIUS

Sebbene la manutenzione dei registri non sia un requisito essenziale per l'implementazione di una soluzione di accesso remoto basata su smart card, Microsoft la consiglia vivamente. Se si utilizza IAS, uno dei vantaggi che ne derivano è il supporto incorporato per il provider dell'accounting RADIUS, in cui vengono registrate le richieste e le sessioni dei client. Woodgrove National Bank desidera monitorare gli utenti che si connettono alla rete aziendale, controllandone l'ora di accesso e la durata della connessione. Grazie a RADIUS, Woodgrove è in grado di analizzare le tendenze di connessione con lo scopo di esaminare e migliorare il servizio.

Ciascun server IAS raccoglie i dati sulle sessioni utente e li memorizza in Microsoft SQL Server™ Desktop Engine (Windows) (WMSDE) su Windows Server 2003 o in SQL Server 2000 Desktop Engine (MSDE 2000) su Windows 2000 Server e versioni precedenti. IAS trasferisce le informazioni di accounting da WMSDE o MSDE a un database SQL Server 2000 centrale quasi in tempo reale. Questa impostazione garantisce un utilizzo conveniente delle licenze SQL Server e non influisce negativamente sulle prestazioni del server.

Woodgrove National Bank ha distribuito nelle varie aree geografiche i server preposti alla raccolta dati basati su SQL Server per raccogliere i dati delle sessioni di accesso remoto IAS.

##### Implementare i progetti pilota

Il reparto IT di Woodgrove National Bank esegue test delle soluzioni in un ambiente di laboratorio e in più progetti pilota prima di iniziarne la distribuzione nella rete di produzione. Il personale IT di Woodgrove ha sviluppato due progetti pilota per la distribuzione delle smart card per l'accesso remoto: un progetto ha coinvolto un piccolo gruppo di utenti esperti mentre l'altro ha visto la partecipazione di un gruppo più diversificato di utenti distribuiti in diversi Paesi/aree geografiche, che utilizzavano vari tipi di accesso remoto.

Il progetto pilota con gli utenti più esperti ha consentito a Woodgrove National Bank di individuare i problemi maggiori associati alla distribuzione delle smart card. Gli utenti esperti sono stati capaci di affrontare interruzioni di servizio di minore entità e finestre di dialogo impreviste. Al termine del primo progetto pilota, il reparto IT di Woodgrove sapeva che la soluzione basata sulle smart card funzionava ma era necessario apportare alcune modifiche di ottimizzazione.

Il secondo progetto pilota, che includeva una vasta gamma di utenti, ha consentito al reparto IT di Woodgrove di sperimentare il genere di richieste di aiuto prevedibili nella distribuzione completa. Questo progetto pilota ha consentito al reparto help desk di risolvere i problemi tecnici e ha indicato gli eventuali sviluppi necessari prima della distribuzione delle smart card a tutti gli utenti remoti.

##### Garantire un'elevata disponibilità

Lo scenario della soluzione deve essere altamente affidabile perché il mantenimento della produttività rappresenta un requisito chiave per la soluzione di accesso remoto. Woodgrove National Bank deve valutare soluzioni che garantiscano un'elevata disponibilità del sistema. In tale configurazione rientra quanto segue:

-   Server di accesso remoto con bilanciamento del carico

-   Server IAS con bilanciamento del carico

-   Percorsi di rete ridondanti

    **Nota:** Woodgrove Bank ha dislocato geograficamente i punti di ingresso RRAS/IAS in ragione del layout fisico della rete.

##### Garantire una larghezza di banda adeguata per la rete

Gli architetti di sistema devono valutare i percorsi di rete attuali, i tempi di connessione previsti e il tipo e l'estensione del traffico di accesso remoto previsto. La larghezza di banda aggiuntiva di cui necessitano gli utenti remoti non deve essere sottovalutata. Le implementazioni dei progetti pilota devono contribuire all'analisi dei modelli di traffico ad accesso remoto e dell'effetto che questo traffico può avere sull'infrastruttura di rete attuale. È importante che queste prove includano anche utenti non esperti e modelli di utilizzo tipici per simulare i problemi che potrebbero verificarsi durante la distribuzione completa. Gli switch hardware che includono il controllo della larghezza di banda e le reti LAN virtuali (VLAN) possono ridurre gli effetti del traffico ad accesso remoto sugli altri utenti.

Woodgrove National Bank utilizza più provider di servizi Internet per ottenere una buona connettività Internet. La maggior parte della larghezza di banda attuale fornisce accesso a Internet per eseguire le ricerche Web e utilizzare la posta elettronica. Il reparto IT di Woodgrove deve rivalutare le impostazioni attuali per consentire il traffico aggiuntivo derivante dalle connessioni con accesso remoto.

##### Eccezioni

Gli architetti di sistema di Woodgrove National Bank sono consapevoli che qualsiasi soluzione deve essere in grado di affrontare anche situazioni in cui le esigenze aziendali richiedono che uno o più dispositivi siano esonerati dal rispetto dei requisiti di protezione solitamente validi. Ad esempio, l'accesso remoto per i dirigenti durante una riunione importante potrebbe anche essere concesso senza l'autenticazione delle smart card, al contrario di ciò che prevedono i requisiti. Se la soluzione basata sulle smart card non è in grado di garantire l'esonero dei singoli dispositivi, il reparto IT sarà costretto a disattivare tutti i requisiti di accesso remoto protetto per permettere un solo esonero. Per questo motivo è opportuno che la soluzione di accesso remoto mediante smart card supporti le eccezioni.

**Nota:** il gruppo di protezione del reparto IT di Woodgrove è l'unica autorità che può determinare se le esigenze aziendali giustificano il rischio di protezione che un eventuale esonero comporta.

Per affrontare le eccezioni, il personale IT di Woodgrove ha creato un nuovo gruppo di protezione chiamato RemoteSmartCardUsersTempException per le eccezioni temporanee ai requisiti delle smart card per l'accesso remoto. I criteri di accesso remoto per il server di accesso remoto in ingresso sono poi stati configurati come indicato nella seguente tabella.

**Tabella 4.1: condizioni dei criteri di accesso remoto di Woodgrove National Bank**

 
<table style="border:1px solid black;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Requisiti</th>
<th style="border:1px solid black;" >Condizioni del criterio</th>
<th style="border:1px solid black;" >Tipo di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">Richiede l'autenticazione mediante smart card per i membri del gruppo di utenti con accesso remoto</td>
<td style="border:1px solid black;">Gruppo di Windows corrispondente a &quot;WOODGROVE\RemoteSmartCardUsers&quot;</td>
<td style="border:1px solid black;">EAP - Solo smart card o altri certificati.</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Non richiede l'autenticazione mediante smart card per i membri del gruppo di esclusioni temporanee</td>
<td style="border:1px solid black;">Gruppo di Windows corrispondente a &quot;WOODGROVE\RemoteSmartCardUsersTempException&quot;</td>
<td style="border:1px solid black;">MSCHAP v2</td>
</tr>
</tbody>
</table>
  
Questa impostazione impone il requisito delle smart card ai membri del gruppo RemoteSmartCardUsers ma non ai membri del gruppo RemoteSmartCardUsersTempException. Per ulteriori informazioni su come richiedere l'autenticazione delle smart card per gli utenti remoti, consultare l'articolo relativo alla configurazione dell'accesso remoto con smart card (in inglese) all'indirizzo <http://technet.microsoft.com/en-us/library/cc739449.aspx>.
  
##### Procedure consigliate
  
Il reparto IT di Woodgrove National Bank ha stilato il seguente elenco di procedure consigliate e suggerimenti:
  
-   **Coinvolgere il reparto help desk**. In tutti i progetti basati sulle smart card dovrebbe essere presente un reparto help desk ben preparato. Dopo la distribuzione, il reparto help desk deve svolgere un vero e proprio ruolo di manutenzione. È fondamentale mantenere aggiornato il personale dell'help desk relativamente a qualsiasi modifica nel sistema interno e a eventuali sviluppi tecnologici che ne influenzano l'utilizzo.
  
-   **Assicurare la gestione dei PIN**.** **Poiché l'obiettivo principale dell'utilizzo delle smart card è migliorare la protezione di rete, la sicurezza dei dati archiviati sulla smart card è indispensabile. I PIN dimenticati rappresentano un problema durante e dopo la distribuzione delle smart card. È opportuno verificare con il proprio produttore di smart card la fornitura degli strumenti di gestione dei PIN e implementare i processi di ripristino dei PIN per gli utenti che non sono in grado di ripristinare il proprio PIN da una sede aziendale (ad esempio mentre sono in viaggio).
  
-   **Implementare misure anti-alterazione**. Le smart card richiedono la protezione anti-alterazione che prevede il blocco della scheda quando un utente inserisce un PIN errato per cinque volte di seguito.
  
-   **Mantenere un team di post-distribuzione**. Un team di post-distribuzione può essere molto più piccolo del team di distribuzione iniziale, ma è necessario per controllare l'integrità del sistema con cadenza regolare e per verificare e coordinare eventuali aggiornamenti dell'infrastruttura delle smart card.
  
#### Monitoraggio e gestione
  
Una soluzione che utilizza le smart card per la protezione dell'accesso remoto deve includere la funzionalità per il controllo dell'integrità operativa della soluzione. Questo processo deve essere in grado di controllare l'intera rete, una singola risorsa o un elenco di risorse in tempo reale. Gli strumenti di monitoraggio devono mostrare tutte le informazioni che un'organizzazione deve fornire al personale di supporto operativo. Se la soluzione non soddisfa questo requisito, il personale addetto alla protezione non può determinare se la soluzione gestisce le connessioni di accesso remoto protette in modo efficace.
  
##### Considerazioni operative
  
Il reparto IT di Woodgrove ha rispettato le seguenti considerazioni di carattere operativo durante la distribuzione della soluzione:
  
-   **Verificare l'autenticazione nelle applicazioni interne**. Una smart card dovrebbe agire unicamente sull'accesso iniziale. Il programma pilota dovrebbe testare e verificare il funzionamento dell'autenticazione nelle applicazioni interne.
  
-   **Risolvere i problemi dei client remoti**. Per risolvere i problemi dei client potrebbe essere necessaria la stretta collaborazione di più team che potrebbero essere situati in zone con fusi orari diversi. Test rigorosi e un'implementazione adeguata dei progetti pilota contribuiscono a ridurre le richieste di supporto.
  
-   **Comprendere gli scenari e le minacce associati all'accesso remoto all'organizzazione**. È necessario comprendere gli scenari di accesso remoto e le minacce alla protezione dell'organizzazione e trovare un equilibrio. È opportuno assegnare la priorità ai beni che richiedono la protezione maggiore. La decisione che riguarda il giusto equilibrio tra i costi e i rischi è strategica e deve essere presa dai dirigenti di più alto livello.
  
-   **Anticipare le difficoltà tecniche**. È opportuno anticipare le difficoltà tecniche, come le routine di installazione e la distribuzione degli strumenti di gestione delle smart card. Potrebbe essere necessario integrare la soluzione basata sulle smart card negli strumenti di gestione dell'azienda esistenti.
  
-   **Monitorare e gestire i problemi delle prestazioni**. È necessario monitorare e gestire i problemi delle prestazioni e stabilire in anticipo le aspettative degli utenti sulla distribuzione. Ad esempio, gli utenti remoti che accedono per la prima volta potrebbero riscontrare un tempo di accesso piuttosto lento se selezionano la casella di controllo **Utilizza connessione remota** nella finestra di dialogo **Accesso a Windows**. È opportuno accertarsi che gli utenti remoti siano consapevoli di questo ritardo.
  
-   **Mantenere gli aggiornamenti**. Se si pianifica di effettuare gli aggiornamenti più recenti della tecnologia, eseguire queste operazioni nelle fasi iniziali del processo di implementazione del progetto. Questa strategia fornisce client di base e una piattaforma server e rimuove diverse variabili che si potrebbero altrimenti incontrare durante la distribuzione. Verificare l'aumento della stabilità del servizio e la diminuzione dei costi di supporto agli utenti.
  
-   **Implementare le fasi del progetto**. È opportuno pianificare la suddivisione del progetto in fasi e prevedere il passaggio di un intervallo di tempo adeguato tra le fasi per agevolare l'adozione da parte dell'utente e la stabilizzazione di sistemi e processi. La sovrapposizione delle fasi potrebbe influire negativamente sul servizio e impedire l'identificazione dei problemi di servizio.
  
-   **Considerare la presenza dei beni personali**. Ricordare che i computer di casa dei dipendenti sono di loro proprietà e non vengono gestiti dal reparto IT dell'azienda. Se un dipendente non desidera o non è in grado di installare l'hardware e il software necessari per supportare l'accesso remoto protetto con le smart card è possibile vagliare altre opzioni. Ad esempio, Microsoft Outlook® Web Access fornisce ai dipendenti l'accesso protetto alla propria casetta postale di Microsoft Exchange Server.
  
-   **Gestire le modifiche alla soluzione**. È necessario gestire le eventuali modifiche e gli sviluppi alla soluzione ricorrendo a processi simili a quelli necessari per la distribuzione iniziale.
  
-   **Ottimizzare la soluzione.** Tutti gli aspetti della soluzione basata sulle smart card richiedono un esame e un'ottimizzazione periodici. A scadenza regolare, il reparto IT di Woodgrove deve esaminare i processi di registrazione e le esigenze di eccezioni degli account con l'obiettivo di incrementare la sicurezza e l'integrità.
  
##### Come ampliare la soluzione
  
Le smart card offrono un potenziale considerevole per lo sviluppo dell'applicazione. Ad esempio, i programmatori potrebbero adattare la piattaforma aperta ampliabile delle smart card e la memoria protetta a utilizzi come i sistemi di pagamento non in contanti per il bar.
  
Sebbene l'utilizzo delle smart card per proteggere l'accesso remoto riduca gli attacchi di utenti non autorizzati, la soluzione non garantisce che i computer ad accesso remoto siano conformi ai criteri di protezione della rete. Network Access Quarantine Control, una funzionalità di Windows Server 2003 con SP1, può confermare che i computer remoti eseguano gli ultimi aggiornamenti per gli antivirus e la protezione. Il controllo per la quarantena NAQC può eseguire altre verifiche, ad esempio controllare che Windows Firewall su Windows XP con SP2 sia attivato. Per ulteriori informazioni sul controllo quarantena, fare riferimento alla Guida alla pianificazione dell'implementazione di servizi di quarantena con la rete privata virtuale Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=41307](http://www.microsoft.com/italy/technet/security/prodtech/windowsserver2003/quarantineservices/default.mspx).
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Riepilogo
  
L'implementazione delle smart card per autenticare le connessioni di accesso remoto garantisce una maggiore protezione rispetto alle semplici combinazioni di nome utente e password. Le smart card implementano l'autenticazione a due fattori tramite una combinazione di smart card e PIN. L'autenticazione basata su due fattori è decisamente più difficile da compromettere e il PIN è più facile da ricordare di una password complessa.
  
La fornitura dell'autenticazione basata sulle smart card per gli utenti con accesso remoto è un metodo affidabile e conveniente che incrementa la protezione della rete. In questa guida sono stati descritti i passaggi necessari per pianificare e implementare questa soluzione.
  
**Download**
  
[Scarica la guida alla pianificazione dell'accesso protetto mediante smart card](http://go.microsoft.com/fwlink/?linkid=41314)
  
**Notifiche di aggiornamento**
  
[Iscriviti per ricevere informazioni su aggiornamenti e nuovi rilasci](http://go.microsoft.com/fwlink/?linkid=54982)
  
**Commenti**
  
[Inviaci i tuoi commenti o suggerimenti](mailto:secwish@microsoft.com?oggetto=guida%20alla%20pianificazione%20dell'accesso%20protetto%20mediante%20smart%20card)
  
[](#mainsection)[Inizio pagina](#mainsection)
