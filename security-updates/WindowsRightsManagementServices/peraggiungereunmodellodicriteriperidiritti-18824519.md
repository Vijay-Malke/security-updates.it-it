---
TOCTitle: Per aggiungere un modello di criteri per i diritti
Title: Per aggiungere un modello di criteri per i diritti
ms:assetid: '1a5555cd-6d39-4078-a879-4106864674be'
ms:contentKeyID: 18824519
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720206(v=WS.10)'
---

Per aggiungere un modello di criteri per i diritti
==================================================

Per eseguire questa procedura, è necessario avere effettuato l'accesso locale al sito Web di amministrazione con un account utente di dominio che faccia parte del gruppo Administrators nel computer in cui si sta effettuando l'accesso. La procedura può essere inoltre eseguita dai membri del gruppo Domain Admins. Per garantire maggiore protezione, eseguire la procedura utilizzando **Esegui come**.

Per visualizzare la pagina **Amministrazione globale**, fare clic su **Start**, scegliere **Tutti i programmi**, quindi **Windows RMS** e infine **Amministrazione di Windows RMS**.

Aggiunta di un modello di criteri per i diritti
-----------------------------------------------

#### Per aggiungere un modello di criteri per i diritti

1.  Visualizzare la pagina **Amministrazione globale** e selezionare **Amministra RMS in questo sito Web** accanto al sito Web in cui si desidera aggiungere un modello di criteri per i diritti.

2.  Nell'area **Collegamenti per l'amministrazione,** selezionare **Modelli criteri diritti**.

3.  In **Lingua**, fare clic per selezionare la lingua che si desidera utilizzare con il modello.

4.  Scegliere **Aggiungi un modello criteri diritti**.

5.  Nell'area **Identificazione modello,** specificare un nome, una descrizione e l'URL richiesta diritti per il modello.

6.  Nel campo **Aggiungi utenti o gruppi** dell'area **Utenti e gruppi,** digitare un indirizzo di posta elettronica valido dell'utente o del gruppo da aggiungere e scegliere **Aggiungi**. Ripetere la procedura per aggiungere altri utenti o gruppi.

7.  In **Utenti o gruppi correnti,** selezionare l'indirizzo di posta elettronica di un utente o di un gruppo a cui si desidera assegnare i diritti.

8.  Selezionare le caselle di controllo relative a tutti i diritti che si desidera concedere all'utente o al gruppo selezionato. Ripetere la procedura per garantire i diritti agli altri utenti o gruppi.

9.  Nell'area **Criterio scadenza,** selezionare una delle tre opzioni di scadenza e specificare una data o un'ora di scadenza, come richiesto. Se necessario, selezionare **Le licenze d'uso per il contenuto devono essere rinnovate ogni** e specificare il numero di giorni che devono trascorrere tra i rinnovi.

10. Nell'area **Criterio esteso,** selezionare una o più delle quattro opzioni. Qualora si selezioni **Applica dati specifici dell'applicazione**, specificare un nome e un valore per i dati da applicare e scegliere **Aggiungi**.

11. Per applicare le revoche, nell'area **Criterio revoca,** selezionare la casella di controllo **Richiedi revoca** e attenersi alla procedura descritta di seguito.

    1.  Nella casella **URL o UNC**, digitare l'URL in cui è inserito il file dell'elenco di revoche. Se si desidera offrire supporto agli utenti disconnessi o esterni, tale URL deve essere accessibile sia dalla rete aziendale che da Internet.
    2.  In **Intervallo di aggiornamento elenco revoche,** digitare il numero di giorni desiderati per la validità dell'elenco di revoche. Qualora un utente disponga di una copia dell'elenco meno recente rispetto al valore specificato, dovrà ottenere una copia aggiornata per utilizzare il contenuto.
    3.  Nella casella **File chiave pubblica,** digitare il percorso e il nome file oppure scegliere **Sfoglia** per individuare il file della chiave pubblica per l'elenco di revoche. Per ulteriori informazioni su questo file, vedere "Aggiunta di una firma in un elenco di revoche", più indietro in questo argomento.

    | ![](images/Cc720206.Caution(WS.10).gif)Attenzione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
    |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | Prestare attenzione quando si applicano le revoche. In base all'intervallo di aggiornamento specificato, è necessario rinnovare l'elenco di revoche periodicamente affinché non scada automaticamente impedendo di conseguenza agli utenti di utilizzare i contenuti che richiedono tale elenco. Per assicurarsi di non impedire involontariamente agli utenti di utilizzare i contenuti, valutare attentamente l'intervallo necessario per l'aggiornamento dell'elenco di revoche. Per ulteriori informazioni, vedere "[Gestione delle revoche](https://technet.microsoft.com/df732a7d-1fb0-4845-87ca-fab4bc5f98a0)" più indietro in questo argomento. |

12. Scegliere **Invia**.

Per ulteriori informazioni sulle revoche, vedere "[Gestione delle revoche](https://technet.microsoft.com/df732a7d-1fb0-4845-87ca-fab4bc5f98a0)" più indietro in questo argomento.

Per osservazioni sul modo per specificare le opzioni di revoca, vedere "[Definizione dei criteri di revoca](https://technet.microsoft.com/e2fffe9f-def7-439b-a8aa-43f8a065813d)" più indietro in questo argomento.

Per osservazioni sul modo per eseguire questa procedura, vedere "[Creazione e modifica dei modelli di criteri per i diritti](https://technet.microsoft.com/6014176f-ef71-4d29-b3e3-da129c18563d)" più indietro in questo argomento.
