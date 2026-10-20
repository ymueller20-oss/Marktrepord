# Marktlabor – Hinweise für Claude Code

Marketing-Lernspiel auf Deutsch: Labore, Entscheidungsspiele und Wirtschaftssimulationen mit KI-Konkurrenz, Glossar, Tutorials und 16-Bit-Pixel-Szenen. Alle Texte in der App sind Deutsch.

## Aufbau
- **Eine Datei:** `index.html` enthält CSS, Markup und das komplette Script (kein Build, keine Abhängigkeiten außer Google Fonts).
- **Router:** `go(view)` setzt `current` und rendert neu. Jede Ansicht hat eine `view…()`-Funktion, die `#view` per `innerHTML` füllt, danach bindet eine `…Bind()`-Funktion die Events.
- **Spielerprofil:** Objekt `P` (XP, Badges, Bestwerte, Lektionen, Einstellungen `P.fx`). `save()` speichert es.
- **Spielstände:** Autosave über einen MutationObserver auf `#view` (`svSchedule` → `svWriteLocal` → `svWriteCloud`). Lokal in `localStorage`, in der Cloud über `window.claude.use('db')` unter `data/users/{id}/save_{modul}`.
- **KI:** `window.claude.use('sample')` (nur im claude.ai-Artifact verfügbar). Außerhalb davon zeigt die App „KI offline“ und nutzt Fallbacks.
- **Glossar:** Array der Begriffe (`{k,t,a,f,de,c,g,al,d,ex,fx,r}`), automatische Verlinkung per `linkify()` (case-sensitive Regex `GRE`).
- **Pixel-Engine:** `PXS` (Szenen je Modul, `draw(c,t)` auf 256×72-Canvas), `PXMAP` (Modul → Szene), `pxMount`/`pxLoop` (~12 fps, nur sichtbare Canvases).
- **Effekte:** `FX` (Münzen, Flash, Shake, Banner), `SFX` (WebAudio), `cntRun()` erkennt geänderte KPIs (`.kpi .k`/`.kpi .v`) und `.verdict`-Elemente und löst Feedback aus. Stufen: `P.fx.level` = full | calm | off.
- **Wichtig:** Schrift und Zahlen nie in Pixel-Fonts. Pixel-Look nur für Bilder, Rahmen und Effekte.

## Module (Auswahl)
Budget-Simulator, A/B-Test-Labor, Churn-Radar, KI-Arena, Quiz, Mentor, Funnel-Doktor, Attributions-Detektiv, KI-Verhandlung, Marktkampf, Thronfolge, Preis, Krise, Meta-Ads-Simulator (CBO/ABO, Retargeting-Gruppe), Social-Media-Simulator, Markenimperium (Tycoon), Agentur-Tycoon, Produktlebenszyklus (Bass-Modell), Akademie mit Lektionen, Kompetenz-Kompass und Meisterprüfung.

## Testen
- Syntax: Script aus `index.html` extrahieren und `node --check` laufen lassen.
- Browser: Playwright, Seite per `file://` öffnen; Spiele lassen sich über `go('modul')` und die globalen Zustände (z. B. `ME`, `TY`, `AG`) skripten.

## Veröffentlicht als
claude.ai-Artifact mit den Capabilities `sample`, `db`, `user`, `downloads`.
