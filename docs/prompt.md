# Prompt per Claude Code — App "Trillo" (nome provvisorio)

## Il progetto in una frase
Costruisci un'app mobile **di svago** per ragazzi e ragazze **dai 13 ai 20 anni**, ispirata allo spirito di **MSN Messenger** dei primi anni 2000: **trilli** che fanno vibrare la chat per far sapere a qualcuno che lo stai pensando, ed **emoticon collezionabili**, che puoi avere solo se qualcuno te le manda.

**Trillo non è un'alternativa a WhatsApp.** Non deve sostituire la messaggistica di tutti i giorni: è un posto dove giocare con gli amici, collezionare, scambiarsi attenzioni. La chat esiste, ma è leggera e serve da palcoscenico per trilli ed emoticon. Quando devi scegliere tra "più utile" e "più divertente", scegli divertente.

Prima di scrivere codice entra in plan mode, leggi tutto questo documento, crea un `CLAUDE.md` con le regole del progetto e proponimi un piano a fasi. Chiedimi conferma prima delle scelte difficili da cambiare dopo: stack, schema del database, regole dell'economia delle emoticon, regole di sicurezza per i minori.

---

## Il trillo come segnale di interesse
Il trillo è il gesto principale dell'app: costa un tocco e dice "ci sei?", "ti penso", "mi stai simpatico/a". Deve essere **leggero, giocoso e mai invadente**.

- Un trillo fa **tremare lo schermo della chat** del destinatario, con vibrazione e suono dedicato. Ad app chiusa arriva una push con suono personalizzato (su iOS la vibrazione delle push non si può personalizzare: va bene così).
- Si manda **solo agli amici** (amicizia reciproca, richiesta + accettazione).
- **Trillo combo**: se due amici si mandano un trillo a vicenda entro 3 secondi, parte un'animazione speciale doppia.
- **Cotta segreta**: ogni utente può segnare in segreto fino a 3 amici come "cotta". Nessuno lo vede. Se la cotta è **reciproca**, a entrambi arriva un "trillo del destino" con animazione speciale e un'emoticon esclusiva. Se non è reciproca, non succede niente e nessuno lo saprà mai. Niente messaggi anonimi: l'unica cosa che si rivela è una corrispondenza reciproca. Solo tra utenti della stessa fascia d'età (vedi sicurezza).
- **Anti-spam e rispetto**: cooldown per conversazione, limite giornaliero (configurabili), possibilità di silenziare i trilli di una persona. Chi silenzia non viene notificato.
- **Ore di silenzio**: per i minori, di default dalle 23 alle 7 i trilli arrivano senza suono né vibrazione e si vedono al risveglio.
- Il contatore di trilli ricevuti/inviati è **visibile solo a se stessi**: niente classifiche di popolarità.

---

## Emoticon collezionabili (il cuore dell'app)

**Regola base**: un'emoticon la puoi usare solo se ce l'hai. E l'unico modo per averla è **riceverla da qualcun altro**.

- **Pacchetto iniziale**: alla registrazione ognuno riceve un set casuale (8 comuni + 1 non comune), diverso per ognuno, così le emoticon iniziano subito a circolare.
- **Prendila!**: quando ricevi in chat un'emoticon che non hai, la vedi comunque e sotto compare il pulsante **"Prendila!"** con un'animazione da figurina. Toccandolo entra nella tua collezione.
- **Rarità**: Comune, Non comune, Rara, Epica, Leggendaria.
- **Provenienza**: ogni emoticon ricorda chi te l'ha passata e quando ("Ricevuta da Marco, 12 ottobre"). Statistiche globali: quante persone ce l'hanno, quante volte è passata di mano.
- **Paziente zero**: badge per i primi possessori di un'emoticon.
- **Scorciatoie da tastiera** stile MSN: `:)`, `;)`, `(Y)`, `(H)` diventano emoticon **solo se la possiedi**, altrimenti restano testo.
- **Album**: schermata stile album di figurine, con le sagome grigie delle emoticon mancanti, divise per rarità e serie.

### Economia (regole di partenza, tutte configurabili in una tabella `economy_config`)
Mandare un'emoticon in chat non la consuma mai. Quello che è limitato è **passarla a qualcuno di nuovo**: il "passaggio" si conta solo quando il destinatario tocca "Prendila!".

| Rarità | Passaggi a settimana | Altri limiti |
|---|---|---|
| Comune | illimitati | — |
| Non comune | 10 | — |
| Rara | 3 | — |
| Epica | 1 | account con almeno 7 giorni di vita |
| Leggendaria | 1 al mese | numero massimo di possessori (`max_holders`) obbligatorio |

Se finisci i passaggi, il destinatario vede l'emoticon ma il pulsante dice "Riprova la settimana prossima". Proponimi tu eventuali correzioni dopo aver simulato la diffusione con il seed (vedi qualità).

### Anti-trucco
- L'assegnazione avviene **solo lato server** (funzione Postgres o Edge Function), mai dal client.
- Controlli: mittente diverso dal destinatario, amicizia valida, mittente che possiede davvero l'emoticon, account verificato, limiti dell'economia, limiti di frequenza contro le farm di account finti.
- Le immagini delle emoticon che l'utente non possiede si servono con **URL firmati a scadenza**, così non si può scaricare tutto il catalogo dallo Storage.
- Le ricette delle fusioni restano solo sul server: il client manda due emoticon e riceve il risultato, non vede mai la tabella.

---

## Vincolo importante sugli asset
L'app deve **evocare** MSN, non copiarlo. Non usare emoticon, suoni, loghi, nomi o grafiche di Microsoft/MSN. Tutte le emoticon, i suoni (incluso quello del trillo e del "contatto online") e le skin devono essere **originali**, nello stile nostalgico anni 2000 riletto per la Gen Z: faccine tonde, colori saturi, animazioni piccole e ironiche, effetti "glossy". Per l'MVP crea placeholder originali (SVG o Lottie semplici) e una struttura che mi permetta di sostituirli con gli asset di un illustratore.

Prima del lancio va verificata la disponibilità del nome "Trillo" come marchio (in italiano era anche il nome del "nudge" di MSN).

---

## Stack consigliato
- **App**: React Native + Expo + TypeScript, Expo Router. **Development build fin dalla Fase 0** (le push su Android non funzionano in Expo Go).
- **Backend**: Supabase (Postgres, Auth, Realtime, Storage, Edge Functions), progetto in regione UE.
- **Animazioni**: Lottie (`lottie-react-native`) o Rive per emoticon e trilli; Reanimated per lo scuotimento della chat.
- **Vibrazione e suoni**: `expo-haptics`, `expo-audio` (non `expo-av`, che è deprecato).
- **Notifiche push**: Expo Notifications, con suono personalizzato del trillo.
- **Stato client**: Zustand + TanStack Query.
- **Analytics**: eventi anonimi salvati nel nostro database (o uno strumento self-hosted in UE). **Nessun SDK pubblicitario o di tracciamento di terze parti.**
- **Test**: Jest per la logica, pgTAP per le funzioni del database (assegnazione emoticon, economia, amicizie, trilli, cotte).

Se hai una proposta migliore, spiegamela prima di procedere.

---

## Funzionalità

### 1. Registrazione e amici
- Registrazione con **numero di telefono (OTP)** oppure **email (magic link)**, con **data di nascita** obbligatoria.
- Username unico e "nickname" libero e decorato, stile anni 2000 (es. `~*Simo*~`).
- Aggiunta amici tramite: **QR code** (il modo principale, di persona), **link di invito**, username esatto, rubrica.
- **Rubrica**: solo con consenso esplicito, i numeri si caricano come **HMAC con chiave segreta lato server** (un hash semplice si inverte in pochi minuti, perché i numeri di telefono sono pochi).
- **Link di invito**: quando un amico invitato si registra, entrambi ricevono un'emoticon rara esclusiva della serie "Inviti". È il motore principale di crescita.
- I profili **non sono ricercabili** da sconosciuti: niente suggerimenti di "persone che potresti conoscere" tra sconosciuti, niente elenco pubblico.
- Blocco e segnalazione utenti.

### 2. Chat leggera
- Chat 1:1 in tempo reale, con trilli ed emoticon in primo piano.
- "Sta scrivendo...", invio di foto (con moderazione), cronologia.
- **Stati alla MSN**: Online, Occupato, Torno subito, Al telefono, A pranzo, Invisibile.
- **Messaggio personale** sotto il nome, visibile agli amici.
- **Avviso "è online"**: opzione per ricevere un avviso quando un amico specifico si collega.
- Eliminazione dei propri messaggi.
- Niente vocali, niente conferme di lettura nell'MVP: non stiamo rifacendo WhatsApp.
- Messaggi non cifrati end-to-end nell'MVP: la scelta va scritta in modo chiaro nell'informativa privacy.

### 3. Profilo
- Foto, nickname, messaggio personale, **vetrina** con 3 emoticon scelte dalla collezione.
- Cornice della foto profilo che cambia in base alla rarità più alta posseduta.
- Profilo visibile **solo agli amici**.

---

## Sicurezza e benessere (target 13-20 anni)
Questa sezione ha la precedenza su qualsiasi funzionalità. Se una funzione la mette in discussione, fermati e chiedimi.

- **Età minima**: in Italia sotto i 14 anni serve il **consenso dei genitori** per il trattamento dei dati. Proposta: **MVP aperto dai 14 anni**; i 13enni in una fase successiva, con flusso di consenso del genitore (email del genitore + conferma). Chiedimi conferma.
- **Fasce d'età**: 14-17 e 18-20 (più 13 quando aperto). Tra minorenni e maggiorenni:
  - l'amicizia è possibile **solo tramite QR code di persona o contatto reciproco in rubrica**, mai tramite username o link;
  - la cotta segreta funziona **solo dentro la stessa fascia**;
  - regole configurabili, da rivedere con me.
- **Privacy di default al massimo** per i minori: profilo solo amici, stato "online" visibile solo agli amici, nessuna posizione, mai.
- **Moderazione**: controllo automatico delle foto per nudità e violenza prima della consegna (servizio esterno o modello, da propormi), segnalazioni con priorità per i contenuti che coinvolgono minori, filtro opzionale per le parole offensive, strumenti di revisione per noi.
- **No dark pattern**: niente streak che si perdono, niente classifiche pubbliche di popolarità, niente feed infinito, niente notifiche "ti stai perdendo qualcosa". Le ore di silenzio notturne sono attive di default per i minori.
- **Soldi**: nessun acquisto nell'MVP. In futuro solo oggetti estetici (skin, temi), **mai pacchetti di emoticon a sorpresa a pagamento** (assomigliano alle loot box) e nessuna pubblicità profilata ai minori (DSA, art. 28).
- **GDPR**: informativa scritta in modo comprensibile per un 14enne, consenso, **esportazione e cancellazione dell'account dall'app** (Apple la richiede), conservazione minima dei dati.
- **App store**: policy sui contenuti generati dagli utenti, segnalazione e blocco ben visibili, classificazione dell'età corretta.

---

## Funzionalità extra (valuta e dimmi quali inserire e in quale fase)
1. **Fusioni**: unendo due emoticon possedute se ne ottiene una nuova (faccina + cuore = faccina innamorata). Ricette segrete; chi ne scopre una per primo riceve un badge.
2. **Animazioni a schermo intero** ("occhiolini" alla MSN), anch'esse collezionabili.
3. **Storie 24h** solo per gli amici, con le proprie emoticon come sticker (chi le vede può prenderle).
4. **Chat di gruppo** (per la classe o la compagnia), con trillo di gruppo.
5. **Scambi**: proposta di scambio di emoticon tra due amici, accettata da entrambi.
6. **Eventi stagionali**: a Halloween, Natale, fine scuola un account ufficiale manda un'emoticon speciale a pochi utenti a caso; da lì si diffonde.
7. **Mappa della diffusione**: un grafo che mostra come un'emoticon è passata tra i tuoi amici.
8. **Badge e obiettivi**: Collezionista (50 emoticon), Untore (hai passato un'emoticon a 20 persone), Alchimista (5 fusioni scoperte), Trillatore seriale.
9. **"Sto ascoltando"**: la canzone che stai ascoltando su Spotify sotto il nome.
10. **Giochi in chat**: tris, forza 4, battaglia navale.
11. **Messaggi scritti a mano**: disegni a mano libera.
12. **Skin retrò** per la chat e scelta di sfondo e font, sbloccabili.

---

## Modello dati di partenza (da rivedere con me)
- `profiles` (id, username, nickname, avatar, birth_date, age_band, status, personal_message, phone_hmac, email, quiet_hours)
- `parental_consents` (user_id, parent_email, confirmed_at) — per quando apriremo ai 13enni
- `friendships` (user_a, user_b, status: pending/accepted/blocked, method: qr/invite/username/contacts, created_at)
- `invites` (code, inviter_id, used_by, used_at)
- `conversations`, `conversation_members`, `messages` (tipo: testo, immagine, emoticon, trillo, sistema; deleted_at)
- `emoticons` (id, code, name, shortcut, rarity, series, asset_path, is_fusion, max_holders)
- `user_emoticons` (user_id, emoticon_id, acquired_at, source_user_id, source_message_id, is_patient_zero)
- `emoticon_passes` (giver_id, receiver_id, emoticon_id, passed_at) — per i limiti dell'economia
- `economy_config` (rarity, weekly_passes, monthly_passes, min_account_age_days, ...)
- `fusion_recipes` (input_a, input_b, output, discovered_by, discovered_at)
- `nudges` (sender, receiver, conversation_id, sent_at) per cooldown e statistiche
- `crushes` (user_id, target_id, created_at) — mai leggibile dal client, solo il match
- `reports`, `blocks`, `mutes`
- `events`, `badges`, `user_badges`, `analytics_events`
- Row Level Security attiva su tutte le tabelle.

---

## Piano di sviluppo a fasi
1. **Fase 0** — Setup progetto, `CLAUDE.md`, struttura cartelle, Supabase locale, development build, CI di base.
2. **Fase 1** — Registrazione con data di nascita e fasce d'età, profili, amicizie (QR, invito, username, rubrica con HMAC), blocco e segnalazione, stati e messaggio personale.
3. **Fase 2** — Chat 1:1 leggera e trilli: animazione, vibrazione, suono, push, cooldown, combo, silenzia, ore di silenzio.
4. **Fase 3** — Emoticon collezionabili: catalogo, pacchetto iniziale, "Prendila!", economia, scorciatoie, album, provenienza, premio per gli inviti, analytics, anti-trucco con test.
   **→ Qui c'è l'MVP**: lo facciamo provare a un gruppo ristretto (20-30 persone, con i consensi necessari) e misuriamo se le emoticon circolano davvero.
5. **Fase 4** — Cotta segreta, fusioni, badge, eventi stagionali, moderazione automatica delle foto.
6. **Fase 5** — Vetrina avanzata, storie, chat di gruppo.
7. **Fase 6** — Extra scelti dalla lista sopra; apertura ai 13enni con consenso dei genitori.

Alla fine di ogni fase: fermati, riassumimi cosa hai fatto, come provarlo sul telefono (development build) e cosa resta aperto.

---

## Criteri di qualità
- Codice TypeScript tipizzato, componenti piccoli e riutilizzabili.
- Tutta la logica che assegna emoticon, applica l'economia, controlla amicizie, fasce d'età, cotte e limiti dei trilli sta sul server ed è coperta da test.
- Animazioni fluide (60 fps) anche su telefoni di fascia media.
- Interfaccia in italiano, tono giovane e ironico, predisposta per altre lingue (i18n).
- Seed del database con utenti ed emoticon di prova, più uno **script di simulazione** che fa girare la diffusione delle emoticon per qualche settimana virtuale, per verificare che le rare restino rare.
- Metriche da tracciare fin dall'MVP: emoticon prese per utente a settimana, inviti accettati, trilli al giorno, utenti attivi dopo 7 e 30 giorni.
