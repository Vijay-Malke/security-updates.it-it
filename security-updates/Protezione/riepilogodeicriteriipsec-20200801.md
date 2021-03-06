---
TOCTitle: Riepilogo dei criteri IPSec
Title: Riepilogo dei criteri IPSec
ms:assetid: '892a8129-115b-4a81-82cd-b7aea8c56d9b'
ms:contentKeyID: 20200801
ms:mtpsurl: 'https://technet.microsoft.com/it-it/library/Dd536201(v=TechNet.10)'
---

Isolamento del server e del dominio tramite IPsec e criteri di gruppo
=====================================================================

### Appendice B: Riepilogo dei criteri IPSec

Aggiornato: 16 febbraio 2005

In questa appendice viene fornito un conciso elenco di informazioni relative a tutte le impostazioni dei criteri per i gruppi di isolamento utilizzati in questa soluzione.

##### In questa pagina

[](#eeaa)[Configurazione generale dei criteri](#eeaa)
[](#edaa)[Criteri del dominio di isolamento](#edaa)
[](#ecaa)[Criteri del gruppo di isolamento Nessun fallback](#ecaa)
[](#ebaa)[Criteri del gruppo di isolamento Limite](#ebaa)
[](#eaaa)[Criteri del gruppo di isolamento Crittografia](#eaaa)

### Configurazione generale dei criteri

Tutti i criteri definiti all'interno di questa soluzione contengono le seguenti informazioni.

**Impostazioni generali dei criteri:**

-   **Intervallo di aggiornamento**: 5 minuti per la distribuzione graduale nell'ambiente di test. Questo valore deve essere aumentato a 60 minuti nell'ambiente di produzione. Una volta trascorsi 60 minuti, l'host aggiorna il criterio dal servizio di directory Active Directory®. Questa funzionalità consente di modificare un criterio IPSec già assegnato distribuendolo all'intera rete dell'organizzazione in un'ora al massimo, al fine di rispondere rapidamente a eventuali violazioni della rete.

-   **Durata modalità principale IKE**: 3 ore.

-   **Sessioni per modalità principale**: 0, infinito.

-   **PFS master**: non utilizzato, questa funzione è sconsigliata per IKE (Internet Key Association) in Microsoft® Windows® in quanto non supporta altri prodotti e al fine di eliminare la duplicazione di funzionalità. Risultati analoghi si ottengono impostando le sessioni per modalità principale su 1.

-   **Metodi di protezione scambio chiave modalità principale IKE**: 3DES/SHA1/High (2048), 3DES/SHA1/Medium (2), 3DES/MD5/Medium (2).

**Nota:** l'impostazione High (2048) è supportata solo in Microsoft Windows Server™ 2003 e Windows XP SP2 e viene ignorata in Windows 2000 e versioni precedenti di Windows XP. In Windows 2000, Windows XP SP1 e versioni precedenti la compatibilità con IKE è assicurata utilizzando l'impostazione Medium (2).

**Regola di risposta predefinita** = disabilitata

**Regola 1**:

**Elenco filtri**: "IPSEC - Elenco esenzioni VIP cluster"

**Filtro**:     Indirizzo IP &lt;-&gt; Indirizzo IP specifico, Speculare - Correntemente vuoto

**Descrizione**: "Indirizzi IP per tutti i VIP cluster dell'organizzazione"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 2**:

**Elenco filtri**: "IPSEC - DHCP, Traffico di negoziazione"

**Filtro**:     Indirizzo IP &lt;-&gt; Qualsiasi, UDP, Da porta 68 SRC a porta 67 DST, Speculare

**Descrizione**: "Consente il traffico di negoziazione DHCP"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 3**:

**Elenco filtri**: "IPSEC - Elenco esenzioni DNS"

**Filtro**:    Qualsiasi &lt;-&gt; 192.168.1.21, Speculare

              Qualsiasi &lt;-&gt; 192.168.1.22, Speculare

**Descrizione**: "Indirizzi IP per tutti i server DNS dell'organizzazione"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 4**:

**Elenco filtri**: "IPSEC - Elenco esenzioni controller di dominio"

**Filtro**:    Qualsiasi &lt;-&gt; 192.168.1.21, Speculare

              Qualsiasi &lt;-&gt; 192.168.1.22, Speculare

**Descrizione**: "Indirizzi IP per tutti i controller di dominio dell'organizzazione"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 5**:

**Elenco filtri**: "IPSEC - Elenco esenzioni WINS"

**Filtro**:    Qualsiasi &lt;-&gt; 192.168.1.22, Speculare

**Descrizione**: "Indirizzi IP per tutti i server WINS dell'organizzazione"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 6**:

**Elenco filtri**: "IPSEC - Elenco esenzioni server applicazioni LOB"

**Filtro**:    Qualsiasi &lt;-&gt; 192.168.1.10, Speculare

**Descrizione**: "Indirizzi IP per tutti i server Line-Of-Business dell'organizzazione"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 7**:

**Elenco filtri**: "IPSEC - ICMP, Tutto il traffico"

**Filtro**:    Indirizzo IP &lt;-&gt; Qualsiasi, ICMP, Speculare

**Descrizione**: "Consente tutto il traffico ICMP"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 8**:

**Elenco filtri**: "IPSEC - Indirizzi esentati"

**Filtro**:     Qualsiasi &lt;-&gt; Indirizzo IP specifico, Speculare – Correntemente vuoto

**Descrizione**: "Indirizzi IP da esentare dalle comunicazioni IPSec"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 9**:

**Elenco filtri**: "IPSEC - Subnet esentate"

**Filtro**:     Indirizzo IP &lt;-&gt; Subnet IP specifica, Speculare - Correntemente vuoto

**Descrizione**: "Subnet da esentare dalle comunicazioni IPSec"

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

**Regola 10**:

**Elenco filtri**: "IPSEC - Versione criterio: (1.0.041001.1600)"

**Filtro**:     1.1.1.1 &lt;-&gt; 1.1.1.2, ICMP, Speculare

**Descrizione**: "Non è un vero elenco filtri.  Utilizzato per identificare la versione di un criterio IPSec."

**Operazione filtro**: IPSEC-Autorizza

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

#### Spiegazione del comportamento delle regole

**Regola 1**. Impostare questa regola per esentare il traffico in uscita verso i VIP cluster. Non utilizzare questa regola se non è necessario che il server comunichi con i VIP cluster.

**Regola 2**. Questa regola consente l'utilizzo della negoziazione DHCP (Dynamic Host Configuration Protocol) non IPSec.

**Regola 3**. Questa regola consente la comunicazione non IPSec verso i sistemi DNS (Domain Name System) nell'elenco esenzioni.

**Regola 4**. Questa regola consente la comunicazione non IPSec verso i sistemi dei controller di dominio nell'elenco esenzioni.

**Regola 5**. Questa regola consente la comunicazione non IPSec verso i sistemi WINS (Windows Internet Naming Service) nell'elenco esenzioni.

**Regola 6**. Questa regola consente la comunicazione non IPSec verso gli host nell'elenco esenzioni. Questo elenco filtri è stato utilizzato dalla Woodgrove Bank per i server delle applicazioni LOB (Line-Of-Business).

**Regola 7**. Questa regola consente di utilizzare il traffico ICMP (Internet Control Message Protocol) non IPSec.

**Regola 8**. Questa regola consente la comunicazione non IPSec verso gli host nell'elenco esenzioni. Non utilizzare questa regola se l'elenco filtri è vuoto.

**Regola 9**. Questa regola consente la comunicazione non IPSec verso le subnet nell'elenco esenzioni. Non utilizzare questa regola se l'elenco filtri è vuoto.

**Regola 10**. Questa regola contiene unicamente informazioni sulla versione del criterio. Il filtro utilizzato per implementare l'elenco filtri è un filtro fittizio, composto da due indirizzi IP specifici che consentono il traffico ICMP, richiesto in quanto non è possibile aggiungere a un criterio un elenco filtri vuoto.

[](#mainsection)[Inizio pagina](#mainsection)

### Criteri del dominio di isolamento

In questa sezione vengono fornite informazioni dettagliate sui filtri, le operazioni filtro, i criteri e gli oggetti Criteri di gruppo (GPO) utilizzati per creare il dominio di isolamento della soluzione della Woodgrove Bank.

**Regola 11**:

**Elenco filtri**: IPSEC – Subnet organizzative

**Filtro**: Qualsiasi &lt;-&gt; Subnet interne, Tutto il traffico, Speculare

**Operazione filtro**: "IPSEC - Modalità di richiesta protetta (Ignora in ingresso, Consenti in uscita)"

**Ordine di preferenza metodo di protezione**: ESP senza crittografia/SHA1, ESP senza crittografia/MD5,
  ESP-3DES/SHA1, quindi ESP-3DES/MD5

  NON accettare comunicazioni non protette

  Consenti comunicazioni non protette con host che non utilizzano IPSec

**Autenticazione**: Kerberos

**Tunnel**: No    

**Tipo di connessione**: ALL

Tutte le altre impostazioni dei criteri sono identiche a quelle descritte in precedenza nella sezione "Configurazione generale dei criteri" in questa appendice.

#### Spiegazione del comportamento delle regole

**Regola 11**. Questa regola è la più generica tra le regole definite nel criterio. Corrisponde al traffico verso le subnet protette e richiede la negoziazione di IPSec. Non vengono accettate le richieste di comunicazioni non protette dai client senza IPSec, tuttavia le comunicazioni con tali client sono consentite se vengono avviate tramite la regola.

[](#mainsection)[Inizio pagina](#mainsection)

### Criteri del gruppo di isolamento Nessun fallback

In questa sezione vengono fornite informazioni dettagliate sui filtri, le operazioni filtro, i criteri e gli oggetti Criteri di gruppo (GPO) utilizzati per creare il gruppo di isolamento Nessun fallback della soluzione della Woodgrove Bank.

**Regola 11**:

**Elenco filtri**: IPSEC – Subnet organizzative

**Filtro**: Qualsiasi &lt;-&gt; Subnet interne, Tutto il traffico, Speculare

**Operazione filtro**: "IPSEC – Modalità di richiesta completa (Ignora in ingresso, Impedisci in uscita)"

**Ordine di preferenza metodo di protezione**: ESP senza crittografia/SHA1, ESP senza crittografia/MD5,

  ESP-3DES/SHA1, quindi ESP-3DES/MD5

  NON accettare comunicazioni non protette

  NON consentire comunicazioni non protette con host che non utilizzano IPSec

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

Tutte le altre impostazioni dei criteri sono identiche a quelle descritte in precedenza nella sezione "Configurazione generale dei criteri" in questa appendice.

#### Spiegazione del comportamento delle regole

**Regola 11**. Questa regola è la più generica tra le regole definite nel criterio. Corrisponde al traffico verso le subnet protette e richiede la negoziazione di IPSec. Non consente le comunicazioni non protette con i client che non utilizzano IPSec.

[](#mainsection)[Inizio pagina](#mainsection)

### Criteri del gruppo di isolamento Limite

In questa sezione vengono fornite informazioni dettagliate sui filtri, le operazioni filtro, i criteri e gli oggetti Criteri di gruppo (GPO) utilizzati per creare il gruppo di isolamento Limite della soluzione della Woodgrove Bank.

Si presuppone che l'host limite non sia portatile. L'host può pertanto utilizzare le subnet per definire la sua rete e deve essere protetto quasi come un host Bastion della Guida per la protezione di Windows Server 2003. È necessario assicurare a tale host un'elevata protezione contro gli attacchi da parte di computer non attendibili. Di conseguenza, è opportuno unire il criterio IPSec a filtri che riducano al massimo la superficie di attacco, ove possibile.

**Impostazioni generali dei criteri**:

**Durata modalità principale IKE**: 20 minuti

**Regola 11**:

**Elenco filtri**: IPSEC – Subnet organizzative

**Filtro**: Qualsiasi &lt;-&gt; Subnet interne, Tutto il traffico, Speculare

**Operazione filtro**: "IPSEC – Modalità di richiesta (Accetta in ingresso, Consenti in uscita)"

**Ordine di preferenza metodo di protezione**: ESP senza crittografia/SHA1, ESP senza crittografia/MD5,

  ESP-3DES/SHA1, quindi ESP-3DES/MD5

  Accetta comunicazioni non protette

  Consenti comunicazioni non protette con host che non utilizzano IPSec

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

Tutte le altre impostazioni dei criteri sono identiche a quelle descritte in precedenza nella sezione "Configurazione generale dei criteri" in questa appendice.

#### Spiegazione del comportamento delle regole

**Regola 11**. Questa regola è la più generica tra le regole definite nel criterio. Corrisponde al traffico verso le subnet protette e richiede la negoziazione di IPSec. La regola consente l'accettazione del traffico proveniente dai client che non utilizzano IPSec e l'avvio delle comunicazioni verso tali client.

[](#mainsection)[Inizio pagina](#mainsection)

### Criteri del gruppo di isolamento Crittografia

In questa sezione vengono fornite informazioni dettagliate sui filtri, le operazioni filtro, i criteri e gli oggetti Criteri di gruppo (GPO) utilizzati per creare il gruppo di isolamento Crittografia della soluzione della Woodgrove Bank.

**Regola 11**:

**Elenco filtri**: IPSEC – Subnet organizzative

**Filtro**: Qualsiasi &lt;-&gt; Subnet interne, Tutto il traffico, Speculare

**Operazione filtro**: "Modalità di richiesta crittografia (Ignora in ingresso, Impedisci

in uscita)"

**Ordine di preferenza metodo di protezione**: ESP-3DES/SHA1, quindi ESP-3DES/MD5

  NON accettare comunicazioni non protette

  NON consentire comunicazioni non protette con host che non utilizzano IPSec

**Autenticazione**: Kerberos

**Tunnel**: No

**Tipo di connessione**: ALL

Tutte le altre impostazioni dei criteri sono identiche a quelle descritte in precedenza nella sezione "Configurazione generale dei criteri" in questa appendice.

#### Spiegazione del comportamento delle regole

**Regola 11**. Questa regola è la più generica tra le regole definite nel criterio. Corrisponde al traffico verso le subnet protette e richiede la negoziazione della crittografia IPSec. Non consente le comunicazioni non protette con i client che non utilizzano IPSec.

**Scarica la soluzione completa**

[Isolamento del server e del dominio tramite IPsec e criteri di gruppo](http://go.microsoft.com/fwlink/?linkid=33947)

[](#mainsection)[Inizio pagina](#mainsection)
