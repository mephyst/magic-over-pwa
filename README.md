# Magic Over PWA - Betting Progress Manager

## 📱 Installazione su Smartphone

### Metodo 1: Server Locale (Consigliato)

Per usare la PWA in locale sul tuo smartphone, hai bisogno di un semplice server web. Ecco le opzioni:

#### Opzione A: Python (se hai Python installato sul PC)

1. Metti tutti i file in una cartella (es. `magic-over`)
2. Apri il terminale/prompt nella cartella
3. Esegui:
   ```bash
   python -m http.server 8080
   ```
4. Sul telefono, collegati alla stessa rete WiFi del PC
5. Apri il browser e vai a: `http://[IP-DEL-TUO-PC]:8080`
   - Per trovare l'IP: su Windows `ipconfig`, su Mac/Linux `ifconfig`

#### Opzione B: Servizio cloud gratuito (Più semplice)

1. Crea un account su [Netlify](https://www.netlify.com/) o [Vercel](https://vercel.com/)
2. Trascina la cartella con i file sul sito
3. Ottieni un URL pubblico accessibile da qualsiasi dispositivo

#### Opzione C: File locale (Limitazioni)

Puoi aprire `index.html` direttamente nel browser, ma:
- Il Service Worker non funzionerà (no offline mode)
- L'app non sarà installabile
- I dati saranno comunque salvati in IndexedDB

### Metodo 2: Installazione come App

Una volta aperto nel browser:

**Android (Chrome):**
1. Apri la pagina nel browser Chrome
2. Tocca i tre puntini in alto a destra
3. Seleziona "Installa app" o "Aggiungi a schermata Home"

**iPhone (Safari):**
1. Apri la pagina in Safari
2. Tocca l'icona di condivisione (quadrato con freccia)
3. Scorri e seleziona "Aggiungi a Home"

---

## 🎯 Funzionalità

### Dashboard
- Visualizza il bankroll totale
- Monitora lo stato di tutti gli 8 slot (A-H)
- Identifica slot in attenzione (giallo) o critici (rosso)

### Gestione Slot
- 8 slot indipendenti (A-H)
- Ogni slot ha la propria cassa e progressione
- Registrazione scommesse con esiti: WIN, LOSE, 1/2 WIN, NULLA
- Calcolo automatico di stake, vincita e guadagno

### Statistiche
- ROI globale e per slot
- Win rate e precisione
- Totale puntato e guadagni

### Impostazioni
- Configurazione individuale di ogni slot
- Cassa iniziale personalizzabile
- Stake base (% della cassa)
- Modalità recupero (Alto, Basso, Nessuno)
- Stop Win / Stop Lose opzionali

### Backup & Restore
- Esporta tutti i dati in formato JSON
- Importa dati da backup precedenti
- Perfetto per trasferire dati tra dispositivi

---

## 💾 Persistenza Dati

I dati sono salvati su **Firebase Realtime Database**, un database cloud che offre:
- **Sincronizzazione automatica** tra dispositivi
- **Backup automatico** su cloud
- **Accesso da qualsiasi dispositivo** con lo stesso codice
- **Funzionamento offline** con sincronizzazione automatica alla riconnessione
- Persistenza permanente dei dati

### Sistema di Autenticazione

L'app utilizza un sistema di **codici di accesso** per proteggere i tuoi dati:
- Al primo avvio, inserisci un codice di accesso valido
- Il dispositivo viene registrato e associato al tuo account
- I dati sono salvati in un percorso privato: `users/{deviceId}/`
- Lo stesso codice può essere usato su più dispositivi per accedere agli stessi dati

**IMPORTANTE:**
- Ricorda il tuo codice di accesso per accedere da altri dispositivi
- I dati sono sincronizzati automaticamente tra tutti i tuoi dispositivi
- La funzione di backup è disponibile per esportazioni aggiuntive

---

## 📁 File Inclusi

```
magic-over-pwa/
├── index.html      # App principale
├── manifest.json   # Configurazione PWA
├── sw.js           # Service Worker (offline)
├── icon-192.png    # Icona piccola
├── icon-512.png    # Icona grande
└── README.md       # Questo file
```

---

## 🔧 Requisiti

- Browser moderno (Chrome, Safari, Firefox, Edge)
- **Connessione internet** per la sincronizzazione Firebase
- Codice di accesso valido (fornito dall'amministratore)
- Funziona offline dopo il primo caricamento (i dati si sincronizzano alla riconnessione)

---

## 🔑 Gestione Codici di Accesso (Solo Amministratori)

Per creare nuovi codici di accesso, è necessario accedere alla console Firebase:

1. Vai su [Firebase Console](https://console.firebase.google.com/)
2. Seleziona il progetto **magic-over-auth**
3. Vai su **Realtime Database**
4. Aggiungi un nuovo codice nel percorso `codes/`:
   ```
   codes/
     └── TUO-CODICE/
           ├── active: true
           └── description: "Descrizione utente"
   ```

I codici devono essere in **MAIUSCOLO** e possono essere alfanumerici.

---

## ⚠️ Note

- **I tuoi dati sono al sicuro su Firebase Cloud** e sincronizzati automaticamente
- Conserva il tuo **codice di accesso**: è necessario per accedere da nuovi dispositivi
- Puoi usare la stessa app su più dispositivi contemporaneamente
- La funzione di backup/export rimane disponibile per esportazioni locali aggiuntive
- Se perdi il codice di accesso, non potrai più accedere ai tuoi dati
