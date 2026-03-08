# OpenClaw Managed OnboardingBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-onboardingbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der OnboardingBot führt neue Kunden/Users durch Schritte und sammelt fehlende Infos.

## 2) Nutzen
- Weniger Support
- Schnellere Aktivierung
- Einheitlicher Start

## 3) Benötigte Daten
### Minimum
- User-Kontakt
- Schritt-Liste
- Ziel

### Empfohlen
- Links
- Eskalation
- Stop-Regeln

## 4) Beispiele
### Beispiel‑Input
```
User: Ich bin neu, wie starte ich?
```

### Beispiel‑Output
```
Schritt 1... Schritt 2...
```

## 5) Workflow (komplett)
1) Begrüßen
2) Schrittfolge
3) Validieren
4) Abschluss
5) Log

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	user	step	completed	status	note
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

