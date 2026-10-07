# CLAUDE.md – UKT Wartungsprotokoll

## Zweck
Mobile PWA für Servicetechniker der Kammerlander Umwelt- und Klimatechnik GmbH: Wartungsprotokoll für
Klimaanlagen (Lidl Markt/Lager) am Handy ausfüllen, mit Finger unterschreiben, als PDF im Browser
erzeugen und über das Teilen-Menü verschicken. Prototyp, digitalisiert das Papierformular 1:1.

## Stack
- Reines HTML/CSS/JavaScript, kein Build-Schritt, kein `package.json`, keine npm-Abhängigkeiten
- jsPDF 2.5.1 lokal eingebunden (`vendor/jspdf.umd.min.js`)
- PWA: Web-Manifest + Service Worker (offline), `localStorage` für Entwürfe/Techniker-Stammdaten

## Struktur
- `index.html` – die komplette App (Formular, Logik, PDF-Erzeugung, Firmendaten in `FIRMA`)
- `filialen.js` – Filialliste (`FILIALEN`: Nr, Adresse, FM-Region, Info), laut Kopfzeile aus
  `Wartungen_Lidl_1.xlsx` generiert; das Generator-Skript und die Excel-Datei liegen nicht im Repo
- `sw.js` – Service Worker, Cache-Name `ukt-protokoll-vN`, Network-first mit Cache-Fallback
- `manifest.webmanifest`, `icon.svg`, `icon-192.png`, `icon-512.png` – PWA-Metadaten/Icons
- `README.md` – Funktionsbeschreibung; `docs/POZNAMKY.md` – laufende Notizen

## Befehle
- Lokal starten: im Repo-Ordner `python3 -m http.server 8000`, dann http://localhost:8000
  (am Handy über die LAN-IP; Service Worker und Teilen brauchen sonst HTTPS bzw. localhost)
- Tests: keine vorhanden. Bauen: nicht nötig.

## Deployment
- GitHub Pages (legacy) aus Branch `gh-pages` → https://dendak.github.io/Ukt/
- Kein Workflow, kein Deploy-Skript, kein gh-pages-Paket im Repo. `gh-pages` zeigt auf denselben
  Commit wie `main` (Stand ce0bd64) – wird offenbar von Hand nachgezogen, z. B. `git push origin main:gh-pages`.
- Ein Push auf `main` allein deployt nichts; erst ein Push auf `gh-pages` geht live.

## Vorsicht
- Push auf `gh-pages` = sofort live für alle Techniker. Die installierte PWA holt Updates network-first.
- Bei Änderungen an Dateien der App-Shell den Cache-Namen in `sw.js` hochzählen und neue Dateien in `ASSETS` eintragen.
- Repo ist öffentlich: `filialen.js` enthält Kundendaten (Lidl-Filialen mit Adressen) aus einer internen
  Excel-Liste, `index.html` Firmendaten der UKT. Keine weiteren internen Daten, Personennamen,
  Zertifikatsnummern oder Schlüssel einchecken.
- Protokolle enthalten personenbezogene Daten (Techniker, Auftraggebervertreter, Unterschriften); sie
  bleiben im `localStorage` des Geräts – nicht an Server senden ohne Absprache.
- Keine API-Keys im Frontend (alles ist öffentlich auslesbar). Derzeit gibt es keine.

## Arbeit über mehrere Geräte
- GitHub (Dendak/Ukt) ist die Quelle der Wahrheit. Repo lokal unter `C:\Users\holub\code\Ukt`, nie in OneDrive.
- Session-Start: `git pull`, dann diese Datei und [docs/POZNAMKY.md](docs/POZNAMKY.md) lesen.
- Session-Ende: `docs/POZNAMKY.md` aktualisieren (Offen + Verlauf), committen, pushen.
- Größere/riskante Änderungen über Branch + PR. Da nur `gh-pages` live geht, ist `main` der sichere
  Arbeitsstand; `gh-pages` erst nach Prüfung auf `main` nachziehen.
