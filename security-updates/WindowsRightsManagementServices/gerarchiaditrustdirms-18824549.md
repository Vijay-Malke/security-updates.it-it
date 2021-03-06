---
TOCTitle: Gerarchia di trust di RMS
Title: Gerarchia di trust di RMS
ms:assetid: '2d44182f-a653-4383-aba1-dade53f7cf9a'
ms:contentKeyID: 18824549
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Cc720232(v=WS.10)'
---

Gerarchia di trust di RMS
=========================

Tra i componenti che fanno parte del sistema RMS vi sono il servizio di Enrollment Microsoft, i server RMS aziendali, i computer client e gli utenti del sistema. A ogni componente viene rilasciato un certificato che ne stabilisce l'identità all'interno del sistema. Una gerarchia di trust definisce la relazione di trust esistente tra tali certificati e, di conseguenza, tra le entità in loro possesso. Inoltre, definisce la relazione di trust esistente tra entità attendibili e le licenze da esse rilasciate per altre entità attendibili.

La gerarchia di trust consente di connettere certificati e licenze in una catena di trust su cui RMS si basa sempre per passare da un particolare certificato o licenza a una coppia di chiavi attendibili. La catena di trust include il certificato corrente, il certificato dell'entità che lo ha rilasciato, il certificato dell'entità che ha rilasciato il certificato di questa entità e così via fino all'elemento principale della catena di trust.

Per RMS, l'elemento principale della catena di trust, o "gerarchia di trust", è una coppia di chiavi Microsoft. Questo elemento principale comune del trust consente a un'organizzazione di creare un ecosistema di trust comprendente entità attendibili, ad esempio utenti e partner, sia interne che esterne all'organizzazione.

Nella figura riportata di seguito è illustrata la gerarchia di trust di un'organizzazione. La catena di trust risale fino ai servizi Microsoft che rilasciano i certificati di base.

![](images/Cc720232.6c169175-94fb-4ec0-93bc-12748aae3ac4(WS.10).gif)
1.  Ciascun computer client riceve un archivio protetto univoco contenente la chiave pubblica principale Microsoft.
2.  Quando riceve una richiesta di licenza, RMS ne convalida le entità seguendo il percorso indicato nella gerarchia di trust fino all'elemento principale della catena di trust.
3.  RMS verifica l'autenticità dell'entità attendibile indicata nella licenza.
4.  RMS verifica che il certificato dell'entità attendibile sia stato emesso da un server presente nella gerarchia di trust.

A ogni livello della catena di certificati, RMS convalida la licenza o il certificato, quindi verifica che siano in grado di connettersi con un elemento principale della catena di trust rilevato attraverso una catena di certificati. Ogni licenza o certificato presenti nella catena viene controllato da RMS per verificare le seguenti condizioni:

-   Il linguaggio XrML sia valido.
-   La firma dell'autorità emittente sia valida.
-   La semantica della licenza sia appropriata per l'uso previsto.
-   Siano soddisfatte condizioni quali le date di validità.
-   La licenza non sia stata revocata.
-   Le chiavi della firma della licenza e dell'autorità emittente certificata corrispondano.
