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
