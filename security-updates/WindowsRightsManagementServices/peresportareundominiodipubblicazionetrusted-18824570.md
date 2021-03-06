---
TOCTitle: Per esportare un dominio di pubblicazione trusted
Title: Per esportare un dominio di pubblicazione trusted
ms:assetid: '3fb138dd-e324-43f8-97e0-da0027a036a3'
ms:contentKeyID: 18824570
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720252(v=WS.10)'
---

Per esportare un dominio di pubblicazione trusted
=================================================

Per eseguire questa procedura, è necessario avere effettuato l'accesso locale al sito Web di amministrazione con un account utente di dominio che faccia parte del gruppo Administrators nel computer in cui si sta effettuando l'accesso. La procedura può essere inoltre eseguita dai membri del gruppo Domain Admins. Per garantire maggiore protezione, eseguire la procedura utilizzando **Esegui come**.

Per visualizzare la pagina **Amministrazione globale**, fare clic su **Start**, scegliere **Tutti i programmi**, quindi **Windows RMS** e infine **Amministrazione di Windows RMS**.

Esportazione di un dominio di pubblicazione trusted
---------------------------------------------------

#### Per esportare un dominio di pubblicazione trusted

1.  Visualizzare la pagina **Amministrazione globale** e selezionare **Amministra RMS in questo sito Web** accanto al sito Web in cui si desidera aggiungere un dominio di pubblicazione trusted.

2.  Nell'area **Collegamenti per l'amministrazione,** selezionare **Criteri di trust**.

3.  Nella pagina **Criteri di trust**, nell'area **Domini di pubblicazione trusted**, fare clic su **Esporta** accanto al contenitore della chiave per il server RMS

4.  Viene visualizzata la finestra di dialogo **Esportazione dominio di pubblicazione trusted**.

5.  Digitare la password da utilizzare per la crittografia del file del dominio di pubblicazione trusted. Per importare il file su un altro server RMS, è obbligatorio l'uso della password. È necessario specificare una password complessa.

6.  Inserire nuovamente la password per confermare la correttezza della password immessa.

7.  Digitare il percorso e il nome file da utilizzare per il file .xml del dominio di pubblicazione trusted. Assicurarsi di specificare l'estensione .xml del nome file.

8.  Fare clic su **Esporta** per creare il file del dominio di pubblicazione trusted.

Per ulteriori informazioni sull'esecuzione di questa procedura, vedere "[Aggiunta e rimozione di domini di pubblicazione trusted](https://technet.microsoft.com/d87b502d-5497-4ccd-badf-f6807d587cee)", più indietro in questo argomento.
