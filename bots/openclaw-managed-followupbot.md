# OpenClaw Managed FollowUpBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-followupbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der FollowUpBot fasst automatisch nach (Leads/Angebote) und stoppt, sobald jemand antwortet.

## 2) Nutzen
- Mehr Antworten
- Mehr Abschlüsse
- Systematisches Nachfassen

## 3) Benötigte Daten
### Minimum
- Lead-Liste
- Zeitregeln
- Vorlagen

### Empfohlen
- Max Follow-ups
- Stop-Regeln
- Hot-Reply Eskalation

## 4) Beispiele
### Beispiel‑Input
```
Lead seit 7 Tagen ohne Antwort
```

### Beispiel‑Output
```
Follow-up gesendet (Stage 2)
```

## 5) Workflow (komplett)
1) Liste prüfen
2) Kandidaten finden
3) Vorlage wählen
4) Senden
5) Loggen + Stop bei Antwort

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
lead_id	name	email	last_contacted	followup_stage	next_followup_at	status
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

