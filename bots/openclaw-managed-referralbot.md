# OpenClaw Managed ReferralBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-referralbot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der ReferralBot fragt bestehende Kunden freundlich nach Empfehlungen und sammelt neue Kontakte strukturiert.

## 2) Nutzen
- Mehr Empfehlungen
- Planbarer Referral-Prozess
- Saubere Kontaktdaten

## 3) Benötigte Daten
### Minimum
- Liste der Bestandskunden (oder Trigger nach Kauf)
- Textvorlage
- Zielsystem (Sheet/CRM)

### Empfohlen
- Double-Opt-In (wenn nötig)
- Reward-Regeln
- No-Spam Regeln

## 4) Beispiele
### Beispiel‑Input
```
Bot: Kennst du 1 Person, der das hilft? (Name + Kontakt)
```

### Beispiel‑Output
```
Referral gespeichert: referrer + referral_contact + status NEW
```

## 5) Workflow (komplett)
1) Kunden ansprechen
2) Referral-Daten abfragen
3) Optional Opt-In
4) Übergabe an Sales
5) Loggen

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
created_at	referrer	referral_name	referral_contact	status	note
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

