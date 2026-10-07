# Notizen – UKT Wartungsprotokoll

Laufende Arbeitsnotizen über Geräte und Sessions hinweg: offene Punkte und Verlauf.

## Offen / nächste Schritte
- Deploy-Weg dokumentieren/vereinfachen: `gh-pages` wird offenbar manuell auf den Stand von `main` gebracht;
  klären, ob Pages künftig direkt aus `main` (oder per Action) laufen soll.
- Prüfen, ob die Filialliste (`filialen.js`, Kundendaten aus interner Excel) in einem öffentlichen Repo liegen darf.
- Generator für `filialen.js` (aus `Wartungen_Lidl_1.xlsx`) fehlt im Repo – Aktualisierung derzeit nicht nachvollziehbar.
- README veraltet: „Filial-Stammdaten“ steht noch unter „Nächste Ausbaustufen“, ist aber umgesetzt;
  `cd ukt` passt nicht zum Ordnernamen `Ukt`.
- Aus README (optional): Fotos ins PDF; Mailversand + Archiv über kleines Backend.

## Verlauf

### 2026-10-07
Repo nach C:\Users\holub\code geklont, CLAUDE.md und diese Datei angelegt.
Stand: `ce0bd64` – Eigene Filial-Vorschlagsliste statt Browser-datalist (main = gh-pages).
