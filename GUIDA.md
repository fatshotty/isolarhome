# iSolar Home — Setup rapido (dominio + sito + email)

Obiettivo: online con spesa minima. Tempo totale ~45 min (poi qualche ora di attesa per la propagazione DNS).
Costo indicativo: **~10–15 €/anno per il .it**, tutto il resto **gratis**.

---

## Riepilogo dello stack (tutto gratis tranne il dominio)

| Pezzo | Servizio | Costo |
|-------|----------|-------|
| Dominio | Registrar (es. Aruba / Tophost) | ~10–15 €/anno (.it) |
| DNS + email forwarding | **Cloudflare** (gratis) | 0 € |
| Sito | **GitHub Pages** (gratis) | 0 € |
| Casella email | Cloudflare Email Routing → **la tua Gmail** | 0 € |

> Perché Cloudflare in mezzo: fa da DNS gratuito **e** inoltra `info@isolarhome.it` alla tua Gmail senza costi. GitHub Pages da solo non gestisce le email.

---

## STEP 1 — Comprare il dominio (~10 min)

1. Vai su un registrar. Consigliati per il `.it`:
   - **Tophost** o **Serverplan** (italiani, economici)
   - oppure **Aruba** / **Register.it** (se vuoi tutto in italiano con assistenza telefonica)
2. Cerca e acquista **`isolarhome.it`**.
3. (Consigliato) acquista anche **`isolarhome.net`** per proteggere il nome.
4. Se c'è l'opzione **privacy WHOIS**, attivala.

> Nota: Cloudflare **non vende** domini `.it`, per questo il dominio si compra altrove e poi si "collega" a Cloudflare nello step 2.

---

## STEP 2 — Collegare il dominio a Cloudflare (~10 min)

1. Crea un account gratuito su **cloudflare.com**.
2. **Add a site** → inserisci `isolarhome.it` → piano **Free**.
3. Cloudflare ti mostrerà **2 nameserver** (es. `xxx.ns.cloudflare.com`).
4. Torna nel pannello del registrar (dove hai comprato il dominio) → sezione **Nameserver / DNS** → sostituisci i nameserver con quelli di Cloudflare.
5. Attendi la conferma di Cloudflare (da pochi minuti a qualche ora).

---

## STEP 3 — Pubblicare il sito su GitHub Pages (~15 min)

1. Crea un account gratuito su **github.com**.
2. Crea un nuovo repository **pubblico**. Nome: `isolarhome` (va bene qualsiasi).
3. Carica i due file che ti ho preparato: **`index.html`** e **`CNAME`**
   (pulsante **Add file → Upload files** → trascina i file → **Commit**).
4. Vai su **Settings → Pages**:
   - **Source**: `Deploy from a branch`
   - **Branch**: `main` / cartella `/root` → **Save**.
5. Sempre in **Settings → Pages**, campo **Custom domain**: scrivi `isolarhome.it` → **Save**.
   (Il file `CNAME` che ti ho dato lo imposta già, ma verifica.)
6. Spunta **Enforce HTTPS** appena diventa disponibile.

### DNS per il sito (da fare in Cloudflare, sezione DNS)
Aggiungi questi record (tipo **A**, name `@`, proxy **DNS only / grigio**):

```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
CNAME  www   <tuo-utente>.github.io
```

> Sostituisci `<tuo-utente>` con il tuo username GitHub.
> Importante: per GitHub Pages i record devono essere **DNS only** (nuvoletta grigia, non arancione).

---

## STEP 4 — Email `info@isolarhome.it` sulla tua Gmail (~10 min)

1. In Cloudflare, apri **Email → Email Routing** → **Enable**.
   (Cloudflare aggiunge da solo i record MX necessari.)
2. **Destination addresses** → aggiungi la tua Gmail → conferma dal link che ricevi.
3. **Routing rules** → **Create address**:
   - Custom address: `info@isolarhome.it`
   - Action: **Send to** → la tua Gmail.
4. Fatto: le email a `info@isolarhome.it` arrivano nella tua Gmail. **Gratis.**

### (Opzionale) Rispondere DA info@isolarhome.it
Per inviare, non solo ricevere, in Gmail:
`Impostazioni → Account e importazione → Invia messaggi come → Aggiungi un altro indirizzo email`.
Ti servirà un server SMTP: la via più semplice e gratuita è **Brevo** (ex Sendinblue), piano free.
Se per ora ti basta **ricevere**, salta questo punto.

---

## Ordine consigliato
STEP 1 → STEP 2 → (aspetta che Cloudflare sia attivo) → STEP 3 e STEP 4 in parallelo.

## Check finale
- [ ] `https://isolarhome.it` mostra la pagina
- [ ] Il lucchetto HTTPS è attivo
- [ ] Un'email di test a `info@isolarhome.it` arriva in Gmail

---

## Promemoria importante (marchio)
Dominio libero ≠ marchio registrabile. "iSolar" è già usato da diverse aziende del solare
(e Apple è storicamente attiva sui marchi "i-"). Prima di stampare biglietti, furgone e insegne,
fai una ricerca di anteriorità su **UIBM** (uibm.mise.gov.it) ed **EUIPO**.
