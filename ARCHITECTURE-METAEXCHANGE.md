# MetaExchange — Architettura Pagamenti & Scambio (v1.0)

MetaExchange è il layer di **scambio di valore** dell’ecosistema Hermeticum.
Funziona sopra:
- **IPR-Personale** (identità operativa)
- **GitJoker C2** (traccia, prova, audit)
- endpoint finanziari **off-chain** (IBAN / wallet) mai pubblici su Git

Principio:
> **Decidi, e paghi la traccia per rimanere nel tempo.**

---

## 1) Obiettivo

Abilitare pagamenti e fatturazione per:
- attivazione IPR
- mantenimento annuale
- ancore aggiuntive
- audit / freeze / export UE
- servizi modulari (energia, spazio, governance)

MetaExchange deve garantire:
- separazione tra **identità**, **prova**, **pagamento**
- tracciabilità del pagamento senza esporre dati bancari
- auditabilità UE-grade

---

## 2) Regole fondamentali (NO leak)

- IBAN, wallet address personali, KYC documenti: **MAI** su repo pubblici
- Su Git solo:
  - ID transazione (interno)
  - hash ricevuta/quietanza
  - importo, valuta, data
  - stato (PAID / PENDING / FAILED / REFUNDED)
  - riferimento a IPR-ID (pseudonimo se necessario)

---

## 3) Oggetti principali

### IPR-ID
Identità operativa del soggetto.

### ORDER-ID
Identificativo ordine (attivazione, rinnovo, ancora, audit).

### PAYMENT-RECEIPT
Ricevuta/quietanza (PDF o JSON) conservata **privatamente**.
Su Git si pubblica solo:
- hash della ricevuta
- metadata minimi

### TRACE-ANCHOR
Traccia pubblica: commit + release + pagina di verifica.

---

## 4) Flusso operativo (standard)

### Step A — Creazione ordine
- Genera ORDER-ID
- Associa IPR-ID
- Definisce importo e scadenza

### Step B — Pagamento (off-chain)
- Bonifico (IBAN) / card / wallet
- MetaExchange riceve conferma pagamento
- Genera ricevuta privata

### Step C — Prova su GitJoker (pubblica)
- commit su repo proof (o registry)
- pubblica:
  - ORDER-ID
  - stato: PAID
  - hash della ricevuta
  - timestamp

### Step D — Esecuzione servizio
- attiva IPR / rinnovo / ancora / audit
- produce output (documento, release, freeze)

---

## 5) Stati pagamento (canonici)

- PENDING  → ordine creato, in attesa
- PAID     → pagamento ricevuto
- FAILED   → pagamento fallito o scaduto
- REFUNDED → rimborsato (con hash nota)

---

## 6) Proof Registry (consigliato)

Creare un repository dedicato:
`metaexchange-proof-registry`

Contiene record minimi tipo:

- ORDER-ID
- IPR-ID (o pseudonimo)
- AMOUNT / CURRENCY
- STATUS
- RECEIPT_HASH
- TIMESTAMP
- SERVICE_TYPE (IPR_INIT / IPR_RENEW / ANCHOR_ADD / AUDIT / FREEZE / EXPORT)

In questo modo:
- la prova è pubblica
- i dati finanziari restano privati

---

## 7) Privacy & UE compliance (principi)

- minimizzazione dati
- separazione degli archivi
- nessun dato bancario in pubblico
- audit trail verificabile
- conservazione ricevute in storage privato controllato

---

## 8) Listino collegato (integrazione)

MetaExchange deve leggere come fonte prezzi:
- `hermeticum-bce-ipr/PRICING-IPR.md`
e produrre ordini coerenti (ORDER-ID).

---

## 9) Endpoint di pagamento (implementazione)

### Modalità 1 — Bonifico (IBAN)
- più semplice
- scalabile
- UE-friendly
- richiede riconciliazione manuale o semi-automatica

### Modalità 2 — Stripe / PSP
- automatico
- costi di commissione
- KYC del provider

### Modalità 3 — Crypto wallet
- tracciabile on-chain
- gestione volatilità e compliance
- policy anti-riciclaggio (se applicabile)

---

## 10) Output finale (quando PAID)

Ogni pagamento valido produce:
- prova pubblica (hash + stato)
- release o update IPR correlato
- documento / servizio eseguito

---

Signed: Manuel Coletta  
Hermeticum B.C.E. — MetaExchange Architecture
