---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: /assets/images/background.png
# some information about your slides (markdown enabled)
title: Organizzazione Agile e Workflow di GitHub
class: text-center
author: Maurizio Tolomeo
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# duration of the presentation
duration: 30min
---

# Organizzazione Agile e Workflow di GitHub

Presentazione per team dev

<div class="abs-br m-6 text-xl">
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
GitHub non è solo un repository, ma uno strumento di gestione.
Obiettivo: Migliorare la collaborazione e la qualità del codice.
-->

---
layout: default
---

# Agenda

1. **Modulo 1**: Organizzazione Agile in GitHub
2. **Modulo 2**: Il Workflow di Git (Branching)
3. **Modulo 3**: Il Ciclo della Pull Request (PR) e Code Review
4. **Modulo 4**: Best Practices e Consigli
5. **Conclusione**: Il Mindset Finale

---
layout: section
---

# Modulo 1
Organizzazione Agile in GitHub

---

# GitHub come Strumento di Gestione

Non è solo un posto dove "mettere il codice".

<div class="grid grid-cols-3 gap-4 mt-10">
<div>
<h3 class="text-primary">1. Sprints</h3>
<p>Contenitore temporale (solitamente 2 settimane). Definisce il <b>"cosa"</b> verrà fatto.</p>
</div>

<div>
<h3 class="text-primary">2. Tasks</h3>
<p>Descrizione dettagliata e chiara. Se possibile, con <b>criteri di accettazione</b>.</p>
</div>

<div>
<h3 class="text-primary">3. Dashboard</h3>
<p>Vista <b>Kanban (Board)</b>: To Do → In Progress → Review → Done.</p>
</div>
</div>

<div class="mt-10 border-l-4 border-primary pl-4 italic">
"La Board è la fonte di verità: se la Board dice che sei in Progress, ma non hai ancora aperto il branch, c'è un problema di allineamento."
</div>

---

# Stati Operativi sulla Board

| Stato | Significato Operativo | Azione su GitHub |
|:---|:---|:---|
| **To Do** | Task prioritarie. Nessuno ci lavora. | Issue aperta, senza assegnatario. |
| **In Progress** | Qualcuno ha preso in carico il lavoro. | Assegnazione Issue. Creazione Branch. |
| **Review** | Codice pronto per il giudizio dei pari. | Apertura Pull Request (PR). |
| **Done** | Approvato, testato e unito a main. | PR chiusa (Merged) e Issue chiusa. |

<br>

<div class="flex items-center gap-2 text-xl font-bold text-orange-500">
  <carbon:warning-filled />
  Regola aurea: "Se non c'è una Task, il branch non può esistere".
</div>

---
layout: section
---

# Modulo 2
Il Workflow di Git (Branching)

---

# La Sacralità del Main

Proteggere l'integrità del prodotto finale.

*   **Branch `main` (o `master`):** Rappresenta la versione stabile (ciò che l'utente vede).
*   **Read-only:** Non si tocca mai direttamente.
*   **Stabilità:** Se si rompe `main`, si rompe il progetto/deploy.

<div class="mt-10 p-4 bg-gray-100 rounded dark:bg-gray-800">
<p class="font-bold mb-2 text-primary">Regola aurea:</p>
"Il branch main è sacro, un branch 'read-only', non si tocca direttamente."
</div>

<!--
Tutti i cambiamenti devono passare attraverso una PR.
-->

---

# Il Ciclo di Vita di un Branch

Ambiente isolato per ogni singola Task.

1.  **Creazione:** Ogni Task = Nuovo Branch.
2.  **Isolamento:** Lavora senza influenzare il codice principale.
3.  **Merge:** Pull Request per unire il lavoro una volta completo e testato.

<div class="grid grid-cols-2 gap-4 mt-8">
<div class="p-4 border border-gray-200 rounded">
<h3 class="text-sm font-bold uppercase text-gray-500 mb-2">Nomenclatura</h3>
<code>feature/issue-123-descrizione</code>
<p class="text-xs mt-2 italic">Aiuta la tracciabilità e la revisione.</p>
</div>

<div class="p-4 border border-gray-200 rounded">
<h3 class="text-sm font-bold uppercase text-gray-500 mb-2">Isolamento</h3>
Solo cambiamenti relativi alla Task.
<p class="text-xs mt-2 italic">Mantiene la coerenza e facilita il debug.</p>
</div>
</div>

---

# L'Arte del Commit

Il commit è un punto di ripristino narrativo, non un semplice salvataggio.

*   **Commit Atomici:** Ogni commit = un cambiamento logico completo.
    *   `feat: aggiunta funzionalità X`
    *   `fix: risolto bug Y`
*   **Messaggi Chiari:** Spiegare *cosa* è cambiato e *perché*. Evitare "aggiornamento" o "correzione".
*   **Frequenza:** Commit frequenti = storia chiara e debug facile.
*   **Push Responsabile:** Chiediti: *"Questo codice è pronto per essere condiviso? È testato? È chiaro?"*

---

# Manutenzione e Conflitti

Evitare il "Merge Hell" facendo vivere il branch vicino al `main`.

*   **Allineamento Regolare:** `git pull origin main` frequentemente.
*   **Risoluzione Consapevole:** Capire la logica del codice, non solo "accettare tutto".
*   **Pulizia:** Eliminare il branch (locale e remoto) dopo il merge.

<div class="mt-8 p-4 bg-blue-50 dark:bg-blue-900/20 border-l-4 border-blue-500 rounded-r">
  <h3 class="font-bold text-blue-700 dark:text-blue-300">GitHub Flow Recap:</h3>
  <ul class="text-sm mt-2">
    <li><b>Main:</b> Sempre stabile.</li>
    <li><b>Feature Branch:</b> Uno per ogni Task.</li>
    <li><b>Commit:</b> Piccoli, frequenti, messaggi chiari.</li>
    <li><b>Push:</b> Solo quando pronto e testato.</li>
  </ul>
</div>

---
layout: section
---

# Modulo 3
Il Ciclo della Pull Request (PR) e Code Review

---

# La PR come Conversazione

Non è solo un merge, è il cancello della qualità.

<v-clicks>

*   **Anatomia di una PR Efficace:**
    *   **Titolo Chiaro:** `feat: aggiunta funzionalità X`
    *   **La regola del perché:** Il codice dice *cosa*, la descrizione dice *perché*.
    *   **Context Checklist:** Screenshot, link al task, test eseguiti.

*   **La PR deve "vendere" la soluzione al team.**

</v-clicks>

---

# Check-list per il Revisore

Cosa guardare durante la Code Review?

<div class="grid grid-cols-2 gap-x-8 gap-y-4 text-sm mt-4">
<div>
  <h4 class="font-bold text-primary flex items-center gap-2"><carbon:checkmark-outline /> Logica e Obiettivo</h4>
  Il codice fa quello che chiede la Task? (Evita lo "scope creep").
</div>
<div>
  <h4 class="font-bold text-primary flex items-center gap-2"><carbon:view /> Leggibilità</h4>
  Un collega capirà il codice tra 6 mesi senza chiamarti?
</div>
<div>
  <h4 class="font-bold text-red-500 flex items-center gap-2"><carbon:locked /> Sicurezza</h4>
  <b>MAI</b> committare password, token o API keys. Usa <code>.env</code>.
</div>
<div>
  <h4 class="font-bold text-primary flex items-center gap-2"><carbon:flash /> Performance</h4>
  Il codice è efficiente? Ci sono operazioni ridondanti?
</div>
<div>
  <h4 class="font-bold text-primary flex items-center gap-2"><carbon:test-tool /> Test</h4>
  Ci sono test? Sono passati? Mai approvare PR con test falliti.
</div>
<div>
  <h4 class="font-bold text-primary flex items-center gap-2"><carbon:color-palette /> Stile</h4>
  Segue le convenzioni del progetto?
</div>
</div>

---

# La Cultura del Feedback

Il punto dove i team si uniscono o si dividono.

<div class="grid grid-cols-2 gap-8 mt-10">
<div class="bg-red-50 dark:bg-red-900/20 p-4 rounded border-t-4 border-red-500">
<h3 class="font-bold text-red-700 dark:text-red-300">Il Revisore</h3>
Linguaggio costruttivo.<br><br>
<span class="text-xs italic">"Penso che questa funzione sia troppo complessa, potremmo scomporla?"</span>
</div>

<div class="bg-green-50 dark:bg-green-900/20 p-4 rounded border-t-4 border-green-500">
<h3 class="font-bold text-green-700 dark:text-green-300">L'Autore</h3>
Separare se stessi dal codice.<br><br>
<span class="text-xs italic">"Un commento è un regalo: qualcuno spende tempo per insegnarti."</span>
</div>
</div>

---

# Il Ciclo Iterativo della PR

1.  **Apertura:** Il dev apre la PR collegandola alla Task.
2.  **Revisione:** I colleghi lasciano commenti e feedback.
3.  **Feedback:** Il dev risponde e applica i correttivi.
4.  **Approvazione:** Tutti i revisori sono soddisfatti.
5.  **Merge:** Merge su main ed eliminazione del branch.

---
layout: section
---

# Modulo 4
Best Practices e Consigli

---

# Documentazione e Automazione

Scrivere codice che il team può gestire.

<div class="grid grid-cols-2 gap-8">
<div>
<h3 class="text-primary flex items-center gap-2"><carbon:document /> Documentazione</h3>
<ul>
<li><b>README:</b> Aggiorna variabili d'ambiente o config subito.</li>
<li><b>Commenti:</b> Spiega il <b>perché</b> di scelte non ovvie, non il "cosa".</li>
</ul>
</div>

<div>
<h3 class="text-primary flex items-center gap-2"><carbon:bot /> Automazione</h3>
<ul>
<li><b>GitHub Actions:</b> Controlla il semaforo (Rosso = Responsabilità tua).</li>
<li><b>SonarQube:</b> Non ignorare i Code Smells. Guida gratuita per migliorare.</li>
</ul>
</div>
</div>

<div class="mt-8 text-sm italic border-t pt-4">
"Revisione di Copilot: Non accettare passivamente l'AI, valuta se è sicuro e allineato."
</div>

---

# Comunicazione e Allineamento

*   **Daily Standups:** Non sono interrogazioni.
    *   *"Sono bloccato qui, chi mi aiuta?"*
    *   *"Ho completato questo, cosa faccio dopo?"*
*   **Chiedere aiuto precocemente:** Non passare più di un'ora bloccato senza consultare il team.

<div class="mt-20 text-center text-2xl font-serif italic text-primary">
"Il codice è di proprietà del team, non del singolo."
</div>

---
layout: center
class: text-center
---

# Conclusione

<p class="text-3xl font-serif mb-10">
"Lavorare bene su GitHub significa rispettare il tempo dei propri colleghi presenti e futuri."
</p>

<div class="flex justify-center gap-4">
<div class="px-6 py-2 bg-primary text-white rounded-full">Grazie!</div>
</div>
