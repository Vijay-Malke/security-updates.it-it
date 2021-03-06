---
TOCTitle: Architettura della soluzione di rete LAN senza fili protetta
Title: Architettura della soluzione di rete LAN senza fili protetta
ms:assetid: 'fe7bd1e1-80a7-4c95-b926-cc0ac1a57186'
ms:contentKeyID: 20200855
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Dd536256(v=TechNet.10)'
---

Pianifica la protezione di una LAN wireless con Windows Server 2003 Certificate Services
========================================================================================

### Architettura della soluzione di rete LAN senza fili protetta

##### In questa pagina

[](#eiaa)[Argomenti del modulo](#eiaa)
[](#ehaa)[Obiettivi](#ehaa)
[](#egaa)[Ambito di applicazione](#egaa)
[](#efaa)[Utilizzo del modulo](#efaa)
[](#eeaa)[Progettazione concettuale](#eeaa)
[](#edaa)[Criteri di progettazione della soluzione](#edaa)
[](#ecaa)[Progettazione logica della soluzione](#ecaa)
[](#ebaa)[Riesame dei criteri di progettazione](#ebaa)
[](#eaaa)[Riepilogo](#eaaa)

### Argomenti del modulo

Nel presente modulo la soluzione di rete LAN senza fili (WLAN, Wireless LAN) protetta e basata su 802.1X con EAP-TLS viene descritta a un livello concettuale. Da questa soluzione concettuale, e utilizzando i criteri di progettazione di un'azienda campione, è scaturita una progettazione logica che può essere impiegata come base per l'implementazione di una soluzione per la propria organizzazione.

[](#mainsection)[Inizio pagina](#mainsection)

### Obiettivi

Il modulo consente di:

-   Comprendere i componenti principali di una rete WLAN protetta e le relative modalità di funzionamento.

-   Definire i criteri di progettazione di una soluzione per una rete WLAN protetta.

-   Produrre una progettazione logica coerente per una rete WLAN protetta.

-   Descrivere le modalità di scalabilità della soluzione di rete WLAN.

-   Indicare il modo in cui estendere la progettazione proposta al fine di creare altre soluzioni di accesso alla rete.

[](#mainsection)[Inizio pagina](#mainsection)

### Ambito di applicazione

Questo modulo si applica ai seguenti prodotti e tecnologie:

-   Microsoft® Windows® Server™ 2003

-   Protocollo RADIUS (Remote Authentication Dial-In User Service)

-   Microsoft Windows Internet Authentication Services

-   Servizi certificati Microsoft Windows 2000

-   Hardware di rete 802.1X WLAN

[](#mainsection)[Inizio pagina](#mainsection)

### Utilizzo del modulo

In questo modulo viene fornita una panoramica concettuale delle modalità di progettazione di una soluzione di rete WLAN protetta, basata sulle tecnologie 802.1X con EAP-TLS (Extensible Authentication Protocol-Transport Layer Security). Le soluzioni di progettazione fornite possono essere adattate a situazioni ed esigenze specifiche.

Per sfruttare al massimo il presente modulo:

-   Leggere il modulo "[Scelta di una strategia di rete senza fili protetta](http://technet.microsoft.com/it-it/library/dd536255)", in cui è possibile acquisire una conoscenza più ampia delle modalità di protezione della rete WLAN.

-   Apprendere le nozioni di base relative al protocollo RADIUS: <http://technet.microsoft.com/en-us/library/cc737273.aspx> (in inglese)

-   Apprendere le nozioni di base relative all'infrastruttura PKI (Public Key Infrastructure): <http://www.microsoft.com/windowsserver2003/technologies/pki/default.mspx> (in inglese)

[](#mainsection)[Inizio pagina](#mainsection)

### Progettazione concettuale

Già nel modulo precedente sono stati descritti numerosi punti deboli inerenti alla sicurezza delle reti senza fili. Questi punti deboli vengono, nel migliore dei casi, solo parzialmente eliminati mediante l'uso di tecnologie WEP (Wired Equivalent Privacy) come specificato nello standard IEEE (Institute of Electrical and Electronics Engineers) 802.11. La soluzione proposta deve risolvere il problema in modo tale da garantire la massima protezione delle comunicazioni di rete senza fili. A tal fine, la soluzione ideale deve presentare le seguenti caratteristiche:

-   Autenticazione affidabile dei client senza fili, inclusa l'autenticazione reciproca del client, del punto di accesso (AP, Access Point) senza fili e del server RADIUS.

-   Processo di autorizzazione per identificare gli utenti autorizzati o non autorizzati ad accedere alla rete senza fili.

-   Controllo dell'accesso per consentire l'accesso alla rete ai client autorizzati ed impedirlo a quelli non autorizzati.

-   Crittografia di alto livello del traffico di rete senza fili.

-   Gestione protetta delle chiavi di crittografia.

-   Capacità di recupero da attacchi di negazione del servizio (DoS, Denial of Service).

La combinazione dello standard 802.1X per il controllo degli accessi di rete con un metodo di autenticazione protetto come EAP-TLS, soddisfa alcuni di questi requisiti. Il WEP di alto livello garantisce una crittografia protetta del traffico, ma riduce le funzionalità di gestione delle chiavi. Microsoft, insieme ad altri fornitori, ha sviluppato metodi basati su standard per aumentare la protezione delle chiavi di crittografia WEP durante il processo di autenticazione EAP. Lo standard WPA (WiFi Protected Access) è una raccolta di standard di settore che comprende tutti gli standard appena descritti, più (tra gli altri miglioramenti) un protocollo standardizzato per la gestione delle chiavi, noto come TKIP (Temporal Key Integrity Protocol). L'introduzione di questo protocollo rappresenta un notevole passo avanti per la protezione della rete WLAN ed è stato avallato dalla maggior parte degli analisti.

**Nota:** nessuno dei miglioramenti WPA è in grado di risolvere i punti deboli DoS con tecnologie 802.11 e 802.1X. I punti deboli DoS non sono tanto gravi come quelli WEP, e quasi tutti gli attacchi di questo tipo dimostrati causano solo un'interruzione temporanea. Tuttavia, questo rappresenta ancora un serio problema per alcune organizzazioni ed è improbabile che possa essere risolto prima del rilascio dello standard IEEE 802.11i nel 2004.

Sebbene il sistema operativo Microsoft Windows XP supporti lo standard WPA, al momento della creazione di questa soluzione nessun fornitore di punti di accesso senza fili disponeva di un prodotto commercializzato in grado di supportare tale standard. Di conseguenza, la soluzione è stata realizzata per gestire entrambe le implementazioni di WEP e WPA dinamico. La prima è supportata dalla maggior parte dei fornitori. Relativamente allo scopo di questo modulo di progettazione, i due approcci verranno trattati indistintamente poiché l'uso dell'uno rispetto all'altro non produce nessun impatto significativo sulla progettazione.

Nella seguente figura è illustrato in dettaglio il diagramma concettuale della soluzione scelta (autenticazione 802.1X EAP-TLS).

![](images/Dd536256.SGFG16901(it-it,TechNet.10).jpg "Soluzione concettuale basata sull'autenticazione 802.1X EAP-TLS")

*Figura 1*
*Soluzione concettuale basata sull'autenticazione 802.1X EAP-TLS*

Nel diagramma sono illustrati quattro principali componenti:

-   **Client senza fili**. Si tratta di un computer o una periferica in cui viene eseguita un'applicazione che richiede l'accesso alle risorse di rete. Il client è in grado di crittografare il traffico di rete, di archiviare e scambiare le credenziali in modo protetto (ad esempio chiavi o password).

-   **Punto di accesso senza fili**. Nella terminologia di rete più generica, è noto anche come NAS (Network Access Service). Il punto di accesso senza fili è in grado di implementare le funzioni di controllo dell'accesso per consentire o negare l'accesso alla rete e di crittografare il traffico senza fili. Inoltre dispone dei mezzi per scambiare in modo protetto le chiavi di crittografia con il client al fine di proteggere il traffico di rete. Infine può inviare query a un servizio di autenticazione e di autorizzazione per le decisioni di autorizzazione.

-   **Processo del servizio di autenticazione e autorizzazione di rete (SAAR)**. È in grado di archiviare e verificare le credenziali di utenti validi e di prendere decisioni di autorizzazione in base a un criterio di accesso. Inoltre consente di raccogliere le informazioni di accounting e di controllo sull'accesso client alla rete.

    **Nota:** l'acronimo SAAR non è ufficiale; la scelta di utilizzare questo acronimo in questo modulo è legata solo a motivi di convenienza.

-   **Rete interna**. Si tratta di un'area protetta dei servizi di rete necessaria per l'applicazione client senza fili al fine di ottenere l'accesso.

I numeri riportati in figura illustrano il processo di accesso alla rete, che verrà descritto in dettaglio nella procedura riportata di seguito:

1.  Il client senza fili deve, in un determinato punto, definire le credenziali con un'autorità centrale prima di stabilire l'accesso di rete senza fili. Questa operazione può essere eseguita mediante alcuni strumenti fuori banda, ad esempio un disco floppy oppure una rete cablata o altra rete protetta.

2.  Quando il client richiede un accesso di rete, questo passa le credenziali (o, più precisamente, mostra di possedere le credenziali) al punto di accesso senza fili, il quale le passerà a sua volta al servizio SAAR per richiedere l'autorizzazione.

3.  Il servizio SAAR controlla le credenziali, consulta i relativi criteri di accesso e garantisce o nega l'autorizzazione al client.

4.  Se il client ha ottenuto l'autorizzazione, gli sarà consentito di accedere alla rete e quindi di scambiare in modo protetto le chiavi di crittografia con il punto di accesso senza fili. Queste chiavi vengono attualmente generate dal servizio SAAR e trasmesse al punto di accesso senza fili su un canale protetto. Se il client, invece, non ha ottenuto l'autorizzazione da parte del servizio SAAR, l'accesso gli verrà negato e quindi non potrà stabilire ulteriori comunicazioni.

5.  Utilizzando le chiavi di crittografia, il client e il punto di accesso senza fili stabiliscono una connessione protetta sul collegamento senza fili e quindi viene stabilita una connettività tra il client e la rete interna.

6.  Il client inizia a comunicare con le periferiche sulla rete interna.

Questo processo è illustrato in maniera più dettagliata nel diagramma riportato di seguito.

![](images/Dd536256.SGFG16902(it-it,TechNet.10).jpg "Processo di accesso 802.1X EAP-TLS")

*Figura 2*
*Processo di accesso 802.1X EAP-TLS*

In questo diagramma i singoli componenti vengono illustrati in maniera più dettagliata. Le sezioni successive faranno riferimento a questa figura durante la descrizione di questo processo; tuttavia, per il momento, è necessario porre l'attenzione sui sottocomponenti che appartengono a ciò che questa soluzione definisce con il nome di SAAR: autorità di certificazione (CA, Certification Authority), directory e RADIUS. Sebbene questi sottocomponenti eseguano concettualmente una serie di attività relativamente semplici, per effettuare queste operazioni in modo protetto e in una modalità che sia scalabile, gestibile e affidabile, è necessaria un'infrastruttura di supporto alquanto sofisticata. La maggior parte degli sforzi di pianificazione, implementazione e gestione nei restanti moduli di questa guida vengono impiegati in queste aree.

[](#mainsection)[Inizio pagina](#mainsection)

### Criteri di progettazione della soluzione

Avendo già descritto i concetti di base della soluzione, è necessario approfondire i principali criteri di progettazione per la soluzione. Tali criteri forniranno le istruzioni per convertire la soluzione in una progettazione che possa essere attualmente implementata.

Per eseguire questa operazione, è necessario delineare un profilo dell'organizzazione in cui verrà implementata la soluzione.

#### Organizzazione di destinazione

L'organizzazione descritta in questa sezione è intesa solo a fornire un contesto per i criteri di progettazione. Quando si stabilisce l'idoneità della soluzione per la propria organizzazione, è opportuno valutare se i criteri di progettazione sono validi per la propria azienda e non se la propria azienda appare come quella ivi descritta.

L'organizzazione di destinazione ha distribuito una rete WLAN in alcune sedi in modo da ridurre i costi di infrastruttura di rete ed aumentare la mobilità e la produttività del personale. Essa è consapevole delle esigenze inerenti alla protezione e ha già distribuito una quantità di tecnologie per il miglioramento della protezione IT, ad esempio l'autenticazione di dominio, i firewall Internet, i programmi antivirus e una soluzione di accesso remoto o VPN. Ha già sviluppato piani a lungo termine al fine di utilizzare numerose altre applicazioni altamente protette (come ad esempio la crittografia dei file e la posta elettronica protetta).

La struttura di rete logico-fisica di questa organizzazione può somigliare a quella raffigurata nel seguente diagramma (in una forma estremamente semplificata).

![](images/Dd536256.SGFG16903(it-it,TechNet.10).jpg "Diagramma schematico della struttura fisica e della rete dell'organizzazione di destinazione.")

*Figura 3*
*Diagramma schematico della rete e della struttura fisica dell'organizzazione di destinazione*

Sebbene nel diagramma siano raffigurati solo due filiali, rispettivamente di grandi e piccole dimensioni, in realtà potrebbero esistere diversi uffici di questo tipo. Per maggiore chiarezza, nell'esempio è riportato solo un piccolo numero di server e client e questo non vuole essere in alcun modo indicativo delle dimensioni dell'organizzazione.

Entro certi limiti, le dimensioni dell'organizzazione di destinazione hanno relativamente scarso impatto sui criteri di progettazione della soluzione. All'estremità più piccola della scala, la sede centrale può ospitare alcune centinaia di dipendenti e possedere piccole filiali con decine di dipendenti. All'estremità più grande della scala, la sede centrale può ospitare migliaia di dipendenti e possedere uffici periferici con centinaia di dipendenti. Le due organizzazioni illustrate in figura presentano filiali più piccole con un numero non elevato di dipendenti.

#### Requisiti dell'organizzazione

Un'organizzazione, come quella ivi descritta, dispone generalmente dei requisiti riportati di seguito:

-   Maggiore protezione della rete WLAN per eliminare o ridurre notevolmente i seguenti rischi:

    -   Intrusi che intercettano le trasmissioni di dati attraverso la rete WLAN.

    -   Intrusi che intercettano e modificano le trasmissioni di dati attraverso la rete WLAN.

    -   Intrusi o altri utenti non autorizzati che si collegano alla rete WLAN introducendo virus o altro codice dannoso sulla rete interna.

    -   Attacchi di negazione del servizio (DoS, Denial of Service) a livello di rete (e non a livello di trasmissione radio).

    -   Intrusi che eseguono il piggyback sulla rete aziendale WLAN per ottenere l'accesso a Internet.

-   Le misure di protezione non devono in alcun modo influire sull'utilizzabilità della rete o indurre un aumento significativo delle chiamate all'helpdesk.

-   I costi di distribuzione e di gestione continuativa devono essere sufficientemente bassi da essere giustificabili per un numero relativamente piccolo di utenti di rete WLAN (meno del 10% della forza lavoro) che utilizzano questa soluzione.

-   La progettazione deve supportare una vasta gamma di client e periferiche.

Oltre a questi requisiti esiste un numero di requisiti tecnici più generali:

-   Capacità di recupero in caso di guasti a singoli componenti.

-   Scalabilità per gestire livelli di utilizzo più elevati in futuro (oltre il 100% della forza lavoro esistente per consentire l'espansione); il costo per supportare un numero maggiore di utenti deve essere minimo o almeno proporzionale all'espansione richiesta.

-   Riutilizzabilità dei componenti, se possibile, la soluzione deve riutilizzare l'infrastruttura esistente e qualsiasi nuovo componente introdotto dalla soluzione deve poter essere riutilizzato in progetti futuri.

-   Facile gestione mediante l'uso dell'infrastruttura di gestione e di controllo esistente (dove possibile).

-   Funzioni di recupero in caso di danni irreversibili (ad esempio, ripristinando i backup su hardware alternativo).

-   Conformità ai protocolli e ai formati standard di settore e, laddove non esistono standard, visibilità di un chiaro percorso verso standard futuri.

-   Protezione affidabile (compreso l'aggiornamento regolare) per le credenziali e le chiavi utilizzate nella soluzione.

-   Informazioni di controllo totale per la registrazione utente e l'accesso client alla rete.

#### Criteri di progettazione della soluzione

Da questi requisiti, è possibile determinare i criteri riportati nella seguente tabella per supportare la progettazione della soluzione.

**Tabella 1. Criteri di progettazione della soluzione**

 
<table style="border:1px solid black;">
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Fattore di progettazione</th>
<th style="border:1px solid black;" >Criteri</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">Protezione</td>
<td style="border:1px solid black;">- Autenticazione e autorizzazione affidabile dei client senza fili<br />
- Controllo dell'accesso affidabile per consentire o negare rispettivamente ai client autorizzati o non autorizzati l'accesso alla rete<br />
- Crittografia di alto livello del traffico di rete senza fili<br />
- Gestione protetta delle chiavi di crittografia<br />
- Capacità di recupero da attacchi di negazione del servizio (DoS, Denial of Service)</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Scalabilità</td>
<td style="border:1px solid black;">Progettazione di base con scalabilità crescente e decrescente per adattarsi alle diverse dimensioni aziendali</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Utenti supportati min./max.</td>
<td style="border:1px solid black;">500/15.000+ utenti WLAN - 500/15,000+ utenti certificati</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Numero di siti supportati</td>
<td style="border:1px solid black;">- Siti di grandi dimensioni, con controller del dominio di autenticazione locale e IAS (Microsoft Internet Authentication Service), supportati con capacità di recupero in caso di guasti alla rete WAN (Wide Area Network)<br />
- Siti di piccole dimensioni multipli supportati senza capacità di recupero in casi di guasti alla rete WAN</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Riutilizzo dei componenti (uso dell'infrastruttura esistente)</td>
<td style="border:1px solid black;">Utilizzo di Active Directory, dei servizi di rete e dei client Windows XP</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Riutilizzo dei componenti (utilizzabilità da parte delle applicazioni future)</td>
<td style="border:1px solid black;">- Supporto per altre applicazioni di accesso alla rete (accesso alla rete VPN e alla rete cablata 802.1X) mediante l'infrastruttura di autenticazione<br />
- Supporto per una varietà di applicazioni, EFS (Encrypting File System) e VPN, mediante l'infrastruttura di certificazione</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Disponibilità</td>
<td style="border:1px solid black;">Capacità di recupero in caso di guasto a singoli componenti o al collegamento di rete</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Espansione</td>
<td style="border:1px solid black;">- Espandibile per supportare capacità e standard futuri (ad esempio, 802.11i, WPA, 802.11a per WLAN)<br />
- Infrastruttura dei Servizi certificati espandibile per supportare gli usi più frequenti dei certificati a chiavi pubbliche (posta elettronica protetta, accesso con smart card, firma del codice, protezione del servizio Web e così via)</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Facilità di gestione</td>
<td style="border:1px solid black;">Integrazione con le soluzioni di gestione aziendale esistenti (comprende il controllo del sistema e del servizio, il backup, la gestione della configurazione e così via)</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Struttura dell'organizzazione IT</td>
<td style="border:1px solid black;">Scelta del reparto IT centralizzato (almeno cinque ma generalmente 20-30 persone)</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Conformità agli standard</td>
<td style="border:1px solid black;">Adesione ai principali standard correnti e chiaro percorso di migrazione verso i principali standard futuri</td>
</tr>
</tbody>
</table>
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Progettazione logica della soluzione
  
In questa sezione viene descritta la progettazione logica e logico-fisica della soluzione. Questa presenta le specifiche e il posizionamento dei componenti attuali, sebbene non vengano trattati i dettagli della progettazione fisica, come ad esempio le specifiche hardware del server.
  
#### Analisi della progettazione concettuale
  
Il seguente diagramma è già stato illustrato precedentemente all'interno di questo modulo. Nella seguente sezione verranno esaminati i diversi componenti riportati in figura e le relative modalità di raggruppamento all'interno della progettazione complessiva.
  
![](images/Dd536256.SGFG16904(it-it,TechNet.10).jpg "Vista concettuale del processo di accesso alla rete")
  
*Figura 4*  
*Vista concettuale del processo di accesso alla rete*
  
#### Progettazione logica
  
Il raggruppamento dei componenti, così come illustrato nel diagramma precedente, è significativo se si intende comprendere il processo di accesso alla rete WLAN. Tuttavia, per produrre una progettazione logica che sia modulare e che semplifichi l'implementazione, è consigliabile raggruppare i componenti in base alle modalità di distribuzione dei servizi IT richiesti in modo che siano relativamente indipendenti gli uni dagli altri.
  
Il raggruppamento dei componenti scelto consente di esaminare l'intera progettazione in maniera modulare per un riutilizzo ottimale di tali componenti. Ad esempio, il componente PKI potrebbe essere implementato semplicemente come un mezzo di autenticazione degli utenti di rete WLAN. Tuttavia, questo potrebbe limitare la riutilizzabilità del componente PKI per altre applicazioni. Allo stesso modo, il componente RADIUS deve essere progettato nella prospettiva di ciò che le altre applicazioni potrebbero richiedere per eventuali usi futuri. Ovviamente questo implica dei costi e le esigenze di modularità e di riutilizzo non devono avere la precedenza sul valore commerciale della soluzione.
  
I servizi IT presenti nella progettazione verranno combinati nei seguenti gruppi logici:
  
-   Componenti WLAN: client e punti di accesso senza fili
  
-   Componente RADIUS
  
-   Componente PKI: Autorità di certificazione
  
-   Componente dei servizi di infrastruttura
  
Quest'ultimo componente, che comprende una directory e servizi di rete di supporto, è costituito da servizi IT che in genere già esistono nell'organizzazione, ma con cui la soluzione in qualche modo interagisce.
  
![](images/Dd536256.SGFG16905(it-it,TechNet.10).jpg "Progettazione logica della soluzione di rete WLAN protetta")
  
*Figura 5*  
*Progettazione logica della soluzione di rete WLAN protetta*
  
##### Progettazione logico-fisica
  
A livello logico-fisico, una progettazione può essere attualmente sviluppata in modo da illustrare come questi componenti verranno implementati come server fisici, come verranno collegati tra loro e come verranno distribuiti tra i diversi siti dell'organizzazione di destinazione. Tuttavia, sebbene i numeri di server riportati nei seguenti diagrammi sono generalmente corretti, essi sono semplicemente a scopo illustrativo. La definizione finale dei numeri di server e del posizionamento verrà discussa più avanti all'interno di questa guida nei moduli di pianificazione dettagliata.
  
**Sedi centrali**
  
Nel seguente diagramma viene illustrata l'implementazione del server nella sede centrale. Solo i tre componenti riportati nella parte superiore della figura rappresentano i nuovi server o i componenti che devono essere acquistati. I componenti dei servizi di infrastruttura generalmente già esistono nella maggior parte delle organizzazioni. Se l'organizzazione ha già distribuito l'apparecchiatura di rete WLAN in grado di supportare la tecnologia 802.1X, il componente di rete WLAN potrebbe anche già esistere e quindi non richiedere nuovi acquisti.
  
![](images/Dd536256.SGFG16906(it-it,TechNet.10).jpg "Implementazione del server nella sede centrale")
  
*Figura 6*  
*Implementazione del server nella sede centrale*
  
**Filiale di grandi dimensioni**
  
Nel seguente diagramma è illustrata la struttura fisica di una filiale di grandi dimensioni, che si distingue dalla filiale di piccole dimensioni in quanto dispone di un controller di dominio locale. All'ufficio remoto viene distribuito un solo server IAS. Sebbene sia raffigurato come un server separato, può essere eseguito come un servizio del controller di dominio.
  
**Nota:** se il collegamento WAN alla sede centrale è affidabile (vale a dire che esistono collegamenti di rete ridondanti) e non eccessivamente congestionato, la filiale di grandi dimensioni potrà utilizzare i servizi RADIUS della sede centrale e quindi evitare di averne dei propri. Questo argomento verrà discusso più avanti nel modulo "[Progettazione di un'infrastruttura RADIUS per la protezione di reti LAN senza fili](http://technet.microsoft.com/it-it/library/dd536258)" di questa guida.
  
Tutti gli altri servizi (ad esempio, i servizi CA) vengono forniti dalla sede centrale.
  
![](images/Dd536256.SGFG16907(it-it,TechNet.10).jpg "Struttura fisica di una filiale di grandi dimensioni")
  
*Figura 7*  
*Struttura fisica di una filiale di grandi dimensioni*
  
**Filiale di piccole dimensioni**
  
La filiale di piccole dimensioni può disporre o meno di alcune tecnologie informatiche (IT) locali, ad esempio, un file server e una stampante, ma generalmente non dispone di un'infrastruttura di autenticazione. La filiale di piccole dimensioni non verrà illustrata all'interno di questo documento poiché non dispone di un'infrastruttura di server installata. Alcune organizzazioni ritengono che questi uffici non richiedano o giustifichino alcun servizio WLAN. Per altre organizzazioni, invece, la flessibilità di utilizzare uffici temporanei, senza che sia necessario installare e gestire cavi di rete, rappresenta una prospettiva interessante.
  
Se i servizi WLAN sono necessari per gli uffici di piccole dimensioni che non dispongono di un controller di dominio locale, i punti di accesso senza fili locali si baseranno sullo IAS e sull'infrastruttura di autenticazione di dominio presenti nelle sedi centrali. Il problema principale è che la connettività di rete WLAN andrà persa se si verifica un guasto al collegamento WAN alla sede centrale. Questo problema può essere risolto con costi aggiuntivi fornendo una ridondanza WAN, sebbene non esista una facile soluzione a questo scenario. È opportuno ricordare che se i client perdono l'accesso a un controller di dominio, questi non potranno in nessun caso ottenere l'autenticazione ad accedere alle risorse locali o remote.
  
Un'alternativa meno sicura è quella di distribuire i punti di accesso senza fili che supportano il WEP statico e lo scambio di chiavi. Queste funzionalità del punto di accesso senza fili sono specifiche per il fornitore; tuttavia consentono di migliorare la protezione del WEP statico e tra l'altro possono funzionare senza un server RADIUS.
  
##### Strategia di scalabilità
  
Uno dei principali criteri di progettazione era rappresentato dalla scalabilità. La soluzione deve essere in grado di supportare implementazioni di diverse dimensioni a costi adeguati al tipo di implementazione (vale a dire che un'implementazione di 500 utenti deve avere un costo proporzionalmente inferiore a quella di 5000 utenti). La complessità dell'implementazione e della gestione deve essere anche conforme al tipo di organizzazione.
  
**Organizzazione di grandi dimensioni**
  
Nel seguente diagramma sono illustrate le modalità di scalabilità della progettazione in maniera crescente in modo da poter ospitare un elevato numero di utenti sia nella sede centrale che nelle filiali di grandi dimensioni. Inoltre è probabile che i server IAS utilizzeranno altre applicazioni di rete, come ad esempio VPN. Per ulteriori informazioni, consultare la sezione "Facilità di estensione della progettazione" di questo modulo. L'esatta struttura dei server dovrà quindi essere definita considerando questi aspetti. Gli altri server IAS proxy RADIUS verranno mostrati solo a scopo illustrativo.
  
I server richiesti per la versione con scalabilità crescente della soluzione sono mostrati in grigio.
  
![](images/Dd536256.SGFG16908(it-it,TechNet.10).jpg "Illustrazione della strategia con scalabilità crescente")
  
*Figura 8*  
*Illustrazione della strategia con scalabilità crescente*
  
**Organizzazione di piccole dimensioni**
  
Per le organizzazioni di piccole dimensioni, la soluzione può essere implementata con una numero contenuto di nuovi componenti hardware e software. Questo risultato si ottiene combinando il servizio IAS con i controller di dominio esistenti. Tale soluzione è stata già ampiamente collaudata ed è consigliata per numerosi scenari. Nel seguente diagramma è illustrata questa variante della progettazione.
  
![](images/Dd536256.SGFG16909(it-it,TechNet.10).jpg "Illustrazione della strategia con scalabilità decrescente")
  
*Figura 9*  
*Illustrazione della strategia con scalabilità decrescente*
  
Il componente RADIUS è ancora illustrato come un elemento logicamente separato (in modo da poter effettuare un confronto con la struttura del diagramma precedente), anche se è ora implementato come un processo sui controller di dominio già esistenti. Tuttavia i server richiesti in questa versione della soluzione sono server CA e sono raffigurati in grigio.
  
#### Facilità di estensione della progettazione
  
Un altro criterio chiave della progettazione è la riutilizzabilità dei componenti in applicazioni future. I componenti RADIUS e PKI possono essere riutilizzati per fornire l'autenticazione e altri servizi di protezione per una varietà di applicazioni.
  
##### Rete LAN senza fili per l'accesso guest
  
Alcune organizzazioni potrebbero decidere di consentire l'accesso non autenticato a parti limitate delle reti senza fili messe a disposizione dei clienti o dei consulenti che visitano gli edifici aziendali. Sebbene questa funzionalità non sia inclusa in questa soluzione, la progettazione può essere configurata in modo da consentire l'accesso alle diverse reti WLAN a seconda delle credenziali del client (se esistenti) presentate. Questo consente ai visitatori di accedere ad una rete WLAN non protetta al di fuori del firewall aziendale, attraverso cui viene fornito l'accesso a Internet e la possibilità di collegarsi alla propria organizzazione.
  
Un altro utilizzo in relazione alla rete VLAN con accesso guest è quello di abilitare nuovi client ad acquisire credenziali (ad esempio, per registrare un certificato) senza doversi collegare ad una rete cablata. Ovviamente, questo presuppone l'esistenza di un'autenticazione sufficientemente dettagliata e di un meccanismo di accesso in grado di controllare a chi sia consentito o meno acquisire le credenziali, ma tale argomento esula dallo scopo di questo documento.
  
##### Altri servizi di accesso alla rete
  
La progettazione RADIUS utilizzata in questa soluzione può fornire servizi di autenticazione, autorizzazione e rilevazione account per altri server di accesso alla rete, come l'autenticazione di rete cablata con standard 802.1X e l'autenticazione di accesso remoto e VPN.
  
**Autenticazione di rete cablata 802.1X**
  
L'applicazione più semplice, che non richiede alcuna modifica della progettazione RADIUS di base, è l'autenticazione cablata 802.1X. Le organizzazioni dotate di un'infrastruttura di rete cablata ampiamente distribuita potrebbero incontrare delle difficoltà nel controllare l'uso non autorizzato della rete aziendale. Ad esempio, è spesso difficile evitare che i visitatori si colleghino ai computer portatili o che i dipendenti aggiungano computer non autorizzati alla rete. Alcune parti della rete, ad esempio i centri dati, possono essere designate come zone altamente protette. Su queste reti sono consentite solo periferiche autorizzate, escludendo persino i dipendenti con computer aziendali.
  
Nel seguente diagramma è illustrata la modalità di integrazione della soluzione di accesso alla rete cablata con la progettazione. Il riquadro in grigio, che indica i componenti cablati 802.1X, e i riquadri in bianco, che contengono i principali servizi, sono illustrati nel precedente diagramma della progettazione.
  
![](images/Dd536256.SGFG16910(it-it,TechNet.10).jpg "Utilizzo dell'autenticazione cablata 802.1X")
  
*Figura 10*  
*Utilizzo dell'autenticazione cablata 802.1X*
  
Gli switch di rete in grado di supportare la tecnologia 802.1X svolgono un ruolo identico a quello dei punti di accesso senza fili all'interno della soluzione e possono sfruttare la stessa infrastruttura RADIUS per autenticare i client e autorizzare in modo selettivo l'accesso al segmento di rete appropriato. Questo include gli ovvi vantaggi della centralizzazione della gestione degli account nella directory aziendale, lasciando i criteri di accesso alla rete ancora sotto il controllo dell'amministratore di sicurezza della rete.
  
Un altro vantaggio derivante dall'uso del componente RADIUS (in particolare di IAS) consiste nella capacità di utilizzare i criteri di quarantena. Questa prevede l'esecuzione dei controlli sul client al momento della connessione (per garantire, ad esempio, che il client disponga di software antivirus aggiornati o che esegua versioni di sistemi operativi approvati dall'azienda) e la presa di decisioni sulla base di questi controlli. Quindi è possibile che a un utente o a un computer autorizzato venga negato l'accesso al fine di proteggere la rete da eventuali pericoli.
  
**Autenticazione della connessione remota e VPN**
  
Un altro servizio di accesso alla rete che potrebbe utilizzare i componenti RADIUS è la connessione remota e VPN. In particolare nelle organizzazioni di grandi dimensioni, è probabile che sia necessario apportare delle aggiunte alla progettazione, come ad esempio l'aggiunta di proxy RADIUS. La struttura di questa soluzione estesa è illustrata nel seguente diagramma.
  
![](images/Dd536256.SGFG16911(it-it,TechNet.10).jpg "Estensione del componente RADIUS per il supporto del server VPN")
  
*Figura 11*  
*Estensione del componente RADIUS per il supporto del server VPN*
  
I server VPN di questa soluzione svolgono lo stesso ruolo NAS dei punti di accesso senza fili all'interno della progettazione. Questi passano le richieste di autenticazione dei client all'infrastruttura RADIUS. Sebbene sia possibile far passare le richieste RADIUS direttamente ai server IAS interni, è più sicuro utilizzare un livello proxy RADIUS per inoltrare le richieste ai server IAS interni.
  
Questa soluzione ha il vantaggio di sfruttare l'infrastruttura esistente e di centralizzare la gestione degli account, lasciando il controllo dei criteri di accesso ancora sotto la supervisione dell'amministratore di protezione della rete. Alla strategia di protezione globale fornita dalla soluzione vengono aggiunti ulteriori miglioramenti, ad esempio la richiesta dell'autenticazione utente basata sulla smart card e la messa in quarantena dei client. Microsoft utilizza una configurazione molto simile per il proprio personale interno affinché venga garantito loro un collegamento protetto alla rete aziendale.
  
L'accesso remoto funziona allo stesso modo del NAS, se si utilizzano le funzionalità di RRAS (Routing and Remote Access Service) del server remoto, anziché le funzionalità VPN.
  
##### Applicazioni PKI
  
Poiché i criteri di riutilizzabilità e di espansione sono considerati molto importanti, il componente PKI è stato progettato in modo da poter essere utilizzato in futuro per diverse applicazioni di protezione. Come verrà descritto nel modulo successivo, la progettazione del componente PKI rappresenta pertanto una strategia, da un lato, di riduzione dei costi e della complessità come parte di una soluzione senza fili protetta e, dall'altro lato, di mantenimento della flessibilità, in modo tale da essere utilizzata come base per altre applicazioni future.
  
Nel seguente diagramma vengono illustrate alcune delle applicazioni supportabili dal componente PKI, insieme all'applicazione senza fili protetta. Alcune di esse sono applicazioni relativamente semplici e possono utilizzare il componente PKI sviluppato in questa soluzione con qualche lieve cambiamento alla progettazione. Altre, come ad esempio la posta elettronica protetta e l'accesso con smart card, sono più complesse e quasi certamente richiedono una maggiore considerazione e un'estensione della soluzione PKI.
  
![](images/Dd536256.SGFG16912(it-it,TechNet.10).jpg "Applicazioni PKI")
  
*Figura 12*  
*Applicazioni PKI*
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Riesame dei criteri di progettazione
  
Prima di chiudere il modulo, è opportuno riesaminare i criteri di progettazione per verificare fino a che punto la progettazione proposta rispetta gli obiettivi definiti precedentemente. Tali criteri vengono riepilogati nell'elenco riportato di seguito. Molti di questi elementi verranno trattati in maniera dettagliata nei moduli di progettazione successivi.
  
-   **Protezione**. La progettazione include un'autenticazione, un'autorizzazione e un controllo dell'accesso affidabili. La crittografia di alto livello (128 bit) è una funzione dei componenti hardware di rete ed è supportata sulla maggior parte delle periferiche attualmente disponibili. La gestione della protezione delle chiavi di crittografia viene fornita da una combinazione del client 802.1X Microsoft, del punto di accesso senza fili con 802.1X abilitato e del server RADIUS.  
    La capacità di recupero dagli attacchi di negazione del servizio (DoS, Denial of Service) è una delle aree in cui c'è ancora molto da lavorare. Gli standard di settore attuali (fino all'avvento della tecnologia 802.11i) sono ancora vulnerabili ad una varietà di attacchi DoS normalmente non distruttivi (vale a dire, non permanenti).
  
-   **Scalabilità**. La progettazione di base si adatta ad una vasta gamma di organizzazioni, a costi ridotti, da poche centinaia a molte migliaia di utenti. La progettazione è flessibile anche relativamente alla struttura geografica e della rete. Gli uffici di piccole dimensioni senza controller di dominio locale dipendono dall'affidabilità della rete WAN o da una soluzione di protezione di livello inferiore.
  
-   **Riutilizzo dei componenti (uso dell'infrastruttura esistente)**. La progettazione utilizza il servizio Microsoft Active Directory® e molti servizi di rete esistenti, ad esempio DHCP (Dynamic Host Configuration Protocol) e DNS (Domain Name System).
  
-   **Riutilizzo dei componenti (utilizzabilità dalle applicazioni future)**. La progettazione IAS è pronta per l'uso oppure può essere estesa per supportare altre applicazioni di accesso alla rete (ad esempio accesso VPN, accesso alla rete cablata 802.1X e accesso remoto); il componente PKI è allo stesso modo capace di supportare applicazioni semplici, come EFS, ma pone le basi per applicazioni più complesse, come l'accesso con smart card.  
    Questo elemento copre anche i criteri di **espansione**.
  
-   **Disponibilità**. La soluzione è dotata di capacità di recupero in caso di guasti a singoli componenti o al collegamento di rete per la sede centrale e per tutti gli uffici periferici in cui può essere distribuito un server RADIUS. Gli uffici di piccole dimensioni sono vulnerabili ad eventuali guasti della rete WAN.
  
-   **Facilità di gestione**. La facilità di gestione della soluzione non è un elemento importante nella progettazione; tuttavia, questo criterio dovrà essere preso in considerazione successivamente nella progettazione dell'infrastruttura operativa per garantire che il sistema venga gestito in maniera ottimale.
  
-   **Struttura dell'organizzazione IT**. Per la distribuzione e la gestione di una soluzione di questo tipo è essenziale avere un minimo di esperienza nel reparto IT dell'organizzazione.
  
-   **Conformità agli standard**. La soluzione è conforme, dove possibile, agli standard di settore e ufficiali attuali. Questo criterio assume particolare importanza nell'area della protezione della rete WLAN dove la soluzione è basata sulle tecnologie 802.1X, EAP-TLS e WEP o WPA a 128 bit. Microsoft recentemente ha annunciato un servizio di supporto per il WPA per Windows XP, offrendo standard di protezione della rete WLAN di alto livello. La progettazione supporterà sia il WPA che il WEP dinamico.
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Riepilogo
  
In questo modulo è stata esaminata la progettazione concettuale di una soluzione 802.1X con EAP-TLS e sono stati illustrati i componenti chiave a livello di architettura. Inoltre è stata descritta anche la struttura dell'organizzazione di destinazione per questa soluzione, nonché i criteri di progettazione utilizzati per realizzare la soluzione.
  
I criteri di progettazione sono stati quindi utilizzati per tradurre la progettazione concettuale in una progettazione logica della soluzione. Questo ha richiesto una panoramica delle opzioni di implementazione per la scalabilità verso le diverse esigenze e dimensioni dell'organizzazione, estendendo la progettazione di base in modo da fornire supporto per le altre applicazioni di protezione e di acceso alla rete. Infine sono stati riesaminati i principali criteri di progettazione in relazione alla progettazione proposta. Quest'analisi può essere utilizzata come base di partenza per il resto della *Guida alla pianificazione*.
  
I successivi tre moduli analizzano in dettaglio la progettazione per ciascuno dei principali componenti della soluzione, il PKI, l'infrastruttura RADIUS e la progettazione di una rete WLAN protetta.
  
[](#mainsection)[Inizio pagina](#mainsection)
