# Prompt per la Creazione del Gioco "Uccello di Fuoco"

## Obiettivo Generale
Crea un gioco 2D single-page chiamato "Uccello di Fuoco" utilizzando HTML, CSS e JavaScript vanilla. Il gioco deve essere contenuto in un unico file `index.html`. L'obiettivo è guidare un uccello attraverso 4 livelli, ognuno con un obiettivo diverso, evitando ostacoli e raccogliendo oggetti.

---

## 1. Struttura del File
- **`index.html`**: Il file principale.
- **`<head>`**:
    - Include i Google Fonts: 'Cinzel', 'Lora', 'Fredoka One'.
    - Contiene un unico blocco `<style>` con tutto il CSS del gioco.
- **`<body>`**:
    - Contiene un `div` principale `.game-wrapper` che funge da contenitore.
    - All'interno, ci sono i `div` per le varie schermate (gioco, start, game over, caricamento) e per gli elementi di gioco (giocatore, ostacoli, ecc.).
    - Un singolo blocco `<script>` alla fine del `<body>` conterrà tutta la logica del gioco.

---

## 2. Meccaniche di Gioco Principali
- **Controllo del Giocatore**:
    - Il giocatore (un uccello) viene controllato trascinando il mouse o il dito sullo schermo (`mousedown`/`touchstart` e `mousemove`/`touchmove`).
    - Il giocatore deve seguire la posizione del puntatore all'interno dell'area di gioco.
- **Game Loop**:
    - Utilizza `requestAnimationFrame` per un'animazione fluida e un aggiornamento costante dello stato del gioco.
    - Il loop deve calcolare il `deltaTime` (il tempo trascorso dall'ultimo frame) per garantire che la velocità sia costante su hardware diversi.
- **Scrolling Verticale**:
    - Il mondo di gioco si muove verticalmente verso il basso. Ostacoli e collezionabili appaiono dall'alto e si muovono verso il basso.
    - La velocità di scorrimento (`dy`) aumenta gradualmente con il punteggio (`score`) e il livello (`currentLevel`).
- **Collisioni**:
    - Implementa una funzione `checkCol(element1, element2)` che utilizza `getBoundingClientRect()` per rilevare le collisioni tra il giocatore e gli altri oggetti (ostacoli, monete, ecc.). Aggiungi un po' di "padding" per rendere la collisione più permissiva.
- **Stato di Gioco**:
    - Utilizza variabili globali per gestire lo stato, come `isRunning`, `isMuted`, `score`, `currentLevel`, `playerX`, `playerY`, ecc.
    - Usa array per gestire insiemi di oggetti dinamici: `obstacles`, `coins`, `flyingNests`.
- **Audio**:
    - Crea un oggetto `audioContext` per contenere tutte le istanze `new Audio()`.
    - Suoni richiesti: musica di sottofondo (`bg`), esplosione/morte (`crash`), raccolta moneta (`coin`), distruzione ostacolo (`smash`), vittoria/successo (`win`).
    - Implementa una funzione per il muto che ferma e riprende la musica e i suoni.

---

## 3. Descrizione dei Livelli e degli Obiettivi

### Schermata di Avvio e Caricamento
- **Start Screen**: Una schermata (`#startScreen`) visibile all'inizio con il titolo del gioco, le istruzioni base e un pulsante "INIZIO GIOCO".
- **Loading Screen**: Cliccando su "INIZIO GIOCO", mostra una schermata di caricamento con una barra di avanzamento e un uccellino che si muove lungo di essa. Dopo il caricamento, inizia il gioco.

### Livello 1: Corsa ai Punti
- **Obiettivo**: Raggiungere 3000 punti.
- **Gameplay**:
    - **Ostacoli**: Fai apparire ostacoli (`.obstacle`) a intervalli regolari dall'alto. La collisione con un ostacolo causa il "Game Over".
    - **Monete**: Fai apparire gruppi di monete (`.coin`). Ogni moneta raccolta aumenta il punteggio di 50 punti.
    - **Power-ups**:
        - **Super Mode**: Si attiva a intervalli di punteggio (es. ogni 200 punti). Rende il giocatore invincibile per 10 secondi e gli permette di distruggere gli ostacoli al contatto, guadagnando punti. Cambia l'aspetto del giocatore (es. con un `filter` CSS).
        - **Ultra Mode**: Una versione più potente che si attiva a intervalli di punteggio più alti (es. ogni 1000 punti).
- **UI**: Mostra il punteggio attuale e il Livello 1.

### Livello 2: Salvare i Pulcini
- **Obiettivo**: Salvare 3 pulcini (`MAX_BABIES`) portandoli ai nidi sicuri.
- **Gameplay**:
    - **Pulcini Seguaci**: All'inizio del livello, 3 pulcini (`.chick-follower`) seguono il giocatore principale.
    - **Nidi Volanti**: Fai apparire nidi (`.flying-nest`) dall'alto.
        - **Nidi Sicuri**: Se il giocatore tocca un nido sicuro, un pulcino viene "consegnato" (un'animazione mostra un uccellino che vola verso il nido). Il contatore dei pulcini da salvare diminuisce.
        - **Nidi con Predatori**: Alcuni nidi contengono predatori (serpenti `🐍`, lucertole `🦎`). Toccare questi nidi causa "Game Over".
- **UI**: Mostra il Livello 2 e un contatore dei pulcini salvati (es. `🐣 1/3`). Il punteggio non è l'obiettivo principale.

### Livello 3: Nutrimento
- **Obiettivo**: Nutrire 3 pulcini (`MAX_FED`).
- **Gameplay**:
    - **Nidi Affamati**: Fai apparire nidi affamati (`.hungry-nest`) che mostrano un pulcino che chiede cibo.
    - **Vermi**: Al posto delle monete, ora appaiono vermi (`.worm`). Il giocatore li raccoglie.
    - **Consegna Cibo**: Se il giocatore ha raccolto almeno un verme e tocca un nido affamato, consegna il cibo. Il contatore dei pulcini nutriti aumenta. Se tocca un nido senza vermi, non succede nulla (o appare un messaggio di avviso).
- **UI**: Mostra il Livello 3, un contatore dei vermi posseduti (`🪱 2`) e un contatore dei pulcini nutriti (`🐣 1/3`).

### Livello 4: Lezioni di Volo
- **Obiettivo**: Insegnare a tutti e 3 i pulcini a volare.
- **Meccanica Ispirata a Flappy Bird**:
    - I 3 pulcini appaiono nella parte alta dello schermo.
    - **Gravità**: I pulcini cadono verso il basso a causa della gravità (`GRAVITY`).
    - **Salto**: Se il giocatore principale vola sotto un pulcino e lo tocca, il pulcino riceve una spinta verso l'alto (`JUMP_FORCE`), simulando un "colpetto".
    - **Confidenza di Volo**: Ogni volta che un pulcino viene colpito, la sua "confidenza" aumenta. Quando la confidenza di un pulcino raggiunge il 100%, smette di cadere e vola via fuori dallo schermo.
    - **Perdita**: Se anche un solo pulcino cade fuori dallo schermo in basso, è "Game Over".
- **UI**: Mostra il Livello 4 e una barra di "Confidenza" totale che si riempie man mano che i pulcini imparano a volare.

---

## 4. Fine del Gioco e Progressione
- **Game Over**:
    - Ferma il `gameLoop`.
    - Mostra una schermata di "Game Over" con il riepilogo del livello (punteggio, pulcini salvati, ecc.).
    - Offri un pulsante per riprovare il livello corrente e uno per tornare all'inizio del gioco.
- **Progressione tra Livelli**:
    - Quando un livello è completato, mostra una breve animazione di transizione o un messaggio di "Livello Completato!".
    - **Salvataggio**: Usa `sessionStorage` per salvare il livello raggiunto (`currentLevel`) e i progressi rilevanti (es. `babiesDelivered`).
    - Alla morte, il gioco deve dare l'opzione di ripartire dal livello salvato in `sessionStorage`. Al riavvio completo, `sessionStorage` deve essere pulito.
- **Vittoria Finale**: Dopo aver completato il Livello 4, mostra una schermata di vittoria finale ("Famiglia Riunita").

---

## 5. Asset
- **Immagini**:
    - `bird-sprite-removebg-preview.png`: Lo sprite sheet per l'uccello (madre e pulcini).
    - `fire-36.gif`: L'animazione per gli ostacoli di fuoco.
- **Audio**:
    - `Epoq-Lepidoptera.ogg`: Musica di sottofondo.
    - `explosion.mp3`: Suono di collisione/morte.
    - `week7-brrring.mp3`: Suono per raccolta monete/vittoria.
    - `missile.mp3`: Suono per la distruzione di un ostacolo in modalità power-up.



si sono persi le ultime modifiche del file /www/index.html
le modifiche lo visto usando il comando resume
Index │ Msgs │ Age  │ Name
❯ #1    │ 88   │ 3m   │ Fix game bugs and improve bomb visibility.
mi puoi dare la lista di promt eseguite: Fix game bugs and improve bomb visibility.
come faccio a ripristinare le modifiche





1. Rimozione Modalità Infinita: Eliminato il pulsante e il relativo file per la modalità "endless", rendendo il gioco basato solo sui livelli.
2. Accesso Rapido ai Livelli: Aggiunti i pulsanti nella schermata iniziale per saltare direttamente ai livelli 1, 2, 3 e 4 senza dover giocare i precedenti.
3. Correzione Fine Gioco: Modificata la logica di chiusura del gioco per assicurarsi che il giocatore torni correttamente alla schermata iniziale (introdotto il reload della pagina tramite il link "RITORNA").
4. Nuove Meccaniche Livello 4 (Insegnare a volare): Implementate tre varianti diverse per sostituire la vecchia meccanica:
  * Variante 1 - Segui il Leader: Il giocatore traccia un percorso e il pulcino lo imita.
  * Variante 2 - Volo a Ritmo: Un mini-gioco musicale dove bisogna colpire le note che cadono.
  * Variante 3 - Raccogli e Guida: Raccogliere piume magiche per sollevare i pulcini e guidarli sui posatoi (quella attualmente attiva).
5. Fix Bug "RIPROVA LIVELLO": Corretto l'errore per cui premendo "Riprova" al Livello 4 si veniva riportati erroneamente al Livello 1.
6. Restyling Bombe: Modificato il CSS per rendere le bombe rotonde, nere e con l'emoji 💣, migliorandone drasticamente la visibilità rispetto alla vecchia versione fumosa.
7. Reset Stato Gioco: Ottimizzata la funzione fullReset per pulire la sessione e garantire un riavvio pulito ad ogni nuova partita.