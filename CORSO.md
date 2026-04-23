# Organizzazione Agile e Workflow di GitHub

## Modulo 1: Organizzazione Agile in GitHub

L'obiettivo è far comprendere che GitHub non è solo un repository, ma uno strumento di gestione.

Concetti chiave:

1. Sprints: contenitore temporale (solitamente 2 settimane). Spiega che lo Sprint definisce il "cosa" verrà fatto.
2. Task: una descrizione dettagliata chiara e, se possibile, con i criteri di accettazione.
3. Dashboard (mappa di lavoro): Utilizzare la vista "Board" (Kanban) per spostare le card (task) da To Do a In Progress a Review a Done. La Board è la fonte di verità: se la Board dice che sei in "Progress", ma non hai ancora aperto il branch, c'è un problema di allineamento.

|Stato|Significato Operativo|Azione su GitHub|
|-----|------------------|----------------|
|To Do|Task prioritarie per lo sprint. Nessuno ci sta lavorando.|Issue aperta, senza assegnatario.|
|In Progress|Qualcuno ha preso in carico il lavoro.|Assegnazione Issue a se stessi. Creazione Branch.|
|Review|Il codice è pronto per essere giudicato dai pari.|Apertura della Pull Request (PR) collegata all'issue.|
|Done|Il codice è approvato, testato e unito al ramo principale.|PR chiusa (Merged) e Issue chiusa automaticamente.|

> Regola aurea: "Se non c'è una Task, il branch non può esistere". Ogni branch deve essere collegato a una Task.

## Modulo 2: Il Workflow di Git (Branching)

### La Sacralità del Main

L'obiettivo è proteggere l'integrità del prodotto finale (Main) garantendo al contempo totale libertà di sperimentazione nei rami laterali.

È fondamentale che ogni dev del team capisca che il branch main (o master) è sacro è rappresenta la versione stabile del prodotto (ciò che l'utente finale vede). Non deve mai essere toccato direttamente. Il branch serve per deployare il codice in produzione, quindi deve essere sempre stabile e funzionante. Se si commette un errore su main, si rischia di compromettere l'intero progetto.

> Regola aurea: "Il branch main è sacro un branch "read-only", non si tocca direttamente". Tutti i cambiamenti devono passare attraverso un processo di revisione (PR) per garantire la qualità e la stabilità del codice.

### Il ciclo di vita di un branch

Ogni volta che si inizia una Task, si deve creare un nuovo branch. Il branch è un ambiente isolato dove si può lavorare senza influenzare il codice principale. Il branch esiste solo per isolare il cambiamento finché non è pronto. Una volta che il lavoro è completo e testato, si apre una Pull Request (PR) per unire il branch a main.

> Nomenclatura: "Il branch deve essere nominato in modo chiaro e collegato alla Task (esempio: feature/issue-123-descrizione)". Questo aiuta a mantenere la tracciabilità e facilita la revisione del codice.
> Isolamento: "Il branch deve contenere solo i cambiamenti relativi alla Task". Questo mantiene la coerenza e facilita la revisione del codice.

### L'arte del commit

Il commit non è un semplice salvataggio, è un punto di ripristino narrativo.

- Commit atomici: Ogni commit dovrebbe rappresentare un cambiamento logico completo (esempio: "feat: aggiunta funzionalità X" o "fix: risolto bug Y").
- Messaggi chiari: Il messaggio del commit deve spiegare cosa è cambiato e perché. Evitare messaggi vaghi come "aggiornamento" o "correzione".
- Frequenza: Fare commit frequenti aiuta a mantenere la storia del progetto chiara e facilita il debug in caso di problemi.
- Push Responsabile: Il push rende il codice visibile agli altri. Fare il push solo quando il lavoro è pronto e testato per evitare di condividere codice incompleto o instabile. Prima di farlo mi devo chiedere "Questo codice è pronto per essere condiviso con il team? È testato? È chiaro?" Se la risposta è no, è meglio fare un commit locale e continuare a lavorare prima di fare il push.

### Gestione dei conflitti e manutenzione del branch

Per evitare l'inferno dei conflitti (Merge Hell), il branch deve "vivere" vicino al main.

- Allineamento regolare: Eseguire regolarmente un pull da main (git pull origin main) per mantenere il branch aggiornato e ridurre la probabilità di conflitti futuri.
- Risoluzione dei conflitti: Se si verificano conflitti, è importante risolverli con attenzione, comprendendo la logica del codice. Non basta accettare tutto da una parte o dall'altra, bisogna capire cosa è cambiato e perché, e trovare una soluzione che mantenga la funzionalità e la stabilità del codice.
- Pulizia: Dopo il merge, è buona pratica eliminare il branch per mantenere il repository pulito e organizzato. Un branch che non viene eliminato può creare confusione e rendere più difficile la navigazione del repository. Va eliminato sia localmente che su GitHub per non trasformare il repository in un "cimitero di rami morti".

Strategia consigliata (GitHub Flow):

- Main: Sempre stabile e deployabile.
- Feature Branch: Creare un nuovo branch per ogni Task.
- Commit: Piccoli, frequenti e con messaggi chiari (convenzione del formato esempio: feat: descrizione o fix: descrizione).
- Push: Pubblicare il branch sul repository remoto (fare il push solo quando il lavoro è pronto e testato).

Punti chiave:

- Mai fare commit direttamente su main.
- Il branch esiste solo per isolare il cambiamento finché non è pronto.
- Il branch deve essere collegato alla Task corrispondente per mantenere la tracciabilità.
- Il branch deve essere aggiornato regolarmente con main per evitare conflitti futuri (git pull origin main).
- Il branch deve essere eliminato dopo il merge per mantenere il repository pulito.
- Il branch deve essere nominato in modo chiaro (esempio: feature/issue-123-descrizione).
- Il branch deve essere testato localmente prima di fare il push (eseguire i test e verificare che tutto funzioni).
- Il branch deve contenere solo i cambiamenti relativi alla Task per mantenere la coerenza e facilitare la revisione del codice.

## Modulo 3: Il Ciclo della Pull Request (PR) e Code Review

La Pull Request non è solo un merge del codice, ma una conversazione attorno al codice. È il cancello che separa il lavoro individuale dal prodotto ufficiale.
Qui avviene la vera collaborazione. La PR è il punto di controllo qualità.

### L'Anatomia di una PR Efficace

Aprire una PR non significa solo cliccare un tasto. Una buona PR deve "vendere" la soluzione al team.

- Titolo: Deve essere chiaro e descrittivo (esempio: "feat: aggiunta funzionalità X").
- La regola del perché: La PR deve spiegare non solo cosa è cambiato, ma anche perché. Il codice dice cosa è stato fatto, la descrizione della PR deve dire perché.
- Context Checklist: La PR deve includere informazioni sul contesto, uno screenshot, link al task,  i test eseguiti correttamente. Questo aiuta i revisori a comprendere rapidamente il cambiamento e a concentrarsi sui punti chiave durante la revisione.

### Check-list per il Revisore (Cosa guardare?)

Tutti i devs che fanno parte del team devono revisionare il codice degli altri. Ecco su cosa focalizzarsi:

- Logica e Obiettivo: Il codice fa davvero quello che chiede la Task? (Evitare lo "scope creep", ovvero fare più di quanto richiesto).
- Leggibilità: Se un collega legge il codice tra 6 mesi, capirà cosa succede senza chiamarti al telefono?
- Sicurezza (Punto Critico): Mai, in nessun caso, committare password, token o chiavi API. Usa file .env e aggiungili al .gitignore.
- Performance: Il codice è efficiente? Non ci sono operazioni inutili o ridondanti?
- Stile: Il codice segue le convenzioni del progetto? (esempio: indentazione, nomi delle variabili, ecc.).
- Test: Ci sono test che coprono il nuovo codice? I test sono passati? (Evitare di approvare PR senza test o con test falliti).

### La Cultura del Feedback (Soft Skills)

Questo è il punto dove i team si uniscono o si dividono.

- Per chi fa il Revisore: Usa un linguaggio costruttivo.
  - Sbagliato: "Questo codice è orribile".
  - Corretto: "Penso che questa funzione sia troppo complessa, potremmo scomporla per renderla più leggibile?".
- Per il dev che ha scritto il codice: Separare il proprio valore come persona dalla qualità del codice scritto. Un commento sulla PR è un regalo: qualcuno sta spendendo tempo per insegnarti qualcosa.

### Il ciclo iterativo della PR

1. Apertura della PR: Il dev apre la PR collegandola alla Task.
2. Revisione: I colleghi revisionano il codice, lasciano commenti e chiedono chiarimenti se necessario.
3. Feedback: Il dev risponde ai commenti, fa i correttivi e aggiorna la PR.
4. Approvazione: Una volta che tutti i revisori sono soddisfatti, la PR viene approvata.
5. Merge: Il dev esegue il merge della PR su main e elimina il branch.

## Modulo 4: Best Practices e Consigli

L'obiettivo è elevare lo standard qualitativo: passare dal "scrivere codice che il computer capisce" al "scrivere codice che il team può gestire".

### La Documentazione: Il Codice non parla da solo

Un task è realmente "Done" solo se anche la documentazione è aggiornata.

- README: Se la nuova feature richiede una nuova variabile d'ambiente o una configurazione specifica, va scritta subito nel README. Non lasciare vuoto il README con informazioni mancanti, altrimenti il prossimo dev che arriva si sentirà perso e potrebbe commettere errori.
- Commenti nel Codice: Evitare di commentare cosa fa il codice (dovrebbe essere chiaro dal nome delle funzioni), ma commentare il perché di scelte non ovvie. 

### Sinergia con l'Automazione (CI/CD)

- GitHub Actions: Ogni volta che aprono una PR, partono dei processi automatici (test, build). Controllare il "semaforo" della PR: se è rosso (fallito), la responsabilità di correggere è loro prima ancora che il revisore guardi il codice.

- SonarQube (Il Revisore Silenzioso):
  - non ignorare i "Code Smells" o le segnalazioni di complessità ciclica.
  - Punto Chiave: SonarQube vede cose che un occhio umano può mancare (es. vulnerabilità di sicurezza latenti o duplicazioni di codice). Trattare i suoi suggerimenti come una guida gratuita per diventare sviluppatori migliori.

- Revisione di Copilot: Se il team utilizza strumenti di AI come Copilot, è importante revisionare attentamente il codice generato. Non accettare passivamente il codice suggerito, ma valutare se è appropriato, sicuro e allineato con le convenzioni del progetto.

### Comunicazione e Allineamento

- Allineamenti Giornalieri (Daily): Non sono interrogazioni, ma momenti per dire: "Sono bloccato qui, chi mi aiuta?", "Come si fa questo?", "Ho completato questo task, cosa faccio dopo?".
- Chiedere aiuto precocemente: Un dev non dovrebbe mai passare più di un'ora bloccato su un singolo problema senza consultare la documentazione o chiedere un parere veloce a un altro dev.

## Conclusione del Corso: Il Mindset Finale

Chiudi il corso con un messaggio motivazionale forte:

> "Il codice è di proprietà del team, non del singolo. Lavorare bene su GitHub significa rispettare il tempo dei propri colleghi presenti e futuri."
