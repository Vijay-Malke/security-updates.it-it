---
TOCTitle: Utilizzo di WPA nella soluzione
Title: Utilizzo di WPA nella soluzione
ms:assetid: '472f2650-c32e-4b1d-a7d7-b322c5e61592'
ms:contentKeyID: 20200838
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Dd536239(v=TechNet.10)'
---

Protezione delle reti LAN senza fili con PEAP e password
========================================================

### Appendice B: Utilizzo di WPA nella soluzione

Aggiornato: 2 aprile 2004

La soluzione per reti LAN senza fili (WLAN) descritta in questa guida funziona ugualmente bene con la protezione WEP (Wired Equivalent Privacy) dinamica o con la protezione WPA (Wi-Fi Protected Access). Le differenze di implementazione tra i due tipi di protezione sono poche e vengono descritte in questa appendice.

Attualmente l'utilizzo di WPA può presentare alcune difficoltà, dettate da:

-   **Configurazione manuale delle impostazioni WPA:** nelle versioni di Windows® precedenti Windows Server™ 2003 Service Pack 1 non è disponibile il supporto per la definizione delle impostazioni WPA per i client Windows® XP mediante criteri di gruppo. Finché non si distribuisce il Service Pack 1 nell'organizzazione, è necessario configurare i client a mano (non vi è alcun modo per applicare tramite script le impostazioni WLAN per Windows XP). Il Service Pack 1 deve essere installato solo nel server in cui verrà modificato l'oggetto Criteri di gruppo delle impostazioni WLAN. Non è necessario installarlo nei client, nei controller di dominio o nei server IAS.

-   **Disponibilità limitata dei client della WLAN:** al momento della stesura di questa documentazione, Microsoft® fornisce il supporto WPA solo per Windows XP Service Pack 1 e versioni successive.

-   **Disponibilità di hardware compatibile con WPA:** ora tutto l'hardware certificato Wi-Fi deve supportare obbligatoriamente WPA, tuttavia nell'organizzazione potrebbero esistere apparecchiature che non supportano WPA e che, quindi, devono essere aggiornate. Sarà necessario procurarsi gli aggiornamenti firmware per i punti di accesso o le schede di rete che non supportano WPA. In alcuni rari casi può essere necessario sostituire le apparecchiature se il produttore non distribuisce aggiornamenti per WPA.

##### In questa pagina

[](#edaa)[Utilizzo di WPA al posto di WEP](#edaa)
[](#ecaa)[Migrazione da WEP a WPA](#ecaa)
[](#ebaa)[Riferimenti](#ebaa)

### Utilizzo di WPA al posto di WEP

La maggior parte delle informazioni della guida possono essere applicate sia a WPA che a WEP dinamico, tuttavia vi sono due punti in cui le istruzioni sono diverse:

-   La sezione "Creating an IAS Remote Access Policy for WLAN" del capitolo 5 "Creazione dell'infrastruttura di protezione per LAN senza fili".

-   La sezione "Creating the WLAN Settings GPO" del capitolo 6 "Configurazione dei client delle reti LAN senza fili".

#### Creazione di un criterio di accesso remoto IAS per reti WLAN con WPA

Per utilizzare la protezione basata su WPA anziché su WEP dinamico, è necessario impostare il valore di timeout della sessione client su 8 ore anziché su 60 minuti. WPA ha un meccanismo incorporato che genera nuove chiavi di crittografia WLAN, quindi non richiede frequenti riautenticazioni dei client. Otto ore è un valore ragionevole, che garantisce che i client abbiano credenziali aggiornate (ad esempio, garantisce che nessun client rimanga connesso per periodi eccessivi dopo che il suo account è stato disattivato). In ambienti con requisiti molto elevati in termini di protezione, è possibile ridurre questo valore di timeout, se necessario.

Nella sezione "Modifica delle impostazioni del profilo dei Criteri di accesso WLAN" del capitolo 5 "Creazione dell'infrastruttura di protezione per LAN senza fili", utilizzare la seguente procedura per definire le impostazioni del profilo del criterio di accesso remoto:

**Per modificare le impostazioni del profilo dei criteri di accesso senza fili:**

1.  Nella console MMC Servizo autenticazione Internet, aprire la pagina delle proprietà del criterio **Consenti accesso senza fili**, quindi fare clic su **Modifica profilo**.

2.  Nella scheda **Limitazioni chiamate in ingresso** selezionare l'opzione **Limite massimo di minuti per la connessione del client (timeout sessione)**, quindi digitare il valore **480 minuti** (480 minuti o 8**ore).

3.  Nella scheda **Avanzate** aggiungere l'attributo **Ignore-User-Dialin-Properties**, impostarlo su **True**, quindi aggiungere l'attributo **Termination-Action** e impostarlo su **RADIUS Request**.

È necessario modificare, inoltre, il timeout sessione nel punto di accesso senza fili, in modo che corrisponda al valore di timeout impostato in questa procedura.

#### Configurazione manuale delle impostazioni WLAN di Windows XP per WPA

Finché non si applica Windows Server 2003 Service Pack 1, che rende disponibile il supporto per gli oggetti Criteri di gruppo, è necessario configurare le impostazioni WPA nel client manualmente. WPA è supportato in Windows XP Service Pack 1 con installato il download per il client WPA (oppure in Windows XP Service Pack 2).

**Nota:** se è disponibile il supporto per gli oggetti Criteri di gruppo, è possibile anche utilizzare la seguente procedura per creare un criterio di rete senza fili con le stesse impostazioni.

**Per configurare manualmente le impostazioni per la protezione WPA per la rete WLAN:**

1.  Aprire la finestra **Proprietà rete senza fili**. Se nell'elenco **Reti disponibili** è visualizzata la rete LAN senza fili, selezionarla e fare clic su **Configura**, altrimenti fare clic su **Aggiungi** (nella sezione **Reti preferite**).

2.  Digitare il nome della rete WLAN nel campo **Nome di rete (SSID)** (se non è già visualizzato) e immettere una descrizione della rete nel campo **Descrizione**.

    **Nota:** se esiste già una rete WLAN e si desidera utilizzarla unitamente alla rete WLAN basata su 802.1X di questa soluzione, è necessario usare un SSID (Service Set Identifier) diverso per la nuova rete WLAN. Questo nuovo SSID deve essere specificato qui.

3.  Nella sezione **Chiave rete senza fili** selezionare **WPA** (non **WPA PSK**) nella casella **Autenticazione di rete** e **TKIP** nella casella **Crittografia dati**. Se supportato dall'hardware, è possibile scegliere **AES** (Advanced Encryption Standard) al posto di **TKIP**.

4.  Fare clic sulla scheda **IEEE 802.1x** e selezionare **PEAP (Protected EAP)** nell'elenco a discesa **Tipo EAP**.

5.  Fare clic su **Impostazioni** per modificare le impostazioni PEAP. Nell'elenco **Autorità di certificazione principale attendibili** selezionare il certificato di autenticazione all'origine per la CA. (Si tratta della CA installata per il rilascio dei certificati dei server IAS. Per ulteriori informazioni, vedere il capitolo 4).

    **Importante:** se fosse necessario reinstallare la CA ex-novo (e non semplicemente ripristinarla da un backup), si dovrebbero modificare le impostazioni client e si dovrebbe selezionare il certificato di autenticazione all'origine per la nuova CA.

6.  Verificare che nella casella **Selezionare il metodo di autenticazione** sia selezionato **Password protetta(EAP-MS-CHAP v2)** e selezionare l'opzione **Abilita riconnessione rapida**.

7.  Chiudere tutte le finestre delle proprietà scegliendo **OK**.

#### Configurazione di Pocket PC 2003 per WPA

Al momento della stesura di questa guida, la protezione WPA non è supportata in Pocket PC 2003, tuttavia potrebbe venire implementata in futuro. Inoltre, il supporto per la protezione WPA potrebbe venire fornito da terzi.

[](#mainsection)[Inizio pagina](#mainsection)

### Migrazione da WEP a WPA

Se è stata distribuita una soluzione per reti LAN senza fili protette basata sulla protezione WEP dinamica e si desidera passare a WPA, è necessario eseguire la procedura descritta in questa sezione. Prima di effettuare la migrazione, è necessario avere distribuito il supporto software per WPA (ad esempio il componente WPA di Windows XP) e il supporto hardware (aggiornamenti del firmware dei punti di accesso e dei driver delle schede di rete). I riferimenti contenuti in questa procedura alla configurazione delle impostazioni per la protezione WPA in oggetti Criteri di gruppo sono validi solo se l'oggetto Criteri di gruppo viene modificato in Windows Server 2003 Service Pack 1 o versione successiva. Al momento della stesura di questa guida, questo service pack non è ancora disponibile. Se non si utilizza Windows Server 2003 Service Pack 1 o versione successiva, seguire le istruzioni contenute nella sezione "Configurazione manuale delle impostazioni WLAN di Windows XP" in questa appendice.

**Per migrare da WEP a WPA, se i punti di accessi supportano contemporaneamente la protezione WEP dinamica e WPA, procedere come segue:**

1.  Configurare tutti i punti di accesso senza fili in modo che supportino la protezione WEP dinamica e la protezione WPA.

2.  Creare un nuovo oggetto Criteri di gruppo per le impostazioni dei client della rete WLAN. Creare un criterio Rete senza fili che configuri le impostazioni corrette per WPA (vedere la procedura descritta nella sezione "Configurazione manuale delle impostazioni WLAN di Windows XP" in questa appendice). Disattivare, quindi, l'oggetto Criteri di gruppo per WEP esistente e attivare l'oggetto Criteri di gruppo per WPA, in modo che tutte le impostazioni WPA vengano trasmesse a tutti i client. I client inizieranno a utilizzare WPA nella rete WLAN dopo il successivo aggiornamento dell'oggetto Criteri di gruppo.

    **Nota:** se si configurano i client manualmente, è necessario disattivare l'oggetto Criteri di gruppo che contiene le impostazioni WEP. In caso contrario, le impostazioni WPA manuali verranno sovrascritte dall'oggetto Criteri di gruppo.

3.  Infine, è necessario aggiornare il valore di timeout sessione del criterio di accesso remoto di IAS e il valore di timeout sessione dei client nel punto di accesso (come descritto nella sezione "Creazione di un criterio di accesso remoto IAS con WPA" più indietro in questa appendice).

**Per migrare da WEP a WPA, se i punti di accesso non supportano l'uso contemporaneo di WEP e WPA, procedere come segue:**

1.  Creare un nuovo SSID di rete WLAN per la rete WPA.

2.  Modificare l'oggetto Criteri di gruppo con le impostazioni di rete per i client e aggiungere il nuovo SSID con i parametri per WPA (come descritto nella sezione "Configurazione manuale delle impostazioni WLAN di Windows XP per WPA" più indietro in questa appendice). Se si configurano i client manualmente, configurarli con il nuovo SSID e con le impostazioni WPA per tale SSID. In entrambi i casi non rimuovere le impostazioni per il vecchio SSID WEP.

3.  Procedendo di sito in sito, riconfigurare i punti di accesso da WEP a WPA, modificando il SSID del punto di accesso. Man mano che si riconfigurano i punti di accesso, i client passano al nuovo SSID e iniziano a utilizzare WPA.

4.  Dopo aver riconfigurato tutti i punti di accesso, è possibile aggiornare i criteri di accesso remoto in tutti i server IAS. È necessario aumentare il valore di timeout sessione nel criterio di accesso remoto (passando da 60 minuti a 8 ore) e modificare la stessa impostazione nei punti di accesso senza fili (come descritto nella sezione "Creazione di un criterio di accesso remoto IAS per reti WLAN" in questa appendice).

5.  Al termine della migrazione, è possibile rimuovere il SSID WEP dall'oggetto Criteri di gruppo.

[](#mainsection)[Inizio pagina](#mainsection)

### Riferimenti

Questa sezione contiene rimandi a informazioni supplementari importanti e ad altro materiale relativo al contenuto di questa appendice.

-   The Cable Guy — March 2003, Wi-Fi Protected Access™ (WPA) Overview, disponibile all'indirizzo:

    [http://technet.microsoft.com/it-it/library/Dd536258](http://technet.microsoft.com/it-it/library/dd536258) (in inglese)

-   Articolo della Microsoft Knowledge Base 815485 "Panoramica dell'aggiornamento per la protezione wireless WPA in Windows XP", disponibile all'indirizzo:

    <http://support.microsoft.com/kb/815485>.

-   Microsoft Press Pass Announcement on WPA Availability, disponibile all'indirizzo:

    [http://www.microsoft.com/presspass/press/2003/mar03/03-31WiFiProtectedAccessPR.asp](http://www.microsoft.com/presspass/press/2003/mar03/03-31wifiprotectedaccesspr.asp) (in inglese)

-   Documento "Wireless 802.11 Security with Windows XP", disponibile all'indirizzo:

    [http://download.microsoft.com/download/b/b/b/bbbb5a3c-1518-4c0a-910b-15a92902fe6d/XP80211Security.doc](http://download.microsoft.com/download/b/b/b/bbbb5a3c-1518-4c0a-910b-15a92902fe6d/xp80211security.doc) (in inglese)

**Scarica la soluzione completa**

[Protezione delle reti LAN senza fili con PEAP e password](http://go.microsoft.com/fwlink/?linkid=23481)

[](#mainsection)[Inizio pagina](#mainsection)
