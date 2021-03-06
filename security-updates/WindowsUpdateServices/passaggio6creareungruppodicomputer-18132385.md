---
TOCTitle: 'Passaggio 6: Creare un gruppo di computer'
Title: 'Passaggio 6: Creare un gruppo di computer'
ms:assetid: '6039e5dc-d2ce-4d4b-b737-17ebcadbd4a7'
ms:contentKeyID: 18132385
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720536(v=WS.10)'
---

Passaggio 6: Creare un gruppo di computer
=========================================

I gruppi di computer rappresentano una parte molto importante della distribuzione di WSUS e consentono di distribuire gli aggiornamenti a computer specifici. Sono disponibili due gruppi di computer predefiniti, ovvero Tutti i computer e Computer non assegnati. Per impostazione predefinita, un computer client che contatta il server di WSUS per la prima volta viene aggiunto a entrambi i gruppi.

È possibile creare gruppi di computer personalizzati. La creazione dei gruppi di computer è utile poiché consente di testare gli aggiornamenti prima di distribuirli in modo diffuso. Se i risultati del test sono soddisfacenti, gli aggiornamenti possono essere distribuiti al gruppo Tutti i computer. È possibile creare un numero illimitato di gruppi personalizzati.

La configurazione dei gruppi di computer è un processo costituito da tre passaggi. È innanzitutto necessario specificare la modalità di assegnazione dei computer ai gruppi di computer. Sono disponibili due opzioni: *distribuzione degli aggiornamenti sul lato server* e *distribuzione degli aggiornamenti sul lato client*. Se si utilizza la distribuzione degli aggiornamenti sul lato server, ogni computer deve essere aggiunto manualmente al proprio gruppo mediante WSUS. Se si utilizza la distribuzione degli aggiornamenti sul lato client, i client vengono aggiunti automaticamente mediante Criteri di gruppo o le chiavi del Registro di sistema. In secondo luogo, è necessario creare il gruppo di computer in WSUS. I computer vengono infine spostati nei gruppi mediante la modalità scelta nel primo passaggio.

Il presente documento contiene istruzioni per l'utilizzo della distribuzione degli aggiornamenti sul lato server, nonché lo spostamento manuale dei computer nei gruppi mediante la console WSUS. Se si dispone di numerosi computer client da assegnare ai gruppi, è consigliabile utilizzare la distribuzione degli aggiornamenti sul lato client che consente di automatizzare lo spostamento dei computer nei gruppi di computer.

È possibile utilizzare il passaggio 6 per configurare un gruppo Test contenente almeno un computer per il test.

In questo passaggio vengono illustrate le procedure seguenti:

-   Specificare la distribuzione degli aggiornamenti sul lato server.
-   Creare un gruppo.
-   Spostare i computer nel gruppo.

**Per specificare la modalità di assegnazione dei computer ai gruppi**
1.  Sulla barra degli strumenti della console WSUS fare clic su **Opzioni** e quindi fare clic su **Opzioni computer**.

2.  Nella casella **Opzioni computer** fare clic su **Usa l'attività Sposta computer in Windows Server Update Services**.

3.  In **Attività** fare clic su **Salva impostazioni** e quindi fare clic su **OK** nella finestra di dialogo che verrà visualizzata.

**Per creare un gruppo**
1.  Sulla barra degli strumenti della console WSUS fare clic su **Computer**.

2.  In **Attività** fare clic su **Crea gruppo di computer**.

3.  Nella casella **Nome gruppo** digitare **Test** e quindi fare clic su **OK**.

Utilizzare la procedura seguente per assegnare un computer client appropriato per il test al gruppo Test. Un computer client appropriato è rappresentato da qualsiasi computer che dispone dei requisiti hardware e software comuni alla maggior parte dei computer della rete ma non svolge un ruolo importante. In questo modo, è possibile valutare l'impatto degli aggiornamenti approvati nei computer con caratteristiche analoghe a quelle del computer utilizzato per il test.

**Per aggiungere manualmente un computer al gruppo Test**
1.  Sulla barra degli strumenti della console WSUS fare clic su **Computer**.

2.  Nella casella **Gruppi** fare clic sul gruppo di computer che si desidera spostare.

3.  Nell'elenco dei computer fare clic sul computer che si desidera spostare.

4.  In **Attività** fare clic su **Sposta il computer selezionato**.

5.  Nell'elenco **Gruppo di computer** selezionare il gruppo nel quale si desidera spostare il computer e quindi fare clic su **OK**.
