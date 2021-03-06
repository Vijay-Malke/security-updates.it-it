---
TOCTitle: 'Appendice A: Formati e strumenti di protezione'
Title: 'Appendice A: Formati e strumenti di protezione'
ms:assetid: 'bb480ff2-c590-4af4-8f5d-b8d09bb272bf'
ms:contentKeyID: 20213197
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc163100(v=TechNet.10)'
---

Appendice A: Formati e strumenti di protezione
==============================================

### Appendice A: Formati e strumenti di protezione

Creare, verificare, sviluppare e gestire un'intera serie di criteri e modelli per la propria organizzazione può rappresentare una sfida. Questa appendice offre una panoramica sugli strumenti di Microsoft disponibili e gli eventuali formati dei criteri di protezione.

##### In questa pagina

[](#ebaa)[Strumenti per la protezione](#ebaa)
[](#eaaa)[Formati di file di protezione](#eaaa)

### Strumenti per la protezione

I seguenti strumenti sono disponibili sia con il sistema operativo Windows Server 2003 o come download gratuiti dal sito Web di Microsoft.

#### Configurazione guidata impostazioni di sicurezza

La Configurazione guidata impostazioni di sicurezza (SCW) è stato introdotta in Windows* *Server* *2003 SP1. A differenza dei Criteri di gruppo, non è integrata al servizio directory Active* *Directory, per questo non può essere utilizzata per configurare i criteri a livello di dominio. Tuttavia, offre una metodologia di protezione avanzata coerente che si basa sui ruoli e che utilizza configurazioni guidate, facilitando la creazione di criteri sicuri.

Con SCW è possibile creare in modo facile e rapido criteri prototipo per i ruoli di server multipli basati sulle ultime indicazioni e sulle procedure consigliate da Microsoft. SCW gestirà automaticamente le impostazioni di servizio, le impostazioni del Registro di sistema, le eccezioni di Windows Firewall e molto altro ancora. Comprende la capacità di mettere a punto a distanza il profilo dei computer di destinazione, di sviluppare e di rieseguire criteri. Lo strumento della riga di comando Scwcmd consente a SCW e ai Criteri di gruppo di essere utilizzati insieme per sviluppare criteri per gruppi di computer o per convertire criteri in oggetti Criteri di gruppo (GPO).

#### Editor di configurazione della protezione

Gli strumenti Editor di configurazione della protezione (SCE) sono usati per definire i modelli dei criteri di protezione che possono essere applicati ai computer individuali o a gruppi di computer tramite il criterio di gruppo Active Directory. SCE è apparso dapprima come un componente aggiuntivo per Windows NT 4.0 ed è diventato una parte integrante dei Criteri di gruppo.

SCE non è più un componente separato ed è utilizzato nei seguenti snap-in e utilità amministrative di Microsoft Management Console (MMC):

-   Snap-in Configurazione e analisi della protezione MMC

-   Snap-in Modelli di protezione MMC.

-   Snap-in Editor Criteri di gruppo (utilizzato per la porzione di Impostazioni di protezione della struttura Configurazione computer)

-   Strumento Impostazioni di protezione locale

-   Strumento Criterio di protezione del controller di dominio

-   Strumento Criterio di protezione del dominio

Poiché tutti questi strumenti utilizzano SCE, gli amministratori di Windows hanno a loro disposizione un'interfaccia potente e costante per creare e modificare i criteri, sia che servano per un computer autonomo, sia che vengano sviluppati come GPO.

Per ulteriori informazioni su SCE consultare la Guida di Windows.

#### Utenti e computer di Active Directory

Lo snap-in Utenti e computer Active* *Directory MMC offre la e Computer fornisce la GUI primaria per creare e gestire le unità organizzative (OU) all'interno del dominio. È possibile collegare i GPO e le OU, controllare ordine ed eredità dei criteri e lanciare l'Editore dell'oggetto Criteri di gruppo come un processo separato per modificare i GPO. Lo snap-in non offre comunque un modo coerente e integrato per inventariare, creare e gestire i criteri di gruppo.

È possibile trovare ulteriori informazioni sullo snap-in Utenti e computer Active Directory della MMC nella Guida di Windows.

#### Console di gestione Criteri di gruppo

La Console di gestione Criteri di gruppo (GPMC) è stata ideata da Microsoft in risposta a commenti e suggerimenti dei clienti che necessitavano di un modo migliore per controllare i criteri di gruppo in un ambiente di vaste dimensioni. La GPMC deve essere eseguita su Windows XP con SP1 o Windows Server 2003 ed è composta da uno snap-in MMC e da una serie di interfacce utilizzabili tramite script che possono essere usate per gestire i Criteri di gruppo. Essa è in grado di gestire entrambi i domini Windows 2000 Server e Windows Server 2003.

La GPMC offre le seguenti funzioni:

-   Un'interfaccia utente che si concentra su uso e gestione di Criteri di gruppo.

-   La capacità di eseguire velocemente back-up, ripristino, importazione, esportazione e copia e incolla di GPO.

-   La gestione semplificata della protezione relativa a Criteri di gruppo.

-   Segnalare le capacità dei dati degli strumenti GPO e RSoP (Gruppo di criteri risultante).

-   Operazioni GPO eseguibili tramite script.

La [Console di gestione Criteri di gruppo con Service Pack 1](http://www.microsoft.com/downloads/details.aspx?familyid=0a6d4c24-8cbd-4b35-9272-dd3cbfc81887&displaylang=en) può essere scaricata gratuitamente da parte di tutti i clienti di Windows* *Server* *2003 all'indirizzo www.microsoft.com/downloads/details.aspx?FamilyID=0a6d4c24-8cbd-4b35-9272-dd3cbfc81887&DisplayLang=en.

[](#mainsection)[Inizio pagina](#mainsection)

### Formati di file di protezione

I criteri di protezione possono essere creati e memorizzati in tutta una serie di formati. I seguenti paragrafi forniscono dettagli sui formati dei file utilizzati da Windows Server 2003 più comuni:

#### Criterio SCW (.xml)

SCW introduce un nuovo formato di file basato su XML. I criteri SCW nativi sono salvati con l'estensione .xml. Questi file di criteri XML non hanno uno schema ufficiale, ma possono essere identificati dall'elemento &lt;SecurityPolicy Version="1.0"&gt;.

Il file di criteri SCW è un esempio evidente e completo di vari tipi diversi di impostazioni:

-   Modalità di avvio servizi di sistema

-   Eccezioni di Windows Firewall

-   Ruoli selezionati dei computer

-   Attività selezionate dei computer

-   Impostazioni del Registro di sistema

-   Impostazioni dei criteri

-   Criteri di controllo

I criteri SCW possono anche essere collegati a uno o più modelli di criteri per offrire una funzionalità aggiuntiva che non è nativa di SCW, come i servizi di sistema o gli elenchi di controllo di accesso (ACL) al registro di sistema.

#### Modello dei criteri (.inf)

I modelli dei criteri sono dei file di testo che seguono un formato standard per i file di dati di Windows: una o più sezioni che sono messe in risalto da speciali parole chiave tra parentesi quadre, seguite da una o più coppie di attributi/valori.

I modelli dei criteri possono contenere una o più sezioni che definiscono i seguenti tipi di dati:

-   Criteri password

-   Criteri di blocco

-   Criteri del protocollo di autenticazione Kerberos

-   Criteri di controllo

-   Impostazioni del Registro eventi

-   Valori del registro di sistema

-   Modalità di avvio del servizio

-   Autorizzazioni di servizio

-   Diritti utente

-   Restrizioni per l'appartenenza ai gruppi

-   Autorizzazioni del Registro di sistema

-   Autorizzazioni del file system

I modelli dei criteri sono supportati da quasi tutti gli strumenti elencati in precedenza in questa appendice e il medesimo formato di modello può essere utilizzato per entrambi i criteri del computer locale e i Criteri di gruppo Active* *Directory. Prima di poter essere utilizzati, i modelli devono essere importati dallo strumento idoneo.

#### Oggetti Criteri di gruppo

Gli oggetti Criteri di gruppo (GPO) sono i dati memorizzati sia nella Active Directory sia come raccolta di file in directory speciali sui controller di dominio. Questi file di criterio rappresentano i criteri utente e quelli del computer e generalmente non sono manipolati direttamente. Per modificare le impostazioni o esportare il GPO in un modello di criterio è possibile usare uno strumento tipo la console GPMC.

Per salvare tutte le informazioni memorizzate nel GPO nel file system è possibile esportare o eseguire il back-up del GPO dall'interno della console GPMC. I back-up dei GPO che sono stati creati in questo modo mantengono le seguenti informazioni:

-   Il GUID dell’oggetto Criteri di gruppo e le

-   impostazioni dell’oggetto Criteri di gruppo del dominio

-   L’elenco di controllo di accesso discrezionale (DACL) per l’oggetto Criteri di gruppo

-   Il collegamento al filtro WMI, se presente, ma non il filtro

-   I collegamenti ai criteri di protezione di IP, se presenti

-   Un report in formato XML delle impostazioni dell’oggetto Criteri di gruppo, che può essere visualizzato come file HTML dalla console GPMC

-   Data e ora del backup

-   Descrizione del backup fornita dall’utente

Questo back-up non salva comunque nessuno dei dati esterni al GPO. In particolare, questo file non conterrà le informazioni sui collegamenti di siti, domini o OU e non conterrà filtri WMI reali o criteri di protezione IP.

**Download**

[Utilizzo della Guida per la protezione di Windows Server 2003](http://go.microsoft.com/fwlink/?linkid=14846)

**Notifiche di aggiornamento**

[Iscriversi per ottenere aggiornamenti e nuove versioni](http://go.microsoft.com/fwlink/?linkid=54982)

**Commenti e suggerimenti**

[Inviare commenti o suggerimenti](mailto:%20secwish@microsoft.com?subject=guida%20per%20la%20protezione%20di%20windows%20server%202003)

[](#mainsection)[Inizio pagina](#mainsection)
