# OpenClaw Managed StatusBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-statusbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der StatusBot beantwortet Status-Anfragen (Ticket/Auftrag/Lieferung) aus einer Datenquelle.

## 2) Nutzen
- Weniger Rückfragen
- Schnell Klarheit
- Entlastung fürs Team

## 3) Benötigte Daten
### Minimum
- Ticket- oder Auftragsnummer (oder E-Mail)
- Statusquelle (Sheet/CRM)

### Empfohlen
- Identitätscheck
- Owner/SLA Texte
- Eskalation

## 4) Beispiele
### Beispiel‑Input
```
User: Status zu Ticket 4829?
```

### Beispiel‑Output
```
Antwort: IN_BEARBEITUNG, nächstes Update bis ...
```

## 5) Workflow (komplett)
1) Statusfrage
2) ID abfragen
3) Datensatz suchen
4) Status antworten
5) Nicht gefunden -> Anleitung/Eskalation

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
ticket_id	email	status	last_update	next_step	owner
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

