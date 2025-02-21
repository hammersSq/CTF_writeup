Active Directory è una tecnologia Microsoft che sta alla base della maggior parte delle aziende nel mondo. 

> **Active Directory**: è un sistema centralizzato utilizzato per organizzare e gestire risorse di rete, come **Utenti**, **Macchine** **Gruppi**, e altre risorse di sistema in una rete aziendale. 

# Active Directory Basic
## Windows Domains
Il concetto di **Domain** nasce dall'esigenza di semplificare l'amministrazione dei vari componenti che vanno a costruire una rete di Computer Windows:
mentre in aziende molto piccole può sembrare fattibile configurare macchine  e creare utenze singolarmente, questo è decisamente impensabile in aziende con centinaia se non migliaia di di utenze e macchine.

> **Windows Domain**: è un gruppo di Computer e Utenze amministrati da una determinata azienda

Il concetto dietro un Windows Domain è quello di centralizzare l' amministrazione dei componenti della rete aziendale in un unica cartella chiamata **Active Directory**. 
Il server che garantisce l'accesso all' Active Directory è chiamato **Domain Controller**.

Benefici di avere un Windows Domain:
- **Gestione centralizzata delle utenze**: tutti gli utenti nella rete aziendale possono essere configurati e gestiti dall'Active Directory con il minimo sforzo.
- **Gestione delle policy di sicurezza**: Le policy di sicurezza vengono configurate direttamente dall'Active Directory e applicate a tutti i computer e utenti nella rete.
### Esempio uso dei Domain e Active Directory
Un esempio che probabilmente ti suonerà familiare è la gestione delle utenze all'interno della rete aziendale: Appena entrato in azienda ti vengono dati uno username e una password che puoi utilizzare per accedere a qualsiasi computer presente all'interno dell' Azienda. 
Questo è possibile grazie all'Active Directory: Le tue credenziali non devono essere presenti in ogni macchina e sono disponibili su tutta le rete. 

Questo è quello che succede quando un utente prova ad accedere con le proprie credenziali a una macchina nella rete aziendale:
1. La macchina invia una richiesta di autenticazione al Domain Controller.
2. Il Domain Controller verifica le credenziali dell'utente confrontandole con le informazioni salvate nell'Active Directory. Se le credenziali sono corrette, l'utente viene autenticato.
3. Una volta autenticato, viene generato un **Token** di accesso che contiene i diritti e i privilegi dell'utente (e.g. i gruppi di cui fa parte e i permessi associati)

## Active Directory Domain Service (AD DS)
**Active Directory Domain Service** è il servizio che contiene e fornisce le informazioni su tutti gli *oggetti* che esistono all'interno della rete. 
Tra i tipi di oggetti più comuni abbiamo:
- Utenti (Users)
- Macchine (Machines)
- Stampanti (Printers)
- Shares (Cartelle condivise)
### Users
Gli utenti sono il tipo di oggetto più comune dentro l'Active Directory. Gli utenti fanno parte di un insieme di oggetti chiamato **Security Principals**, ovvero *oggetti che possono essere autenticati da un Domain Controller e i quali possono possedere privilegi su altre risorse all' interno del dominio (come stampanti o file).*

> Un **Security Principal** è un oggetto che opera su altre risorse nella rete

Gli utenti possono rappresentare due tipi di entità:
- **Persone**: Questo è il caso più comune, ad ogni persona nella rete (e.g. ad ogni dipendente) viene associato un utente.
- **Servizi**: Un utente viene creato per uno specifico servizio, come ad esempio per gestire un database SQL. Le utenze di servizio vengono create con l'insieme minimo di privilegi per lanciare quel servizio.
### Machines
Ad ogni computer nella rete aziendale viene associato un oggetto Macchina nell'Active Directory. Le macchine sono considerate dei **Security Principals** e per ogni macchina viene creato un account, come accade per gli utenti.

L'account macchina è un admin locale nel computer a cui viene assegnato e generalmente nessuno dovrebbe accedervi se non il computer stesso. 
Per prevenire l'accesso a questo tipo di account le loro password sono cambiate automaticamente e sono formate da 120 caratteri casuali.

I nomi degli account macchina seguono una specifica naming convention: se il nome macchina è **DC01** l'account associato sarà **DC01$**.

### Security Groups

Un gruppo è un oggetto utilizzato principalmente per assegnare privilegi a un insieme di Users contemporaneamente invece di farlo singolarmente per ogni utente. 

Un esempio potrebbe essere quello di voler dare a un utente il permesso ad accedere a tutte le stampanti dentro il Dominio: invece di dover impostare per quell'utente i permessi ad accedere a tutte le stampanti, utilizzando i gruppi sarà necessario solo aggiungerlo al gruppo con quei privilegi.

Un gruppo può avere sia macchine e utenti come membri. Se necessario un gruppo può contenere altri gruppi.

Gruppi creati di default:
- **Domain Admins**: Gli utenti che appartengono a questo gruppo hanno privilegi di amministratore su tutto il dominio. Loro possono amministrare ogni computer nel dominio, inclusi i Domain Controllers.
- **Server Operators**: Gli utenti in questo dominio possono amministrare i Domain Controllers. Gli utenti in questo gruppo non possono aggiungere o rimuovere utenti dai gruppi amministratore.
- **Backup Operators**: Gli utenti in questo gruppo possono accedere ad ogni file, ignorando i loro permessi. Questo tipo di utenza è addetta a creare backup nei computers.
- **Account Operators**: Gli utenti in questo gruppo possono creare e modificare altri account nel dominio.
- **Domain Users**: Questo gruppo contiene tutti gli User nel dominio.
- **Domain Computers**: Questo gruppo contiene tutti i computer nel dominio.
- **Domain Controllers**: Questo gruppo contiene tutti i Domain Controllers nel dominio.

### Organizational Units
Le Organizational Units  sono strutture che consentono di organizzare e gestire oggetti come Utenti, Gruppi, Computer e altre risorse all' interno del dominio. 
Queste sono fondamentali per garantire la gestione efficiente e sicura della rete aziendale.
Le OUs permettono di definire insieme di utenti con requisiti di policy simili. 