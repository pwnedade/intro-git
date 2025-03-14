# Seminario Git
Introduzine a Git e a GitHub.

Le informazioni riguardanti la configurazione di Git e la creazione di chiavi SSH per GitHub sono state recuperate dalle relative documentazioni ufficiali.

## Cos'è Git?
Git è uno strumento di controllo versione distribuito, progettato per facilitare la gestione e il tracciamento delle modifiche nel codice sorgente di un progetto. Permette a più sviluppatori di collaborare contemporaneamente sugli stessi file, mantenendo una cronologia dettagliata delle modifiche apportate.

## Cos'è una repository (o repo)?
Una repository è uno spazio in cui vengono conservati, organizzati e gestiti i file di un progetto. Può essere vista come una cartella virtuale che racchiude tutto il codice sorgente, i documenti e gli asset legati al progetto, permettendo di tenerli sotto controllo e di monitorare le modifiche nel tempo.

## Git VS GitHub
Git e GitHub sono due concetti correlati ma distinti, spesso confusi tra loro.

Git è un sistema di controllo versione distribuito, utilizzato per gestire e tracciare le modifiche al codice sorgente di un progetto. È uno strumento da linea di comando che permette agli sviluppatori di lavorare in modo collaborativo, tenendo traccia delle modifiche nel tempo.

GitHub è una piattaforma basata su web che ospita repository Git. Offre uno spazio online per archiviare, condividere e collaborare su progetti Git.

## Installazione e configurazione di Git

> Prima di proseguire con le seguenti istruzioni è fortemente consigliato aver già creato un account [GitHub](https://github.com/)

1. Scarica git dal [sito ufficiale](https://git-scm.com/)

2. Seguiamo la configurazione secondo la guida ufficiale di [Git](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

    ```bash
    git config --global user.name "Nome Cognome"
    git config --global user.email "your_email@exaple.com"
    ```
    *consiglio: inserisci la stessa mail utilizzata per creare l'account GitHub*

> Per verificare di aver inserito correttamente le istruzione puoi usare i seguenti comandi:
> ```bash
> git config --global user.email
> ```
> Per vedere la mail
> ```bash
> git config --global user.name
> ```
> Per vedere il nome utente

## Comandi base di Git

| Comando      | Funzione |
| ------------ | -------- |
| `git clone`  | Scarica una repository remota e crea una copia locale sul tuo computer. |
| `git add`    | Aggiunge file al "gioco" di Git, segnalandogli quali file dovrebbero essere tracciati e inclusi nel prossimo commit. |
| `git commit` | Salva i cambiamenti locali, registrandoli in una nuova versione nel repository. |
| `git push`   | Invia i commit dalla tua repository locale a una repository remota (es. GitHub). |
| `git pull`   | Recupera gli aggiornamenti da una repository remota e li integra nella tua repository locale. |


## Chiavi SSH (Windows) 2025
Secondo la documentazione ufficiale di [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

### Generazione delle chiavi
1. Aprire Git Bash
2. Eseguire questo comando, utilizzando la mail utilizzata per creare l'account GitHub: 

    ```bash
    ssh-keygen -t ed25519 -C "your_email@example.com"
    ```

> Questo comando crea 2 file nel percorso `c:/Users/YOU/.ssh`: `id_ed25519` e `id_ed25519.pub`. Questi due file contengono rispettivamente la chiave privata e la chiave pubblica. La chiave privata dovrà essere aggiunta al ssh-agent. La chiave pubblica dovrà essere aggiunta al proprio profilo GitHub.

### Chiave privata e chiave pubblica

#### Cosa sono? 
Le chiavi SSH di GitHub sono un metodo di autenticazione sicura che consentono di connettersi a GitHub senza dover inserire username e password ogni volta. Si basano su un sistema di crittografia a chiave pubblica e privata.

La chiave pubblica deve essere caricata nell'account GitHub. Non consente a nessuno di accedere direttamente al proprio account senza la chiave privata corrispondente.

La chiave privata deve rimanere sul proprio computer e deve essere strettamente protetta. Viene utilizzata per dimostrare la propria identità.

#### Come utilizzarle?
In un nuova shell di PowerShell con i privilegi di Amministratore esegui questi comandi:

```powershell
Get-Service -Name ssh-agent | Set-Service -StartupType Manual
Start-Service ssh-agent
```

In un'altra shell di PowerShell senza i privilegi di Amministratore esegui questo comando:

```powershell
ssh-add c:/Users/YOU/.ssh/id_ed25519
```

> Ricorda che la chiave pubblica è contenuta nel file `id_ed25519.pub`. *La chiave privata non deve essere condivisa con NESSUNO.*

- I primi due comandi servono per assicurarsi che il servizio ssh-agent sia in esecuzione.
- Il secondo comando serve per aggiungere la chiave privata SSH all'ssh-agent.

Dopo aver eseguito correttamente queste istruzioni potrai aggiungere la chiave pubblica al tuo profilo GitHub.