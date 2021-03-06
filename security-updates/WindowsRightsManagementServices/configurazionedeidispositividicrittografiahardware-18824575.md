---
TOCTitle: Configurazione dei dispositivi di crittografia hardware
Title: Configurazione dei dispositivi di crittografia hardware
ms:assetid: '3a35a8ea-696c-4005-9892-cac6e773497a'
ms:contentKeyID: 18824575
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720248(v=WS.10)'
---

Configurazione dei dispositivi di crittografia hardware
=======================================================

RMS può utilizzare i provider del servizio di crittografia (CSP) standard di Windows, come i CSP di base e avanzato, per generare le chiavi pubbliche e private che verranno archiviate nel database di configurazione e utilizzate per proteggere i contenuti. Si raccomanda di applicare alle chiavi un'ulteriore protezione in quanto sono registrate nel software. Per fornire un livello di protezione più elevato, è possibile utilizzare un CSP basato su un modulo di protezione hardware (HSM).

Se si utilizza un HSM per fornire un'ulteriore protezione alle chiavi del server, installare e configurare l'hardware sui server prima di avviare l'installazione di RMS.
