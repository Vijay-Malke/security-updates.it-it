    ---
    TOCTitle: Configurazione di Windows Firewall mediante Criteri di gruppo in aziende di piccole dimensioni
    Title: Configurazione di Windows Firewall mediante Criteri di gruppo in aziende di piccole dimensioni
    ms:assetid: 'be4467be-5a2c-4ae2-925a-c2e1f6e33e4b'
    ms:contentKeyID: 20213190
    ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc875816(v=TechNet.10)'
    ---

    Configurazione di Windows Firewall mediante Criteri di gruppo in aziende di piccole dimensioni
    ==============================================================================================

    ##### In questa pagina

    [](#ehaa)[Introduzione](#ehaa)  
    [](#egaa)[Prima di iniziare](#egaa)  
    [](#efaa)[Installazione degli aggiornamenti rapidi per le workstation amministrative e per Windows Small Business Server 2003](#efaa)  
    [](#eeaa)[Creazione e aggiornamento degli oggetti Criteri di gruppo](#eeaa)  
    [](#edaa)[Configurazione delle impostazioni di Windows Firewall mediante Criteri di gruppo](#edaa)  
    [](#ecaa)[Applicazione della configurazione tramite GPUpdate](#ecaa)  
    [](#ebaa)[Verifica dell'applicazione delle impostazioni di Windows Firewall](#ebaa)  
    [](#eaaa)[Informazioni correlate](#eaaa)  

    ### Introduzione

    In questo documento vengono illustrate le procedure per configurare le funzionalità di Windows Firewall nei computer che eseguono Microsoft Windows XP Professional Service Pack 2 (SP2) in aziende di piccole o medie dimensioni. Nelle aziende di questo tipo è possibile che siano presenti controller di dominio che eseguono Microsoft Windows Small Business Server 2003, Microsoft Windows Server 2003 oppure Microsoft Windows 2000 Server.

    Il modo più efficace per gestire le impostazioni di Windows Firewall in una rete aziendale è utilizzare il servizio directory Active Directory e configurare tali impostazioni in Criteri di gruppo. Tramite Active Directory e Criteri di gruppo è possibile eseguire la configurazione centralizzata delle impostazioni di Windows Firewall e applicare tali impostazioni a tutti i computer client che eseguono Windows XP SP2.

    In Windows XP SP2 sono disponibili nuovi modelli amministrativi per gli oggetti Criteri di gruppo (GPO, Group Policy Object). Tali modelli consentono di migliorare il livello di protezione del computer client e del dominio in uso, comprese le funzionalità di Windows Firewall. A seconda del sistema operativo del server di dominio o della workstation in uso è possibile che per applicare questi modelli sia necessario installare aggiornamenti rapidi.

    Dopo aver applicato tali modelli, tutti gli aggiornamenti di Criteri di gruppo includeranno le impostazioni di Windows Firewall. Gli aggiornamenti di Criteri di gruppo vengono inviati dal controller di dominio a tutti i membri del dominio. Tali aggiornamenti possono essere inoltre richiesti dai membri del dominio tramite l'utilità GPUpdate.

    Per configurare Windows Firewall, accedere come membro del gruppo Domain Admins o del gruppo di protezione Proprietari autori criteri di gruppo e utilizzare l'Editor oggetti Criteri di gruppo.

    Nella tabella seguente vengono elencate le impostazioni predefinite di Windows Firewall.

    **Tabella 1. Impostazioni predefinite di Windows Firewall**

    
    <table style="border:1px solid black;">
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th style="border:1px solid black;" >Opzione</th>
    <th style="border:1px solid black;" >Configurazione predefinita</th>
    <th style="border:1px solid black;" >Caso in cui apportare modifiche</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td style="border:1px solid black;">Impostazioni connessione di rete</td>
    <td style="border:1px solid black;">Tutte le connessioni</td>
    <td style="border:1px solid black;">Necessità di interrompere la protezione di Windows Firewall per una determinata connessione di rete o di implementare impostazioni specifiche per ogni connessione di rete.</td>
    </tr>
    <tr class="even">
    <td style="border:1px solid black;">Eccezioni programmi</td>
    <td style="border:1px solid black;">Soltanto Assistenza remota</td>
    <td style="border:1px solid black;">Necessità di ricevere sul computer in uso connessioni provenienti da altri programmi o servizi.</td>
    </tr>
    <tr class="odd">
    <td style="border:1px solid black;">Eccezioni porte</td>
    <td style="border:1px solid black;">Nessuna</td>
    <td style="border:1px solid black;">Necessità di accettare sul computer in uso connessioni provenienti da un altro computer che utilizza porte specifiche.</td>
    </tr>
    <tr class="even">
    <td style="border:1px solid black;">Eccezioni ICMP</td>
    <td style="border:1px solid black;">Nessuna</td>
    <td style="border:1px solid black;">Necessità che gli altri computer verifichino che il computer in uso sia in funzione e che il protocollo TCP/IP sia configurato correttamente.</td>
    </tr>
    <tr class="odd">
    <td style="border:1px solid black;">Notifiche</td>
    <td style="border:1px solid black;">Attivate</td>
    <td style="border:1px solid black;">Necessità di interrompere la ricezione delle notifiche relative ai tentativi non riusciti di connessione al computer in uso da parte di altri computer.</td>
    </tr>
    <tr class="even">
    <td style="border:1px solid black;">Registrazione</td>
    <td style="border:1px solid black;">Disattivata</td>
    <td style="border:1px solid black;">Necessità di registrare le connessioni e i tentativi di connessione al computer in uso.</td>
    </tr>
    <tr class="odd">
    <td style="border:1px solid black;">Non consentire eccezioni</td>
    <td style="border:1px solid black;">Disattivata</td>
    <td style="border:1px solid black;">Individuazione di una vulnerabilità di protezione o utilizzo del computer in un ambiente a protezione ridotta, ad esempio la sala d'attesa di un aeroporto.</td>
    </tr>
    </tbody>
    </table>
    
    Le attività per configurare Windows Firewall mediante Criteri di gruppo sono le seguenti:
    
    -   Installazione degli aggiornamenti rapidi per le workstation di amministrazione di GPO e per Windows Small Business Server 2003.
    
    -   Creazione e aggiornamento di GPO.
    
    -   Configurazione delle impostazioni di Windows Firewall mediante Criteri di gruppo.
    
    -   Applicazione della configurazione tramite GPUpdate.
    
    -   Verifica dell'applicazione delle impostazioni di Windows Firewall.
    
    Le attività descritte nel presente documento consentono di proteggere il computer in uso da worm e altro codice dannoso, senza tuttavia impedire le connessioni Internet in ingresso e in uscita.
    
    Al fine di garantire che la configurazione di Criteri di gruppo non causi interruzioni delle attività aziendali o perdite di produttività, prima di distribuire le impostazioni di Criteri di gruppo di Windows Firewall nell'ambiente di produzione è consigliabile verificarle in un ambiente di prova.
    
    Per conoscere le definizioni dei termini correlati alla protezione, consultare la risorsa seguente:
    
    -   [Microsoft Security Glossary](http://go.microsoft.com/fwlink/?linkid=35468), disponibile nel sito Web Microsoft all'indirizzo http://go.microsoft.com/fwlink/?LinkId=35468 (in inglese).
    
    #### Scopo del presente documento relativo alla protezione
    
    Grazie all'esecuzione delle procedure descritte dettagliatamente nel presente documento sarà possibile implementare un firewall basato su host in grado di proteggere i client Windows XP Professional in uso da accessi non autorizzati e malware. Tali procedure consentiranno inoltre di attivare la gestione della protezione avanzata mediante Active Directory.
    
    [](#mainsection)[Inizio pagina](#mainsection)
    
    ### Prima di iniziare
    
    **Importante**   Le istruzioni contenute nel presente documento sono state sviluppate avendo come riferimento il menu predefinito che viene visualizzato quando si fa clic sul pulsante **Start**. Se il menu Start è stato modificato, la procedura potrebbe essere leggermente diversa.
    
    Per poter utilizzare il sistema operativo Windows XP con SP2 in computer client appartenenti a un dominio di Active Directory è necessario che il controller di dominio utilizzato esegua uno dei sistemi operativi seguenti:
    
    -   Windows Server 2003
    
    -   Windows Small Business Server 2003
    
    -   Windows 2000 Server SP4 o versioni successive
    
    Nella maggior parte delle reti, il firewall hardware di rete, il proxy e gli altri sistemi con funzionalità analoghe offrono ai computer di rete un livello di protezione da Internet.
    
    Se le connessioni di rete del computer in uso non sono protette da un firewall host (ovvero da un firewall software installato localmente) quale Windows Firewall, il sistema utilizzato risulta vulnerabile all'introduzione di programmi dannosi da parte di altri computer connessi in rete. Tale vulnerabilità, inoltre, si presenta quando il computer viene utilizzato all'esterno della rete aziendale, come accade ad esempio nel caso di computer portatili aziendali utilizzati in casa o connessi alla rete di un hotel o di un aeroporto.
    
    Prima di installare gli aggiornamenti rapidi, assicurarsi di aver eseguito correttamente un backup del computer, incluso un backup del Registro di sistema.
    
    Per ulteriori informazioni sull'esecuzione di un backup del Registro di sistema, consultare l'articolo seguente:
    
    -   Articolo della Microsoft Knowledge Base 322756, "[HOW TO: Eseguire il backup, modificare e ripristinare il Registro di sistema in Windows XP](http://go.microsoft.com/fwlink/?linkid=36365)" disponibile nel sito Web Supporto Tecnico Microsoft all'indirizzo http://go.microsoft.com/fwlink/?linkid=36365.
    
    [](#mainsection)[Inizio pagina](#mainsection)
    
    ### Installazione degli aggiornamenti rapidi per le workstation amministrative e per Windows Small Business Server 2003
    
    Se i computer utilizzati per gestire le impostazioni degli oggetti Criteri di gruppo presentano versioni precedenti di sistemi operativi o Service Pack (ad esempio Windows XP con SP1 oppure Windows Server 2003), è necessario installare un aggiornamento rapido ([KB842933](http://go.microsoft.com/fwlink/?linkid=35474)). Tale aggiornamento è necessario affinché le impostazioni dei criteri vengano visualizzate correttamente nell'Editor oggetti Criteri di gruppo.
    
    Se si utilizza Small Business Server 2003, è necessario installare un aggiornamento rapido aggiuntivo ([KB872769](http://go.microsoft.com/fwlink/?linkid=35477)). Per impostazione predefinita, Windows Firewall viene disattivato da Small Business Server 2003. Il suddetto aggiornamento rapido consente di risolvere questo problema.
    
    **Nota**   Gli aggiornamenti rapidi elencati non sono inclusi in Microsoft Update e devono essere installati a parte. Tali aggiornamenti devono essere applicati singolarmente a ogni computer da aggiornare.
    
    L'aggiornamento rapido KB842933 si applica ai sistemi operativi seguenti:
    
    -   Microsoft Windows Server 2003, Web Edition
    
    -   Microsoft Windows Server 2003, Standard Edition (per sistemi a 32 bit con processore x86)
    
    -   Microsoft Windows Server 2003, Enterprise Edition (per sistemi a 32 bit con processore x86)
    
    -   Microsoft Windows Server 2003, Enterprise Edition per sistemi con processore Itanium
    
    -   Microsoft Windows XP Professional SP1
    
    -   Microsoft Windows Small Business Server 2003 Premium Edition
    
    -   Microsoft Windows Small Business Server 2003 Standard Edition
    
    -   Microsoft Windows 2000 Advanced Server
    
    -   Microsoft Windows 2000 Server
    
    -   Microsoft Windows 2000 Professional Edition
    
    L'aggiornamento rapido KB872769 si applica ai sistemi operativi seguenti:
    
    -   Microsoft Windows Small Business Server 2003 Standard Edition
    
    -   Microsoft Windows Small Business Server 2003 Premium Edition
    
    Per ulteriori informazioni o per ottenere i suddetti aggiornamenti rapidi, consultare gli articoli seguenti:
    
    -   Articolo della Microsoft Knowledge Base [842933](http://go.microsoft.com/fwlink/?linkid=35474), disponibile nel sito Web Supporto Tecnico Microsoft all'indirizzo http://go.microsoft.com/fwlink/?linkid=35474.
    
    -   Articolo della Microsoft Knowledge Base [872769](http://go.microsoft.com/fwlink/?linkid=35477), disponibile nel sito Web Supporto Tecnico Microsoft all'indirizzo http://go.microsoft.com/fwlink/?linkid=35477.
    
    Per ulteriori informazioni su come scaricare i file di supporto Microsoft, consultare la risorsa seguente:
    
    -   "[Come ottenere file di supporto Microsoft dai servizi online](http://support.microsoft.com/kb/119591)", disponibile nel sito Web Supporto Tecnico Microsoft all'indirizzo http://support.microsoft.com/kb/119591.
    
    #### Requisiti per l'esecuzione dell'attività
    
    Per completare questa attività è necessario disporre di quanto segue:
    
    -   **Credenziali**: è necessario accedere al computer client con un account membro del gruppo di protezione Domain Admins o Administrators locale.
    
    -   **Strumenti**: è necessario scaricare e installare l'aggiornamento rapido appropriato per il sistema operativo in uso, come spiegato negli articoli 842933 e 872769 della Knowledge Base.
    
    #### Installazione degli aggiornamenti rapidi
    
    **Per installare l'aggiornamento rapido 842933 per Windows Small Business Server 2003,** **Windows 2000 Server SP4 o versioni successive,** **Windows XP SP1** **oppure Windows Server 2003**
    
    1.  Nel desktop di Windows, fare clic sul pulsante **Start**, scegliere **Esegui**, digitare il percorso e il nome del file dell'aggiornamento rapido scaricato, quindi fare clic su **OK**.
    
    2.  Nella schermata **Installazione guidata di KB842933**, fare clic su **Avanti**.
    
    3.  Nella pagina **Contratto di Licenza**, leggere le condizioni del contratto di licenza. Per continuare, fare clic su **Accetto** e quindi su **Avanti**.
    
    4.  Nella schermata **Completamento Installazione guidata di KB842933**, fare clic su **Fine** per completare l'installazione dell'aggiornamento rapido e riavviare il computer.
    
    5.  Ripetere i passaggi da 1 a 4 per tutti i computer su cui occorre installare l'aggiornamento rapido (server e workstation di gestione).
    
    **Per installare l'aggiornamento rapido 872769 per Windows Small Business Server 2003**
    
    1.  Nel desktop di Windows, fare clic sul pulsante **Start**, scegliere **Esegui**, digitare il percorso e il nome del file dell'aggiornamento rapido scaricato, quindi fare clic su **OK**.
    
    2.  Nella schermata **Installazione guidata di KB872769**, fare clic su **Avanti**.
    
    3.  Nella pagina **Contratto di Licenza**, leggere le condizioni del contratto di licenza. Per continuare, fare clic su **Accetto** e quindi su **Avanti**.
    
    4.  Nella pagina **Completamento Installazione guidata di KB872769**, fare clic su **Fine** per completare l'installazione dell'aggiornamento rapido e riavviare il computer.
    
    [](#mainsection)[Inizio pagina](#mainsection)
    
    ### Creazione e aggiornamento degli oggetti Criteri di gruppo
    
    In Windows XP SP2 sono disponibili nuove impostazioni per i Modelli amministrativi. Per configurare queste impostazioni è necessario aggiornare ogni GPO con i nuovi Modelli amministrativi contenuti in Windows XP SP2. In caso contrario, le impostazioni di Windows Firewall non saranno disponibili.
    
    Nei computer Windows XP SP2 per aggiornare un GPO è sufficiente aprirlo utilizzando la console MMC (Microsoft Management Console) in cui è stato installato lo snap-in Editor oggetti Criteri di gruppo.
    
    Dopo aver eseguito l'aggiornamento di un GPO è possibile configurare le impostazioni di protezione di rete appropriate per i computer Windows XP SP2 in uso. Nell'esercizio seguente viene descritta la procedura per creare un nuovo GPO in cui le suddette impostazioni di protezione di rete aggiornate saranno immediatamente disponibili.
    
    #### Requisiti di esecuzione dell'attività
    
    Per completare questa attività è necessario disporre degli elementi seguenti:
    
    -   **Credenziali**: è necessario accedere come membro del gruppo Domain Admins o del gruppo di protezione Proprietari autori criteri di gruppo a un computer Windows XP SP2 che funzioni come client di dominio di Active Directory.
    
    -   **Strumenti**: Microsoft Management Console (MMC) in cui è stato installato lo snap-in Editor oggetti Criteri di gruppo.
    
    #### Creazione e aggiornamento di oggetti Criteri di gruppo
    
    **Per aggiornare gli oggetti Criteri di gruppo con i nuovi Modelli amministrativi di Windows XP SP2**
    
    1.  Nel desktop di Windows XP SP2, fare clic sul pulsante **Start**, scegliere **Esegui** e digitare **mmc**. Fare quindi clic su **OK**.
    
    2.  Scegliere **Aggiungi/Rimuovi snap-in** dal menu **File**.
    
    3.  Nella scheda **Autonomo**, fare clic su **Aggiungi**.
    
    4.  Nell'elenco **Snap-in autonomi disponibili**, individuare e scegliere **Editor oggetti Criteri di gruppo**. Fare quindi clic su **Aggiungi**.
    
    5.  Nella finestra di dialogo **Selezione oggetto Criteri di gruppo**, fare clic su **Sfoglia**.
    
    6.  Nella finestra di dialogo **Ricerca oggetto Criteri di gruppo** (illustrata nella figura seguente), fare clic su **Crea nuovo oggetto Criteri di gruppo** e denominare il GPO appena creato **Criteri di prova di Windows Firewall per client**.
    
        ![](images/Cc875816.WFGP01(it-it,TechNet.10).gif "WFGP01.GIF")
    
    7.  Fare clic su **OK** e quindi su **Fine** per chiudere la Procedura guidata Criteri di gruppo e applicare i nuovi modelli amministrativi al GPO selezionato.
    
    8.  Nella finestra di dialogo **Aggiungi snap-in autonomo**, fare clic su **Chiudi**.
    
    9.  Nella finestra di dialogo **Aggiungi/Rimuovi snap-in**, fare clic su **OK**.
    
    10. Chiudere MMC, scegliere **Esci** dal menu **File**. Non salvare le modifiche apportate alle impostazioni della console.
    
        **Nota**   Anche se le modifiche alla console non vengono salvate, al termine della procedura appena descritta i nuovi Modelli amministrativi di Windows XP SP2 verranno importati nel GPO. I Modelli devono essere importati in ogni GPO definito.
    
    11. Ripetere la suddetta procedura per ogni GPO utilizzato per applicare Criteri di gruppo ai computer Windows XP SP2.
    
    Per aggiornare i GPO negli ambienti di rete in cui si utilizzano Active Directory e Windows XP SP2 è consigliabile ricorrere alla console Gestione Criteri di gruppo, disponibile gratuitamente. Per ulteriori informazioni, consultare la risorsa seguente:
    
    -   "[Enterprise Management with the Group Policy Console](http://go.microsoft.com/fwlink/?linkid=35479)", disponibile nel sito Web Microsoft Windows Server 2003 all'indirizzo http://go.microsoft.com/fwlink/?linkID=35479 (in inglese).
    
    [](#mainsection)[Inizio pagina](#mainsection)
    
    ### Configurazione delle impostazioni di Windows Firewall mediante Criteri di gruppo
    
    Le impostazioni di Windows Firewall da configurare possono essere raggruppate nei due insiemi seguenti:
    
    -   **Profilo di dominio**: queste impostazioni vengono utilizzate dai computer connessi a una rete in cui sono presenti controller di dominio a cui tali computer appartengono.
    
    -   **Profilo predefinito**: queste impostazioni vengono utilizzate dai computer quando non sono connessi a una rete, come accade ad esempio nel caso di un computer portatile utilizzato in viaggio.
    
    Se le impostazioni dei profili predefiniti non vengono configurate, i valori predefiniti non subiscono modifiche. Per entrambi i profili è consigliabile eseguire sia la configurazione delle impostazioni sia l'attivazione di Windows Firewall. Ciò vale a meno che non si utilizzi un firewall host (ovvero un firewall software installato localmente) di terze parti, nel qual caso è opportuno disattivare Windows Firewall.
    
    Le impostazioni del profilo di dominio sono in genere meno restrittive rispetto a quelle del profilo predefinito. Queste, infatti, non riguardano applicazioni e servizi utilizzati esclusivamente in ambienti di domini gestiti.
    
    Nei GPO, entrambi i profili contengono lo stesso insieme di impostazioni di Windows Firewall. Per stabilire quali impostazioni di profilo applicare, Windows XP SP2 prevede l'esecuzione di un'apposita analisi di rete.
    
    **Nota**   Per ulteriori informazioni sulla suddetta analisi, vedere [Network Determination Behavior for Network-Related Group Policy Settings](http://technet.microsoft.com/en-us/library/bb878049.aspx), disponibile nel sito Web Microsoft TechNet all'indirizzo http://go.microsoft.com/fwlink/?linkid=35480 (in inglese).
    
    In questa sezione vengono descritte le impostazioni possibili di un GPO, le impostazioni consigliate per le aziende di piccole o medie dimensioni e le procedure per configurare i quattro tipi principali di impostazioni di GPO.
    
    #### Requisiti di esecuzione dell'attività
    
    Per completare questa attività è necessario disporre di quanto segue:
    
    -   **Credenziali**: è necessario accedere come membro del gruppo di protezione Domain Admins o Proprietari autori criteri di gruppo a un computer Windows XP SP2 che funzioni come client di dominio di Active Directory.
    
    -   **Strumenti**: Microsoft Management Console (MMC) in cui è stato installato lo snap-in Editor oggetti Criteri di gruppo.
    
    **Nota**   Per aprire un GPO, utilizzare la console Utenti e computer di Active Directory oppure lo strumento MMC in cui è stato installato lo snap-in Editor oggetti Criteri di gruppo. Per poter utilizzare la console Utenti e computer di Active Directory in un computer client Windows XP è necessario eseguire il file Aadminpak.msi contenuto nel CD di Windows Server 2003.
    
    #### Configurazione delle impostazioni di Windows Firewall mediante Criteri di gruppo
    
    Utilizzare lo snap-in Criteri di gruppo per modificare le impostazioni di Windows Firewall nei GPO appropriati.
    
    Dopo aver completato la procedura descritta di seguito per configurare le impostazioni di Windows Firewall, utilizzare l'utilità GPUpdate nei computer client. In alternativa, attendere che le impostazioni vengano applicate ai computer client nel corso dei cicli di aggiornamento standard. Per impostazione predefinita, tali cicli si verificano a intervalli di 90 minuti, con un ritardo o un anticipo casuale di 30 minuti. Durante l'aggiornamento dei Criteri di gruppo della configurazione del computer, le nuove impostazioni di Windows Firewall verranno scaricate e applicate ai computer in cui è in esecuzione Windows XP SP2.
    
    **Per configurare le impostazioni di Windows Firewall mediante Criteri di gruppo**
    
    1.  Nel desktop di Windows XP SP2, fare clic sul pulsante **Start**, scegliere **Esegui** e digitare **mmc**. Fare quindi clic su **OK**.
    
    2.  Scegliere **Aggiungi/Rimuovi snap-in** dal menu **File**.
    
    3.  Nella scheda **Autonomo**, fare clic su **Aggiungi**.
    
    4.  Nell'elenco **Snap-in autonomi disponibili**, individuare e scegliere l'opzione **Editor oggetti Criteri di gruppo**. Fare quindi clic su **Aggiungi**.
    
    5.  Nella finestra di dialogo **Selezione oggetto Criteri di gruppo**, fare clic su **Sfoglia**.
    
    6.  Selezionare il **GPO Criteri di prova di Windows Firewall per client**. Fare clic su **OK** e quindi su **Fine**.
    
    7.  Fare clic su **Chiudi** per chiudere la finestra di dialogo **Aggiungi snap-in autonomo** e quindi, nella finestra di dialogo **Aggiungi/Rimuovi snap-in** fare clic su **OK**.
    
    8.  Nella struttura della console dell'Editor oggetti Criteri di gruppo, come mostrato nella figura seguente, aprire **Configurazione computer**, **Modelli amministrativi**, **Rete**, **Connessioni di rete** e quindi **Windows Firewall**.
    
        ![](images/Cc875816.WFGP02(it-it,TechNet.10).gif "WFGP02.GIF")
    
    9.  Selezionare **Profilo di dominio** (come mostrato nella figura seguente) oppure **Profilo standard**.
    
        ![](images/Cc875816.WFGP03(it-it,TechNet.10).gif "WFGP03.GIF")
    
        Nella tabella seguente sono elencate le impostazioni consigliate di Criteri di gruppo per Windows Firewall relativamente al profilo di dominio e al profilo predefinito.
    
        **Tabella 2. Impostazioni consigliate di Windows Firewall**
        
        <table style="border:1px solid black;">
        <colgroup>
        <col width="25%" />
        <col width="25%" />
        <col width="25%" />
        <col width="25%" />
        </colgroup>
        <thead>
        <tr class="header">
        <th style="border:1px solid black;" >Impostazione</th>
        <th style="border:1px solid black;" >Descrizione</th>
        <th style="border:1px solid black;" >Profilo di dominio</th>
        <th style="border:1px solid black;" >Profilo predefinito</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td style="border:1px solid black;">Proteggi tutte le connessioni di rete</td>
        <td style="border:1px solid black;">Consente di attivare Windows Firewall su tutte le connessioni di rete.</td>
        <td style="border:1px solid black;">Attivata.</td>
        <td style="border:1px solid black;">Attivata.</td>
        </tr>
        <tr class="even">
        <td style="border:1px solid black;">Non consentire eccezioni</td>
        <td style="border:1px solid black;">Se questa opzione è attivata il traffico in ingresso non richiesto viene ignorato, compreso il traffico consentito.</td>
        <td style="border:1px solid black;">Non configurata.</td>
        <td style="border:1px solid black;">Attivata, a meno che non sia necessario configurare eccezioni programmi.</td>
        </tr>
        <tr class="odd">
        <td style="border:1px solid black;">Definisci eccezioni programmi</td>
        <td style="border:1px solid black;">Consente di definire il traffico consentito in termini di nomi di file di programma.</td>
        <td style="border:1px solid black;">Attivata e configurata per i programmi (applicazioni e servizi) utilizzati dai computer Windows XP SP2 connessi alla rete in uso.</td>
        <td style="border:1px solid black;">Attivata e configurata per i programmi (applicazioni e servizi) utilizzati dai computer Windows XP SP2 connessi alla rete in uso.</td>
        </tr>
        <tr class="even">
        <td style="border:1px solid black;">Consenti eccezioni programmi locali</td>
        <td style="border:1px solid black;">Consente la configurazione locale delle eccezioni programmi.</td>
        <td style="border:1px solid black;">Disattivata, a meno che non si desideri che gli amministratori locali configurino localmente le eccezioni programmi.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        <tr class="odd">
        <td style="border:1px solid black;">Consenti eccezione per amministrazione remota</td>
        <td style="border:1px solid black;">Consente la configurazione remota mediante strumenti.</td>
        <td style="border:1px solid black;">Disattivata, a meno che non si desideri poter amministrare in remoto i computer in uso utilizzando snap-in MMC.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        <tr class="even">
        <td style="border:1px solid black;">Consenti eccezione condivisione file e stampanti</td>
        <td style="border:1px solid black;">Permette di specificare se il traffico di condivisione di file e stampanti è consentito.</td>
        <td style="border:1px solid black;">Disattivata, a meno che i computer Windows XP SP2 non condividano risorse locali.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        <tr class="odd">
        <td style="border:1px solid black;">Consenti eccezioni ICMP</td>
        <td style="border:1px solid black;">Permette di specificare i tipi di messaggi ICMP consentiti.</td>
        <td style="border:1px solid black;">Disattivata, a meno che non si desideri utilizzare il comando ping per la risoluzione dei problemi.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        <tr class="even">
        <td style="border:1px solid black;">Consenti eccezione per Desktop remoto</td>
        <td style="border:1px solid black;">Consente di specificare se il computer è autorizzato ad accettare una richiesta di connessione basata su Desktop remoto.</td>
        <td style="border:1px solid black;">Attivata.</td>
        <td style="border:1px solid black;">Attivata.</td>
        </tr>
        <tr class="odd">
        <td style="border:1px solid black;">Consenti eccezione per framework UPnP</td>
        <td style="border:1px solid black;">Consente di specificare se il computer è autorizzato a ricevere messaggi UPnP non richiesti.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        <tr class="even">
        <td style="border:1px solid black;">Proibisci notifiche</td>
        <td style="border:1px solid black;">Consente di disattivare le notifiche.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        <tr class="odd">
        <td style="border:1px solid black;">Consenti registrazione</td>
        <td style="border:1px solid black;">Consente di creare e gestire registri riguardanti il traffico e di configurare le impostazioni dei file di registro.</td>
        <td style="border:1px solid black;">Non configurata.</td>
        <td style="border:1px solid black;">Non configurata.</td>
        </tr>
        <tr class="even">
        <td style="border:1px solid black;">Impedisci risposte unicast a richieste multicast o broadcast</td>
        <td style="border:1px solid black;">Consente di ignorare i pacchetti unicast ricevuti in risposta a un messaggio di richiesta multicast o broadcast.</td>
        <td style="border:1px solid black;">Attivata.</td>
        <td style="border:1px solid black;">Attivata.</td>
        </tr>
        <tr class="odd">
        <td style="border:1px solid black;">Definisci eccezioni porte</td>
        <td style="border:1px solid black;">Permette di specificare il traffico consentito in termini di TCP e UDP.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        <tr class="even">
        <td style="border:1px solid black;">Consenti eccezioni porte locali</td>
        <td style="border:1px solid black;">Consente la configurazione locale delle eccezioni porte.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        <td style="border:1px solid black;">Disattivata.</td>
        </tr>
        </tbody>
        </table>
    
    10. Fare doppio clic su ogni impostazione elencata nella tabella 2, fare clic su **Attivata**, **Disattivata** o **Non configurata**, quindi, fare clic su **OK**.
    
    #### Attivazione delle eccezioni porte
    
    **Per attivare le eccezioni porte**
    
    1.  Nell'area delle impostazioni di **Profilo di dominio** o **Profilo standard**, fare doppio clic su **Windows Firewall: definisci eccezioni porte**. Verrà visualizzata la finestra di dialogo seguente.
    
        ![](images/Cc875816.WFGP04(it-it,TechNet.10).gif "WFGP04.GIF")
    
    2.  Selezionare **Attivata**, quindi fare clic su **Mostra**. Verrà visualizzata la finestra di dialogo **Visualizzazione contenuto**, come illustrato nella figura seguente.
    
        [![](images/Cc875816.WFGP05(it-it,TechNet.10).gif "WFGP05.GIF")](https://technet.microsoft.com/it-it/cc875816.wfgp05_big(it-it,technet.10).gif)
    
    3.  Fare clic su **Aggiungi**. Verrà visualizzata la finestra di dialogo **Aggiunta elemento**. Digitare le informazioni riguardanti la porta che si desidera bloccare o abilitare. La sintassi è la seguente:
    
        porta:trasporto:ambito:stato:nome
    
        -   **porta** indica il numero di porta
    
        -   **trasporto** può assumere i valori TCP o UDP
    
        -   **ambito** può assumere il valore \* per indicare tutti i computer, oppure può contenere l'elenco dei computer autorizzati ad accedere alla porta
    
        -   **stato** può assumere i valori "enabled" (porta abilitata) o "disabled" (porta disabilitata)
    
        -   **nome** indica la stringa di testo utilizzata come etichetta dell'elemento da aggiungere
    
        L'esempio illustrato nella figura seguente riguarda un elemento denominato TestWeb e prevede l'abilitazione della porta TCP 80 per tutte le connessioni.
    
        ![](images/Cc875816.WFGP06(it-it,TechNet.10).gif "WFGP06.GIF")
    
    4.  Dopo aver immesso le informazioni, fare clic su **OK** per chiudere la finestra di dialogo **Aggiunta elemento**. Verrà visualizzata la finestra di dialogo **Visualizzazione contenuto** illustrata nella figura seguente.
    
        [![](images/Cc875816.WFGP07(it-it,TechNet.10).gif "WFGP07.GIF")](https://technet.microsoft.com/it-it/cc875816.wfgp07_big(it-it,technet.10).gif)
    
    5.  Fare clic su **OK** per chiudere la finestra di dialogo **Visualizzazione contenuto**.
    
    6.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà Windows Firewall: definisci eccezioni porte**.
    
    #### Attivazione delle eccezioni programmi
    
    **Per attivare le eccezioni programmi**
    
    1.  Nell'area delle impostazioni di **Profilo di dominio** o **Profilo standard**, fare doppio clic su **Windows Firewall: definisci eccezioni programmi**. Verrà visualizzata la finestra di dialogo seguente.
    
        ![](images/Cc875816.WFGP08(it-it,TechNet.10).gif "WFGP08.GIF")
    
    2.  Selezionare **Attivata**, quindi fare clic su **Mostra**. Verrà visualizzata la finestra di dialogo **Visualizzazione contenuto** illustrata nella figura seguente.
    
        [![](images/Cc875816.WFGP09(it-it,TechNet.10).gif "WFGP09.GIF")](https://technet.microsoft.com/it-it/cc875816.wfgp09_big(it-it,technet.10).gif)
    
    3.  Fare clic su **Aggiungi**. Verrà visualizzata la finestra di dialogo **Aggiunta elemento**. Digitare le informazioni riguardanti il programma che si desidera bloccare o abilitare. La sintassi è la seguente:
    
        percorso:ambito:stato:nome
    
        -   **percorso** indica il percorso e il nome del file del programma
    
        -   **ambito** può assumere il valore \*, a indicare tutti i computer, oppure può contenere l'elenco dei computer autorizzati ad accedere al programma
    
        -   **stato** può assumere i valori "enabled" (programma abilitato) o "disabled" (programma disabilitato)
    
        -   **nome** indica la stringa di testo utilizzata come etichetta dell'elemento da aggiungere
    
        L'esempio illustrato nella figura seguente riguarda un elemento denominato Messenger e prevede l'abilitazione del programma Windows Messenger, memorizzato nel percorso %program files%\\messenger\\msmsgs.exe, per tutte le connessioni.
    
        ![](images/Cc875816.WFGP10(it-it,TechNet.10).gif "WFGP10.GIF")
    
    4.  Dopo aver immesso le informazioni, fare clic su **OK** per chiudere la finestra di dialogo **Aggiunta elemento**. Verrà visualizzata la finestra di dialogo **Visualizzazione contenuto** illustrata nella figura seguente.
    
        [![](images/Cc875816.WFGP11(it-it,TechNet.10).gif "WFGP11.GIF")](https://technet.microsoft.com/it-it/cc875816.wfgp11_big(it-it,technet.10).gif)
    
    5.  Fare clic su **OK** per chiudere la finestra di dialogo **Visualizzazione contenuto**.
    
    6.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà Windows Firewall: definisci eccezioni programmi**.
    
    #### Configurazione delle opzioni di base di ICMP
    
    **Per configurare le opzioni di base di ICMP**
    
    1.  Nell'area delle impostazioni di **Profilo di dominio** o **Profilo standard**, fare doppio clic su **Windows Firewall: consenti eccezioni ICMP**. Verrà visualizzata la finestra di dialogo seguente.
    
        ![](images/Cc875816.WFGP12(it-it,TechNet.10).gif "WFGP12.GIF")
    
    2.  Selezionare **Attivata**, quindi, selezionare le eccezioni ICMP appropriate da attivare. Nell'esempio illustrato nella figura seguente viene selezionata l'opzione **Consenti richiesta echo in ingresso**.
    
        È inoltre possibile selezionare **Disattivata** per disattivare una o più eccezioni ICMP.
    
    3.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà Windows Firewall: consenti eccezioni ICMP**.
    
    #### Registrazione dei pacchetti in ingresso ignorati e delle connessioni riuscite
    
    **Per registrare i pacchetti in ingresso ignorati e le connessioni riuscite**
    
    1.  Nell'area delle impostazioni di **Profilo di dominio** o **Profilo standard**, fare doppio clic su **Windows Firewall: consenti registrazione**. Verrà visualizzata la finestra di dialogo seguente.
    
        ![](images/Cc875816.WFGP13(it-it,TechNet.10).gif "WFGP13.GIF")
    
    2.  Selezionare **Attivata**, quindi, selezionare le opzioni **Registra pacchetti in ingresso ignorati** e **Registra connessioni riuscite**. Immettere un valore in **Percorso e nome del file registro** e non modificare la **Dimensione massima (KB)** predefinita del file di registro, quindi, fare clic su **OK**.
    
        **Nota**   Assicurarsi di salvare il file di registro in un percorso protetto per impedire che venga modificato involontariamente o volontariamente.
    
    3.  Dopo aver apportato tutte le modifiche desiderate alle impostazioni di Windows Firewall, chiudere la console.
    
        **Nota**   Quando si chiude la console, verrà richiesto se si desidera salvarla. Indipendentemente dalla scelta effettuata, le impostazioni GPO verranno salvate.
    
    4.  Se viene richiesto di salvare la console, fare clic su **No**.
    
    [](#mainsection)[Inizio pagina](#mainsection)
    
    ### Applicazione della configurazione tramite GPUpdate
    
    L'utilità GPUpdate consente di aggiornare le impostazioni di Criteri di gruppo basate su Active Directory. Dopo aver configurato Criteri di gruppo è possibile attendere che le impostazioni vengano applicate ai computer client nel corso dei cicli di aggiornamento standard. Per impostazione predefinita, tali cicli si verificano a intervalli di 90 minuti, con un ritardo o un anticipo casuale di 30 minuti. L'utilità GPUpdate consente invece di aggiornare immediatamente Criteri di gruppo.
    
    #### Requisiti di esecuzione dell'attività
    
    Per completare questa attività è necessario disporre di quanto segue:
    
    -   **Credenziali**: è necessario accedere come membro del gruppo Domain Users a un computer Windows XP SP2 che funzioni come client di dominio di Active Directory.
    
    #### Esecuzione di GPUpdate
    
    **Per eseguire GPUpdate**
    
    1.  Nel desktop di Windows XP SP2, fare clic sul pulsante **Start** e scegliere **Esegui**.
    
    2.  Nella finestra di dialogo **Esegui**, digitare **cmd**, quindi, fare clic su **OK**.
    
    3.  Al prompt dei comandi, digitare **GPUpdate** e premere INVIO. Verrà visualizzata una schermata simile alla seguente:
    
        [![](images/Cc875816.WFGP14(it-it,TechNet.10).gif "WFGP14.GIF")](https://technet.microsoft.com/it-it/cc875816.wfgp14_big(it-it,technet.10).gif)
    
    4.  Per chiudere il prompt dei comandi, digitare **Exit** e premere INVIO.
    
    [](#mainsection)[Inizio pagina](#mainsection)
    
    ### Verifica dell'applicazione delle impostazioni di Windows Firewall
    
    **Nota**   Quando si utilizza Criteri di gruppo per configurare Windows Firewall è possibile impedire agli amministratori locali di accedere ad alcuni elementi di configurazione. In tal caso, nei computer locali alcune schede e opzioni della finestra di dialogo Windows Firewall risulteranno non disponibili.
    
    #### Requisiti di esecuzione dell'attività
    
    Per completare questa attività è necessario disporre di quanto segue:
    
    -   **Credenziali**: è necessario accedere come membro del gruppo Domain Users a un computer Windows XP SP2 che funzioni come client di dominio di Active Directory.
    
    **Per verificare l'applicazione delle impostazioni di Windows Firewall**
    
    1.  Nel desktop di Windows XP SP2, fare clic sul pulsante **Start** e scegliere **Pannello di controllo**.
    
    2.  In **Scegliere una categoria**, fare clic su **Centro sicurezza PC**. Verrà visualizzata una schermata simile alla seguente:
    
        [![](images/Cc875816.WFGP15(it-it,TechNet.10).gif "WFGP15.GIF")](https://technet.microsoft.com/it-it/cc875816.wfgp15_big(it-it,technet.10).gif)
    
    3.  In **Gestione impostazioni di protezione per**, fare clic su **Windows Firewall**.
    
    4.  Fare clic sulle schede **Generale**, **Eccezioni** e **Avanzate** e verificare che nel computer client la configurazione di Criteri di gruppo sia stata applicata anche a Windows Firewall.
    
    Se le impostazioni della configurazione non sono state applicate è necessario effettuare la risoluzione dei problemi dell'applicazione di Criteri di gruppo. A tale scopo, consultare la risorsa seguente:
    
    -   "[Risoluzione dei problemi di Criteri di gruppo in Microsoft Windows Server](http://go.microsoft.com/fwlink/?linkid=35481)", disponibile nell'Area download Microsoft all'indirizzo http://go.microsoft.com/fwlink/?linkid=35481 (in inglese).
    
    [](#mainsection)[Inizio pagina](#mainsection)
    
    ### Informazioni correlate
    
    Per ulteriori informazioni sul firewall di Windows XP, consultare le risorse seguenti:
    
    -   "[Deploying Windows Firewall Settings for Microsoft Windows XP with Service Pack 2](http://go.microsoft.com/fwlink/?linkid=35303)", disponibile nell'Area download Microsoft all'indirizzo http://go.microsoft.com/fwlink/?linkid=35303 (in inglese).
    
    -   "[Informazioni su Windows Firewall](http://www.microsoft.com/italy/windowsxp/using/security/internet/sp2_wfintro.mspx)" nel sito Web Microsoft Windows XP all'indirizzo http://www.microsoft.com/italy/windowsxp/using/security/internet/sp2\_wfintro.mspx.
    
    Per ulteriori informazioni sulla protezione di Windows XP SP2, consultare la risorsa seguente:
    
    -   [*Windows XP Security Guide*](http://go.microsoft.com/fwlink/?linkid=35309), disponibile nell'Area download Microsoft all'indirizzo http://go.microsoft.com/fwlink/?linkid=35309 (in inglese).
    
    Per conoscere le definizioni dei termini correlati alla protezione, consultare la risorsa seguente:
    
    -   [Microsoft Security Glossary](http://www.microsoft.com/security/glossary.mspx), disponibile nel sito Web Microsoft all'indirizzo http://go.microsoft.com/fwlink/?linkid=35468 (in inglese).
    
    **Download**
    
    [Download della guida Configurazione di Windows Firewall mediante Criteri di gruppo in aziende di piccole dimensioni](http://go.microsoft.com/fwlink/?linkid=70393)
    
    [](#mainsection)[Inizio pagina](#mainsection)
