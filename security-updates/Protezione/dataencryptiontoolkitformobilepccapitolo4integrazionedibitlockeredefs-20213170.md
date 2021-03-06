---
TOCTitle: 'Data Encryption Toolkit for Mobile PC: Capitolo 4: integrazione di BitLocker ed EFS'
Title: 'Data Encryption Toolkit for Mobile PC: Capitolo 4: integrazione di BitLocker ed EFS'
ms:assetid: '80c0d0af-2c2e-45d6-9b29-f850926296bb'
ms:contentKeyID: 20213170
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc162807(v=TechNet.10)'
---

Data Encryption Toolkit for Mobile PC - Analisi della protezione
================================================================

### Capitolo 4: integrazione di BitLocker ed EFS

Pubblicato: 4 aprile 2007

Crittografia unità Microsoft® BitLocker™ (BitLocker) ed EFS (Encrypting File System) sono due tecnologie indipendenti che possono essere combinate per fornire una soluzione complessiva adeguata per la protezione dei dati. Una soluzione di crittografia che utilizza la combinazione di vantaggi di BitLocker ed EFS forniti dalla crittografia per computer di BitLocker e la crittografia per utente di EFS.

##### In questa pagina

[](#ebaa)[Scelta di una combinazione di BitLocker ed EFS](#ebaa)

### Scelta di una combinazione di BitLocker ed EFS

Un'organizzazione può implementare molte combinazioni diverse di BitLocker ed EFS. Sebbene esista un numero ridotto di combinazioni comuni di BitLocker ed EFS, sarebbe impossibile illustrare tutte le possibili combinazioni in questo documento. In questa sezione viene riportato un riepilogo di alcune combinazioni e vengono trattate le relative attenuazioni dei rischi. Le attenuazioni dei rischi sono le seguenti:

-   BitLocker con TPM (Trusted Platform Module) ed EFS

-   BitLocker con TPM, codice PIN ed EFS

-   BitLocker con TPM, codice PIN ed EFS con smart card

#### BitLocker con TPM ed EFS con Archiviazione chiavi software

La combinazione di BitLocker con un TPM ed EFS con Archiviazione chiavi software fornisce una protezione base con costi e requisiti di formazione degli utenti minimi.

La soluzione più fruibile per le organizzazioni che desiderano combinare BitLocker ed EFS sarebbe la combinazione delle opzioni BitLocker con TPM ed EFS (senza smart card) trattate precedentemente in questa guida. Nella seguente sottosezione vengono fornite informazioni sulle caratteristiche di questa soluzione.

##### Rischi attenuati: BitLocker con TPM ed EFS con Archiviazione chiavi software

BitLocker insieme a EFS attenua i seguenti rischi per i dati:

-   **Dati crittografati leggibili dall'interno**. Un vantaggio specifico di EFS rispetto a BitLocker consiste nel fatto che le chiavi di crittografia vengono memorizzate in un archivio chiavi sicuro protetto con le credenziali dell'utente. In questa configurazione, la credenziale è una password. Tuttavia, altri utenti autorizzati del computer possono effettuare l'accesso in modo interattivo o in rete, ma non saranno in grado di accedere ai file riservati presenti nel computer protetti da un altro utente con EFS, a meno che quell'utente conceda espressamente l'accesso ai file.

-   **Individuazione della chiave tramite attacchi offline**. La VMK viene crittografata utilizzando una chiave che si trova nell'hardware del TPM insieme a un codice PIN. Se non si è a conoscenza del codice PIN, per chi effettua l'attacco sarà molto difficoltoso determinare il valore della FVEK.

-   **Attacchi offline contro il sistema operativo**. Gli attacchi offline contro il sistema operativo vengono attenuati dal fatto che chi effettua l'attacco deve recuperare correttamente la SRK dal TPM e quindi utilizzarla per decrittografare la VMK oppure effettuare un attacco a forza bruta sulla FVEK. Inoltre, BitLocker configurato con la relativa tecnologia di diffusione (attivata per impostazione predefinita) attenua attacchi mirati di questa natura, poiché le piccole modifiche apportate al testo crittografato si propagheranno su un'area più grande.

-   **Perdita di dati non crittografati tramite il file ibernazione**. Uno degli obiettivi principali di BitLocker è quello di proteggere i dati nel volume del sistema operativo del disco rigido quando il computer viene spento o entra in modalità di ibernazione. Quando BitLocker è attivo, il file ibernazione viene crittografato.

-   **Perdita di dati non crittografati tramite il file di paging del sistema**. In Windows Vista, EFS può essere configurato in modo che esegua la crittografia del file di paging utilizzando una chiave simmetrica temporanea generata al momento dell'avvio, ma mai scritta sul disco. All'arresto del sistema, questa chiave viene eliminata in modo che per recuperare i dati dal file di paging sia necessario un attacco a forza bruta per trovare la chiave simmetrica utilizzata per crittografare il file. Se è attivato anche BitLocker, chi effettua l'attacco dovrebbe disattivare BitLocker *e* completare correttamente un attacco a forza bruta sulla chiave del file di paging per recuperare informazioni utili.

-   **Errore dell'utente**. Poiché BitLocker è una tecnologia di crittografia completa dei volumi, crittografa tutti i file che si trovano nel volume del sistema operativo Windows Vista. Questa funzionalità consente di impedire errori dell'utente nel prendere decisioni sbagliate riguardo l'applicazione della crittografia.

##### Attenuazioni e rischi residui: BitLocker con TPM ed EFS con Archiviazione chiavi software

BitLocker insieme a EFS non attenua i seguenti rischi senza l'utilizzo di controlli e criteri aggiuntivi. È possibile trovare informazioni su questi rischi e le relative attenuazioni nelle discussioni sullo scenario nel [Capitolo 2: Crittografia unità BitLocker](http://www.microsoft.com/italy/technet/security/guidance/clientsecurity/dataencryption/analysis/4e6ce820-fcac-495a-9f23-73d65d846638.mspx) e [Capitolo 3: crittografia del file system](http://www.microsoft.com/italy/technet/security/guidance/clientsecurity/dataencryption/analysis/dc2cde72-a84d-4716-9a30-f62b608efda1.mspx), in questa *Analisi della protezione*.

-   **Computer in modalità di ibernazione**. Se l'utente non configura il computer in modo che richieda una password alla ripresa del computer, il sistema operativo non è in grado di riconoscere che l'utente corrente non è l'utente appropriato. Se il computer è configurato in modo da richiedere le credenziali dell'utente alla ripresa dalla modalità di ibernazione, il rischio viene attenuato.

-   **Computer in modalità sospensione (standby)**. Come per la modalità di ibernazione, lo stato del portatile e le chiavi di crittografia di BitLocker non vengono modificati quando il portatile entra in modalità sospensione. Alla ripresa dalla modalità sospensione, la FVEK rimane accessibile sul computer. Questo rischio può essere attenuato attivando l'impostazione **Chiedi la password al termine della modalità standby**.

-   **Computer lasciato con accesso effettuato e desktop sbloccato**. Un utente che può accedere al desktop di un computer protetto con BitLocker ed EFS ha essenzialmente accesso all'intero computer. Questo rischio può essere attenuato fornendo una formazione nell'ambito della consapevolezza in materia di protezione e considerando l'utilizzo delle impostazioni Criteri di gruppo per bloccare automaticamente il computer dopo un periodo di attività.

-   **Individuazione della password di dominio/locale**. Le chiavi EFS vengono decrittografate in una sequenza che inizia con una chiave derivata dalla password dell'utente. Tuttavia, se la password dell'utente è compromessa, la crittografia EFS risulta compromessa.

-   **Attacchi online contro il sistema operativo**. Gli attacchi online contro il sistema operativo *non* vengono attenuati da questa opzione. Chiunque sia in grado di attaccare con successo il sistema operativo durante l'esecuzione può anche eseguire un codice per recuperare i dati crittografati.

-   **Attacchi alla piattaforma**. Né BitLocker né EFS forniscono una protezione completa contro gli attacchi alla piattaforma.

-   **Fattore di autenticazione richiesto nel computer**. Se gli utenti conservano la password di accesso insieme al computer, un utente malintenzionato può accedere e impersonare l'utente, acquisendo l'accesso completo alle risorse. Questo rischio può essere attenuato fornendo una formazione nell'ambito della consapevolezza in materia di protezione agli utenti.

#### BitLocker con TPM, codice PIN ed EFS con Archiviazione chiavi software

L'aggiunta di un requisito PIN a un computer che supporta BitLocker migliora significativamente la protezione della tecnologia BitLocker in termini di usabilità e gestibilità. In questa opzione, all'utente vengono richieste due password per utilizzare il computer: una per BitLocker (all'avvio) e una per il computer o il dominio all'accesso. Le due password dovrebbero essere e probabilmente saranno diverse perché il codice PIN deve contenere caratteri numerici immessi attraverso i tasti funzione (F0 - F9) e perché la maggior parte dei criteri password dominio rifiuterebbe una password composta esclusivamente da caratteri numerici. In questa combinazione, EFS continua a fornire l'attenuazione di alcuni attacchi che BitLocker non è in grado di attenuare da solo.

##### Rischi attenuati: BitLocker con TPM, codice PIN ed EFS con Archiviazione chiavi software

-   **Computer in modalità di ibernazione**. BitLocker con TPM e codice PIN attenua questo rischio perché all'utente viene richiesto di fornire il codice PIN alla ripresa del computer dalla modalità di ibernazione.

-   **Individuazione della password di dominio/locale**. Uno dei vantaggi principali dell'opzione BitLocker con TPM e codice PIN è costituito dal fatto che la soluzione introduce un altro fattore o credenziale, che deve essere fornito per avviare il computer o per la ripresa dalla modalità di ibernazione. Questo vantaggio è importante per utenti a rischio di attacchi di social engineering o che sono soliti utilizzare password non adeguate, come le password Windows su computer non attendibili.

-   **Dati crittografati leggibili dall'interno**. Un vantaggio specifico di EFS rispetto a BitLocker consiste nel fatto che le chiavi di crittografia vengono memorizzate in un archivio chiavi sicuro protetto con le credenziali dell'utente. In questa configurazione, la credenziale è una password. Tuttavia, altri utenti autorizzati del computer possono effettuare l'accesso in modo interattivo o in rete, ma non saranno in grado di accedere ai file riservati presenti nel computer protetti da un altro utente con EFS a meno che quell'utente conceda espressamente l'accesso ai file.

-   **Individuazione della chiave tramite attacchi offline**. La VMK viene crittografata utilizzando una chiave che si trova nell'hardware del TPM insieme a un codice PIN. Se non si è a conoscenza del codice PIN, per chi effettua l'attacco sarà molto difficoltoso determinare il valore della FVEK.

-   **Attacchi offline contro il sistema operativo**. Gli attacchi offline contro il sistema operativo vengono prevenuti dal fatto che chi effettua l'attacco deve recuperare correttamente la SRK dal TPM e poi utilizzarla per decrittografare la VMK oppure effettuare un attacco a forza bruta sulla FVEK. Inoltre, BitLocker configurato con la relativa tecnologia di diffusione (attivata per impostazione predefinita) attenua attacchi mirati di questa natura, poiché le piccole modifiche apportate al testo crittografato si propagheranno su un'area più grande.

-   **Perdita di dati non crittografati tramite il file ibernazione**. Uno degli obiettivi principali di BitLocker è quello di proteggere i dati nel volume del sistema operativo del disco rigido quando il computer viene spento o entra in modalità di ibernazione. Quando BitLocker è attivo, il file ibernazione viene crittografato.

-   **Perdita di dati non crittografati tramite il file di paging del sistema**. In Windows Vista, EFS può essere configurato in modo che esegua la crittografia del file di paging utilizzando una chiave simmetrica temporanea generata al momento dell'avvio, ma mai scritta sul disco. All'arresto del sistema, questa chiave viene eliminata in modo che per recuperare i dati dal file di paging sia necessario un attacco a forza bruta per trovare la chiave simmetrica utilizzata per crittografare il file. Se è attivato anche BitLocker, chi effettua l'attacco dovrebbe disattivare BitLocker e completare correttamente un attacco a forza bruta sulla chiave del file di paging per recuperare informazioni utili.

-   **Fattore di autenticazione richiesto nel computer**. Il codice PIN è un secondo fattore di autenticazione non fisico che non può essere perso insieme al computer a meno che non sia scritto su carta o lasciato in un posto facilmente individuabile.

-   **Errore dell'utente**. Poiché BitLocker è una tecnologia di crittografia completa dei volumi, crittografa tutti i file che si trovano nel volume del sistema operativo Windows Vista. Questa funzionalità consente di impedire errori dell'utente nel prendere decisioni sbagliate riguardo l'applicazione della crittografia.

##### Attenuazioni e rischi residui: BitLocker con TPM, codice PIN ed EFS con Archiviazione chiavi software

BitLocker insieme a EFS non attenua i seguenti rischi senza l'utilizzo di controlli e criteri aggiuntivi. È possibile trovare informazioni su questi rischi e le relative attenuazioni nelle discussioni sullo scenario nel [Capitolo 2: Crittografia unità BitLocker](http://www.microsoft.com/italy/technet/security/guidance/clientsecurity/dataencryption/analysis/4e6ce820-fcac-495a-9f23-73d65d846638.mspx) e [Capitolo 3: crittografia del file system](http://www.microsoft.com/italy/technet/security/guidance/clientsecurity/dataencryption/analysis/dc2cde72-a84d-4716-9a30-f62b608efda1.mspx) della presente *Analisi della protezione*.

-   **Computer in modalità sospensione (standby)**. Lo stato del portatile e le chiavi di crittografia di BitLocker non vengono modificati quando il portatile entra in modalità sospensione. Alla ripresa dalla modalità sospensione, la FVEK rimane accessibile sul computer. Questo rischio può essere attenuato attivando l'impostazione **Chiedi la password al termine della modalità standby**.

-   **Computer lasciato con accesso effettuato e desktop sbloccato**. Un utente che può accedere al desktop di un computer protetto con BitLocker ed EFS ha essenzialmente accesso all'intero computer. Questo rischio può essere attenuato fornendo una formazione nell'ambito della consapevolezza in materia di protezione e considerando l'utilizzo delle impostazioni Criteri di gruppo per bloccare automaticamente il computer dopo un periodo di attività.

-   **Attacchi online contro il sistema operativo**. Gli attacchi online contro il sistema operativo *non* vengono attenuati da questa opzione. Chiunque sia in grado di attaccare con successo il sistema operativo durante l'esecuzione può anche eseguire un codice per recuperare i dati crittografati.

-   **Attacchi alla piattaforma**. Né BitLocker né EFS forniscono una protezione completa contro gli attacchi alla piattaforma.

#### BitLocker con TPM, codice PIN ed EFS con smart card (modalità chiave memorizzata nella cache)

BitLocker con un TPM, codice PIN ed EFS con smart card in modalità chiave memorizzata nella cache attenua quasi tutti i rischi significativi descritti in questa guida. Tuttavia, questa combinazione di tecnologie richiede un sostanziale investimento nella distribuzione dell'infrastruttura delle smart card, quindi risulta più appropriata per le organizzazioni che hanno importanti requisiti aziendali per questo livello di protezione.

##### Rischi attenuati: BitLocker con TPM, codice PIN ed EFS con smart card

-   **Computer in modalità di ibernazione**. BitLocker con TPM e codice PIN attenua questo rischio perché all'utente viene richiesto di fornire il codice PIN alla ripresa del computer dalla modalità di ibernazione.

-   **Individuazione della password di dominio/locale**. Uno dei vantaggi principali dell'opzione BitLocker con un TPM e codice PIN è costituito dal fatto che la soluzione introduce un altro fattore o credenziale, che deve essere fornito per avviare il computer o per la ripresa dalla modalità di ibernazione. Questo vantaggio è importante per utenti a rischio di attacchi di social engineering o che sono soliti utilizzare password non adeguate, come le password Windows su computer non attendibili.

-   **Dati crittografati leggibili dall'interno**. Un vantaggio specifico di EFS rispetto a BitLocker consiste nel fatto che le chiavi di crittografia vengono memorizzate in un archivio chiavi sicuro protetto con le credenziali dell'utente. In questa configurazione, la credenziale è una password. Tuttavia, altri utenti autorizzati del computer possono effettuare l'accesso in modo interattivo o in rete, ma non saranno in grado di accedere ai file riservati presenti nel computer protetti da un altro utente con EFS a meno che quell'utente conceda espressamente l'accesso ai file.

-   **Individuazione della chiave tramite attacchi offline**. La VMK viene crittografata utilizzando una chiave che si trova nell'hardware del TPM insieme a un codice PIN. Se non si è a conoscenza del codice PIN, per chi effettua l'attacco sarà molto difficoltoso determinare il valore della FVEK.

-   **Attacchi offline contro il sistema operativo**. Gli attacchi offline contro il sistema operativo vengono prevenuti dal fatto che chi effettua l'attacco deve recuperare correttamente la SRK dal TPM e poi utilizzarla per decrittografare la VMK oppure effettuare un attacco a forza bruta sulla FVEK. Inoltre, BitLocker configurato con la relativa tecnologia di diffusione (attivata per impostazione predefinita) attenua attacchi mirati di questa natura, poiché le piccole modifiche apportate al testo crittografato si propagheranno su un'area più grande.

-   **Perdita di dati non crittografati tramite il file ibernazione**. Uno degli obiettivi principali di BitLocker è di proteggere i dati che si trovano nel volume del sistema operativo del disco rigido quando il computer viene spento o entra in modalità di ibernazione. Quando BitLocker è attivo, il file ibernazione viene crittografato.

-   **Perdita di dati non crittografati tramite il file di paging del sistema**. In Windows Vista, EFS può essere configurato in modo che esegua la crittografia del file di paging utilizzando una chiave simmetrica temporanea generata al momento dell'avvio, ma mai scritta sul disco. All'arresto del sistema, questa chiave viene eliminata in modo che per recuperare i dati dal file di paging sia necessario un attacco a forza bruta per trovare la chiave simmetrica utilizzata per crittografare il file. Se è attivato anche BitLocker, chi effettua l'attacco dovrebbe disattivare BitLocker e completare correttamente un attacco a forza bruta sulla chiave del file di paging per recuperare informazioni utili.

-   **Fattore di autenticazione richiesto nel computer**. Il codice PIN è un secondo fattore di autenticazione non fisico che non può essere perso insieme al computer a meno che non sia scritto su carta o lasciato in un posto facilmente individuabile.

-   **Errore dell'utente**. Poiché BitLocker è una tecnologia di crittografia completa dei volumi, crittografa tutti i file che si trovano nel volume del sistema operativo Windows Vista. Questa funzionalità consente di impedire errori dell'utente nel prendere decisioni sbagliate riguardo l'applicazione della crittografia.

##### Attenuazioni e rischi residui: BitLocker con TPM, codice PIN ed EFS con smart card

-   **Computer in modalità sospensione (standby)**. Né Bitlocker né EFS in modalità smart card della chiave memorizzata nella cache attenuano questo rischio. Chiunque effettui un attacco e possa accedere al computer in modalità sospensione può riattivare il computer e accedere a tutti i dati a cui l'utente può accedere.

-   **Computer lasciato con accesso effettuato e desktop sbloccato**. In modalità smart card della chiave memorizzata nella cache, questo rischio non viene attenuato. L'autore di un attacco che può accedere al desktop sbloccato può impersonare l'utente legittimo e accedere a tutti i dati a cui l'utente può accedere.

-   **Attacchi online contro il sistema operativo**. Né BitLocker né EFS attenuano completamente il rischio di un attacco online contro il sistema operativo. Chiunque sia in grado di attaccare con successo il sistema operativo durante l'esecuzione può anche eseguire un codice per recuperare i dati crittografati. Tuttavia, EFS con smart card in modalità chiave non memorizzata nella cache fornisce una valida attenuazione contro gli attacchi online che tentano di recuperare le chiavi di crittografia.

-   **Attacchi alla piattaforma**. In modalità memorizzata nella cache, un computer configurato per l'uso di EFS con archiviazione chiavi smart card manterrà in memoria le chiavi EFS e un attacco alla piattaforma potrebbe riuscire a recuperarle. Bitlocker non fornisce protezione contro gli attacchi alla piattaforma.

#### Riepilogo analisi dei rischi

Nella seguente tabella vengono elencati i rischi per i dati e viene indicato se le diverse combinazioni di BitLocker con un TPM, codice PIN ed EFS con Archiviazione chiavi software attenuano ciascun rischio. I rischi che possono essere attenuati con combinazioni specifiche sono indicati con la lettera **Y**. I trattini **-** indicano i rischi per cui la combinazione specifica fornisce un'attenuazione ridotta o inesistente.

**Tabella 4.1. Attenuazione dei rischi di Bitlocker ed EFS**

![](images/Cc162807.53d5723f-6e99-4b7a-9dde-4c45fd75288c(it-it,TechNet.10).gif "Attenuazione dei rischi di Bitlocker ed EFS")

**Download**

[Get the Data Encryption Toolkit for Mobile PCs (in inglese)](http://go.microsoft.com/fwlink/?linkid=81666)

**Partecipa**

[Iscriviti per partecipare al programma Data Encryption Toolkit Beta](https://connect.microsoft.com/invitationuse.aspx?programid=790&invitationid=desa-r7gd-3f73&siteid=14)

**Notifiche di aggiornamento**

[Iscriviti per ricevere informazioni su aggiornamenti e nuovi rilasci](http://go.microsoft.com/fwlink/?linkid=54982)

**Commenti**

[Inviaci i tuoi commenti o suggerimenti](mailto:secwish@microsoft.com?oggetto=analisi%20della%20protezione%20di%20data%20encryption%20toolkit%20for%20mobile%20pc%20su%20technet)

[](#mainsection)[Inizio pagina](#mainsection)
