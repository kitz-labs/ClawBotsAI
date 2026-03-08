# OpenClaw Managed NewsletterBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-newsletterbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der NewsletterBot erstellt Betreff, Preheader und Text (mit CTA) und liefert Copy/Paste für dein Versandtool.

## 2) Nutzen
- Schneller Content
- Konsistenter Stil
- Bessere CTAs

## 3) Benötigte Daten
### Minimum
- Thema
- Zielgruppe
- CTA

### Empfohlen
- Brand Voice
- Angebot/Link
- Segment-Regeln

## 4) Beispiele
### Beispiel‑Input
```
Thema: Frühjahrsangebot. Ziel: Termin buchen.
```

### Beispiel‑Output
```
Betreff/Preheader/Body/CTA fertig
```

## 5) Workflow (komplett)
1) Input
2) Varianten
3) Freigabe
4) Versand vorbereiten
5) Speichern

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	campaign	segment	subject	preheader	cta	status
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

