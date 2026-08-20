# Roadmap — mail-archiv

## Offen

- [ ] 122 · Paperless OOM-Fix nach RAM-Vorfall (17.08.)
  > Server-OOM-Kaskade am 17.08. durch Paperless OCR ausgelöst (ungültiger
  > PAPERLESS_OCR_MODE + 4 parallele ocrmypdf-Worker + 0% Swap).
  > paperless1/paperless2 sind seitdem gestoppt.
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;↳ 133 · Swap-File auf VPS anlegen (2-4 GB)
  > ***
  > Übergeordnetes Issue: #122 
  > ***
  > VPS hat aktuell 0% Swap bei 3.8 GB RAM - kein Sicherheitsnetz bei Spitzen.
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;↳ 134 · PAPERLESS_OCR_MODE korrigieren (skip → auto)
  > ***
  > Übergeordnetes Issue: #122 
  > ***
  > Aktuell PAPERLESS_OCR_MODE: skip gesetzt - laut Paperless-Warnung ungültig.
  > Auf PAPERLESS_OCR_MODE: auto + PAPERLESS_ARCHIVE_FILE_GENERATION: never
  > umstellen (beide Instanzen).
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;↳ 135 · PAPERLESS_OCR_MAX_WORKERS auf 1 begrenzen
  > ***
  > Übergeordnetes Issue: #122 
  > ***
  > Aktuell 4 parallele ocrmypdf-Worker pro Dokument - Hauptursache der
  > Speicherspitzen. Auf 1 (ggf. 2) reduzieren.
- [ ] 123 · mail-to-pdf Cron
  > Ausführung automatisieren; technischen Block auf eigenständige Seite; Seitenzahl der technischen Seite bei x von n ausnehmen,  sodass optisch Seite x von n-1 auf Seiten x bis n-1 steht
- [ ] 124 · Paperless konfigurieren
- [ ] 125 · Kopia-Verify Skip-Button
- [ ] 126 · Status Mails
- [ ] 127 · NAS-Mirror Git repository
- [ ] 128 · compose-patch.sh deprecated
- [ ] 129 · Design responsiver gestalten
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;↳ 140 · Portal anpassen 
  > ***
  > Übergeordnetes Issue: 129
  > ***
  >
  > ***
  > Übergeordnetes Issue: #129
  > ***
- [ ] 130 · Watchlist service upgraden
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;↳ 131 · Trecking für Streaming hinzufügen
  > ***
  > Übergeordnetes Issue: #130
  > ***
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ 132 · ARD und ZDF einfügen
  > ***
  > Übergeordnetes Issue: #131 
  > ***
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ 137 · Ablauf-Daten berücksichtigen
  > ***
  > Übergeordnetes Issue: #132 
  > ***
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ 136 · Amazon Prime
  > ***
  > Übergeordnetes Issue: #131 
  > ***
- [ ] 142 · nginx crasht komplett, wenn Paperless-Upstream nicht auflösbar istNach dem geplanten Stopp von paperless1/paperless2 (im Rahmen von #122, OOM-Vorfall) startet nginx nicht mehr. Ursache: archiv.conf:48 referenziert paperless1 als statisches upstream. nginx verweigert beim Start komplett, wenn ein Upstream-Host per DNS nicht auflösbar ist — Folge: kompletter Ausfall aller Services hinter nginx (Portal, Bichon, Buchung, Watchlist etc.), nicht nur Paperless.
Fix: Statisches upstream durch DNS-Resolver + Variable ersetzen (resolver 127.0.0.11 valid=10s; + set $paperless_upstream ...; proxy_pass $paperless_upstream;), damit nginx auch bei gestopptem Backend startet und nur die betroffene Route mit 502 antwortet statt den ganzen Stack lahmzulegen.
Blockiert: Ist aktuell Voraussetzung dafür, dass der Server überhaupt wieder erreichbar ist — sollte vor #122-Deployment behoben werden, damit sowas beim nächsten Container-Neustart nicht wieder passiert.
- [ ] 144 · Versionsupdates
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;↳ 145 · Bichon -> 2.0.2
  > ***
  > Übergeordnetes Issue: #144
  > ***
- [ ] &nbsp;&nbsp;&nbsp;&nbsp;↳ 146 · nginx -> 1.31.4
  > ***
  > Übergeordnetes Issue: #144
  > ***

## Erledigt (letzte 20)

- ✅ 63 · Github Actions umstellen auf issues und Generierung von Roadmap.md
- ✅ 70 · aktuelles catch-all einbinden
- ✅ 72 · aktuelles catch-all einbinden
- ✅ 31 · Public Mirror-Repo für ROADMAP.md (Action pusht bei Änderung) ([3762c3f](https://github.com/development-de/langzeitarchiv/commit/3762c3f426661cd7ed63dd25e76e40762d773317))
  - ✅ 31.1 · Leeres public Repo anlegen (neutraler Name) ([dd3a341](https://github.com/development-de/langzeitarchiv/commit/dd3a341e6fe40394af9ea962528d160e2dd10eda))
  - ✅ 31.2 · PAT mit Repo-Schreibrecht als GitHub Secret hinterlegen ([263ca02](https://github.com/development-de/langzeitarchiv/commit/263ca0254b3c45665643811d65b28b42656a261a))
  - ✅ 31.3 · Action: bei ROADMAP.md-Änderung in Mirror pushen ([be6eeea](https://github.com/development-de/langzeitarchiv/commit/be6eeeafa62dc220d30fe2987b0f51590ad98729))
- ✅ 27 · ROADMAP.md auslagern + Auto-Umsortierung offen/erledigt ([1e40c22](https://github.com/development-de/langzeitarchiv/commit/1e40c22a871c29c958c0e06b339369584855c436))
- ✅ 26 · STACK-MANIFEST: [x] durch ✅ ersetzen + todo-check.yml anpassen ([95af90c](https://github.com/development-de/langzeitarchiv/commit/95af90c56d037a042d14c538549c183582242759))
- ✅ 25 · Watchlist-DB reparieren
  - ✅ 25.1 · watchlist-api force-recreate nach #24-Deploy
  - ✅ 25.2 · Playlists neu hinzufügen oder aus Backup wiederherstellen
  - ✅ 25.3 · conn.close Fix verifizieren ([f40f0a6](https://github.com/development-de/langzeitarchiv/commit/f40f0a6ade85e4038088ab7d903ef67e00fdf5ce))
  - ✅ 25.4 · Video-Kacheln klickbar verifizieren → #13 final abhaken
- ✅ 24 · deploy.yml: --force-recreate bei Service-Restart
- ✅ 23 · GitHub Action: Todo-Automatisierung ([4da1e7a](https://github.com/development-de/langzeitarchiv/commit/4da1e7af2040dfbb29f557b49b1944cb8e0c1db1))
- ✅ 22 · deploy.yml: paths-ignore für .md-Dateien ([11d6d55](https://github.com/development-de/langzeitarchiv/commit/11d6d555422199cd146b24e966d31fa799d6e333))
- ✅ 21 · deploy.yml: nginx nach frontend-Rebuild neu starten ([a7c1c08](https://github.com/development-de/langzeitarchiv/commit/a7c1c0807c4080873ee6bd89cef9cb9ab2169a91))
- ✅ 14 · Design-CSS deployen (buchung + watchlist) ([479820b](https://github.com/development-de/langzeitarchiv/commit/479820b9e22e17e29d7ce15a4ae5cc906acadb80))
- ✅ 13 · Watchlist UI: Video-Kacheln klickbar + btn-action größer ([62b5140](https://github.com/development-de/langzeitarchiv/commit/62b514045cf676f929d3f20404a7d29d0ea7a347))
