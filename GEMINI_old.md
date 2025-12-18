# Progetto: Uccello di Fuoco (Uccello Volante)

## Panoramica
"Uccello di Fuoco" è un gioco 2D a scorrimento verticale sviluppato con tecnologie web standard (HTML, CSS, JavaScript Vanilla) e confezionato per Android tramite Capacitor. 
L'obiettivo è guidare un uccello attraverso 4 livelli distinti, ognuno con meccaniche uniche (raccogliere monete, salvare pulcini, nutrirli, insegnare loro a volare).


## Stato Corrente
- **Specifiche Complete:** Vedi `promt.md`. Il gioco completo prevede 4 livelli progressivi e gestione dello stato.
- **Prototipo:** `www/test.html` contiene un prototipo funzionante del Livello 1 (evitare ostacoli, raccogliere monete).
- **Entry Point:** `www/index.html` è attualmente vuoto e deve essere implementato integrando la logica di gioco completa.

## Struttura e Architettura
- **Frontend:** Single Page Application (SPA) contenuta principalmente in `index.html`.
  - **Librerie:** Nessuna libreria esterna per la logica di gioco (Vanilla JS).
  - **Stile:** CSS interno o inline per semplicità, come richiesto nel prompt originale.
- **Mobile Wrapper:** Capacitor (`@capacitor/android`, `@capacitor/core`).
- **Assets:** Tutti i file statici (immagini, audio) si trovano nella cartella `www/`.

## Workflow di Sviluppo
1.  **Modifica Codice:** Lavorare principalmente dentro la cartella `www/`.
2.  **Test Locale:** Usare un server statico (es. `serve .` o l'estensione Live Server).
3.  **Build Android:**
    - Sincronizzare le modifiche web con il progetto Android: `npx cap sync`
    - Aprire Android Studio: `npm run go_android` (alias per `npx cap sync android && npx cap open android`).

## Comandi Utili
- **Git:**
  - Commit e Push rapido: `git fatto "messaggio"` (richiede alias configurato) o `npm run git_commit_push`.
- **NPM Scripts:**
  - `npm run go_android`: Sincronizza e apre il progetto Android.

## Obiettivi Futuri (da `promt.md`)
1.  **Unificazione:** Portare la logica da `test.html` a `index.html`.
2.  **Livelli Mancanti:** Implementare Livello 2 (Nidi/Pulcini), Livello 3 (Nutrimento) e Livello 4 (Lezioni di volo stile Flappy Bird).
3.  **Stato:** Implementare la persistenza tra i livelli e le schermate di Win/Game Over/Menu.
