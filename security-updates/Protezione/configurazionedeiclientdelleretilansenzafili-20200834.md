---
TOCTitle: Configurazione dei client delle reti LAN senza fili
Title: Configurazione dei client delle reti LAN senza fili
ms:assetid: 'ae4d02fb-303a-4c91-90c1-036c52edfd7c'
ms:contentKeyID: 20200834
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Dd536235(v=TechNet.10)'
---

Protezione delle reti LAN senza fili con PEAP e password
========================================================

### Capitolo 6: Configurazione dei client delle reti LAN senza fili

Aggiornato: 2 aprile 2004

##### In questa pagina

[](#ehaa)[Cenni preliminari](#ehaa)
[](#egaa)[Prima di iniziare](#egaa)
[](#efaa)[Operazioni preliminari per l'implementazione](#efaa)
[](#eeaa)[Autorizzazioni di accesso alla rete WLAN per utenti e computer](#eeaa)
[](#edaa)[Configurazione client WLAN per Windows XP](#edaa)
[](#ecaa)[Configurazione dei client Pocket PC 2003](#ecaa)
[](#ebaa)[Riepilogo](#ebaa)
[](#eaaa)[Riferimenti](#eaaa)

### Cenni preliminari

In questo capitolo viene descritto come configurare e distribuire le impostazioni di rete per i client della rete LAN senza fili (WLAN) e come connettere i client alla rete WLAN. Inoltre, sono incluse le procedure per connettere Microsoft® Windows® XP (Professional e Tablet Edition) e i client Pocket PC 2003 alla rete WLAN.

Nel capitolo, inoltre, vengono fornite informazioni dettagliate per verificare l'appartenenza ai gruppi di protezione di utenti e computer della rete WLAN, configurare le impostazioni della rete WLAN mediante l'utilizzo dei criteri di gruppo per i client Windows XP ed eseguire le procedure per la configurazione dei client Pocket PC.

[](#mainsection)[Inizio pagina](#mainsection)

### Prima di iniziare

Oltre ai prerequisiti descritti nel capitolo 3, "Predisposizione dell'ambiente", è richiesta la conoscenza dei seguenti argomenti:

-   Installazione dei driver e configurazione di Windows XP.

-   Configurazione e utilizzo di Pocket PC 2003.

È necessario esaminare e implementare le istruzioni fornite nel capitolo 3 "Predisposizione dell'ambiente", nel capitolo 4 "Creazione dell'autorità di certificazione della rete" e nel capitolo 5 "Creazione dell'infrastruttura di protezione per LAN senza fili". È inoltre necessario leggere le informazioni di progettazione e pianificazione fornite nel capitolo 2 "Pianificazione dell'implementazione della protezione di reti LAN senza fili" nonché comprendere l'architettura e la progettazione della soluzione.

[](#mainsection)[Inizio pagina](#mainsection)

### Operazioni preliminari per l'implementazione

Per eseguire le procedure di configurazione dei criteri di gruppo incluse nel presente capitolo, è necessario accedere con un account che sia membro del gruppo degli amministratori del dominio in cui si esegue la configurazione delle impostazioni della rete WLAN. Per impostazione predefinita, l'account Administrator del dominio è un membro del gruppo, tuttavia è possibile utilizzare qualsiasi altro account appartenente allo stesso gruppo.

Per eseguire le procedure di verifica su un computer client Windows XP è necessario essere membri del gruppo Administrators locale.

#### Strumenti necessari

Nella tabella riportata di seguito sono elencati gli strumenti richiesti per implementare le procedure incluse nel capitolo.

**Tabella 6.1: Strumenti necessari**

 
<table style="border:1px solid black;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Strumento</th>
<th style="border:1px solid black;" >Descrizione</th>
<th style="border:1px solid black;" >Origine</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;"><strong>Console gestione criteri di gruppo</strong></td>
<td style="border:1px solid black;">Strumento di gestione avanzata per l'importazione e l'esportazione degli oggetti Criteri di gruppo.</td>
<td style="border:1px solid black;">Le istruzioni per l'installazione sono incluse nel capitolo 3, &quot;Predisposizione dell'ambiente&quot;.</td>
</tr>
<tr class="even">
<td style="border:1px solid black;"><strong>Utenti e computer di Active Directory</strong></td>
<td style="border:1px solid black;">Strumento di MMC utilizzato per la gestione di utenti, gruppi, computer e altri oggetti Active Directory del servizio directory Microsoft Active Directory®.</td>
<td style="border:1px solid black;">Installato con Windows Server™ 2003.</td>
</tr>
</tbody>
</table>
  
#### Parametri client WLAN
  
Nella seguente tabella sono indicati alcuni dei parametri principali utilizzati nel presente capitolo.
  
**Tabella 6.2: Impostazioni client WLAN**

 
<table style="border:1px solid black;">
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >Elemento di configurazione</th>
<th style="border:1px solid black;" >Impostazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">Gruppo che consente l'accesso alla rete WLAN</td>
<td style="border:1px solid black;">Accesso LAN senza fili</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Gruppo che consente l'accesso utente alla rete WLAN</td>
<td style="border:1px solid black;">Utenti LAN senza fili</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Gruppo che consente l'accesso dei computer alla rete WLAN</td>
<td style="border:1px solid black;">Computer LAN senza fili</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Nome oggetto Criteri di gruppo WLAN</td>
<td style="border:1px solid black;">Impostazioni client WLAN</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Gruppo di protezione filtro oggetti Criteri di gruppo</td>
<td style="border:1px solid black;">Impostazioni computer LAN senza fili</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Nome criteri di rete senza fili</td>
<td style="border:1px solid black;">Impostazioni client WLAN per Windows XP - PEAP (Protected Extensible Authentication Protocol) e WEP (Wired Equivalent Privacy)</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Nome rete WLAN (SSID)</td>
<td style="border:1px solid black;"><em>LucerneWLAN</em> (cambiare il nome nell'identificatore dei set di servizi (SSID))</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Tipo di EAP (Extensible Authentication Protocol)</td>
<td style="border:1px solid black;">PEAP</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">Metodo di autenticazione PEAP</td>
<td style="border:1px solid black;">Password protetta (EAP-MSCHAP v2)</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">Riconnessione rapida PEAP</td>
<td style="border:1px solid black;">Abilitato</td>
</tr>
</tbody>
</table>
  
I valori visualizzati in corsivo devono essere sostituiti con valori di impostazione relativi all'ambiente in uso.
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Autorizzazioni di accesso alla rete WLAN per utenti e computer
  
È possibile controllare l'accesso di utenti e computer ai server di accesso alla rete (ad esempio i punti di accesso senza fili) impostando l'autorizzazione delle chiamate in ingresso sull'account di dominio dell'utente o del computer. Questo era il metodo utilizzato da Windows NT® 4.0 per controllare l'accesso utente al Servizio di accesso remoto (RAS). Tuttavia, controllare l'accesso alla rete di un gran numero di utenti con questo metodo è estremamente complicato. Inoltre, viene utilizzata un'impostazione di tipo "tutto o niente" in base alla quale non è possibile consentire l'accesso VPN quando viene contemporaneamente bloccato l'accesso alla rete WLAN di un utente specifico.
  
Il Servizio di autenticazione Internet (IAS), con Windows 2000 e Windows Server 2003, consente di controllare l'accesso ai servizi di rete mediante l'utilizzo dei gruppi di protezione Active Directory associati ai criteri di accesso remoto. Questo metodo è più flessibile e anche più facile da gestire in quanto consente di utilizzare le appartenenze ai gruppi per controllare l'accesso ai servizi di rete.
  
#### Controllo dell'accesso alla rete WLAN mediante l'utilizzo di gruppi di protezione
  
L'accesso alla rete WLAN viene controllato mediante i criteri di accesso remoto di IAS. Il criterio di accesso remoto per questa soluzione è stato configurato nel capitolo 5, "Creazione dell'infrastruttura di protezione per LAN senza fili". Questo criterio include un filtro che consente l'accesso alla rete WLAN solo ai membri del gruppo di protezione Accesso LAN senza fili.
  
L'accesso alle reti LAN senza fili non prevede l'inserimento diretto degli account di utenti e computer. Sono infatti disponibili due gruppi di protezione come membri, ovvero Utenti LAN senza fili e Computer LAN senza fili. Nella soluzione, gli utenti di dominio e i computer di dominio diventano membri di questi gruppi il che consente, per impostazione predefinita, la connessione alla rete WLAN di tutti gli utenti e i computer. Informazioni generali relative a questo argomento sono incluse nella sezione "Modello di amministrazione per utenti e computer di reti WLAN" del capitolo 2 "Pianificazione dell'implementazione della protezione di reti LAN senza fili".
  
##### Utilizzo dei gruppi di protezione per un controllo più accurato
  
Il modello di amministrazione che consente l'accesso alla rete WLAN a tutti gli utenti e computer è molto semplice, tuttavia è possibile esercitare maggiore controllo sugli utenti e i computer che possono accedere alla rete WLAN. A questo scopo, è necessario rimuovere gli utenti di dominio e i computer di dominio rispettivamente dal gruppo Utenti LAN senza fili e dal gruppo Computer LAN senza fili. È quindi possibile aggiungere utenti e computer specifici a cui si intende consentire l'accesso come membri di questi gruppi.
  
È necessario non aggiungere gli utenti e i computer direttamente in Accesso LAN senza fili in quanto si tratta di un gruppo universale la cui appartenenza viene pubblicata su un catalogo globale esteso. La pubblicazione sul catalogo globale implica che le modifiche apportate all'appartenenza verranno replicate in tutti i controller di dominio dell'organizzazione. Se invece si aggiungono utenti e computer a gruppi di dominio specifici, ad esempio Utenti LAN senza fili e Computer LAN senza fili, le modifiche alle repliche interesseranno solo i controller di dominio inclusi in un singolo dominio.
  
**Nota:** per i Pocket PC non sono disponibili account di computer Active Directory, pertanto non sarà necessario aggiungerli al gruppo Computer LAN senza fili. Nei Pocket PC viene utilizzato l'account utente per l'autenticazione nella rete WLAN per cui solo questo account è importante.
  
Gli utenti ricevono le informazioni di appartenenza al gruppo solo all'accesso. Pertanto, al temine della creazione e dell'inserimento dei dati nei gruppi di accesso alla rete WLAN, gli utenti dovranno disconnettersi e accedere di nuovo al sistema. Analogamente, sarà necessario riavviare i computer client dopo aver apportato eventuali modifiche alle appartenenze ai gruppi.
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Configurazione client WLAN per Windows XP
  
Nella presente sezione viene descritto come configurare le impostazioni dei client WLAN per Windows XP. Le procedure descritte nella presente sezione consentiranno di configurare l'autenticazione di password PEAP mediante l'utilizzo di un criterio WEP basato su chiavi dinamiche per la protezione dei dati. Le impostazioni possono essere applicate a entrambe le edizioni Windows XP Professional e Windows XP Tablet.
  
Per le istruzioni relative alla modalità di configurazione per la gestione delle chiavi e la protezione dei dati WPA (Wi-Fi Protected Access), vedere l'appendice B "Utilizzo di WPA nella soluzione".
  
#### Installazione di patch e aggiornamenti richiesti
  
È necessario verificare che nei computer client siano installati tutti gli aggiornamenti e le patch importanti, tra cui:
  
-   Patch di protezione importanti.
  
-   Service pack di Windows XP (Service Pack 1 o versioni successive).
  
-   Client WPA per Windows XP (se richiesto).
  
-   Patch di Windows correlate alla rete WLAN, ad esempio il Pacchetto Wireless Update Rollup per Windows XP (vedere l'articolo 826942 della Knowledge Base). È consigliabile installare questo pacchetto a meno che non sia già installato Windows XP SP2.
  
-   Driver WLAN aggiornati dalla scheda di rete o dal fornitore del computer.
  
#### Creazione dell'oggetto Criteri di gruppo per le impostazioni di reti WLAN
  
Per automatizzare l'invio delle impostazioni dei client WLAN, è possibile utilizzare i criteri di gruppo Active Directory. L'Editor criteri di gruppo di Windows Server 2003 include un insieme di impostazioni denominate Criteri di rete senza fili che consentono di configurare le impostazioni dei client speciche per le reti WLAN.
  
**Importante:** per poter ricevere le impostazioni dei client WLAN, si presume che i computer client siano stati aggiunti al dominio e siano in grado di connettersi a una rete LAN senza fili.
  
È possibile creare gli oggetti Criteri di gruppo mediante l'utilizzo della console GPMC oppure di **Utenti e computer di Active Directory**.
  
**Importante:** se l'oggetto Criteri di gruppo viene modificato in un sistema Windows 2000 o Windows XP, le impostazioni dell'oggetto Criteri di gruppo Criteri di rete senza fili non verranno visualizzate nell'Editor oggetti Criteri di gruppo. È quindi necessario modificare le impostazioni in un sistema Windows Server 2003 o in un sistema in cui siano installati gli strumenti di amministrazione di Windows Server 2003. Tali impostazioni, tuttavia, funzionano sia con i controller di dominio di Windows 2000 che di Windows Server 2003. Le impostazioni non sono presenti nell'oggetto dei criteri locali di tutte le versioni di Windows.
  
**Per creare un oggetto Criteri di gruppo per client WLAN mediante GPMC**
  
1.  Aprire la GPMC e selezionare l'oggetto del dominio in fase di configurazione.
  
2.  Fare clic con il pulsante destro del mouse sul dominio e scegliere **Crea GPO e inserisci collegamento...**
  
    **Nota:** l'oggetto Criteri di gruppo viene collegato a livello di dominio, pertanto le impostazioni saranno disponibili in tutti i computer del dominio. Se si preferisce, è possibile restringere l'ambito dell'oggetto Criteri di gruppo collegandolo a un'unità organizzativa di livello inferiore.
  
3.  Quando viene richiesto il nome, digitare **Impostazioni client WLAN**.
  
4.  Nel riquadro di destra fare doppio clic sull'oggetto Criteri di gruppo **Impostazioni client WLAN** appena creato. Nel riquadro di destra verranno visualizzate le proprietà dell'oggetto Criteri di gruppo.
  
5.  Fare clic sulla scheda **Ambito**. Nell'elenco **Security Filtering** selezionare **Utenti Autenticati** ed eliminarlo mediante il pulsante **Elimina**.
  
6.  Scegliere **Aggiungi...** per aggiungere un gruppo diverso.
  
7.  Immettere (o cercare) **Impostazioni computer LAN senza fili**.
  
    **Nota:** il gruppo Impostazioni computer LAN senza fili in realtà appartiene al gruppo Computer di dominio. Computer di dominio è un membro di Computer LAN senza fili che è a sua volta membro del gruppo Impostazioni computer LAN senza fili. L'oggetto Criteri di gruppo a livello di dominio (fare riferimento al passaggio 1) consente a tutti i computer del dominio di ricevere le impostazioni dei client WLAN. Se si desidera restringere le impostazioni a un sottoinsieme più piccolo, rimuovere i computer di dominio dall'appartenenza al gruppo Computer LAN senza fili.
  
8.  Fare clic sulla scheda **Dettagli** e selezionare **Impostazioni configurazione utente disattivata** dall'elenco a discesa **Group Policies Status**. Scegliere **OK** per confermare.
  
9.  Fare clic con il pulsante destro del mouse sull'oggetto Criteri di gruppo nel riquadro di sinistra e scegliere **Modifica...** per modificare le impostazioni dell'oggetto Criteri di gruppo.
  
10. All'apertura dell'Editor oggetti Criteri di gruppo, passare a **\\Configurazione computer\\Impostazioni di Windows\\Impostazioni protezione\\Criteri di rete senza fili (IEEE 802.11)**.
  
11. Selezionare l'oggetto **Criteri di rete senza fili (IEEE 802.11)** dal riquadro di spostamento, quindi scegliere **Crea criterio rete senza fili** dal menu **Azione**.
  
12. Utilizzare la procedura guidata per assegnare al criterio un nome come **Impostazioni client WLAN per Windows XP (PEAP-WEP)**. Lasciare selezionata la casella di controllo **Modifica proprietà**, quindi scegliere **Fine** per chiudere la procedura guidata.
  
13. Fare clic sulla scheda **Reti preferite**, quindi scegliere **Aggiungi...** per aggiungere una nuova rete.
  
14. Nel campo **Nome di rete (SSID)** immettere il nome della rete senza fili.
  
15. Nel campo **Descrizione** immettere una descrizione della rete.
  
    **Nota:** se è già disponibile una rete WLAN e la si intende utilizzare insieme alla rete WLAN basata su 802.1X di questa soluzione, sarà necessario ricorrere a un SSID differente per la nuova rete WLAN.
  
16. Fare clic sulla scheda **IEEE 802.1x** e selezionare **PEAP (Protected EAP)** dall'elenco a discesa **Tipo EAP**.
  
17. Fare clic su **Impostazioni** per modificare le impostazioni PEAP. Dall'elenco **Autorità di certificazione principale attendibili** selezionare il certificato CA principale per la CA installata nel capitolo 4 "Creazione dell'autorità di certificazione della rete".
  
    **Importante:** se è necessario reinstallare completamente la CA senza ripristinarla da una copia di backup, sarà necessario modificare l'oggetto Criteri di gruppo e selezionare il certificato CA principale per la nuova CA.
  
18. Selezionare **Password protetta (EAP-MSCHAP v2)** in **Selezionare il metodo di autenticazione**, quindi l'opzione **Abilita riconnessione rapida**.
  
19. Chiudere tutte le finestre delle proprietà scegliendo **OK**.
  
20. Chiudere l'Editor oggetti Criteri di gruppo e la GPMC.
  
Per creare l'oggetto Criteri di gruppo mediante l'utilizzo di **Utenti e computer di Active Directory** (se non è installata la GPMC), sostituire i passaggi da 1 a 10 della procedura precedente con quelli riportati di seguito.
  
**Per creare un oggetto Criteri di gruppo mediante l'utilizzo di Utenti e computer di Active Directory**
  
1.  Aprire **Utenti e computer di Active Directory** e selezionare l'oggetto di dominio.
  
2.  Fare clic con il pulsante destro del mouse sull'oggetto di dominio e scegliere **Proprietà**.
  
3.  Fare clic sulla scheda **Criteri di gruppo**, quindi scegliere il pulsante **Nuovo...**.
  
4.  Immettere **Impostazioni client WLAN** per il nome dell'oggetto Criteri di gruppo.
  
5.  Scegliere il pulsante **Proprietà**, quindi fare clic sulla scheda **Protezione**.
  
6.  Selezionare **Utenti Autenticati** dall'elenco **Utenti e gruppi**, quindi scegliere il pulsante **Elimina**.
  
7.  Scegliere **Aggiungi...** e immettere (o cercare) **Impostazioni computer LAN senza fili**. Scegliere **OK**.
  
8.  Con il nome del gruppo **Impostazioni computer LAN senza fili** evidenziato nell'elenco **Utenti e gruppi**, selezionare le autorizzazioni **Lettura** e **Applica criteri di gruppo** nella colonna **Consenti** dell'elenco **Autorizzazioni**.
  
9.  Fare clic sulla scheda **Generale** e selezionare **Disattiva impostazioni configurazione utente**. Scegliere **Sì** in tutti i messaggi di avviso.
  
10. Scegliere **OK** per applicare le modifiche e chiudere la finestra delle proprietà dell'oggetto Criteri di gruppo.
  
11. Scegliere il pulsante **Modifica** per modificare il criterio e passare a **\\Configurazione computer\\Impostazioni di Windows\\Impostazioni protezione\\Criteri di rete senza fili (IEEE 802.11).**
  
12. Ripetere i passaggi da 11 a 20 della procedura precedente.
  
#### Distribuzione delle impostazioni di rete WLAN
  
Se si esegue la migrazione da una rete WLAN esistente (non protetta, con WEP statico o di altro tipo), è necessario distribuire le impostazioni dei criteri di gruppo WLAN per la nuova rete basata su 802.1X con alcuni giorni o anche settimane di anticipo rispetto alla configurazione delle impostazioni 802.1X per i punti di accesso senza fili e all'attivazione della nuova rete WLAN. In questo modo verrà garantito ai computer client un ampio margine di tempo per scaricare e applicare il criterio di gruppo **Impostazioni client WLAN** anche se vengono stabilite solo connessioni occasuali con la rete LAN cablata.
  
È inoltre possibile applicare le impostazioni dei criteri di gruppo ai computer client prima che una scheda di rete WLAN venga installata e configurata tramite Windows. Le impostazioni della rete WLAN verranno ignorate finché non viene installata una scheda di rete WLAN valida. Dopo aver completato l'installazione, la scheda di rete verrà configurata automaticamente in base alle impostazioni dei criteri di gruppo WLAN.
  
#### Verifica dell'applicazione dei criteri di gruppo WLAN
  
Per verificare la corretta applicazione delle impostazioni degli oggetti Criteri di gruppo WLAN, è necessario accedere a un computer client. Il gruppo Computer di dominio è un membro del gruppo di protezione Impostazioni computer LAN senza fili utilizzato per filtrare i computer che ricevono le impostazioni di rete WLAN nell'oggetto Criteri di gruppo Impostazioni client WLAN. È quindi necessario che le impostazioni dell'oggetto Criteri di gruppo siano state ricevute da tutti i computer del dominio. Se il computer non è stato riavviato dopo la creazione del gruppo Impostazioni computer LAN senza fili, potrebbe essere necessario riavviarlo adesso.
  
**Nota:** per visualizzare le impostazioni di una rete senza fili, è necessario che sul computer sia installata una scheda di rete WLAN.
  
**Per verificare la corretta distribuzione delle impostazioni di rete WLAN**
  
1.  Accedere al computer client come membro del gruppo Administrators locale.
  
2.  Fare doppio clic sulla cartella **Connessioni di rete** nel **Pannello di controllo**.
  
3.  Visualizzare le proprietà dell'icona **Connessione rete senza fili** corrispondente alla scheda senza fili. Nella scheda **Reti senza fili** verrà visualizzato il nuovo SSID (nome) della rete senza fili sotto **Reti preferite**.
  
4.  Selezionare il nuovo SSID senza fili e scegliere **Proprietà** per visualizzare le impostazioni e verificare se corrispondono a quelle scelte nel criterio di gruppo WLAN.
  
5.  Se l'SSID non appare sotto **Reti preferite** o le impostazioni di rete visualizzate per l'SSID non corrispondono a quelle configurate nel criterio di gruppo WLAN, chiudere le finestre di dialogo Reti senza fili ed eseguire il seguente comando dal prompt.
  
    **Gpupdate /force**
  
    Verificare di nuovo le impostazioni dopo qualche minuto. Se le impostazioni non sono state ancora visualizzate, fare riferimento alla sezione "Risoluzione dei problemi" del capitolo 8 "Gestione della soluzione per reti LAN senza fili protette".
  
#### Verifica del certificato CA principale nel client
  
Per l'autenticazione nel server IAS mediante PEAP, è necessario che nell'archivio dell'Autorità di certificazione principale attendibile dei client sia incluso il certificato per la CA della rete (installata mediante le istruzioni fornite nel capitolo 4 "Creazione dell'autorità di certificazione della rete"). Questo certificato è stato pubblicato in Active Directory durante l'installazione della CA. Tutti i membri dell'insieme di strutture di Active Directory eseguiranno il download e l'installazione automatica del certificato nell'archivio dell'Autorità di certificazione principale attendibile.
  
**Per verificare che il certificato CA principale sia stato installato**
  
1.  Accedere al computer client come amministratore.
  
2.  Eseguire MMC.exe (tramite **Start, Esegui...** o da una shell comandi).
  
3.  Nella MMC scegliere **Aggiungi/Rimuovi snap-in** dal menu **File**.
  
4.  Nella finestra **Aggiungi/Rimuovi snap-in** scegliere il pulsante **Aggiungi...**. Selezionare **Certificati** dall'elenco degli snap-in disponibili.
  
5.  Selezionare **Account computer**, quindi scegliere **Avanti**.
  
6.  Scegliere **Fine**.
  
7.  Chiudere le finestre **Aggiungi snap-in autonomo** e **Aggiungi/Rimuovi snap-in**.
  
8.  Nel riquadro a sinistra passare a Certificati (computer locale)\\Autorità di certificazione principale attendibili\\Certificati.
  
9.  Individuare il certificato della propria CA. (Verrà indicato sotto il nome specificato durante l'installazione della CA).
  
10. Se il certificato non viene visualizzato nell'elenco, aprire una shell comandi e digitare il comando:
  
    **Gpupdate /force**
  
11. Ritornare alla console di gestione **Certificati**. Fare clic con il pulsante destro del mouse sul nodo **Certificati (computer locale)**, quindi scegliere **Aggiorna** e infine controllare di nuovo il certificato CA.
  
    Se il certificato non viene ancora visualizzato, vedere la sezione "Risoluzione dei problemi" del capitolo 8 "Gestione della soluzione per reti LAN senza fili protette".
  
#### Verifica della connessione alla rete WLAN
  
Dopo aver verificato le impostazioni dell'oggetto Criteri di gruppo WLAN e il certificato CA principale, è possibile verificare la connessione alla rete WLAN mediante l'utilizzo di un computer client.
  
**Per verificare la connessione alla rete WLAN**
  
1.  Come utente di dominio con accesso autorizzato alla rete WLAN, accedere a un computer client non connesso alla rete cablata e in cui sia installata una scheda WLAN. Per impostazione predefinita, tutti gli utenti di dominio hanno accesso alla rete WLAN.
  
    **Nota:** se la rete WLAN non è in funzione in un punto specifico e l'utente non dispone di credenziali memorizzate nella cache del computer, l'accesso non verrà completato.
  
2.  Dal prompt dei comandi specificare il comando **ping** per verificare la connettività di rete a un altro computer della rete.
  
    Se il comando **ping** (o l'accesso) non viene eseguito, vedere la sottosezione "Monitoraggio della connessione client alla rete WLAN" della sezione "Risoluzione dei problemi" nel capitolo 8 "Gestione della soluzione per reti LAN senza fili protette".
  
Per ulteriori informazioni sulle procedure di testing per i client WLAN, vedere il capitolo 7 "Testing della soluzione per reti LAN senza fili protette".
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Configurazione dei client Pocket PC 2003
  
Pocket PC 2003 garantisce supporto completo per le reti WLAN 802.1X che utilizzano protocolli PEAP (con password) o EAP-TLS (con certificati). Tuttavia, Pocket PC 2003 è un sistema operativo modulare e il fornitore della periferica portatile può scegliere se includere o meno questo tipo di funzione. Pertanto, non tutte le periferiche Pocket PC 2003 sono supportate dalle reti WLAN. I principali fornitori di queste periferiche forniscono sistemi supportati dalle reti WLAN 802.1X sia con hardware WLAN incorporato sia con schede di rete WLAN aggiuntive. Nella presente sezione viene descritta la configurazione dell'interfaccia WLAN basata su un Pocket PC HP IPAQ 5550. Alcuni fornitori, tuttavia, implementano interfacce e driver personalizzati per le reti WLAN. Poiché le seguenti istruzioni potrebbero non essere appropriate per le periferiche più recenti, è consigliabile seguire le istruzioni del fornitore.
  
Alcuni fornitori di periferiche Pocket PC offrono supporto anche per le reti WLAN 802.1X su Pocket PC 2002. Pocket PC 2002, tuttavia, non è stato testato con questa soluzione. Per informazioni dettagliate sul supporto Pocket PC 2002 per le reti WLAN, è necessario consultare il sito Web del fornitore.
  
#### Preparazione della periferica Pocket PC
  
Prima di configurare la periferica, è necessario ottenere e installare gli aggiornamenti importanti disponibili presso il fornitore del Pocket PC, tra cui:
  
-   Aggiornamenti memoria di sola lettura. (Possono essere inclusi diversi aggiornamenti compresi i driver).
  
-   Aggiornamenti driver di rete.
  
-   Altri aggiornamenti di rete o WLAN importanti per le reti 802.1X.
  
    **Importante:** prima di installare gli aggiornamenti, è necessario leggere attentamente la documentazione fornita. Alcuni aggiornamenti potrebbero essere incompatibili con altri o non soddisfare gli obiettivi dell'utente. Ad esempio, HP ha pubblicato un aggiornamento per la serie IPAQ 555x per supportare la soluzione Cisco LEAP, ma questo aggiornamento è incompatibile con l'aggiornamento del driver WLAN 802.1X e compromette il funzionamento di PEAP.
  
#### Disponibilità del certificato CA
  
È necessario installare il certificato della CA di rete nell'archivio dell'Autorità di certificazione principale attendibile di tutti i Pocket PC che richiedono la connessione alla rete WLAN. A questo scopo, è necessario esportare il certificato dalla CA e renderlo disponibile agli utenti del Pocket PC o allo staff IT.
  
**Per esportare il certificato CA**
  
1.  Accedere al server CA e aprire una shell comandi.
  
2.  Eseguire il seguente comando per esportare il certificato CA in un file:
  
    **certutil -ca.cert rootca.cer**
  
    Se si intende salvare il file Rootca.cer in una cartella differente, è possibile specificare un altro percorso. (Se il percorso e il nome del file contengono spazi, è necessario racchiuderli tra virgolette).
  
3.  Copiare il file del certificato in una condivisione di file o in una directory del server Web in modo che possa essere scaricato facilmente al momento dell'installazione del Pocket PC.
  
#### Configurazione del Pocket PC
  
Prima che venga eseguita la connessione alla rete WLAN, è necessario configurare i Pocket PC con le impostazioni di rete WLAN e del certificato CA. Per eseguire la copia del file del certificato nel Pocket PC sono richiesti alcuni elementi di supporto. Nella seguente procedura si presume l'utilizzo di una connessione ActiveSync® stabilita mediante alloggiamento di espansione, infrarossi o connessione Bluetooth. È inoltre possibile utilizzare supporti rimovibili, ad esempio Compact Flash, Secure Digital o Multimedia Card, per eseguire il trasferimento del file del certificato o per stabilire una connessione WLAN non autenticata e consentire al Pocket PC di scaricare il certificato da un sito Web. Infine, è possibile inviare il certificato all'utente tramite messaggi di posta elettronica, consentirne la sincronizzazione (per trasferire il messaggio con Pocket Outlook®) e definire l'esecuzione del file del certificato collegato.
  
**Per importare il certificato CA nel Pocket PC**
  
1.  Connettere il Pocket PC a un computer host mediante l'utilizzo di ActiveSync (è probabile che sia necessario stabilire una relazione ActiveSync) e del metodo di connessione preferito.
  
2.  Dal computer host utilizzare l'opzione **Explore** di ActiveSync per aprire la finestra di una cartella nella periferica. Verrà aperta la cartella **My Documents**.
  
3.  Ottenere il file del certificato CA dalla posizione di pubblicazione e copiarlo nella cartella **My Documents**. È possibile ignorare l'avviso relativo alla conversione del file. È inoltre possibile disconnettere la periferica da ActiveSync.
  
4.  Nel Pocket PC individuare il file del certificato CA mediante **Esplora file** e toccare due volte il file.
  
5.  Verrà chiesto se si intende installare il certificato. Verificare che il nome CA corriponda al nome della CA di rete e scegliere **Sì** per eseguire l'installazione.
  
    Per verificare se il certificato è stato installato in modo corretto, è sufficiente scegliere **Impostazioni**, **Sistema**, **Certificati** e infine selezionare la scheda **Principale**.
  
**Per configurare le impostazioni della rete WLAN 802.1X nel Pocket PC**
  
1.  Se nella periferica non è stata ancora abilitata la scheda WLAN, abilitarla mediante l'utilizzo di uno switch hardware o di uno strumento software.
  
2.  Se viene visualizzato un messaggio popup in cui viene segnalato che è stata trovata una nuova rete, selezionare **Lavoro** come posizione in cui verrà stabilita la connessione alla rete WLAN. Quindi scegliere **Impostazioni**.
  
    Se non viene visualizzato alcun messaggio popup in quanto la rete WLAN è già stata rilevata in precedenza, attenersi alla seguente procedura:
  
    -   Toccare l'icona **Connettività** (due frecce rivolte in direzioni opposte) nella barra del titolo del Pocket PC e scegliere **Impostazioni**.
  
    -   Selezionare la scheda **Avanzate**, quindi scegliere il pulsante **Scheda di rete**.
  
        Nella scheda **Senza fili** verrà visualizzato l'SSID della rete WLAN nell'elenco delle reti senza fili disponibili (se esistono altre reti WLAN, è possibile che ne vengano visualizzati i nomi).
  
    -   Selezionare il nome della rete WLAN nell'elenco.
  
3.  Nella scheda **Generale** selezionare **Lavoro** dall'elenco **Si connette a:**.
  
4.  Nella scheda **Autenticazione** selezionare le seguenti opzioni:
  
    -   **Crittografia dati (WEP abilitato)**
  
    -   **La chiave viene fornita automaticamente**
  
    -   **Abilita controllo accesso alla rete mediante IEEE 802.1X**
  
    Deselezionare l'opzione **Autenticazione di rete (modalità condivisa)**.
  
5.  Nell'elenco **Extensible Authentication Protocol Type:** selezionare **PEAP**.
  
6.  Scegliere **OK** per chiudere la finestra delle impostazioni.
  
7.  Quando viene richiesto di immettere le credenziali di dominio per la connessione alla rete WLAN, specificare il nome, la password e il dominio di un utente autorizzato a connettersi alla rete WLAN.
  
    **Avviso:** è possibile selezionare l'opzione **Salva password** solo se viene implementato un meccanismo di protezione avanzata contro l'utilizzo non autorizzato della periferica, ad esempio l'analisi delle impronte digitali o l'accesso tramite password complesse. È opportuno tenere presente che le credenziali dell'utente vengono utilizzate per l'autenticazione nelle risorse di dominio e nella rete WLAN. Se le credenziali vengono compromesse, un intruso potrebbe accedere a tutte le risorse di rete interne disponibili sulla rete WLAN senza essere identificato.
  
8.  Se si è passati alle impostazioni della rete WLAN tramite il messaggio popup **Nuova rete** nel passaggio 2, toccare l'icona **Connettività** sulla barra del titolo del Pocket PC e scegliere **Impostazioni** per aprire la schermata **Impostazioni di connessione**.
  
9.  Selezionare la scheda **Avanzate**, quindi scegliere il pulsante **Scheda di rete**. (Schermata visualizzata se non si è scelto il messaggio popup **Nuova rete** nel passaggio 2).
  
10. Nell'elenco **Reti senza fili** verrà visualizzato il nome della rete WLAN appena configurata. Se lo stato visualizzato non è **Connessione**, toccare il nome e tenendolo premuto scegliere **Connetti**. (È possibile che venga richiesto di immettere di nuovo le credenziali dell'utente).
  
11. Se per la rete WLAN viene visualizzato **Connessione**, scegliere **OK** per chiudere le schermate **Configurazione reti senza fili** e **Impostazioni di connessione**.
  
    **Nota:** se per la configurazione delle periferiche vengono fornite le presenti istruzioni, gli utenti dei Pocket PC potranno immettere le proprie credenziali di dominio, quando richieste. Tuttavia, se i Pocket PC vengono preconfigurati dal personale IT, sarà necessario indicare ai responsabili IT account di dominio validi (con accesso alla rete WLAN). Quando vengono utilizzati questi account, è molto importante che non venga selezionata l'opzione **Salva password**. È quindi necessario che gli utenti ricevano istruzioni adeguate per l'immissione delle credenziali quando si connettono per la prima mediante l'utilizzo di Pocket PC.
  
#### Verifica della connessione del Pocket PC alla rete WLAN
  
Esistono diversi modi per verificare se un Pocket PC è connesso alla rete WLAN in modo corretto. Il modo più semplice è quello di connettersi a un'applicazione sulla rete, ad esempio un sito Web. (Se il server non si trova sulla rete LAN, potrebbe essere necessario configurare un server proxy sulla periferica).
  
Se la connessione non viene completata, vedere la sezione "Risoluzione dei problemi" del capitolo 8 "Gestione della soluzione per reti LAN senza fili protette".
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Riepilogo
  
Nel presente capitolo è stata descritta la configurazione delle impostazioni di rete WLAN per i client Windows XP e Pocket PC. Inoltre, sono state fornite ulteriori informazioni sull'utilizzo dei gruppi di protezione per il controllo dell'accesso alla rete WLAN, sulla configurazione dei criteri di gruppo per la distribuzione delle impostazioni di rete WLAN ai client Windows XP e sulle procedure di configurazione per i client Pocket PC 2003.
  
[](#mainsection)[Inizio pagina](#mainsection)
  
### Riferimenti
  
Questa sezione contiene rimandi a informazioni supplementari importanti e ad altro materiale attinente al contenuto di questo capitolo.
  
-   Per ulteriori informazioni relative alla gestione dell'accesso alle reti WLAN da parte degli utenti o mediante l'utilizzo di gruppi di protezione, vedere l'argomento "Introduzione ai criteri di accesso remoto" nella documentazione di Windows Server 2003 disponibile all'URL seguente:
  
    <http://technet.microsoft.com/en-us/library/cc756729.aspx> (in inglese).
  
-   Per ulteriori informazioni sul Pacchetto Wireless Update Rollup per Windows XP, vedere l'articolo disponibile all'URL seguente:
  
    <http://support.microsoft.com/default.aspx?scid=826942>
  
-   Per ulteriori informazioni relative alla configurazione delle impostazioni di rete WLAN mediante l'utilizzo di criteri di gruppo, vedere l'argomento "Define Active Directory-based wireless network policies" nella documentazione di Windows Server 2003 disponibile all'URL seguente:
  
    <http://technet.microsoft.com/en-us/library/cc778277.aspx> (in inglese).
  
-   È possibile ottenere altre informazioni tecniche sul supporto WLAN relativo ai Pocket PC dal fornitore della periferica. Per ulteriori informazioni tecniche, vedere l'articolo "Windows CE .NET Wireless Technology Overview" sul sito Microsoft Developer Network all'URL seguente:
  
    <http://msdn.microsoft.com/en-us/embedded/aa714430.aspx> (in inglese).
  
**Scarica la soluzione completa**
  
[Protezione delle reti LAN senza fili con PEAP e password](http://go.microsoft.com/fwlink/?linkid=23481)
  
[](#mainsection)[Inizio pagina](#mainsection)
