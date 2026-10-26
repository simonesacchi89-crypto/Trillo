# Strategia: profili veri, brand, pagamenti, tutte le età

Nota di lavoro (ottobre 2026). I punti legali e le regole degli store vanno verificati con un legale prima di decidere: qui li riporto come li conosco, senza una verifica fatta per questo documento.

## 1. Niente profili finti o fatti con l'AI

Con utenti dai 14 anni il rischio principale non è lo spam: sono gli adulti che si fingono ragazzi, e i bot con foto generate dall'AI che cercano di agganciare minori. Nessun rilevatore di immagini AI è affidabile al 100%, quindi conviene lavorare su più livelli.

**Il livello più forte è già nel progetto: il grafo di amicizie reali.**
- Si diventa amici solo con richiesta + accettazione, e il modo principale è il QR code scansionato di persona.
- Proposta: un profilo è **"verificato da amici"** quando almeno 3 persone già verificate l'hanno aggiunto via QR di persona. Un bot non può andare a scuola a farsi scansionare il QR.
- Gli account nuovi e non verificati hanno funzioni limitate: niente bacheca pubblica per gli amici di amici, pochi zing al giorno, niente passaggi di emoticon rare.

**Alla registrazione**
- Numero di telefono verificato (OTP). I numeri virtuali e usa-e-getta si bloccano dove possibile.
- **Verifica dell'età** con un servizio di "age assurance" (stima dell'età dal selfie con controllo che sia una persona viva, oppure verifica tramite documento o genitore). In UE sono in arrivo anche gli strumenti ufficiali di verifica dell'età, e l'Italia è tra i paesi pilota: conviene progettare per poterli usare.
- Un selfie di controllo che si muove ("liveness") rende molto più difficile usare una foto generata.

**Sulle foto**
- Controllo automatico di ogni foto caricata: nudità, violenza e probabilità che sia generata dall'AI. Si leggono anche i metadati di provenienza (C2PA / Content Credentials), che molti generatori ormai inseriscono.
- La foto profilo deve essere coerente con il selfie di verifica. Per i minori, in alternativa, l'avatar disegnato invece della foto: elimina il problema alla radice.

**Nel tempo**
- Segnali di comportamento: account che aggiungono molti sconosciuti, scrivono soprattutto a minori, mandano lo stesso messaggio a tanti.
- Pulsante "questo profilo è finto" ben visibile, con revisione umana veloce per le segnalazioni che riguardano minori.
- Regola chiara nei termini: vietati i profili di persone inventate e i bot. Gli account automatici sono permessi solo ai brand, e solo dichiarati come tali.

## 2. Negozi e brand

L'idea forte è far entrare i brand **dentro il gioco delle emoticon**, non con la pubblicità classica.

**Account Brand e Negozio**
- Profilo verificato e chiaramente segnalato ("Brand" o "Negozio"), con la sua bacheca stile MySpace.
- **Non può** scrivere in chat ai ragazzi, mandare zing, chiedere amicizia o vedere chi sono i follower minorenni.
- Gli utenti scelgono di seguirlo; i suoi post appaiono in una sezione separata, mai mescolati con gli amici.

**Cosa possono fare**
- **Serie di emoticon sponsorizzate** come eventi a tempo: poche copie iniziali, poi si diffondono tra amici come tutte le altre.
- **Drop nei negozi**: un QR in vetrina o in cassa regala un'emoticon esclusiva a chi passa di persona. Porta gente nei negozi fisici e collega online e offline, come fanno molte app in Cina.
- **Temi della bacheca** e oggetti per l'avatar firmati dal brand.
- Statistiche aggregate e anonime: quante persone hanno preso l'emoticon, quanto ha girato. Mai dati sui singoli ragazzi.

**Regole fisse**
- Niente pubblicità basata sul profilo per i minori (vietata dal DSA): solo contenuti scelti dall'utente o legati al contesto.
- Sempre segnalato come sponsorizzato. Niente brand di alcol, tabacco, scommesse, integratori dimagranti né incontri.
- Approvazione manuale di ogni campagna.

## 3. Pagamenti e Revolut

**Cosa si paga**
1. **Brand e negozi** che pagano Zing per serie sponsorizzate, drop e pagine: è il primo ricavo sensato.
2. **Utenti** che comprano oggetti estetici (temi, cornici, vestiti per l'avatar). Mai emoticon a sorpresa a pagamento.
3. Più avanti: artisti che vendono le loro serie, con una percentuale a loro.

**Dove ha senso Revolut**
- **Per i brand: sì.** Dashboard web per i brand con pagamento tramite Revolut Business (link di pagamento, fatture, Revolut Pay, carte). Gestione semplice, nessuna commissione degli store.
- **Per gli acquisti degli utenti dentro l'app: no, almeno all'inizio.** Su iPhone e Android i beni digitali venduti nell'app devono passare dai pagamenti di Apple e Google. In UE (Digital Markets Act) e negli Stati Uniti (dopo la causa Epic contro Apple) oggi sono permessi anche pagamenti esterni o link a un negozio web, ma con regole e commissioni che cambiano spesso: da verificare al momento del lancio.
- **Opzione interessante**: Revolut ha i conti per under 18 gestiti dai genitori. Un negozio web di Zing con Revolut Pay permetterebbe ai ragazzi di comprare oggetti estetici con il loro conto, sotto il controllo dei genitori.

**Regole per i minori**: limite di spesa mensile, conferma del genitore sopra una certa soglia, niente acquisti impulsivi a tempo ("solo per 10 minuti!").

## 4. Estendere a tutte le età

La buona notizia: la nostalgia di Zing funziona in due direzioni. Chi ha 30-40 anni **ricorda** MSN e MySpace; chi ne ha 15 lo **scopre** come estetica Y2K. Lo zing come segnale di interesse è universale: tra amici, tra fidanzati, tra genitori e figli.

**Un'app, spazi separati**
- Stesso cuore per tutti: zing, emoticon da collezionare, bacheca.
- **Fasce d'età separate**: i minori non si possono trovare né aggiungere da adulti sconosciuti, come già previsto. La cotta segreta resta dentro la stessa fascia.
- **Collegamento famiglia**: genitore e figlio possono collegarsi esplicitamente. Il genitore non legge le chat, ma può mandare zing e vedere le impostazioni di sicurezza.

**Una UI che piace a tutti: le skin**
L'interfaccia di base resta pulita. Ognuno sceglie l'atmosfera, e questo è già nello spirito MySpace:
- **Classic 2005**: più vicina a MSN, finestre e gradienti azzurri, per chi se lo ricorda;
- **Y2K chrome**: cromata e più scura, per la Gen Z;
- **Clean**: minimale, per chi vuole solo le funzioni.

Le skin cambiano colori, font e decorazioni, non la posizione dei pulsanti: chi aiuta un genitore o un amico trova le cose sempre nello stesso posto.

**Cosa resta uguale per tutti** (ciò che rende Zing unico): lo zing, le emoticon animate e componibili che si hanno solo se te le mandano, la bacheca personale, e nessun feed infinito né algoritmo che decide cosa vedi.

## Priorità proposte
1. Profili veri e verifica dell'età: prima del lancio, non dopo.
2. Account brand e drop nei negozi: dopo l'MVP, come primo ricavo.
3. Pagamenti brand con Revolut Business: insieme al punto 2.
4. Skin e apertura agli adulti: dopo il test con i ragazzi, quando sappiamo che il cuore funziona.
