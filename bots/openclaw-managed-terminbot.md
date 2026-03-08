# OpenClaw Managed TerminBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-terminbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der TerminBot sammelt Terminwünsche ein und führt zu einem passenden Terminlink.

## 2) Nutzen
- Mehr Termine
- Weniger Hin-und-her
- Reminder gegen No-Shows

## 3) Benötigte Daten
### Minimum
- Name
- Kontakt
- Anlass
- Terminlink/Kalender

### Empfohlen
- Regeln (Zeiten)
- Dauer
- Ausschlussfälle

## 4) Beispiele
### Beispiel‑Input
```
User: Ich brauche einen Termin nächste Woche.
```

### Beispiel‑Output
```
Bot: Hier ist dein Terminlink: ...
```

## 5) Workflow (komplett)
1) Wunsch
2) Pflichtfragen
3) Validieren
4) Link senden/buchen
5) Bestätigung/Reminder

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	source	name	contact	reason	preferred_time	booking_link	status
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

