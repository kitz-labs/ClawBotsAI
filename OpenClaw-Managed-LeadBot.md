# OpenClaw Managed LeadBot (AI Kitz) – **Super‑Detail Anleitung**

Produktseite: https://www.aikitz.at/openclaw-managed-leadbot/

> Ziel dieser Datei: **So erklärt**, dass sogar ein Kind (7+) es nachmachen kann – Schritt für Schritt, mit Beispielen.
>
> Wichtig: In dieser Doku stehen **keine echten Passwörter**. Wir verwenden überall Platzhalter wie `DEIN_TOKEN_HIER`.

---

## Inhaltsverzeichnis
1. [Was ist der LeadBot?](#1-was-ist-der-leadbot)
2. [Was bringt er dir (Nutzen)?](#2-was-bringt-er-dir-nutzen)
3. [Welche Daten braucht der Bot? (mit Beispielen)](#3-welche-daten-braucht-der-bot-mit-beispielen)
4. [Wie sieht das Ergebnis aus? (Beispiel-Lead)](#4-wie-sieht-das-ergebnis-aus-beispiel-lead)
5. [Tech‑Stack (einfach erklärt)](#5-techstack-einfach-erklärt)
6. [Infrastruktur (Managed vs Eigenbetrieb)](#6-infrastruktur-managed-vs-eigenbetrieb)
7. [Welche LLMs/Modelle sind am besten?](#7-welche-llmsmodelle-sind-am-besten)
8. [Workflow (wie der Bot arbeitet) – komplett](#8-workflow-wie-der-bot-arbeitet--komplett)
9. [Installation – „Eigenbetrieb“ (Schritt für Schritt)](#9-installation--eigenbetrieb-schritt-für-schritt)
10. [Betrieb/Bedienung (Daily Ops)](#10-betriebbbedienung-daily-ops)
11. [Monitoring, Logs, Fehler](#11-monitoring-logs-fehler)
12. [Sicherheit & Datenschutz (DSGVO‑bewusst)](#12-sicherheit--datenschutz-dsgvobewusst)
13. [Troubleshooting (wenn etwas nicht geht)](#13-troubleshooting-wenn-etwas-nicht-geht)
14. [Checkliste: „Go‑Live in 30 Minuten“](#14-checkliste-go-live-in-30-minuten)

---

## 1) Was ist der LeadBot?
Der **OpenClaw Managed LeadBot** ist ein digitaler Helfer.

Er macht 3 Dinge:
1. **Er beantwortet sofort** neue Anfragen (24/7).
2. **Er stellt ein paar Fragen**, damit die Anfrage „vollständig“ und „sortiert“ wird.
3. **Er speichert** die Anfrage an einem Ort, wo du sie wiederfindest (z. B. Google Sheets oder CRM).

### Beispiel (ganz einfach)
Jemand schreibt auf deiner Website:

> „Hi, ich brauche Hilfe. Was kostet das?“

Der Bot antwortet:
- „Hallo! Kurze Frage: Für welche Branche ist das?“
- „Wie groß ist euer Team?“
- „Wann soll es starten?“

Und danach schreibt er alles in eine Tabelle.

---

## 2) Was bringt er dir (Nutzen)?
### Nutzen 1: Du verlierst weniger Kunden
Viele Menschen schreiben – und wenn niemand schnell antwortet, sind sie weg.

**Der Bot antwortet sofort.**

### Nutzen 2: Du sparst Zeit
Der Bot fragt die typischen Dinge automatisch ab:
- Name
- Kontakt
- Problem
- Budget (oder grob)
- Zeit

Du musst nicht 10× die gleichen Fragen tippen.

### Nutzen 3: Du bekommst bessere Leads
Wenn jemand nur „Hallo“ schreibt, fragt der Bot nach.

Du bekommst dann einen Lead wie:
- „Hotel in Tirol, 24 Zimmer, will WhatsApp‑Anfragen automatisch sortieren, Budget 500–1500, Start in 2 Wochen“

---

## 3) Welche Daten braucht der Bot? (mit Beispielen)
Der Bot kann nur gut arbeiten, wenn er **genug Informationen** hat.

### 3.1 Pflichtdaten (Minimum)
Diese Daten brauchst du **immer**:

- **Kontaktmöglichkeit** (mindestens eins)
  - E‑Mail, z. B. `anna@firma.at`
  - oder Telefonnummer, z. B. `+43 660 1234567`
  - oder Messenger‑User (Telegram/WhatsApp Chat)

- **Name oder Firma**
  - z. B. „Anna Maier“ oder „Hotel Alpenblick“

- **Worum geht’s?**
  - z. b. „Wir wollen Anfragen aus WhatsApp automatisch in eine Liste schreiben.“

### 3.2 Empfohlen (macht Leads wirklich gut)
- **Branche**
  - z. B. „Hotel“, „Handwerk“, „Immobilien“

- **Ziel**
  - z. B. „Mehr Anfragen zu Terminen“ oder „Weniger Support‑Tickets“

- **Zeitrahmen**
  - z. B. „Sofort“, „in 1–2 Monaten“

- **Budget‑Range** (optional, aber hilfreich)
  - z. B. „bis 500 €“, „500–1500 €“, „>1500 €“

- **Tooling** (was ist schon da?)
  - z. B. „Google Workspace“, „Microsoft 365“, „HubSpot“, „Google Kalender“

### 3.3 Daten, wenn du automatisch routen willst (Team/Region)
- Region: „Tirol“, „Wien“, „Deutschland“
- Produktinteresse: „LeadBot“, „FAQBot“, „Setup“, „Managed Hosting“

---

## 4) Wie sieht das Ergebnis aus? (Beispiel-Lead)
So soll ein Lead am Ende aussehen:

```json
{
  "created_at": "2026-03-08T05:00:00+01:00",
  "source": "website",
  "name": "Anna Maier",
  "company": "Hotel Alpenblick",
  "email": "anna@hotel-alpenblick.at",
  "phone": "+43 660 1234567",
  "industry": "Hotel / Tourismus",
  "goal": "Mehr Anfragen zu Terminen",
  "timeframe": "Sofort",
  "budget_range": "500–1500 EUR",
  "message": "Wir bekommen viele WhatsApp-Anfragen. Wir wollen Vorqualifizierung + Terminlink.",
  "tools": "Google Kalender, Gmail",
  "score": "hot",
  "status": "NEW",
  "summary": "Hotel in Tirol möchte WhatsApp-Anfragen vorqualifizieren und Termine automatisiert buchen. Start sofort. Budget 500–1500."
}
```

Das ist extrem praktisch, weil es **sofort übersichtlich** ist.

---

## 5) Tech‑Stack (einfach erklärt)
Stell dir das wie Lego‑Steine vor:

### Baustein A: Chat‑Kanal
Das ist der Ort, wo Menschen schreiben.
- Website
- WhatsApp
- Telegram

### Baustein B: OpenClaw
Das ist der „Chef“, der alles koordiniert.
- Er bekommt die Nachricht
- Er entscheidet, welche Frage als nächstes kommt
- Er ruft Tools auf (z. B. Google Sheets)

### Baustein C: LLM (das „Gehirn“)
Das Modell hilft beim:
- Verstehen von Text
- Zusammenfassen
- Entscheiden „Hot / Warm / Cold“

### Baustein D: Zielsystem (wo Leads landen)
- Google Sheets (einfach)
- CRM (professionell)

---

## 6) Infrastruktur (Managed vs Eigenbetrieb)
### 6.1 Managed Hosting (empfohlen)
**AI Kitz** betreibt:
- Server
- Updates
- Monitoring
- API Keys (wenn vereinbart)

Du bekommst ein fertiges System.

### 6.2 Eigenbetrieb (du betreibst)
Du betreibst selbst:
- Server oder Docker
- API Keys

AI Kitz liefert:
- Setup, Workflow, Regeln, Tests

---

## 7) Welche LLMs/Modelle sind am besten?
Für Lead‑Bots zählt: **stabil + strukturiert + wenig Fehler**.

Empfehlung (einfach):
- **Standardfälle:** ein gutes „Mini“-Modell (schnell & günstiger)
- **Schwierige Fälle:** ein stärkeres Modell (wenn unklar)

### Konkrete Beispiele (Stand heute)
- **OpenAI**: GPT‑4.1 (sehr stabil), GPT‑4.1 mini (schneller)

### Wichtigste Regel
Egal welches Modell: Wir sichern kritische Daten immer extra ab:
- E‑Mail/Telefon → Validierung (z. B. Regex)
- Pflichtfelder → wenn leer, nochmal fragen

---

## 8) Workflow (wie der Bot arbeitet) – komplett
Hier ist der komplette Ablauf in „Menschen‑Sprache“:

1. Jemand schreibt „Hallo“.
2. Bot antwortet freundlich und sagt: „Ich stelle kurz 3–5 Fragen.“
3. Bot fragt:
   - „Wie heißt du / Firma?“
   - „Wie kann ich dich erreichen (E‑Mail/Telefon)?“
   - „Worum geht es genau?“
4. Bot prüft:
   - „Ist das eine echte E‑Mail?“
   - „Fehlt etwas?“
5. Bot schreibt alles in Google Sheets (oder CRM).
6. Bot sagt: „Danke! Wir melden uns.“
7. Optional: Bot sendet dir eine Benachrichtigung.
8. Optional: Wenn der Lead nicht antwortet, folgt ein Follow‑up.

---

## 9) Installation – „Eigenbetrieb“ (Schritt für Schritt)
> Wenn du Managed Hosting nimmst, musst du das NICHT machen.

### 9.1 Du brauchst (wie Einkaufsliste)
- Einen Computer/Server mit Docker
- Internet
- Einen LLM‑API Key (z. B. OpenAI)
- Einen Kanal (z. B. Telegram Bot Token)
- Ein Google Sheet (oder anderes Ziel)

---

### 9.2 Ordnerstruktur (Beispiel)
So sieht ein Projektordner aus:

```txt
clawbots-leadbot/
  docker-compose.yml
  .env              (NICHT in GitHub!)
  .env.example      (darf in GitHub)
  README.md
  data/
  logs/
```

---

### 9.3 Beispiel: `.env.example`
**Wichtig:** Das ist nur ein Beispiel. Keine echten Keys.

```bash
# === Channel ===
TELEGRAM_BOT_TOKEN=DEIN_TELEGRAM_TOKEN_HIER

# === LLM ===
LLM_PROVIDER=openai
OPENAI_API_KEY=DEIN_OPENAI_KEY_HIER
OPENAI_MODEL=gpt-4.1
OPENAI_MODEL_FAST=gpt-4.1-mini

# === Lead Storage ===
LEADS_TARGET=google_sheets
GOOGLE_SHEET_ID=DEIN_SHEET_ID
GOOGLE_SERVICE_ACCOUNT_JSON_BASE64=BASE64_JSON_HIER

# === App Settings ===
APP_ENV=production
TIMEZONE=Europe/Vienna
```

**Warum `.env.example`?**
- Damit jeder sieht, welche Variablen gebraucht werden.

**Warum `.env` nicht in GitHub?**
- Weil darin echte Geheimnisse stehen.

---

### 9.4 Beispiel: `docker-compose.yml`
Das ist ein einfaches Beispiel (kann je Setup anders sein):

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

Wenn du kein fertiges Image hast, kann AI Kitz dir eins bauen.

---

### 9.5 Starten (Kinderleicht‑Modus)
1. Öffne ein Terminal.
2. Gehe in den Ordner.
3. Starte Docker:

```bash
docker compose up -d
```

4. Prüfe Logs:

```bash
docker compose logs -f
```

Wenn du siehst „ready“ oder „listening“, läuft es.

---

### 9.6 Google Sheet vorbereiten (Beispiel)
Erstelle ein Sheet mit Spalten:

```txt
created_at | source | name | company | email | phone | industry | goal | timeframe | budget_range | message | tools | status | summary
```

Beispiel‑Zeile:

```txt
2026-03-08 05:00 | website | Anna Maier | Hotel Alpenblick | anna@... | +43... | Hotel | Mehr Termine | Sofort | 500-1500 | WhatsApp Leads... | Google Kalender | NEW | ...
```

---

## 10) Betrieb/Bedienung (Daily Ops)
### Jeden Tag (2 Minuten)
- Öffne das Sheet/CRM.
- Schau neue Leads an.
- Setze Status:
  - `NEW`
  - `CONTACTED`
  - `WON`
  - `LOST`

### Wenn du etwas ändern willst
- Fragen ändern (z. B. mehr Budget‑Fragen)
- Routing ändern (z. B. Region)

---

## 11) Monitoring, Logs, Fehler
### 11.1 Was du checkst
- Kommen Nachrichten an?
- Werden Leads gespeichert?
- Gibt es Fehler im Log?

### 11.2 Log‑Beispiel
Ein gutes Log sieht so aus:

```txt
[leadbot] inbound message source=telegram chat_id=...
[leadbot] collected fields: name,email,goal
[leadbot] wrote lead to google_sheets row=128
```

---

## 12) Sicherheit & Datenschutz (DSGVO‑bewusst)
- Sammle nur, was du brauchst.
- Speichere Keys als Secrets.
- Keine Passwörter im Repo.
- Wenn ein Lead sensible Daten schreibt → Bot soll sagen: „Bitte nicht senden, wir klären das im Gespräch.“

---

## 13) Troubleshooting (wenn etwas nicht geht)
### Problem: Bot antwortet nicht
- Token falsch?
- Webhook falsch?
- Container läuft?

### Problem: Leads landen nicht im Sheet
- Sheet ID stimmt?
- Rechte stimmen?
- Service Account korrekt?

### Problem: Bot fragt komisch
- Fragenkatalog vereinfachen
- Pflichtfelder klar machen
- Fallback: an Mensch

---

## 14) Checkliste: Go‑Live in 30 Minuten
- [ ] Kanal bereit (Telegram/WhatsApp/Website)
- [ ] `.env` gesetzt (ohne echte Keys im Repo)
- [ ] Google Sheet mit Spalten
- [ ] Bot gestartet (`docker compose up -d`)
- [ ] Test‑Lead geschickt
- [ ] Lead ist im Sheet
- [ ] Benachrichtigung kommt an

---

## Support
Wenn du willst, schreibe AI Kitz:
- Was ist dein Kanal?
- Wohin sollen Leads gespeichert werden?
- Welche 5 Fragen soll der Bot stellen?
