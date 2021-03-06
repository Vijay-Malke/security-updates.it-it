---
TOCTitle: Gestione dei certificati concessore di licenze server
Title: Gestione dei certificati concessore di licenze server
ms:assetid: '549979ad-13ee-4abc-8281-3e002a5a9561'
ms:contentKeyID: 18824600
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720272(v=WS.10)'
---

Gestione dei certificati concessore di licenze server
=====================================================

I certificati concessore di licenze server scadono dopo un periodo specificato, solitamente dopo un anno. Per rinnovare un certificato concessore di licenze server, è necessario eseguire l'accesso come amministratore locale. Quando si rinnova il certificato concessore di licenze server per il cluster di certificazione principale, tramite RMS viene inviata una richiesta per il rinnovo del certificato al Servizio di Enrollment Microsoft. Quando si rinnova il certificato per un server licenze, tramite RMS viene inviata la richiesta di rinnovo al server di certificazione principale da cui è stato emesso il certificato in scadenza.

Vi sono tre eventi inviati da RMS nel Registro eventi di sistema che è consigliabile monitorare. Questi eventi indicano quando si sta avvicinando la data di rinnovo del certificato concessore di licenze server oppure la scadenza del certificato stesso. Nella tabella seguente, vengono elencati i nomi e gli ID di tali eventi.

###  

 
<table style="border:1px solid black;">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th style="border:1px solid black;" >ID evento</th>
<th style="border:1px solid black;" >Nome evento</th>
<th style="border:1px solid black;" >Tipo di evento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="border:1px solid black;">16</td>
<td style="border:1px solid black;">LicensorCertExpiresInOneMonthEvent</td>
<td style="border:1px solid black;">Avvertenza. Il servizio continua a funzionare regolarmente.</td>
</tr>
<tr class="even">
<td style="border:1px solid black;">17</td>
<td style="border:1px solid black;">LicensorCertExpiresInOneWeekEvent</td>
<td style="border:1px solid black;">Avvertenza. Il servizio continua a funzionare regolarmente.</td>
</tr>
<tr class="odd">
<td style="border:1px solid black;">18</td>
<td style="border:1px solid black;">LicensorCertExpiredEvent</td>
<td style="border:1px solid black;">Errore. Il servizio è stato disattivato.</td>
</tr>
</tbody>
</table>
