# OpenClaw Managed ReviewBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-reviewbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der ReviewBot holt Bewertungen ein und eskaliert negatives Feedback intern.

## 2) Nutzen
- Mehr Reviews
- Bessere Qualität
- Negatives früh erkennen

## 3) Benötigte Daten
### Minimum
- Kundenkontakt
- Review-Link
- Timing

### Empfohlen
- Score 1-5
- Eskalation
- Folgefragen bei <=3

## 4) Beispiele
### Beispiel‑Input
```
Bot: Wie zufrieden (1-5)?
```

### Beispiel‑Output
```
Bei 5: Link schicken, bei 2: Ticket an Team
```

## 5) Workflow (komplett)
1) Anfrage
2) Score
3) Gut -> Link
4) Schlecht -> Details+Eskalation
5) Log

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
customer	contact	request_sent_at	rating	comment	status	escalated
```

### .env.example (Minimal)
```bash
CHANNEL=telegram
TELEGRAM_BOT_TOKEN=DEIN_TOKEN_HIER

LLM_PROVIDER=openai
OPENAI_API_KEY=DEIN_KEY_HIER
OPENAI_MODEL=gpt-4.1
OPENAI_MODEL_FAST=gpt-4.1-mini

LEADS_TARGET=google_sheets
GOOGLE_SHEET_ID=DEINE_SHEET_ID
GOOGLE_SERVICE_ACCOUNT_JSON_BASE64=BASE64_JSON_HIER
```

---

## 7) Installation (Kurz)
- Managed: Kanal + Fragen + Zielsystem an AI Kitz
- Eigenbetrieb: Docker starten (`docker compose up -d`) und testen

## 8) Troubleshooting (Kurz)
- Bot antwortet nicht → Token/Container/Webhook
- Speicherung fehlt → Sheet ID / Rechte / Service‑Account

