---
TOCTitle: Nozioni sul processo di rimozione delle autorizzazioni
Title: Nozioni sul processo di rimozione delle autorizzazioni
ms:assetid: '57bd9949-9433-437b-93ed-ffb2dff9992e'
ms:contentKeyID: 18824604
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720276(v=WS.10)'
---

Nozioni sul processo di rimozione delle autorizzazioni
======================================================

Mediante Internet Information Services (IIS), RMS espone vari servizi offerti. Ad esempio, il servizio di certificazione registra gli utenti e i loro computer, mentre il servizio di gestione licenze pubblica i contenuti e fornisce l'accesso alle informazioni protette con RMS. Un servizio aggiuntivo, chiamato servizio di rimozione delle autorizzazioni, deve essere abilitato sul server RMS per avviare il processo di rimozione delle autorizzazioni. Quando il servizio di rimozione delle autorizzazioni è abilitato, tutti gli altri servizi RMS forniti dal server sono disabilitati.

Una volta abilitato il server RMS per la rimozione delle autorizzazioni, le applicazioni possono ottenere dal servizio di rimozione delle autorizzazioni una chiave per i contenuti, che permette all'applicazione di decrittografare in modo permanente il contenuto protetto con RMS.

Quando il server RMS opera in modalità di rimozione delle autorizzazioni, qualsiasi utente, indipendentemente dal fatto che disponga o meno dei diritti sul contenuto originale protetto con RMS, può ottenere una chiave per il contenuto e acquisire diritti completi per accedere ad esso.

Una volta decrittografato il contenuto, l'utente può salvarlo senza la protezione RMS. Tener presente che, per utilizzare il servizio di rimozione delle autorizzazioni, l'utente deve essere registrato nell'infrastruttura RMS. Un utente che non dispone di un client RMS attivato non può utilizzare il servizio di rimozione delle autorizzazioni per ottenere l'accesso al contenuto protetto con RMS.
