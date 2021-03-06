---
TOCTitle: Note sulla versione di Servizi Windows Rights Management con Service Pack 2
Title: Note sulla versione di Servizi Windows Rights Management con Service Pack 2
ms:assetid: '78067886-681f-49a6-b43d-bfd08a369b69'
ms:contentKeyID: 18824664
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc747637(v=WS.10)'
---

Note sulla versione di Servizi Windows Rights Management con Service Pack 2
===========================================================================

*Data di rilascio: dicembre 2006*

Informazioni preliminari
------------------------

Prima di installare Microsoft® Windows® Rights Management Services (RMS) con Service Pack 2 (SP2), leggere con attenzione le informazioni riportate di seguito. Le informazioni contenute nelle presenti note sulla versione si riferiscono al server RMS con SP2, non al client RMS. Per informazioni sui client RMS, vedere la pagina relativa a RMS all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=68637](http://go.microsoft.com/fwlink/?linkid=68637).

#### Requisiti di sistema

Nella tabella riportata di seguito sono elencati i requisiti hardware per l'esecuzione di RMS con SP2.

###  

 
<table style="border:1px solid black;">
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Requisito</th>
<th style="border:1px solid black;" >Consiglio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">Computer con processore Pentium III (800 MHz o superiore)</td>
<td style="border:1px solid black;">Computer con due processori Pentium 4 (1500 MHz o superiori)</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">256 MB di RAM</td>
<td style="border:1px solid black;">512 MB di RAM</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">20 GB di spazio libero su disco rigido</td>
<td style="border:1px solid black;">40 GB di spazio libero su disco rigido</td>
</tr>
</tbody>
</table>
  
| ![](images/Cc747637.note(WS.10).gif)Nota                                                                           |  
|-------------------------------------------------------------------------------------------------------------------------------------------------|  
| Il server RMS con SP2 è stato progettato per i computer a 32 bit. Se installato in un computer a 64 bit, verrà eseguito in modalità emulazione. |
  
Nella tabella che segue sono elencati i requisiti software per i server che eseguono RMS con SP2.
  
###  

 
<table style="border:1px solid black;">
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Componente</th>
<th style="border:1px solid black;" >Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">Sistema operativo</td>
<td style="border:1px solid black;">Microsoft Windows Server® 2003, ad eccezione di Web Edition, per RMS con SP2.</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Rights Management Services con SP2</td>
<td style="border:1px solid black;">Per aggiornare a RMS con SP2, deve essere già installato RMS con Service Pack 1 (SP1). Questo requisito non si applica al client RMS con SP2.</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">File system</td>
<td style="border:1px solid black;">È consigliabile utilizzare il file system NTFS.</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Componenti richiesti</td>
<td style="border:1px solid black;"><ul>
<li>Accodamento messaggi (detto anche MSMQ) con integrazione del servizio directory Active Directory® abilitata.<br />
<br />
</li>
<li>Internet Information Services (IIS) con ASP.NET abilitato.<br />
<br />
</li>
<li>Microsoft .NET Framework 1.1<br />
<br />
</li>
</ul></td>
</tr>
</tbody>
</table>
 

| ![](images/Cc747637.note(WS.10).gif)Nota                                                                                                                                              |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Se si configura RMS con SP2 in modo da consentire l'amministrazione remota, il computer che si connette al servizio di amministrazione di RMS con SP2 deve utilizzare Internet Explorer 6.0 o versione successiva. |

Nella tabella che segue sono elencati i requisiti di infrastruttura per i server che eseguono RMS con SP2.

###  

 
<table style="border:1px solid black;">
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Componente</th>
<th style="border:1px solid black;" >Requisiti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">Servizi directory</td>
<td style="border:1px solid black;">Active Directory su controller di dominio che eseguono Windows Server 2000 con Service Pack 3 (SP3) o successivo, nello stesso dominio in cui è installato RMS. Tutti gli utenti e i gruppi che utilizzano RMS per acquisire licenze e pubblicare contenuti devono disporre di un indirizzo di posta elettronica configurato in Active Directory.</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Server database</td>
<td style="border:1px solid black;">Il funzionamento di RMS con SP2 richiede database e stored procedure. È possibile utilizzare Microsoft SQL Server™ 2000 con SP3a o versione successiva o Microsoft SQL Server 2005. Per il testing o altre distribuzioni in un unico computer, è possibile utilizzare Microsoft SQL Server Desktop Engine (MSDE 2000) versione A o Microsoft SQL Server 2005 Express Edition.</td>
</tr>
</tbody>
</table>
  
Benché sia progettato e testato per server database con Microsoft SQL Server 2000 e Microsoft SQL Server 2005, RMS può essere eseguito su altri server database, purché questi siano conformi ai seguenti criteri:
  
-   Supporto per le interfacce ADO.NET fornite da Microsoft .NET Framework 1.1.  
-   Compatibilità con Transact-SQL, il linguaggio di query utilizzato da Microsoft SQL Server, poiché gli script di inizializzazione e le stored procedure di RMS utilizzano Transact-SQL.  
-   Supporto per tutte le estensioni specifiche di Microsoft SQL Server.  
-   Risposta alle chiamate di metodo dello spazio dei nomi System.Data.SqlClient di .NET Framework.  
-   Disponibilità di una funzionalità corrispondente dello spazio dei nomi System.Data.SqlClient.  
-   Utilizzo della modalità di autenticazione di Windows.
  
Per verificare se il server database soddisfa i criteri descritti sopra, rivolgersi al fornitore del database.
  
Nella tabella riportata di seguito sono elencati i diritti e le autorizzazioni utente necessari per eseguire diverse attività con RMS.
  
###  

 
<table style="border:1px solid black;">
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Attività</th>
<th style="border:1px solid black;" >Requisiti di account</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">Installazione di RMS</td>
<td style="border:1px solid black;">Utente del dominio con credenziali di amministratore del computer locale</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Provisioning di un cluster principale di RMS</td>
<td style="border:1px solid black;">Utente del dominio con credenziali di amministratore del computer locale e ricerca e scrittura in Active Directory</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Provisioning di un cluster licenze RMS</td>
<td style="border:1px solid black;">Utente del dominio con credenziali di amministratore del computer locale e ricerca in Active Directory</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Provisioning quando si utilizza un nuovo database di configurazione</td>
<td style="border:1px solid black;">Utente del dominio con credenziali di amministratore del computer locale e lettura, scrittura e creazione sul computer che esegue SQL Server</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Provisioning quando si utilizza un database di configurazione già esistente</td>
<td style="border:1px solid black;">Utente del dominio con credenziali di amministratore del computer locale e lettura e scrittura sul computer che esegue il server database</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Amministrazione di RMS</td>
<td style="border:1px solid black;">Utente del dominio con credenziali di amministratore del computer locale</td>
</tr>
</tbody>
</table>
  
| ![](images/Cc747637.note(WS.10).gif)Nota                                                                                                                                                                                                         |  
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| Per ulteriori informazioni sulla configurazione di Windows Server, Active Directory, Accodamento messaggi, IIS e file system, vedere il Windows Server TechCenter all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=78135](http://go.microsoft.com/fwlink/?linkid=78135). |
  
Se si utilizza RMS in una distribuzione su cluster, accertarsi di avere risolto i problemi elencati nella tabella riportata di seguito.
  
###  

 
<table style="border:1px solid black;">
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Condizione</th>
<th style="border:1px solid black;" >Consiglio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">RMS verrà utilizzato su un grande numero di desktop</td>
<td style="border:1px solid black;">Utilizzare Systems Management Server (SMS) o Criteri di gruppo per installare il client RMS con SP2.</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Numero di richieste client elevato</td>
<td style="border:1px solid black;">Utilizzare un server con bilanciamento del carico, il servizio Bilanciamento carico di rete del sistema operativo Windows Server o un bilanciamento del carico hardware per distribuire le richieste nel cluster.</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Due adattatori di rete utilizzano l'indirizzamento IP virtuale per soddisfare le richieste Extranet e Intranet</td>
<td style="border:1px solid black;">Accertarsi che ogni eventuale DNS (Domain Name System) che espone l'indirizzo IP virtuale all'Extranet lo esponga anche all'Intranet.</td>
</tr>
</tbody>
</table>
  
| ![](images/Cc747637.Important(WS.10).gif)Importante                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |  
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| Se la registrazione DNS non viene eseguita per l'Intranet, le richieste interne di licenze client avranno esito negativo. Se risulta impossibile modificare le impostazioni DNS, è possibile modificare la tabella host di ciascun server del cluster in modo da associare l'URL del cluster all'indirizzo IP virtuale del cluster. La registrazione DNS deve essere eseguita prima del provisioning di RMS. Se è già stato eseguito il provisioning del servizio, sarà necessario rimuovere RMS dal server e ripetere il processo di provisioning. |
  
#### Client supportati da questa versione
  
È possibile installare il client RMS senza Service Pack, con SP1 o con SP2 su qualsiasi computer che esegue Microsoft Windows 2000, Windows XP o Windows Server 2003. Le versioni precedenti dei sistemi operativi Windows non sono supportati da questa versione.
  
| ![](images/Cc747637.Caution(WS.10).gif)Attenzione                                                                                                |  
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| Se si utilizza il client RMS senza Service Pack, il client non sarà in grado di utilizzare la pubblicazione in linea a fronte di un server RMS con SP1 o versione successiva. |
  
Modifiche alle funzionalità  
---------------------------
  
RMS con SP2 offre diverse nuove funzionalità:
  
-   [Miglioramenti all'espansione dei gruppi su più insiemi di strutture](#bkmk_cif1)  
-   [Modifiche alla registrazione del database](#bkmk_cif2)  
-   [Maggiori dimensioni dei batch sui server](#bkmk_cif3)  
-   [Compatibilità con Microsoft SQL Server 2005](#bkmk_cif4)
  
<span id="BKMK_CIF1"></span>
#### Miglioramenti all'espansione dei gruppi su più insiemi di strutture
  
#### Descrizione della funzione
  
In RMS l'espansione dei gruppi su più insiemi di strutture facilita la capacità di RMS di espandere l'appartenenza ai gruppi universali di Active Directory in un altro insieme di strutture quando le appartenenze ai gruppi non sono replicate tra due insiemi di strutture. Quando un utente in un insieme di strutture invia del contenuto protetto da RMS a un utente in un altro insieme di strutture, RMS avvia un periodo di individuazione durante il quale verifica che l'utente abbia accesso al contenuto. Il processo di verifica viene eseguito mediante una query LDAP da un insieme di strutture all'altro, allo scopo di trovare il punto di connessione del servizio RMS (SCP) dell'insieme remoto. Dopo aver individuato il SCP dell'insieme remoto, l'account del servizio RMS invia una richiesta alla pipeline di espansione dei gruppi per richiedere all'insieme di strutture remoto se un utente appartiene a un gruppo.
  
#### Destinatari della funzione
  
Questa nuova funzione si rivelerà utile per gli utenti di RMS che lavorano in un ambiente Active Directory con più insiemi di strutture, in cui le appartenenze ai gruppi universali non vengono replicate da un insieme di strutture all'altro.
  
#### Importanza della modifica
  
Il nuovo protocollo di espansione del trust tra insiemi di strutture migliorerà l'affidabilità per gli utenti che distribuiscono un ambiente Active Directory con più insiemi di strutture.
  
#### Differenze nel funzionamento
  
Prima di RMS con SP2, l'espansione dei gruppi su più insiemi di strutture veniva effettuata utilizzando chiamate remote .NET. In questa versione l'espansione dei gruppi su più insiemi di strutture è stata trasformata in un servizio Web ASP.NET, che utilizza richieste SOAP/HTTP alla pipeline di espansione dei gruppi del trust tra insiemi di strutture.
  
| ![](images/Cc747637.note(WS.10).gif)Nota                                                                                                                                                                                                          |  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| Per compatibilità con le versioni precedenti, le chiamate remote .NET sono ancora supportate in RMS con SP2. Tuttavia, per sfruttare appieno il nuovo protocollo di espansione dei gruppi su più insiemi di strutture, tutti i cluster RMS devono eseguire almeno RMS con SP2. |
  
#### Impostazioni aggiunte o modificate in RMS con SP2
  
La nuova pipeline di espansione dei gruppi di RMS è configurata per impostazione predefinita con le impostazioni di massima protezione, in base alle quali l'accesso è consentito solo ai gruppi locali Servizio RMS e Administrators. Per consentire l'accesso a un utente, modificare l'elenco di controllo dell'accesso sulla pipeline di espansione dei gruppi in wwwroot\\\_wmcs\\GroupExpansion\\GroupExpansion.asmx.
  
| ![](images/Cc747637.Important(WS.10).gif)Importante                                                                                                                                                                                                                                                                                                                                                                                                                               |  
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| Verificare che l'account del servizio RMS in ciascun insieme di strutture di Active Directory possa accedere alla pipeline di espansione dei gruppi su ciascuno dei server RMS del cluster. In caso contrario, non sarà possibile eseguire l'espansione dei gruppi. In alternativa, è possibile creare lo stesso account in ciascun insieme di strutture e assegnare la stessa password a tutti gli account. In questo caso sarà necessario aggiungere un solo account alla pipeline di espansione dei gruppi. |
  
In RMS con SP2 sono stati aggiunti nuovi eventi per informare l'utente quando si verificano problemi con messaggi che non raggiungono il servizio Accodamento messaggi. I nuovi registri eventi contengono eventi che avvisano l'utente ogni volta che un messaggio non può essere firmato digitalmente o non può essere convalidato. Alcuni esempi di problemi di convalida sono messaggi con formato non valido o con hash o firme mancanti o non corrette.
  
<span id="BKMK_CIF2"></span>
#### Modifiche alla registrazione del database
  
#### Descrizione della funzione
  
RMS utilizza un servizio listener di registrazione attività che invia tutte le comunicazioni RMS al database di registrazione tramite Accodamento messaggi. Il cluster RMS invia messaggi al servizio Accodamento messaggi e il listener di registrazione attività recupera tali messaggi dalla coda di Accodamento messaggi e li scrive nel database di registrazione.
  
#### Destinatari della funzione
  
Questa funzione sarà utile agli utenti attuali di RMS che utilizzano il servizio listener di registrazione delle attività e ai nuovi utenti di RMS con SP2 che pensano di utilizzare il servizio listener di registrazione delle attività di RMS.
  
#### Importanza della modifica
  
Nelle versioni precedenti di RMS la coda di registrazione di RMS era protetta tramite elenchi di controllo di accesso, ma l'autenticazione non era abilitata. Senza autenticazione, un utente malintenzionato avrebbe potuto scrivere messaggi falsi nella coda di registrazione di RMS.
  
#### Differenze nel funzionamento
  
In RMS con SP2 viene fornita ulteriore autenticazione sui messaggi trasmessi dal cluster RMS tramite Accodamento messaggi. Oltre agli elenchi di controllo di accesso che impediscono l'accesso non autorizzato alla coda di messaggi, la coda di Accodamento messaggi è protetta anche mediante un meccanismo di verifica dell'autenticità dei messaggi. Quando un messaggio viene inviato al servizio Accodamento messaggi, le pipeline di RMS generano un hash del messaggio e lo firmano digitalmente utilizzando la chiave privata del cluster RMS. Il servizio listener di registrazione attività calcola separatamente l'hash del messaggio e lo confronta con quello incluso nel messaggio stesso. Se gli hash corrispondono, il servizio listener di registrazione attività verifica la firma utilizzando la chiave pubblica del cluster e l'hash incluso nel messaggio. Se gli hash corrispondono e la firma viene verificata, il messaggio viene inviato al database di registrazione. Se i passaggi di convalida non vengono completati in modo corretto, il messaggio viene eliminato in modo permanente dalla coda di Accodamento messaggi e un evento di avviso viene scritto nel registro applicazioni nel Visualizzatore eventi.
  
#### Impostazioni aggiunte o modificate in RMS con SP2
  
In RMS con SP2 sono stati aggiunti nuovi eventi per informare l'utente quando si verificano problemi con messaggi che non raggiungono la coda del servizio Accodamento messaggi. I nuovi eventi vengono scritti nel registro applicazioni e comprendono messaggi che non possono essere firmati digitalmente o le cui firme digitali non possono essere convalidate. Alcuni esempi di problemi di convalida sono messaggi con formato non valido o con hash o firme mancanti o non corrette.
  
<span id="BKMK_CIF3"></span>
#### Maggiori dimensioni dei batch sui server
  
#### Descrizione della funzione
  
L'uso dei batch in RMS migliora le prestazioni, consentendo di inviare richieste di più licenze al cluster RMS in una singola richiesta invece di dover inviare una richiesta separata per ciascuna licenza.
  
#### Destinatari della funzione
  
Il supporto per batch di maggiori dimensioni sui server interessa le applicazioni abilitate per RMS che devono acquisire contemporaneamente più licenze per contenuti protetti da RMS.
  
#### Importanza della modifica
  
I batch RMS consentono di inviare una singola richiesta alla pipeline di acquisizione licenze di RMS per ottenere licenze d'uso per più certificati per account con diritti (RAC, Rights Accounts Certificates) in base a una o più licenze di pubblicazione. Se non fossero consentite dimensioni dei batch maggiori di 1, l'applicazione abilitata per RMS dovrebbe richiedere separatamente una licenza d'uso per ciascun utente.
  
#### Differenze nel funzionamento
  
Nelle versioni di RMS precedenti a RMS con SP2, la dimensione massima dei batch supportata dal cluster RMS era 1. Se le dimensioni massime fossero state impostate su un numero maggiore di 1, il cluster le avrebbe ignorate. In RMS con SP2, le dimensioni massime dei batch possono arrivare a 100.
  
| ![](images/Cc747637.note(WS.10).gif)Nota           |  
|---------------------------------------------------------------------------------|  
| Solo la pipeline di acquisizione licenze di RMS supporta le richieste in batch. |
  
La segnalazione degli errori è stata migliorata in RMS con SP2 per tenere conto delle richieste in batch. Se, ad esempio, si invia un batch di dieci richieste e la seconda e terza richiesta hanno esito negativo, verrà registrato un evento per ogni errore.
  
<span id="BKMK_CIF4"></span>
#### Compatibilità con Microsoft SQL Server 2005
  
#### Descrizione della funzione
  
In RMS con SP2 Microsoft SQL Server 2005 può essere utilizzato come server database, per supportare i database di configurazione e di registrazione di RMS senza dover effettuare configurazioni aggiuntive.
  
#### Destinatari della funzione
  
Il supporto per Microsoft SQL Server 2005 in RMS con SP2 sarà utile agli utenti di RMS che desiderano utilizzare Microsoft SQL Server 2005 come database di RMS.
  
#### Importanza della modifica
  
Nelle versioni precedenti di RMS, i tipi di dati di alcuni dei parametri utilizzati nella tabella messaggi di sistema non erano compatibili con la specifica di formato di Microsoft SQL Server 2005. Per ulteriori informazioni, vedere l'articolo 913372 nella Microsoft Knowledge Base all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=68638](http://go.microsoft.com/fwlink/?linkid=68638).
  
#### Differenze nel funzionamento
  
Nelle versioni di RMS precedenti a RMS con SP2, venivano utilizzate dichiarazioni RAISERROR di SQL per avvisare l'utente di RMS dell'errore. La dichiarazione RAISERROR invia una query alla tabella messaggi di sistema per recuperare i messaggi di errore RMS memorizzati in tale tabella. RMS con SP2 impiega una tecnica diversa per propagare gli errori di SQL, che non dipende più dalla tabella messaggi di sistema.
  
| ![](images/Cc747637.note(WS.10).gif)Nota                                                                                                                                                                                                                                                             |  
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| Se si esegue l'aggiornamento da RMS con SP1 a RMS con SP2, non verranno più inviate query relative ai messaggi di errore alla tabella messaggi di sistema, ma i messaggi di errore resteranno nella tabella messaggi di sistema. Un'installazione pulita di RMS con SP2 non aggiunge nuove voci alla tabella messaggi di sistema. |
  
Problemi noti  
-------------
  
Nelle sezioni seguenti sono illustrati i problemi noti di questa versione di RMS.
  
#### La Guida in linea fa ancora riferimento a RMS con Service Pack 1
  
Il file della guida in linea incluso nell'installazione di RMS con SP2 fa ancora riferimento a RMS con SP1. Per informazioni su RMS con SP2, vedere le pagine Web dedicate a Rights Management Services all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=68637](http://go.microsoft.com/fwlink/?linkid=68637).
  
#### Windows Update non installa il client RMS con SP2 su computer basati su x64 o Itanium
  
Se il client RMS o il client RMS con SP1 è installato su un computer basato su x64 e si tenta di aggiornarlo a RMS con SP2 (x64) da Windows Update, l'installazione non riesce. Benché i client RMS precedenti, creati per sistemi a 32 bit, funzionassero sui computer basati su x64, non è possibile aggiornarli al client RMS con SP2. È necessario disinstallare il client RMS precedente e riavviare quindi l'aggiornamento. Windows Update rileva la versione del sistema operativo e offre il client RMS con SP2 appropriato. Lo stesso vale per i computer basati su Itanium.
  
#### Quando si ripete il provisioning, il servizio listener di registrazione attività non viene mai attivato
  
Quando il provisioning del cluster viene annullato, il servizio listener di registrazione attività non lascia il servizio nello stato Arrestato. Per arrestare completamente il servizio è necessario riavviare il computer.
  
#### Non è possibile rimuovere un dominio di pubblicazione trusted non basato su software
  
Dopo avere importato un dominio di pubblicazione trusted con implementazione a chiave privata non basata su software, non è possibile eliminarlo. Evitare di importare una chiave privata non basata su software dalla console di amministrazione RMA di Windows. Rivolgersi al fornitore dell'hardware in uso per informazioni sull'esportazione e l'importazione della chiave privata.
  
#### Microsoft .NET Framework 2.0 modifica le directory principali virtuali di IIS quando viene installato sul server RMS
  
RMS con SP2 utilizza il mapping di script ASP.NET incluso in .NET Framework versione 1.1. Il mapping fornito con le versioni successive non è compatibile con RMS con SP2. Tuttavia, entrambe le versioni possono coesistere senza interferire con altre applicazioni dipendenti. Se sul server sono installati .NET Framework 1.1 e .NET Framework 2.0 o versioni successive, anche se l'installazione e il provisioning di RMS con SP2 sembrano essere stati completati con successo, il cluster RMS potrebbe non funzionare correttamente. Il motivo di questo comportamento deriva dalla necessità di registrare le directory principali virtuali di RMS con il mapping di script ASP.NET versione 1.1 anziché con la versione 2.0. Per registrare le directory principali virtuali di RMS con il mapping di script ASP.NET versione 1.1, eseguire il seguente comando dal prompt dei comandi:
  
**%windir%\\Microsoft.NET\\Framework\\v1.1.4322&gt;aspnet\_regiis.exe -s W3SVC/1/ROOT/\_wmcs**
  
Con l'esecuzione di questo comando, le directory principali virtuali di RMS verranno registrate correttamente e verrà abilitata l'esecuzione di RMS con SP2 sul server.
  
#### L'appartenenza ai gruppi potrebbe risultare mancante se si utilizza il livello di funzionalità nativo di Windows 2000 in Active Directory
  
Quando si distribuisce RMS in un ambiente in cui i livelli dell'infrastruttura di Active Directory sono stati innalzati al livello di funzionalità nativo di Windows 2000, RMS potrebbe non essere in grado di leggere l'attributo memberOf degli oggetti Active Directory quando tenta di espandere l'appartenenza ai gruppi delle liste di distribuzione nascoste. Per consentire a RMS di leggere l'attributo memberOf, l'account del servizio RMS deve utilizzare un account di dominio appartenente al gruppo Accesso compatibile precedente a Windows 2000. Per ulteriori informazioni, vedere l'articolo 812841 della Microsoft Knowledge Base all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=78152](http://go.microsoft.com/fwlink/?linkid=78152).
  
#### Il servizio listener di registrazione attività invia messaggi di Accodamento messaggi alla Coda di messaggi non recapitabili quando il database non è accessibile
  
In alcuni casi il servizio listener di registrazione non riesce a raggiungere il database, ad esempio quando il database è inattivo o si verificano problemi di connettività di rete. In questi casi i messaggi vengono inviati a una Coda messaggi non recapitabili. L'unico modo per recuperare tali messaggi, ossia inviarli al database di registrazione, è utilizzare lo strumento RMS Queue Recovery fornito con RMS Administration Toolkit. Per scaricare RMS Administration Toolkit, visitare il sito all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=33841](http://go.microsoft.com/fwlink/?linkid=33841).
  
| ![](images/Cc747637.note(WS.10).gif)Nota                                                                                                                                                                 |  
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
| Recover e RecoverandPurge sono stati rimossi da LogRecoveryCmd. Questo garantisce che tutti i messaggi vengano reindirizzati attraverso il servizio Accodamento messaggi e autenticati prima dell'invio al database di registrazione. |
  
#### È necessario aggiornare RMS con SP2 prima di aggiornare Microsoft SQL Server 2005
  
Quando si aggiorna a RMS con SP2 e da Microsoft SQL Server 2000 a Microsoft SQL Server 2005, accertarsi di aggiornare per primo RMS. In questo modo si eviteranno eventuali problemi di compatibilità con l'aggiornamento di Microsoft SQL Server.
  
#### RMS con SP2 non esegue il provisioning sui siti Web il cui nome include un apostrofo (')
  
Se si cerca di eseguire il provisioning di RMS con SP2 su un sito Web il cui nome include un apostrofo ('), il processo di provisioning non riuscirà e si concluderà con un messaggio di errore **Parametro non valido**. Per eseguire il provisioning di RMS con SP2 sul sito Web, rimuovere l'apostrofo dal nome del sito.
  
#### Abilitazione di ASP.NET versione 1.1 sui server che eseguono una versione a 64 bit di Windows Server 2003
  
L'argomento "Requisiti di sistema" della Guida di RMS spiega come installare .NET Framework 1.1 e abilitare ASP.NET 1.1 dopo avere installato Internet Information Services (IIS). Se però .NET Framework 1.1 viene installato prima di IIS, ASP.NET 1.1 non sarà riportato tra le estensioni dei servizi Web e la procedura documentata non risulterà quindi utile. Se IIS è stato installato dopo l'installazione di .NET Framework 1.1, eseguire il seguente comando dal prompt dei comandi per abilitare ASP.NET:
  
**%SystemRoot%\\Microsoft.NET\\Framework\\v1.1.4322\\aspnet\_regiis.exe -i –enable**
  
Quando si usa una versione di .NET Framework successiva a 1.1, sostituire **-i** con **-ir** nel comando per evitare di reimpostare gli eventuali mapping di script IIS esistenti.
  
#### È necessario aggiungere l'account del servizio RMS dell'insieme di strutture remoto alla pipeline di espansione gruppi
  
È stato risolto un problema di protezione che rimuove BUILTIN\\users dall'ACL sulla pipeline di espansione gruppi. Questo può causare errori negli scenari di espansione dei gruppi su più insiemi di strutture. Per risolvere questo problema, eseguire la procedura seguente:
  
**Aggiungere l'account del servizio RMS all'insieme di strutture remoto.**  
1.  In Insieme1, dove Insieme1 è il cluster principale di RMS nel primo insieme di strutture, passare a inetpub\\wwwroot\\\_wmcs.
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **GroupExpansion** e selezionare **Proprietà**.
  
3.  Nella finestra **Proprietà GroupExpansion**, fare clic sulla scheda **Protezione** e aggiungere la voce per *Insieme2\\RmsServiceAccount* (ad esempio rmil31\\rmsvc), dove Insieme2 è il cluster principale di RMS nel secondo insieme di strutture.
  
4.  Fare clic su **OK**.
  
5.  Fare clic su **Esegui**, digitare **iisreset** e fare clic su**OK**.
  
#### L'aggiornamento di .NET Framework può provocare perdita di dati
  
Se si aggiorna .NET Framework (CLR) versione 1.1 dopo avere eseguito l'installazione e il provisioning di RMS, le directory principali virtuali verranno impostate in modo da utilizzare .NET Framework versione 2.0. In questa situazione le informazioni non vengono registrate nel database di registrazione, con conseguente perdita di dati. Procedere in uno dei seguenti modi:
  
-   Aggiornare .NET Framework prima di effettuare l'installazione e il provisioning di RMS.  
-   Reimpostare le directory principali virtuali in modo da utilizzare 1.1 dopo l'aggiornamento di .NET Framework.
  
Modifiche alla documentazione in questa versione  
------------------------------------------------
  
Di seguito sono elencati gli argomenti modificati in questa versione:
  
-   Per considerare trusted i certificati degli account con diritti basati su Passport ([http://go.microsoft.com/fwlink/?LinkId=70369](http://go.microsoft.com/fwlink/?linkid=70369))  
-   Requisiti software per RMS ([http://go.microsoft.com/fwlink/?LinkId=70371](http://go.microsoft.com/fwlink/?linkid=70371))  
-   Come distribuire il client RMS ([http://go.microsoft.com/fwlink/?LinkId=70373](http://go.microsoft.com/fwlink/?linkid=70373))  
-   Installazione di RMS dal prompt dei comandi ([http://go.microsoft.com/fwlink/?LinkId=70374](http://go.microsoft.com/fwlink/?linkid=70374))  
-   Tabelle di base del database di configurazione RMS ([http://go.microsoft.com/fwlink/?LinkId=70375](http://go.microsoft.com/fwlink/?linkid=70375))  
-   Tabelle di certificazione del database di configurazione RMS ([http://go.microsoft.com/fwlink/?LinkId=70376](http://go.microsoft.com/fwlink/?linkid=70376))  
-   Tabelle del database di registrazione RMS ([http://go.microsoft.com/fwlink/?LinkId=70377](http://go.microsoft.com/fwlink/?linkid=70377))  
-   Valutazione dei requisiti di scalabilità ([http://go.microsoft.com/fwlink/?LinkId=70378](http://go.microsoft.com/fwlink/?linkid=70378))  
-   Protezione della distribuzione di RMS ([http://go.microsoft.com/fwlink/?LinkId=70379](http://go.microsoft.com/fwlink/?linkid=70379))  
-   Abilitazione del servizio Rimozione autorizzazioni ([http://go.microsoft.com/fwlink/?LinkId=70380](http://go.microsoft.com/fwlink/?linkid=70380))  
-   Pianificazione per utenti RMS esterni [http://go.microsoft.com/fwlink/?LinkId=70381](http://go.microsoft.com/fwlink/?linkid=70381))  
-   Abilitazione del supporto server RMS per i dispositivi mobili e i servizi server ([http://go.microsoft.com/fwlink/?LinkId=70382](http://go.microsoft.com/fwlink/?linkid=70382))
  
#### Copyright
  
*Le informazioni contenute in questo documento rappresentano il punto di vista di Microsoft Corporation sui problemi trattati alla data della pubblicazione. Tuttavia, poiché Microsoft deve reagire alle mutevoli condizioni del mercato, questo non deve essere interpretato come un impegno da parte di Microsoft e, dopo la data della pubblicazione, Microsoft non è in grado di garantire l'accuratezza di alcuna delle informazioni presentate.*
  
*Questo documento viene fornito con soli intenti informativi. MICROSOFT NON FORNISCE ALCUNA GARANZIA, ESPLICITA, IMPLICITA O DI LEGGE, RIGUARDO ALLE INFORMAZIONI CONTENUTE IN QUESTO DOCUMENTO.*
  
*Il rispetto di tutte le leggi applicabili in materia di copyright è esclusivamente a carico dell'utente. Fermi restando tutti i diritti coperti da copyright, nessuna parte di questo documento potrà comunque essere riprodotta o inserita in un sistema di riproduzione o trasmessa in qualsiasi forma e con qualsiasi mezzo (in formato elettronico, meccanico, su fotocopia, come registrazione o altro) per qualsiasi scopo, senza il permesso scritto di Microsoft Corporation.*
  
*Microsoft può essere titolare di brevetti, domande di brevetto, marchi, copyright o altri diritti di proprietà intellettuale relativi all'oggetto del presente documento. Salvo quanto espressamente previsto in un contratto scritto di licenza Microsoft, la consegna del presente documento non implica la concessione di alcuna licenza su tali brevetti, marchi, copyright o altra proprietà intellettuale.*
  
*Salvo quanto altrimenti previsto, ogni riferimento a società, organizzazioni, prodotti, nomi di domini, indirizzi di posta elettronica, logo, persone, luoghi ed eventi utilizzati in esempi è puramente casuale e ha il solo scopo di illustrare l'uso del prodotto Microsoft.*
  
*© 2006 Microsoft Corporation. Tutti i diritti riservati.*
  
*Active Directory, Microsoft, MS-DOS, Visual Studio, Windows, Windows Server, SQL Server e Windows NT sono marchi registrati o marchi commerciali di Microsoft Corporation negli Stati Uniti e/o in altri paesi.*
  
*I nomi di prodotti e società reali citati nel presente documento possono essere marchi dei rispettivi proprietari.*
