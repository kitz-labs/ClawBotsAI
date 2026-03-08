# OpenClaw Managed UpsellBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-upsellbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der UpsellBot empfiehlt passende Add-ons/Upgrades basierend auf Kontext und Regeln.

## 2) Nutzen
- Mehr Umsatz
- Passendere Pakete
- Automatisierte Empfehlungen

## 3) Benötigte Daten
### Minimum
- Produktkatalog
- Kontext
- CTA Link

### Empfohlen
- No-Spam Regeln
- Trigger
- Varianten

## 4) Beispiele
### Beispiel‑Input
```
User: Ich habe LeadBot gekauft.
```

### Beispiel‑Output
```
Empfehlung: Managed Hosting + CRM Integration
```

## 5) Workflow (komplett)
1) Kontext
2) Regeln
3) Empfehlung 1-2
4) CTA
5) Log

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
customer	context	suggestion	clicked	status	last_shown_at
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

