# Prompt per Claude Code — App "Zing"

## Il progetto in una frase
Costruisci un'app mobile **di svago** per ragazzi e ragazze **dai 14 ai 20 anni**: un'app **nuova, del 2026**, con le **vibes del 2005-2006**. È un ibrido tra tre mondi:
- **MSN Messenger**: lista contatti con stati, messaggio personale, "sto ascoltando", gli **zing** (i "trilli") che fanno vibrare la chat, emoticon glossy e animate;
- **Instagram**: profilo con vetrina, storie 24h solo per gli amici;
- **WhatsApp**: chat in tempo reale con gli amici, semplice e immediata.

Il centro di tutto sono gli **zing come segnale di interesse** e le **emoticon collezionabili**, che puoi avere solo se qualcuno te le manda. Non deve sostituire WhatsApp per le cose serie: è il posto dove si gioca, si colleziona e ci si fa notare. Quando devi scegliere tra "più utile" e "più divertente", scegli divertente.

L'app è **internazionale**: interfaccia in **inglese di default** e in **italiano**, predisposta per altre lingue. Le parole chiave (Zing!, Grab it!, Combo, Studio) restano uguali in tutte le lingue, come marchio.

Esiste già un prototipo cliccabile in `prototype/index.html`: usalo come riferimento per il tono, lo stile grafico e le interazioni.

Prima di scrivere codice entra in plan mode, leggi tutto questo documento, crea un `CLAUDE.md` con le regole del progetto e proponimi un piano a fasi. Chiedimi conferma prima delle scelte difficili da cambiare dopo: stack, schema del database, regole dell'economia delle emoticon, regole di sicurezza per i minori.

---

## Lo zing come segnale di interesse
Lo zing (il "trillo" di MSN) è il gesto principale dell'app: costa un tocco e dice "ci sei?", "ti penso", "mi stai simpatico/a". Deve essere **leggero, giocoso e mai invadente**.

- Uno zing fa **tremare lo schermo della chat** del destinatario, con vibrazione e suono dedicato. Ad app chiusa arriva una push con suono personalizzato (su iOS la vibrazione delle push non si può personalizzare: va bene così).
- Si manda con il **pulsante a sinistra** del campo di testo (lontano da "invia", così non si sbaglia) oppure con un **doppio tocco sull'avatar** dell'amico, come il "pat" di WeChat. In futuro: frase personalizzabile ("ti ha mandato uno zing *e poi è scappato*").
- Si manda **solo agli amici** (amicizia reciproca, richiesta + accettazione).
- **Same energy**: se due amici si mandano uno zing a vicenda entro 3 secondi, compare "same energy", con i due avatar che pulsano insieme. Animazione sobria: niente scritte urlate né grafica da cartone animato, perché il pubblico (Gen Z e Gen Alpha) è ironico e attento all'estetica, e scappa da tutto ciò che sembra infantile.
- **Cotta segreta**: ogni utente può segnare in segreto fino a 3 amici come "cotta". Nessuno lo vede. Se la cotta è **reciproca**, a entrambi compare **"it's mutual"**, con un'animazione sobria e un'emoticon esclusiva. Se non è reciproca, non succede niente e nessuno lo saprà mai. Niente messaggi anonimi: l'unica cosa che si rivela è una corrispondenza reciproca. Solo tra utenti della stessa fascia d'età (vedi sicurezza).
- **Anti-spam e rispetto**: cooldown per conversazione, limite giornaliero (configurabili), possibilità di silenziare gli zing di una persona. Chi silenzia non viene notificato.
- **Ore di silenzio**: per i minori, di default dalle 23 alle 7 gli zing arrivano senza suono né vibrazione e si vedono al risveglio.
- Il contatore di zing ricevuti/inviati è **visibile solo a se stessi**: niente classifiche di popolarità.

---

## Emoticon collezionabili (il cuore dell'app)

**Regola base**: un'emoticon la puoi usare solo se ce l'hai. E l'unico modo per averla è **riceverla da qualcun altro**.

- **Pacchetto iniziale**: alla registrazione ognuno riceve un set casuale (8 comuni + 1 non comune + una serie di pezzi base), diverso per ognuno, così le emoticon iniziano subito a circolare.
- **Grab it!**: quando ricevi in chat un'emoticon che non hai, la vedi comunque e sotto compare il pulsante **"Grab it!"** con un'animazione da figurina. Toccandolo entra nella tua collezione. Se il messaggio contiene più pezzi che non hai, il pulsante diventa "Grab them! (n)".
- **Animate**: come su MSN, le emoticon si muovono. Ognuna ha un movimento (salta, dondola, pulsa, fluttua, trema) più dettagli come gli occhi che sbattono, le ruote che girano, la fiamma che sfarfalla. Animazioni piccole e leggere, ferme se l'utente ha attivato "riduci movimento".
- **Componibili**: su MSN si mettevano in fila più emoticon per fare disegni più grandi. In Zing esistono i **pezzi** (Parts), collezionabili come le emoticon e disegnati per **incastrarsi** in fila: locomotiva + vagoni + ultimo vagone fanno un treno, punta + corpo + motore fanno un razzo, testa + corpo + coda fanno un bruco che ondeggia. Nella chat si compone un **mix** toccando facce e pezzi, e lo si invia come un unico messaggio. Nuove serie di pezzi possono uscire come eventi. Niente armi né contenuti violenti tra i pezzi ufficiali.
- **Rarità**: Comune, Non comune, Rara, Epica, Leggendaria.
- **Provenienza**: ogni emoticon ricorda chi te l'ha passata e quando ("Ricevuta da Marco, 12 ottobre"). Statistiche globali: quante persone ce l'hanno, quante volte è passata di mano.
- **Paziente zero**: badge per i primi possessori di un'emoticon.
- **Scorciatoie**: funzionano in chat, nei post e nei commenti, e diventano emoticon **solo se la possiedi** (altrimenti restano testo):
  - codici classici stile MSN: `:)`, `;)`, `:D`, `(H)`, `<3`... e **`QQ`** per i lacrimoni dagli occhi dolci (nello slang internazionale QQ sono due occhi che piangono, in Cina "Q" vuol dire anche tenero);
  - codici con nome per tutte le emoticon e i pezzi, internazionali come su Discord e Slack: `:lol:`, `:cool:`, `:loco:`. Scrivendo `:` compaiono i **suggerimenti** con le emoticon che possiedi;
  - **set**: un solo codice per l'insieme intero, se hai tutti i pezzi (`(train)`, `(rocket)`, `(bug)`);
  - chi crea un'emoticon nello Studio sceglie la sua scorciatoia (es. `:simo:`), unica in tutto il catalogo;
  - una schermata "Tutte le scorciatoie" elenca i codici delle emoticon che hai.
- **Collezione**: sobria, non da album di figurine. Non è nella barra principale: sta dentro il Profilo (anteprima più "vedi tutte"). Mostra le emoticon che hai, divise per rarità con un pallino colorato discreto; quelle mancanti si vedono solo se lo chiedi, sbiadite e senza nome. Niente barre di avanzamento e niente "???".

### Economia (regole di partenza, tutte configurabili in una tabella `economy_config`)
Mandare un'emoticon in chat non la consuma mai. Quello che è limitato è **passarla a qualcuno di nuovo**: il "passaggio" si conta solo quando il destinatario tocca "Grab it!".

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

### Emoticon create dalla community (Studio)
Su MSN le emoticon di base le disegnavano i designer di Microsoft, ma c'erano anche le **emoticon personalizzate**: ognuno poteva caricare la sua immagine, e chi la riceveva in chat poteva aggiungerla alla propria lista. Zing riprende quell'idea, in modo sicuro:
- **Studio**: l'utente crea un'emoticon **componendo pezzi** (colore, occhi, bocca, accessorio, movimento). Niente immagini caricate nell'MVP: così la moderazione resta semplice e non entrano contenuti protetti da copyright o inadatti ai minori.
- Ogni creazione va in **revisione** (la "Redazione": all'inizio noi, poi strumenti di moderazione). Se approvata entra nel catalogo come "Community", e chi l'ha creata è **Paziente Zero**.
- Da lì circola come tutte le altre: solo chi la riceve può averla.
- Più avanti: **artisti e illustratori** invitati a creare serie ufficiali, e caricamento di disegni originali con moderazione.

### Brand (dopo, se l'app prende piede)
Non nell'MVP, ma progetta il catalogo in modo che sia possibile: un brand può lanciare una **serie di emoticon sponsorizzata** come evento a tempo (pochi possessori iniziali, poi si diffonde tra amici). Regole fisse: sempre segnalata come sponsorizzata, mai a pagamento per gli utenti, nessuna profilazione dei minori.

### Drops di piccoli brand e negozi
Una sezione **Drops** nella barra principale: uscite limitate di piccoli brand, artisti e negozi locali, che oggi vanno molto. Un drop può essere **qualsiasi cosa**: vestiti, sneakers, trucco, merch, un poster, ma anche un **nuovo singolo** che esce sulle app di musica. La sezione ha i filtri per categoria (Moda, Musica, Trucco, Merch, In negozio) e chi pubblica può essere un brand, un negozio o un **artista**.
- Per la musica il drop è un **pre-salvataggio**: il giorno dell'uscita il brano arriva nella libreria della propria app di musica e chi l'ha pre-salvato riceve l'emoticon esclusiva. Niente da comprare. Più avanti: ascolto insieme a mezzanotte con gli amici.
- Categorie vietate: alcol, svapo, scommesse, prodotti dimagranti, e qualsiasi cosa non adatta ai 14-17enni.
- Prenotazione con **scelta della taglia** (XS-XL, numeri per le scarpe).
- Per i drop più richiesti (per esempio sneakers numerate) un'**estrazione** al posto del "chi arriva prima": una partecipazione a persona, vincitori a caso, si paga solo se si vince. Possono partecipare solo gli account **verificati dagli amici**, quindi niente bot né rivenditori: è un vantaggio concreto da raccontare ai brand. Chi partecipa riceve comunque l'emoticon esclusiva.
- Più avanti: i ragazzi pubblicano in bacheca il "fit check" con il capo preso, collegato al drop.
- Ogni drop ha un negozio verificato, pochi pezzi, un'ora di uscita e un'**emoticon esclusiva** inclusa. L'emoticon poi gira tra amici come le altre, ed è la pubblicità che il brand ottiene.
- Stati del drop: **in arrivo** (promemoria 10 minuti prima), **live** (conto alla rovescia e pezzi rimasti), **in negozio** (un QR alla cassa, che cambia ogni minuto, regala l'emoticon a chi passa di persona).
- **Prenotazione** con ritiro in negozio o spedizione. Per i 14-17enni l'acquisto lo approva un genitore. Pagamento con Revolut Pay, carta, Apple Pay o Google Pay, da verificare con le regole degli store.
- I negozi **non possono** scrivere, aggiungere o vedere chi sono i ragazzi: ricevono solo totali (promemoria, prenotazioni, quanto ha girato l'emoticon).
- Dashboard web per i brand, con pagamento per drop tramite carta o Revolut Business. Dettagli in `docs/strategia.md`.

---

## Skin
L'app ha più skin, che cambiano colori, font e decorazioni ma **mai la posizione dei comandi**.

**Colori di base, da scegliere tra tre proposte** (l'azzurro lucido di partenza era troppo infantile; il lucido resta solo su emoticon e pulsante dello zing):
- **Cobalto**: blu `#2B4FD8`/`#1D36A8`, sfondi `#F4F6FB`, testo `#111A33`, accento corallo `#FF5A6E`. Proposta preferita: va bene per tutte le età.
- **Inchiostro e pesca**: blu notte `#1B2140`, accento pesca `#FF8A5C`, sfondo panna.
- **Pervinca**: blu-lilla `#6C7CFF`, pannelli lilla tenue, bolle lime.

**Regole di coerenza visiva** (valgono per tutte le skin):
- **Lucido e 3D solo su ciò che si colleziona**: emoticon, pezzi e pulsante dello zing. Avatar, barre, pulsanti e card sono piatti.
- **Interfaccia neutra con un solo accento** per le azioni (corallo in Cobalto). La rarità si mostra con un pallino colorato, non con etichette piene. Avatar degli amici in colori con la stessa luminosità e saturazione.
- **Una scala di angoli**: 10 px per gli elementi piccoli, 12 px per i medi, 16 px per card e post, pillola per pulsanti e avatar.
- **Due font**: uno geometrico per titoli e logo, uno per il testo. Il font pixel resta solo come tocco nostalgico negli avvisi di zing e nei codici delle scorciatoie.

**Skin di stile**:
- **Classic 2005**: barre da finestra, Verdana, angoli squadrati, per chi ha usato MSN;
- **Y2K Chrome**: scura, cromata e neon, per la Gen Z;
- **Clean**: bianca e tranquilla, per chi vuole solo le funzioni.

Implementale come set di design token (colori, font, raggi, ombre) sopra gli stessi componenti.

---

## Vincolo importante sugli asset
L'app deve **evocare** MSN, non copiarlo. Non usare emoticon, suoni, loghi, nomi o grafiche di Microsoft/MSN. Tutte le emoticon, i suoni (incluso quello dello zing e del "contatto online") e le skin devono essere **originali**, nello stile nostalgico anni 2000 riletto per la Gen Z: faccine tonde, colori saturi, animazioni piccole e ironiche, effetti "glossy". Includi una famiglia di emoticon con **occhi dolci** (occhioni lucidi e supplichevoli, stile QQ e sticker asiatici): sono tra le più usate per chiedere attenzioni e si sposano con lo zing. Per l'MVP crea placeholder originali (SVG o Lottie semplici) e una struttura che mi permetta di sostituirli con gli asset di un illustratore.

Prima del lancio va verificata la disponibilità del nome "Zing" come marchio e dei domini, in Italia e nei mercati principali. Il repository si chiama ancora `trillo`: si può rinominare su GitHub quando il nome è confermato.

---

## Stack consigliato
- **App**: React Native + Expo + TypeScript, Expo Router. **Development build fin dalla Fase 0** (le push su Android non funzionano in Expo Go).
- **Backend**: Supabase (Postgres, Auth, Realtime, Storage, Edge Functions), progetto in regione UE.
- **Animazioni**: Lottie (`lottie-react-native`) o Rive per emoticon, pezzi e zing; Reanimated per lo scuotimento della chat.
- **Vibrazione e suoni**: `expo-haptics`, `expo-audio` (non `expo-av`, che è deprecato).
- **Riferimenti di mercato**: vedi `docs/trends.md` (Stati Uniti e Cina).
- **Notifiche push**: Expo Notifications, con suono personalizzato dello zing.
- **Stato client**: Zustand + TanStack Query.
- **Analytics**: eventi anonimi salvati nel nostro database (o uno strumento self-hosted in UE). **Nessun SDK pubblicitario o di tracciamento di terze parti.**
- **Test**: Jest per la logica, pgTAP per le funzioni del database (assegnazione emoticon, economia, amicizie, zing, cotte).

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
- Chat 1:1 in tempo reale, con zing ed emoticon in primo piano, e il compositore di mix.
- "Sta scrivendo...", invio di foto (con moderazione), cronologia.
- **Stati alla MSN**: Online, Occupato, Torno subito, Al telefono, A pranzo, Invisibile.
- **Messaggio personale** sotto il nome, visibile agli amici.
- **Avviso "è online"**: opzione per ricevere un avviso quando un amico specifico si collega.
- Eliminazione dei propri messaggi.
- Vocali e conferme di lettura non entrano nell'MVP: prima zing ed emoticon, poi il resto.
- Messaggi non cifrati end-to-end nell'MVP: la scelta va scritta in modo chiaro nell'informativa privacy.

### 3. Profilo e bacheca (MySpace rivisto in chiave 2026)
- Si entra nel profilo di un amico toccando il suo avatar (nella lista amici o in alto nella chat) e si **legge la sua pagina**, come un piccolo blog personale.
- **Pagina personalizzabile** come su MySpace: tema della copertina (cielo, bubblegum, midnight, lime, chrome), mood, **canzone del profilo** ("now playing"), tag di interessi, vetrina con 3 emoticon.
- **Bacheca**: post con **foto** (con didascalia e sticker emoticon) e post **blog** (titolo e testo più lungo). Si reagisce **con le emoticon che si possiedono**: se un amico reagisce con un'emoticon che non hai, toccandola puoi prenderla (rispettando l'economia).
- **Commenti** sotto ogni post e **messaggi in bacheca** (il guestbook di MySpace).
- Tutto visibile **solo agli amici**; foto caricate sempre moderate prima della pubblicazione.
- Niente classifica "Top 8" degli amici: tra i 14-17enni crea drammi. Al massimo una "crew" senza ordine.
- **Più avanti: giornali e pagine** da seguire (giornalino della scuola, riviste di musica, artisti, brand) che pubblicano sulla bacheca come post. Contenuti editoriali scelti, niente pubblicità profilata ai minori.

---

## Sicurezza e benessere (target 14-20 anni)
Questa sezione ha la precedenza su qualsiasi funzionalità. Se una funzione la mette in discussione, fermati e chiedimi.

- **Età minima: 14 anni** (deciso). In Italia sotto i 14 anni serve il consenso dei genitori: per ora non apriamo ai 13enni. Il target ha un'età non troppo alta, quindi il cuore dell'app è la fascia 14-17.
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
4. **Chat di gruppo** (per la classe o la compagnia), con zing di gruppo.
5. **Scambi**: proposta di scambio di emoticon tra due amici, accettata da entrambi.
6. **Eventi stagionali**: a Halloween, Natale, fine scuola un account ufficiale manda un'emoticon speciale a pochi utenti a caso; da lì si diffonde.
7. **Mappa della diffusione**: un grafo che mostra come un'emoticon è passata tra i tuoi amici.
8. **Badge e obiettivi**: Collezionista (50 emoticon), Untore (hai passato un'emoticon a 20 persone), Alchimista (5 fusioni scoperte), Zinger seriale.
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
- `conversations`, `conversation_members`, `messages` (tipo: testo, immagine, mix di emoticon e pezzi, zing, sistema; deleted_at)
- `emoticons` (id, code, kind: face/part, set, name (tradotto), shortcut, rarity, series, animation, asset_path, is_fusion, max_holders)
- `user_emoticons` (user_id, emoticon_id, acquired_at, source_user_id, source_message_id, is_patient_zero)
- `emoticon_passes` (giver_id, receiver_id, emoticon_id, passed_at) — per i limiti dell'economia
- `economy_config` (rarity, weekly_passes, monthly_passes, min_account_age_days, ...)
- `fusion_recipes` (input_a, input_b, output, discovered_by, discovered_at)
- `zings` (sender, receiver, conversation_id, sent_at) per cooldown e statistiche
- `crushes` (user_id, target_id, created_at) — mai leggibile dal client, solo il match
- `reports`, `blocks`, `mutes`
- `events`, `badges`, `user_badges`, `analytics_events`
- Row Level Security attiva su tutte le tabelle.

---

## Piano di sviluppo a fasi
1. **Fase 0** — Setup progetto, `CLAUDE.md`, struttura cartelle, Supabase locale, development build, CI di base.
2. **Fase 1** — Registrazione con data di nascita e fasce d'età, profili, amicizie (QR, invito, username, rubrica con HMAC), blocco e segnalazione, stati e messaggio personale.
3. **Fase 2** — Chat 1:1 leggera e zing: animazione, vibrazione, suono, push, cooldown, combo, silenzia, ore di silenzio.
4. **Fase 3** — Emoticon collezionabili: catalogo con emoticon animate e pezzi componibili, mix in chat, Studio a pezzi con revisione, pacchetto iniziale, "Grab it!", economia, scorciatoie, album, provenienza, premio per gli inviti, analytics, anti-trucco con test.
   **→ Qui c'è l'MVP**: lo facciamo provare a un gruppo ristretto (20-30 persone, con i consensi necessari) e misuriamo se le emoticon circolano davvero.
5. **Fase 4** — Cotta segreta, fusioni, badge, eventi stagionali, moderazione automatica delle foto.
6. **Fase 5** — Bacheca completa (foto, blog, commenti, guestbook, temi del profilo), storie, chat di gruppo.
7. **Fase 6** — Extra scelti dalla lista sopra, Studio con caricamento di disegni, serie di artisti e brand.

Alla fine di ogni fase: fermati, riassumimi cosa hai fatto, come provarlo sul telefono (development build) e cosa resta aperto.

---

## Criteri di qualità
- Codice TypeScript tipizzato, componenti piccoli e riutilizzabili.
- Tutta la logica che assegna emoticon, applica l'economia, controlla amicizie, fasce d'età, cotte e limiti degli zing sta sul server ed è coperta da test.
- Animazioni fluide (60 fps) anche su telefoni di fascia media.
- Interfaccia in inglese e italiano fin dal primo giorno (i18n con file di traduzione), tono giovane e ironico.
- Seed del database con utenti ed emoticon di prova, più uno **script di simulazione** che fa girare la diffusione delle emoticon per qualche settimana virtuale, per verificare che le rare restino rare.
- Metriche da tracciare fin dall'MVP: emoticon prese per utente a settimana, inviti accettati, zing al giorno, utenti attivi dopo 7 e 30 giorni.
