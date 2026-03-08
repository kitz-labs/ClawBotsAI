# OpenClaw Managed LeadBot (AI Kitz) – Dokumentation

Quelle/Produktseite: https://www.aikitz.at/openclaw-managed-leadbot/

## 1) Kurzbeschreibung
Der **OpenClaw Managed LeadBot** ist ein (managed) Lead‑Erfassungs- und Qualifizierungs‑Bot für B2B/B2C‑Anfragen. Er nimmt Leads über definierte Kanäle entgegen (z. B. Website‑Formular/Chat, WhatsApp/Telegram), stellt **strukturierte Qualifizierungsfragen**, prüft Mindestkriterien und übergibt die Anfrage **sauber in ein Zielsystem** (z. B. Google Sheet/CRM/Inbox) – inkl. Kontext und Zusammenfassung.

**Ziel:** weniger manuelles Nachfragen, schnellere Reaktionszeiten, höhere Abschlussquote.

---

## 2) Nutzen (Business Value)
- **Sofortreaktion (24/7)** auf neue Anfragen → weniger Lead‑Verlust.
- **Vorqualifizierung** (Budget, Standort, Anliegen, Dringlichkeit, Kontakt) → Team arbeitet nur „gute“ Leads ab.
- **Strukturierte Übergabe** statt Freitext‑Chaos → schnellere Bearbeitung, bessere Datenqualität.
- **Einheitlicher Prozess** über mehrere Kanäle (Website/Chat/Messenger).
- **Messbarkeit** durch klare Felder, Status & Zeitstempel.

Optional/Erweiterungen:
- **Follow‑up Sequenzen** (wenn der Lead unvollständig bleibt oder nicht antwortet).
- **Routing** (z. B. nach Region/Produkt/Team).
- **Lead‑Scoring** (Regeln + LLM‑Assist).

---

## 3) Welche Daten müssen zur Informationsverarbeitung vorhanden sein?
Damit der Bot zuverlässig qualifizieren und übergeben kann, brauchen wir (je nach Use‑Case) folgende Daten.

### 3.1 Pflichtdaten (Minimal)
- **Kontaktkanal** (E‑Mail oder Telefonnummer/Chat‑Handle)
- **Name** (oder Firmenname)
- **Anliegen / Problemstatement** (1–3 Sätze oder Auswahl)
- **Einwilligung/Datenschutzhinweis** (je nach Kanal/Website rechtlich relevant)

### 3.2 Sinnvolle Qualifizierungsdaten (empfohlen)
- **Firma/Branche**
- **Standort/Region** (wichtig für lokale Services)
- **Budget‑Range** (oder Projektgröße)
- **Zeitrahmen** (sofort/1–2 Monate/3 Monate/Orientierung)
- **Entscheider?** (ja/nein)
- **Ist‑Tooling** (z. B. Microsoft 365, Google, CRM, Kalender)

### 3.3 Daten für Routing/Automatisierung
- **Produktinteresse** (z. B. LeadBot, FAQBot, Setup, Managed Hosting)
- **Team‑Zuordnung** (Sales/Support/Operations)
- **Priorität/Dringlichkeit**

### 3.4 Wissensbasis / Regeln (für saubere Antworten)
- FAQ/Policies (z. B. Öffnungszeiten, SLA, Preise „ab“, No‑Go‑Aussagen)
- Qualifizierungsregeln (z. B. „wenn Budget < X → Beratung anbieten statt Checkout“)
- Übergabeformat (welche Felder in welches System)

---

## 4) Tech Stack (Referenz-Architektur)
> Die genaue Umsetzung hängt von Kanal/Hosting/Policy ab. Unten ist die bewährte, robuste Standard‑Architektur.

### 4.1 Komponenten
- **OpenClaw Runtime** (Orchestrierung, Skills, Guardrails, Tool‑Calls)
- **Bot Channel Adapter**
  - Telegram Bot API / WhatsApp Provider (z. B. Twilio/360dialog je nach Setup) / Website Widget
- **LLM Layer**
  - LLM API (OpenAI / Anthropic / etc.) + Modellwahl nach Aufgabe
- **State/Storage**
  - Konversation‑State (Redis/SQLite/Postgres je nach Umfang)
  - Lead‑Store (Google Sheets / Airtable / CRM)
- **Observability**
  - Logging + Error Tracking (z. B. Sentry) + Metriken

### 4.2 Integrationen (typisch)
- **Google Sheets** (Lead‑Tabelle, Status, Owner)
- **E‑Mail** (Benachrichtigung, Zusammenfassung)
- **Kalender** (Terminbuchung via Link oder API)
- **CRM** (HubSpot/Pipedrive/…)

---

## 5) Infrastruktur (Managed Hosting – typische Ausprägung)
- **Server/Compute:** kleiner VPS oder Container‑Host (Docker)
- **Reverse Proxy:** Nginx/Caddy
- **Secrets:** .env / Secret Manager (niemals im Repo)
- **Backups:** Konfig + DB + Logs (Rotation)
- **Uptime:** optional Healthchecks/Monitoring

**Betriebsmodell:**
- **Eigenbetrieb:** Kunde betreibt API Keys/Infra selbst, AI Kitz liefert Setup/Workflows.
- **Managed:** AI Kitz betreibt Hosting + API + Updates + Monitoring (empfohlen für schnellen Start).

---

## 6) Welche LLMs/Modelle sind am besten?
Für einen LeadBot ist **Zuverlässigkeit** wichtiger als „kreativ“. Empfehlung nach Aufgaben:

### 6.1 Klassifizierung + Routing + knappe Zusammenfassungen
- **Stark:** GPT‑4.1 / GPT‑4.1 mini (Preis/Speed) oder vergleichbare „reliable“ Modelle
- **Warum:** gute Strukturtreue, geringe Halluzinationsrate bei klaren Prompts

### 6.2 Freitext‑Verstehen + saubere Nachfragen
- **Stark:** GPT‑4.1 (oder Top‑Tier Modell) für schwierige/mehrdeutige Leads

### 6.3 Kostenoptimiert (High Volume)
- **Mini‑Modelle** für Standardfälle + „Escalation“ auf großes Modell bei Unsicherheit

**Wichtig:**
- Guardrails (Regeln + Validierung) sind wichtiger als Modell‑Switching.
- Für kritische Felder (E‑Mail, Telefonnummer, Budget) immer **Regex/Validierung** + Rückfrage.

---

## 7) Workflow (End‑to‑End)
### 7.1 Lead Intake
1. Lead kommt über Kanal rein (Website/Messenger).
2. Bot bestätigt Eingang + erklärt kurz den Ablauf.

### 7.2 Qualifizierung
3. Bot stellt 3–7 Fragen (konfigurierbar).
4. Validierung (Pflichtfelder, Format, Plausibilität).

### 7.3 Entscheidung/Next Step
5. Bot entscheidet per Regeln:
   - **Termin buchen** (Link/Slot) oder
   - **Angebot/Checkout** (Stripe Link) oder
   - **Weiterleitung an Mensch** (Hot Lead / Sonderfall)

### 7.4 Übergabe
6. Bot schreibt Lead in Zielsystem (Sheet/CRM) inkl.
   - Zeitstempel
   - Kanal
   - Antworten strukturiert
   - Kurz‑Summary
   - Status (NEW/QUALIFIED/NEEDS_INFO/ESCALATED)

### 7.5 Benachrichtigung
7. Optional: Slack/E‑Mail Nachricht ans Team inkl. Link zum Datensatz.

### 7.6 Follow‑ups
8. Wenn keine Antwort: Follow‑up nach X Stunden/Tagen (konfigurierbar).

---

## 8) Installation (typisch, Managed oder Eigenbetrieb)
> Hinweis: Konkrete Schritte hängen vom Kanal ab. Das hier ist ein praxistauglicher Standard.

### 8.1 Voraussetzungen
- Zugriff auf gewünschte Kanäle (Telegram Bot Token / WhatsApp Provider / Website)
- Zielsystem (Google Sheet/CRM) + API Zugriff
- Hosting (Managed oder eigener Server)

### 8.2 Konfiguration
- `.env` / Secrets:
  - Channel Tokens/Keys
  - LLM API Key
  - Zielsystem Credentials
  - Webhook URL / Callback URLs

### 8.3 Deployment
- Docker/Compose oder Service‑Deployment
- Webhooks setzen (je Kanal)
- Healthcheck aktivieren

### 8.4 Smoke Test
- Test‑Lead über jeden Kanal
- Prüfen: Validierung, Übergabe, Benachrichtigung, Logging

---

## 9) Bedienung (Operations)
### 9.1 Daily
- Neue Leads im Sheet/CRM prüfen
- Status setzen (z. B. CONTACTED / WON / LOST)

### 9.2 Anpassungen
- Fragenkatalog/Regeln aktualisieren
- Routing‑Regeln nachschärfen (z. B. neue Regionen/Produkte)

### 9.3 Monitoring
- Fehlerraten (Webhook/Provider)
- LLM‑Kosten (Tokens/Requests)
- Conversion (Lead → Termin)

---

## 10) Sicherheit, Datenschutz, Qualität
- **Minimalprinzip:** nur notwendige Daten abfragen.
- **Transparenz:** Hinweis, dass ein automatisierter Assistent antwortet.
- **PII‑Handling:** sichere Speicherung, Zugriffskontrollen.
- **Auditability:** Logs/Events ohne unnötige PII.
- **Fallback:** wenn unsicher → an Mensch eskalieren.

---

## 11) Troubleshooting (kurz)
- **Leads kommen nicht an:** Webhook/Provider prüfen, Token gültig?
- **Felder fehlen:** Validierungsregeln/Fragenlogik anpassen.
- **Doppelte Leads:** Idempotency Key (z. B. message_id) nutzen.
- **Kosten zu hoch:** Mini‑Modell für Standardfälle + Escalation.

---

## 12) Nächste Schritte (ToDo)
- Fragenkatalog finalisieren (max. 5–7 Fragen)
- Zielsystem festlegen (Sheet vs CRM)
- SLA für Eskalation definieren
- Tracking/Conversion‑Metriken definieren
