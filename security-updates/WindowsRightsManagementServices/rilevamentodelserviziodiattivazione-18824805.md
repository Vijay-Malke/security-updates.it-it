---
TOCTitle: Rilevamento del Servizio di attivazione
Title: Rilevamento del Servizio di attivazione
ms:assetid: 'e178d81b-b35c-4958-87ef-e077e2204b32'
ms:contentKeyID: 18824805
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc747697(v=WS.10)'
---

Rilevamento del Servizio di attivazione
=======================================

Il servizio di attivazione rende disponibili archivi protetti e certificati computer di RMS per i client RMS versione 1.0. In questo modo, viene garantita la compatibilità con RMS versione 1.0. Il cluster di certificazione principale RMS fornisce il servizio proxy di attivazione che inoltra le richieste di attivazione del computer RMS al servizio di attivazione dai computer client che operano all'interno della rete aziendale.

Per inviare una richiesta di attivazione del computer RMS, per prima cosa il client RMS versione 1.0 deve richiamare da Active Directory l'URL della directory virtuale Certification del server di certificazione principale in cui si trova il servizio proxy di attivazione. Fatto ciò, vi aggiunge il percorso del servizio proxy di attivazione.

Ad esempio, l'URL della directory virtuale Certification del server di certificazione principale è memorizzato in Active Directory nel formato seguente:

http://*nome\_server*/\_wmcs/Certification

Quando un client richiede l'attivazione del computer RMS, aggiunge il nome del file del servizio proxy di attivazione all'URL, come indicato di seguito:

http://*nome\_server*/\_wmcs/Certification/Activation.asmx

I client che operano fuori dalla rete aziendale utilizzano UDDI per il rilevamento dei servizi e per localizzare il servizio di attivazione. Per ulteriori informazioni, vedere "[Pubblicazione di servizi ospitati da Microsoft](https://technet.microsoft.com/7ee8cb4d-1b46-48be-8a4c-5ff6a458231a)" più indietro in questo argomento.

| ![](images/Cc747697.note(WS.10).gif)Nota                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------|
| Qualora SSL sia stato abilitato sul server RMS, gli URL mostrati appariranno con l'indicazione dell'utilizzo del protocollo di connessione https://. |
