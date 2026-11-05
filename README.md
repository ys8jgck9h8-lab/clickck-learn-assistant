# Click & Learn AI

Transparente KI-Lernassistenz für den Führerschein Klasse B.

## Enthalten
- Chrome Extension Manifest V3 erkennt sichtbare Fragen, Antwortoptionen und optionale Bilder.
- Node.js/Express-Backend und SQLite mit FTS5-Volltextsuche.
- RAG mit importierten Wissenseinträgen und optionaler Embedding-Suche.
- Multimodale Analyse über ein serverseitig konfiguriertes OpenAI-kompatibles Chat-Completions-Modell.
- JSON-Import, Duplikatprüfung, Validierung und Dashboard-Statistik.
- Die Extension zeigt eine separate Erklärungshilfe; sie wählt oder sendet keine Antworten ab.

## Installation
Voraussetzung: Node.js 20+, npm und Chrome.
1. `npm install`
2. `.env.example` nach `.env` kopieren und optional `OPENAI_API_KEY` eintragen.
3. `npm run db:init`
4. `npm start` (API auf http://localhost:8787)
5. Chrome: `chrome://extensions` → Entwicklermodus → „Entpackte Erweiterung laden“ → Ordner `extension/`.
6. Popup öffnen und Backend-URL prüfen.

Windows: `scripts\\start-windows.bat`. macOS/Linux: `npm install && npm run db:init && npm start`.

## Importformat
```json
{"questions":[{"id":"q-001","text":"Beispielfrage","answers":[{"id":"a","text":"Antwort A"},{"id":"b","text":"Antwort B"}],"correctAnswerIds":["a"],"explanation":"Begründung","topic":"Vorfahrt","legalBasis":"Quellenangabe","image":{"ref":"lokale Bildreferenz","description":"Beschreibung"},"source":{"name":"Eigene Unterlagen","reference":"Kapitel 1","license":"Nutzungsrecht vorhanden"},"verified":false}]}
```
Import: `npm run import -- ./fragen.json`. Nur rechtmäßig verfügbare Daten importieren.

## API
- GET `/api/health`
- GET `/api/stats`
- POST `/api/analyze`: `{question, answers, imageDataUrl?}`
- POST `/api/questions/import`: Array oder `{questions:[]}`

## Datenstatus und Grenzen
Das Repository enthält keinen offiziellen Fragenkatalog und behauptet nicht, 1.600 Fragen importiert zu haben. Dashboard-Zahlen stammen nur aus tatsächlich importierten Datensätzen. Ein Eintrag wird nur als verifiziert markiert, wenn die Importquelle `verified: true` setzt. API-Schlüssel bleiben im Backend. KI-Ergebnisse können falsch sein und sind Lernhilfe, keine amtliche Rechtsauskunft.
