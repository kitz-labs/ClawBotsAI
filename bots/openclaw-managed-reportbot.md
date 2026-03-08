# OpenClaw Managed ReportBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-reportbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der ReportBot erstellt regelmäßige Reports (KPIs), fasst zusammen und versendet sie an definierte Empfänger.

## 2) Nutzen
- KPIs automatisch
- Weniger manuelles Reporting
- Klare Zusammenfassung

## 3) Benötigte Daten
### Minimum
- Datenquelle (CSV/Sheet/API)
- Report-Rhythmus
- Empfänger

### Empfohlen
- KPI-Definitionen
- Alerts bei Anomalien
- Format (PDF/Email/Slack)

## 4) Beispiele
### Beispiel‑Input
```
Jeden Montag 08:00: Report für Sales + Support
```

### Beispiel‑Output
```
Report: 12 Leads, 4 Termine, 2 Abschlüsse. Nächste Aktion: ...
```

## 5) Workflow (komplett)
1) Daten ziehen
2) KPIs berechnen
3) Zusammenfassen
4) Senden
5) Archivieren

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	period	kpi	value	note	status
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

