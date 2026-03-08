# OpenClaw Managed AngebotsBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-angebotsbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der AngebotsBot sammelt fehlende Informationen für ein Angebot und übergibt ein sauberes Briefing.

## 2) Nutzen
- Schnellere Angebote
- Weniger Rückfragen
- Klarere Anforderungen

## 3) Benötigte Daten
### Minimum
- Kontakt
- Leistung
- Pflichtinfos

### Empfohlen
- Pakete/Preisspannen
- Lieferzeit
- Qualifizierungsfragen

## 4) Beispiele
### Beispiel‑Input
```
User: Angebot für LeadBot
```

### Beispiel‑Output
```
Briefing mit Kanal, Zielsystem, Fragen, Budget, Deadline
```

## 5) Workflow (komplett)
1) Anfrage
2) Pflichtinfos abfragen
3) Zusammenfassung
4) Übergabe
5) Status setzen

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	name	contact	requested_service	requirements	budget	summary	status
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

