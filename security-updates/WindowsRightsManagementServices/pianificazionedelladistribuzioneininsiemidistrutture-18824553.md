---
TOCTitle: Pianificazione della distribuzione in insiemi di strutture
Title: Pianificazione della distribuzione in insiemi di strutture
ms:assetid: '2dfb40b7-95b1-4362-b32e-72867544b705'
ms:contentKeyID: 18824553
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720233(v=WS.10)'
---

Pianificazione della distribuzione in insiemi di strutture
==========================================================

Se si distribuisce RMS in un ambiente con più insiemi di strutture, è necessario determinare il supporto che potrebbe essere necessario per gli utenti o i gruppi esterni all'insieme di strutture in cui è distribuito RMS. Purtroppo, di solito accade che gli oggetti utente o gruppo di altri insiemi di strutture non abbiano oggetti rappresentativi nell'insieme di strutture dove risiede RMS. Se si progetta di utilizzare RMS per limitare le autorizzazioni a utenti o gruppi provenienti da altri insiemi di strutture, è necessario configurare adeguatamente il proprio insieme di strutture per consentire al gruppo di espandersi su più insiemi di strutture.

È possibile implementare per RMS il supporto per l'espansione del gruppo in insiemi di strutture in due modi:

-   Distribuire RMS nell'insieme di strutture in cui sono definiti i gruppi e dove verrà utilizzato per espandere l'appartenenza di questi gruppi.
-   Sincronizzare le definizioni dei gruppi tra gli insiemi di strutture per permettere all'installazione locale RMS di determinare l'appartenenza completa al gruppo per tutti gli utenti. Se l'utente che richiede una licenza d'uso ha un account Windows in un insieme di strutture separato, ci deve anche essere un oggetto contatto nell'insieme di strutture locale per rappresentare l'appartenenza dell'utente al gruppo. È possibile utilizzare metadirectory, come Microsoft® Identity Integration Server (MIIS) 2003 o Identity Integration Feature Pack (IIFP), per implementare una fedele sincronizzazione degli oggetti gruppo su più insiemi di strutture.

Se si prevede di utilizzare RMS per un solo insieme di strutture, è possibile ottimizzare il processo di emissione delle licenze d'uso modificando il criterio **MaxCrossForestCalls** del cluster nel database di configurazione RMS. Questo criterio specifica il numero massimo di volte in cui l'appartenenza a un gruppo può oltrepassare i confini di un insieme di strutture. Il valore predefinito è 10. Per modificare il valore in 0, utilizzare il seguente comando SQL:

`update DRMS_ClusterPolicies set PolicyData=0 dove PolicyName='MaxCrossForestCalls'`
