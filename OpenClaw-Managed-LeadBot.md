# OpenClaw Managed LeadBot (AI Kitz) – **Ultra‑Detail Anleitung**

Produktseite: https://www.aikitz.at/openclaw-managed-leadbot/

> Diese Datei ist absichtlich sehr ausführlich.
>
> Ziel: Du kannst den LeadBot installieren und benutzen, auch wenn du **fast keine Technik‑Erfahrung** hast.
>
> ⚠️ Sicherheitsregel: **Keine echten Keys/Passwörter in GitHub**.
> In dieser Doku sind alle Secrets Platzhalter wie `DEIN_TOKEN_HIER`.

---

## Inhaltsverzeichnis
0. [Ganz kurz: Was bekommst du?](#0-ganz-kurz-was-bekommst-du)
1. [Was ist der LeadBot?](#1-was-ist-der-leadbot)
2. [Was bringt er dir (Nutzen)?](#2-was-bringt-er-dir-nutzen)
3. [Welche Daten braucht der Bot? (mit Beispielen)](#3-welche-daten-braucht-der-bot-mit-beispielen)
4. [Wie sieht das Ergebnis aus? (Beispiel-Lead)](#4-wie-sieht-das-ergebnis-aus-beispiel-lead)
5. [Begriffe ganz einfach erklärt (Token, Webhook, Docker, LLM)](#5-begriffe-ganz-einfach-erklärt-token-webhook-docker-llm)
6. [Tech‑Stack (einfach erklärt)](#6-techstack-einfach-erklärt)
7. [Infrastruktur: Managed vs Eigenbetrieb](#7-infrastruktur-managed-vs-eigenbetrieb)
8. [Welche LLMs/Modelle sind am besten?](#8-welche-llmsmodelle-sind-am-besten)
9. [Workflow (wie der Bot arbeitet) – komplett](#9-workflow-wie-der-bot-arbeitet--komplett)
10. [Variante A: Managed Hosting (die einfachste Installation)](#10-variante-a-managed-hosting-die-einfachste-installation)
11. [Variante B: Eigenbetrieb mit Docker (Schritt für Schritt)](#11-variante-b-eigenbetrieb-mit-docker-schritt-für-schritt)
12. [Google Sheets Setup (so, dass es wirklich funktioniert)](#12-google-sheets-setup-so-dass-es-wirklich-funktioniert)
13. [Telegram Setup (BotFather) – Schritt für Schritt](#13-telegram-setup-botfather--schritt-für-schritt)
14. [WhatsApp Setup (Überblick)](#14-whatsapp-setup-überblick)
15. [Website Setup (Überblick)](#15-website-setup-überblick)
16. [Bedienung (Daily Ops) – wie du Leads abarbeitest](#16-bedienung-daily-ops--wie-du-leads-abbeitest)
17. [Beispiele für Fragen (Copy/Paste)](#17-beispiele-für-fragen-copypaste)
18. [Regeln & Guardrails (damit der Bot nicht „blöd“ wird)](#18-regeln--guardrails-damit-der-bot-nicht-blöd-wird)
19. [Monitoring & Logs (damit du sofort Fehler siehst)](#19-monitoring--logs-damit-du-sofort-fehler-siehst)
20. [Troubleshooting (wenn etwas nicht geht)](#20-troubleshooting-wenn-etwas-nicht-geht)
21. [Checklisten: Start / Go‑Live / Wartung](#21-checklisten-start--go-live--wartung)

---

## 0) Ganz kurz: Was bekommst du?
Du bekommst einen Bot, der:
- **Leads annimmt** (z. B. Telegram/WhatsApp/Website)
- **Fragen stellt** (z. B. Name, Branche, Ziel)
- **Alles in eine Tabelle schreibt** (Google Sheets) oder ins CRM
- Optional: **Benachrichtigungen** sendet (z. B. E‑Mail/Slack)

---

## 1) Was ist der LeadBot?
Der **OpenClaw Managed LeadBot** ist ein Lead‑Erfassungs‑ und Qualifizierungs‑Bot.

Er ist wie ein sehr freundlicher „Empfangs‑Mitarbeiter“:
- Er begrüßt neue Anfragen.
- Er stellt ein paar kurze Fragen.
- Er schreibt alles ordentlich auf.

### Mini‑Beispiel
Kunde schreibt:
> „Hallo, ich brauche Hilfe.“

Bot antwortet:
- „Hallo! Wie heißt du?“
- „Wie kann ich dich erreichen?“
- „Worum geht es genau?“

Danach ist der Lead sauber gespeichert.

---

## 2) Was bringt er dir (Nutzen)?
### 2.1 Du verlierst weniger Leads
Weil der Bot sofort antwortet.

### 2.2 Du sparst Zeit
Weil der Bot die Standard‑Fragen automatisch fragt.

### 2.3 Du bekommst bessere Informationen
Du bekommst keine unbrauchbaren Nachrichten wie „Hallo“.

### 2.4 Du hast Ordnung
Alle Leads sind an einem Ort.

---

## 3) Welche Daten braucht der Bot? (mit Beispielen)
### 3.1 Pflichtdaten
Mindestens:
- **Kontakt**: E‑Mail oder Telefon oder Messenger‑Chat
- **Name/Firma**
- **Problem/Ziel**

Beispiele:
- E‑Mail: `max@firma.at`
- Telefon: `+43 650 1112223`
- Ziel: „Mehr Termine“

### 3.2 Empfehlenswerte Daten
- Branche (z. B. „Hotel“)
- Zeitrahmen (z. B. „Sofort“)
- Budget‑Range (z. B. „500–1500 EUR“)
- Tools (z. B. „Google Kalender“)

---

## 4) Wie sieht das Ergebnis aus? (Beispiel-Lead)
### 4.1 Beispiel als Text (wie in Google Sheets)

| Feld | Beispiel |
|---|---|
| created_at | 2026‑03‑08 05:00 |
| source | telegram |
| name | Anna Maier |
| company | Hotel Alpenblick |
| email | anna@hotel.at |
| phone | +43 660 1234567 |
| industry | Hotel / Tourismus |
| goal | Mehr Anfragen zu Terminen |
| timeframe | Sofort |
| budget_range | 500–1500 EUR |
| message | WhatsApp‑Anfragen vorqualifizieren + Terminlink |
| status | NEW |
| summary | Hotel in Tirol… |

### 4.2 Beispiel als JSON
```json
{
  "created_at": "2026-03-08T05:00:00+01:00",
  "source": "telegram",
  "name": "Anna Maier",
  "company": "Hotel Alpenblick",
  "email": "anna@hotel.at",
  "phone": "+43 660 1234567",
  "industry": "Hotel / Tourismus",
  "goal": "Mehr Anfragen zu Terminen",
  "timeframe": "Sofort",
  "budget_range": "500–1500 EUR",
  "message": "WhatsApp-Anfragen vorqualifizieren + Terminlink",
  "status": "NEW",
  "summary": "Hotel in Tirol möchte WhatsApp-Leads automatisch qualifizieren. Start sofort. Budget 500–1500."
}
```

---

## 5) Begriffe ganz einfach erklärt (Token, Webhook, Docker, LLM)
### Token
Ein **Token** ist wie ein **geheimer Schlüssel**.
- Wer den Token hat, kann den Bot steuern.
- Token darf nie öffentlich sein.

### Webhook
Ein **Webhook** ist eine Adresse im Internet.
- Telegram/WhatsApp schickt dort Nachrichten hin.

### Docker
Docker ist eine „Box“, in der eine App läuft.
- Vorteil: es läuft überall gleich.

### LLM
LLM = „Sprachmodell“.
- Es hilft, Text zu verstehen und sauber zusammenzufassen.

---

## 6) Tech‑Stack (einfach erklärt)
Bausteine:
- **Channel** (Telegram/WhatsApp/Website)
- **OpenClaw** (Orchestrierung)
- **LLM Provider** (z. B. OpenAI)
- **Storage** (Google Sheets/CRM)
- **Monitoring** (Logs, Healthchecks)

---

## 7) Infrastruktur: Managed vs Eigenbetrieb
### Managed Hosting (am einfachsten)
AI Kitz macht:
- Setup
- Hosting
- Monitoring

Du machst:
- Kanal entscheiden
- Fragen bestätigen

### Eigenbetrieb
Du machst:
- Server/Docker
- Keys

AI Kitz kann trotzdem helfen.

---

## 8) Welche LLMs/Modelle sind am besten?
Für Leads brauchst du:
- **Struktur** (Felder richtig)
- **Stabilität**

Empfehlung:
- „Fast“ Modell für Standardfälle
- „Strong“ Modell für schwierige Fälle

Beispiel (OpenAI):
- strong: `gpt-4.1`
- fast: `gpt-4.1-mini`

---

## 9) Workflow (wie der Bot arbeitet) – komplett
1. Nachricht kommt rein.
2. Bot begrüßt.
3. Bot fragt Pflichtfelder.
4. Bot validiert.
5. Bot schreibt in Google Sheet.
6. Bot bestätigt.
7. Optional: Follow‑up.

---

## 10) Variante A: Managed Hosting (die einfachste Installation)
Wenn du Managed nutzt, ist „Installation“ eigentlich nur:

### Schritt 1: Sag uns deinen Kanal
- Telegram?
- WhatsApp?
- Website?

### Schritt 2: Sag uns deine 5 Fragen
Beispiel:
1. Name/Firma
2. E‑Mail
3. Branche
4. Ziel
5. Zeitrahmen

### Schritt 3: Sag uns wohin die Leads sollen
- Google Sheet Link
- oder CRM

### Schritt 4: Test
Du schickst eine Test‑Nachricht.
Wir prüfen, ob sie in der Tabelle landet.

---

## 11) Variante B: Eigenbetrieb mit Docker (Schritt für Schritt)

### 11.1 Du brauchst
- Mac / Windows / Linux
- Internet
- Docker installiert

#### Docker installieren
- Mac/Windows: Docker Desktop installieren
- Linux: Docker Engine installieren

### 11.2 Projektordner erstellen

```bash
mkdir clawbots-leadbot
cd clawbots-leadbot
```

### 11.3 Dateien anlegen
Du legst diese Dateien an:
- `.env` (geheim)
- `.env.example` (öffentlich)
- `docker-compose.yml`

---

### 11.4 `.env.example` (Beispiel)
```bash
TELEGRAM_BOT_TOKEN=DEIN_TELEGRAM_TOKEN_HIER
LLM_PROVIDER=openai
OPENAI_API_KEY=DEIN_OPENAI_KEY_HIER
OPENAI_MODEL=gpt-4.1
OPENAI_MODEL_FAST=gpt-4.1-mini
LEADS_TARGET=google_sheets
GOOGLE_SHEET_ID=DEINE_SHEET_ID
GOOGLE_SERVICE_ACCOUNT_JSON_BASE64=BASE64_JSON_HIER
APP_ENV=production
TIMEZONE=Europe/Vienna
```

### 11.5 `.env` erstellen
Kopiere `.env.example` → `.env` und fülle echte Werte ein.

---

### 11.6 `docker-compose.yml` (Beispiel)
```yaml
services:
  leadbot:
    image: ghcr.io/DEIN_ORG/leadbot:latest
    env_file:
      - .env
    restart: unless-stopped
    ports:
      - "8080:8080"
    volumes:
      - ./data:/app/data
      - ./logs:/app/logs
```

### 11.7 Starten
```bash
docker compose up -d
```

### 11.8 Logs anschauen
```bash
docker compose logs -f
```

---

## 12) Google Sheets Setup (so, dass es wirklich funktioniert)
### 12.1 Sheet erstellen
1. Öffne Google Sheets
2. Neues Sheet
3. Name: `Leads`

### 12.2 Spalten (Copy/Paste)
Erste Zeile (Header):

```txt
created_at	source	name	company	email	phone	industry	goal	timeframe	budget_range	message	tools	status	summary
```

### 12.3 Sheet ID finden
In der URL sieht es so aus:

`https://docs.google.com/spreadsheets/d/SHEET_ID_HIER/edit#gid=0`

Die **SHEET_ID** ist der lange Teil zwischen `/d/` und `/edit`.

### 12.4 Service Account (Kurzfassung)
Du brauchst ein Google Cloud Service Account JSON.

**Wichtig:** Danach musst du das Sheet mit der Service‑Account‑E‑Mail teilen.

### 12.5 Sheet teilen
1. Klicke „Teilen“ im Sheet
2. Füge die Service‑Account‑E‑Mail ein (endet oft mit `...iam.gserviceaccount.com`)
3. Rechte: „Bearbeiter“

### 12.6 JSON → Base64
#### Mac/Linux:
```bash
base64 -w 0 service_account.json
```

#### Windows (PowerShell):
```powershell
[Convert]::ToBase64String([IO.File]::ReadAllBytes("service_account.json"))
```

Dann kopierst du das Ergebnis in:
`GOOGLE_SERVICE_ACCOUNT_JSON_BASE64=...`

---

## 13) Telegram Setup (BotFather) – Schritt für Schritt
### 13.1 Bot erstellen
1. Öffne Telegram
2. Suche nach **BotFather**
3. Schreibe `/newbot`
4. Gib einen Namen ein (z. B. „AIKitz LeadBot“)
5. Gib einen Username ein (muss auf `bot` enden), z. B. `aikitz_leadbot`

### 13.2 Token kopieren
BotFather gibt dir einen Token wie:

`123456789:AAAbbbCCCdddEEEfff`

Das ist dein:
`TELEGRAM_BOT_TOKEN`

### 13.3 Test
1. Öffne deinen neuen Bot
2. Schreibe „Hallo“
3. Bot sollte antworten

---

## 14) WhatsApp Setup (Überblick)
WhatsApp braucht meistens einen Provider (z. B. Twilio/360dialog).

Du brauchst:
- WhatsApp Business API Zugang
- Webhook URL
- Verify Token

AI Kitz richtet das üblicherweise im Managed‑Setup ein.

---

## 15) Website Setup (Überblick)
Du brauchst:
- Ein Kontaktformular oder Chat‑Widget
- Eine Stelle, wo die Nachricht an OpenClaw geschickt wird

Typisch:
- kleines JS Widget → sendet an Backend

---

## 16) Bedienung (Daily Ops) – wie du Leads abbeitest
### Jeden Tag
1. Öffne Google Sheet `Leads`
2. Filter auf `status = NEW`
3. Rufe an oder schreibe zurück
4. Setze Status auf `CONTACTED`

### Wenn verkauft
- Status `WON`

### Wenn nicht
- Status `LOST`

---

## 17) Beispiele für Fragen (Copy/Paste)
Hier sind 2 fertige Frage‑Sets.

### Set A (sehr kurz, 5 Fragen)
1. „Wie heißt du oder wie heißt deine Firma?“
2. „Wie können wir dich erreichen? (E‑Mail oder Telefon)“
3. „Welche Branche?“
4. „Was ist dein Ziel? (z. B. mehr Termine, weniger Support, mehr Ordnung)“
5. „Wann willst du starten? (Sofort / 1–2 Monate / 3 Monate / Orientierung)“

### Set B (qualifizierter, 7 Fragen)
+ „Welche Tools nutzt ihr?“
+ „Budget‑Range?“

---

## 18) Regeln & Guardrails (damit der Bot nicht „blöd“ wird)
Beispiele:
- Wenn keine E‑Mail/Telefon → nochmal fragen.
- Wenn User sensible Daten sendet → warnen.
- Wenn unklar → an Mensch.

---

## 19) Monitoring & Logs (damit du sofort Fehler siehst)
### 19.1 Schnellcheck
- Läuft Container?
- Kommen neue Logs?

### 19.2 Befehle
```bash
docker compose ps
docker compose logs -f
```

---

## 20) Troubleshooting (wenn etwas nicht geht)
### Bot antwortet nicht
- Telegram Token falsch?
- Docker läuft nicht?

### Leads werden nicht gespeichert
- Sheet ID falsch?
- Sheet nicht geteilt?
- Base64 falsch?

### Popup: „permission denied“
- Rechte/Firewall checken

---

## 21) Checklisten: Start / Go‑Live / Wartung
### Start
- [ ] Kanal OK
- [ ] Google Sheet OK
- [ ] `.env` ausgefüllt

### Go‑Live
- [ ] Test‑Lead
- [ ] Lead in Tabelle
- [ ] Status‑Flow klar

### Wartung (monatlich)
- [ ] Updates
- [ ] Backup
- [ ] Kosten checken

---

## Support
Wenn du willst, dass AI Kitz es für dich fertig macht, schick uns:
- Kanal (Telegram/WhatsApp/Website)
- Google Sheet Link
- deine 5–7 Fragen
