# OpenClaw Managed InventoryBot – Ultra‑Detail Doku

Produktseite: https://www.aikitz.at/openclaw-managed-inventorybot/

> Ziel: Eine sehr klare Anleitung mit Beispielen. Keine echten Secrets in GitHub.

---

## 1) Was ist das?
Der InventoryBot hilft bei Bestand/Bestellungen: Abfragen, Warnungen bei Low Stock und Nachbestell-Workflows.

## 2) Nutzen
- Weniger Out-of-Stock
- Klarer Überblick
- Automatische Warnungen

## 3) Benötigte Daten
### Minimum
- Inventar-Liste (SKU, Bestand)
- Schwellenwerte
- Zielsystem

### Empfohlen
- Lieferanteninfos
- Bestellmengen
- Automatische Bestellvorschläge

## 4) Beispiele
### Beispiel‑Input
```
User: Wie viel SKU-123 ist noch da?
```

### Beispiel‑Output
```
Antwort: 8 Stück. Unter Minimum (10). Vorschlag: 30 nachbestellen.
```

## 5) Workflow (komplett)
1) Bestand abfragen
2) Datensatz suchen
3) Antwort + Empfehlung
4) Low-Stock Warnung
5) Nachbestellung anstoßen

## 6) Datei‑Beispiele
### Google Sheet Spalten (Beispiel)
```txt
sku	product	stock	min_stock	supplier	reorder_qty	status
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

