# OpenClaw Managed RechnungsBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-rechnungsbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der RechnungsBot beantwortet Rechnungsfragen (offen/bezahlt) und kann freundlich erinnern.

## 2) Nutzen
- Weniger Buchhaltungspingpong
- Schnellere Klärung
- Saubere Daten

## 3) Benötigte Daten
### Minimum
- Rechnungsnummer oder E-Mail
- Rechnungsdatenquelle

### Empfohlen
- Reminder-Regeln
- Zahlungslink
- Eskalation

## 4) Beispiele
### Beispiel‑Input
```
User: Ist Rechnung R-2026-019 offen?
```

### Beispiel‑Output
```
Antwort: Offen, fällig am ..., Betrag ...
```

## 5) Workflow (komplett)
1) Anfrage
2) Identität prüfen
3) Datensatz suchen
4) Antwort
5) Optional Reminder/Link

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
invoice_id	customer_email	amount	currency	due_date	status	last_reminder_at
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

