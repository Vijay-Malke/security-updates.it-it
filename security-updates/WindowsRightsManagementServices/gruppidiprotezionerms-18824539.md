---
TOCTitle: Gruppi di protezione RMS
Title: Gruppi di protezione RMS
ms:assetid: '25749a83-8c12-48ec-96ad-296d31fd55d4'
ms:contentKeyID: 18824539
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720215(v=WS.10)'
---

Gruppi di protezione RMS
========================

Nel programma di installazione RMS vengono creati due gruppi, il gruppo di servizi RMS e il gruppo di utenti con privilegi avanzati.

Il gruppo di servizi RMS è un gruppo di protezione locale cui vengono assegnati diritti sufficienti ad avere accesso a tutte le risorse necessarie per l'impiego di RMS. Durante l'installazione, l'amministratore specifica l'account utente da utilizzare come account di servizio di RMS. Questo account utente viene aggiunto automaticamente al gruppo del servizio RMS ed eredita pertanto le relative autorizzazioni. Durante la maggior parte delle normali operazioni, RMS viene eseguito impiegando questo account utente.

Un altro importante gruppo di RMS è il gruppo di utenti con privilegi avanzati. Questo gruppo ha il controllo completo di tutto il contenuto, pertanto i membri del gruppo possono decrittografare tutti i file di contenuto protetto con RMS e rimuoverne tutte le protezioni di RMS. Per impostazione predefinita, il gruppo di utenti con privilegi avanzati non ha alcun membro e non comprendere automaticamente gli amministratori di RMS. La gestione dell'appartenenza al gruppo è di fondamentale importanza per la sicurezza del contenuto protetto con RMS. Per ulteriori informazioni, vedere "Utilizzo del gruppo di utenti con privilegi avanzati" in "Gestione di un server RMS", in questa documentazione.
