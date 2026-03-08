# OpenClaw Managed FAQBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-faqbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der FAQBot beantwortet häufige Fragen sofort und eskaliert Sonderfälle an Menschen.

## 2) Nutzen
- Weniger Support-Aufwand
- Schnelle Antworten
- Einheitliche Aussagen

## 3) Benötigte Daten
### Minimum
- User-Frage
- Wissensbasis (FAQ-Liste)
- Eskalationskontakt

### Empfohlen
- Kategorien/Intents
- No-Go Aussagen
- Links zu passenden Seiten

## 4) Beispiele
### Beispiel‑Input
```
User: Was kostet Managed Hosting?
```

### Beispiel‑Output
```
Antwort: Managed Hosting startet ab ... Für genaue Details: 2 Fragen ...
```

## 5) Workflow (komplett)
1) Frage kommt rein
2) Thema erkennen
3) Antwort aus Wissensbasis
4) Unsicher -> Rückfrage/Eskalation
5) Loggen

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	source	question	category	answer_used	confidence	status	escalated_to
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

