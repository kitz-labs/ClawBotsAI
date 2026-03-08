# OpenClaw Managed NPSBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-npsbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der NPSBot fragt Kundenzufriedenheit (0-10), sammelt Feedback und leitet kritische Fälle intern weiter.

## 2) Nutzen
- Frühwarnsystem für Unzufriedenheit
- Mehr positives Feedback
- Messbarer NPS

## 3) Benötigte Daten
### Minimum
- Kundenkontakt
- Fragezeitpunkt (z.B. 7 Tage nach Kauf)
- Speicherung

### Empfohlen
- Folgefragen je Score
- Eskalationsweg
- Dashboard/Report

## 4) Beispiele
### Beispiel‑Input
```
Bot: Wie wahrscheinlich ist es, dass du uns empfiehlst (0-10)?
```

### Beispiel‑Output
```
Score=6 -> Feedbackfrage + Ticket an Team
Score=10 -> Review/Referral anbieten
```

## 5) Workflow (komplett)
1) NPS-Frage senden
2) Score speichern
3) Folgefrage (Warum?)
4) Bei Low Score eskalieren
5) Report erzeugen

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	customer	score	comment	segment	status	escalated
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

