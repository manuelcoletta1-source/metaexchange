# MetaExchange — Layer di scambio tracciato (Hermeticum B.C.E.)

MetaExchange è il **nodo BCE** dedicato allo **scambio tracciato**:
ogni trasferimento di dato, valore o diritto è registrato, verificabile e opponibile.

---

## Nodi Pubblici (GitHub Pages)

- **MetaExchange (Pages)**  
  https://manuelcoletta1-source.github.io/metaexchange/

- **Services (HUB)**  
  https://manuelcoletta1-source.github.io/hermeticum-bce-services/

- **Technology**  
  https://manuelcoletta1-source.github.io/Hermeticum-B.C.E.-Technology/

---

## Scopo

- Tracciare scambi e interazioni
- Collegare scambio → evidenza → tempo
- Garantire auditabilità
- Integrare validità (UNEBDO) e opponibilità (OPC)

---

## Struttura consigliata del repo

- `/index.html` — pagina pubblica
- `/schemas/` — modelli di scambio
- `/records/` — registrazioni e hash
- `/verification/` — controlli e audit
- `/docs/` — specifiche tecniche

---

## Relazioni BCE

- **UNEBDO** → validità
- **OPC** → opponibilità
- **MetaExchange** → tracciamento
- **GitJoker-C2** → esecuzione

---

## Stato

🟢 ATTIVO — sviluppo controllato

---

© Hermeticum B.C.E. — Manuel Coletta
# MetaExchange — Proof Registry

> **Decidi, e paghi la traccia per rimanere nel tempo.**

Questo repository costituisce il **registro pubblico delle prove di pagamento**
dell’ecosistema **Hermeticum B.C.E.**.

MetaExchange separa in modo rigoroso:
- **identità** (IPR-Personale)
- **pagamento** (off-chain)
- **prova** (pubblica e verificabile)

---

## Scopo del repository

Il **Proof Registry** esiste per:
- rendere **verificabile** l’avvenuto pagamento di un servizio
- mantenere **traccia storica nel tempo**
- consentire **audit indipendente**
- evitare qualsiasi esposizione di dati sensibili

👉 Questo repository **NON** gestisce pagamenti.  
👉 Questo repository **NON** contiene IBAN, wallet o dati personali.

Contiene **solo prove**.

---

## Cosa è pubblico (e cosa no)

### Pubblico (su Git)
- ORDER-ID
- riferimento a IPR-ID (o pseudonimo)
- tipo di servizio
- importo e valuta
- metodo (IBAN / CRYPTO)
- stato del pagamento
- hash della ricevuta
- timestamp

### Privato (off-chain)
- IBAN
- wallet address
- ricevuta completa
- dati bancari o fiscali
- documenti di identità

---

## Struttura del repository

Ogni file in `records/` rappresenta **un pagamento**
e viene aggiunto con **commit dedicato**.

---

## Schema di un record di prova

Ogni record deve rispettare lo schema definito in `SCHEMA.md`.

Esempio semplificato:

```md
- ORDER-ID: ORDER-20260308-0001
- IPR-ID: IPR-XXXX
- SERVICE-TYPE: IPR_INIT
- AMOUNT: 390
- CURRENCY: EUR
- METHOD: IBAN
- STATUS: PAID
- RECEIPT-HASH: sha256:____________________
- TIMESTAMP: 2026-03-08T10:15:00Z
