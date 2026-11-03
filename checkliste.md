
Bitte erfülle alle Punkte auf dieser Liste, **bevor** du das Projekt einreichst.
Solltest du weitere Extras eingebaut haben, erwähne das kurz, damit sich die Mentoren bei Bedarf auch diese Änderungen anschauen können.

## Repository

### Vorhandene Dateien

- [x] Das Repository enthält einen Feature-branch `setup-blog`, welcher die Änderungen enthält, die notwendig sind, um das Projekt zu personalisieren und abschließend zu konfigurieren.
- [x] Das Repository enthält mehrere Commits, die zum Konfigurieren des Projektes erstellt wurden.
  - [ ] Der Feature Branch soll über einen Pull-Request in den Hauptbranch des Repositories gemerged werden, sobald das Projekt freigegeben ist.
- [x] Eine Datei namens `README.md` ist vorhanden und entsprechend der Kriterien unten **erweitert** worden.
- [ ] Es befinden sich keine weiteren Dateien im Repository, ohne dass diese explizit in der README.md benannt und beschrieben werden.

### Konfigurationsschritte

Im folgenden Abschnitt werden kurz die notwendigen Änderungen beschrieben, die zum Personalisieren und Einrichten deines Lerntagebuch-Projektes notwendig sind und von uns geprüft werden.

#### `docusaurus.config.ts`

- [x] Der `title` des Config Objektes wurde angepasst und spiegelt wieder, dass es sich um dein Lerntagebuch/Portfolio Projekt handelt.
- [x] Die `tagline` wurde angepasst, sodass dort ein Subtitel vorhanden ist, der kurz den Inhalt der Seite beschreibt, z.B.: “Maxime Musterperson - DevSecOps Enthusiast with a passion for details and efficiency”
- [x] `url` Standardwert soll so angepasst sein, dass der Platzhalter mit **deinem GitHub Usernamen** übereinstimmt.
- [x] Füge der `example.env` Datei einen Wert für `GIT_REPOSITORY_URL` hinzu, indem die
GitHub Repository URL als Wert übergeben werden kann.
  - [x] Erstelle eine TypeScript Variable, die den Wert der Env-Variable ausliest, oder einen Standardwert festlegt. Orientiere dich dazu am existierenden Code für die `blogEnabled` Variable.
- [x] Die `editUrl` sollte so angepasst werden, dass sie den Wert der `GIT_REPOSITORY_URL` enthält.
- [x] Innerhalb des `blog` Objektes soll die Konfiguration dahingehend angepasst werden, dass auch dort die `editUrl` ihren Wert aus der Umgebungsvariable mit der Repository URL bezieht.
- [x] Im `navbar` Objekt der `themeConfig` Sektion der Konfiguration sollten folgende Eigenschaften verändert werden:
  - [x] `title`: Der Angezeigte Titel im Header der Website
  - [x] (optional) `logo`: Ersetze das Bild mit einem eigenen Logo, falls du eins besitzt. Passe den alt Text ggf. auch an.
  - [x] innerhalb der Navbar Items: Stelle sicher, dass die `href` des GitHub Repositories die korrekte URL verwendet
  - [x] Passe den `footer` folgendermaßen an:
    - [x] Erweitere die Docs Spalte und füge einen Link zur Projektseite hinzu (`/docs/projects/overview`)
    - [x] Community Spalte aus dem footer entfernen
    - [x] `More` Spalte:
      - [x] Ersetze den GitHub Link mit einem Link zu deinem Repository wie an den anderen Stellen.
      - [x] Füge einen Link zum Template-Repository hinzu, der das Label “Template” enthält
  - [x] `copyright`:
    - [x] Passe die Copyright Message so an, dass sie auf dich zugeschnitten ist.
    - [x] Erweitere die Copyright Message um dieses Snippet: “extended from the developer-akademie-starter”

#### README.md

- [x] Verändere die Deployment Sektion in der `README` so, dass dort in 1-2 Sätzen beschrieben wird, dass die Website mit Hilfe eines vorbereiteten GitHub Action Workflows automatisch nach GitHub Pages deployed wird, sobald ein Commit auf den Hauptbranch gepusht wird.
  - [x] Du musst dabei nicht erklären, wie das im Detail funktioniert. Zum jetzigen Zeitpunkt ist es ausreichend, diese Änderung vorzunehmen und die vorhandene Deployment Dokumentation mit der oberen Beschreibung zu ersetzen.
  - [x] Stelle auch sicher, dass andere Stellen angepasst wurden, die entweder zur Deployment Sektion verweisen, oder textuell darauf referenzieren.
- [x] Entferne die Contributing Sektion aus der `README`.

#### GitHub Projekt Einstellungen

Um dein Projekt am Ende auch wirklich über GitHub Pages bereitstellen zu können, musst du das auch in deinen Projekteinstellungen des GitHub Repositories konfigurieren.
Befolge dazu die folgenden Schritte:

- [x] Gehe in die **Einstellungen** des Projektes.
- [x] Gehe innerhalb der Einstellungen zu den **Pages** Einstellungen:
  - [x] Ändere die existierende Konfiguration unterhalb des Bereichs Build & Deploy so ab, dass die Quelle **GitHub Actions** ist.


#### `docs/projects/docusaurus-learning-journal.md`

- [x] Lege im Ordner **docs/projects** eine Markdown Datei mit dem Namen `docusaurus-learning-journal.md` an.
  - [x] Wenn du **mehr als eine Datei** für dieses Projekt hinterlegen willst, solltest du einen Ordner für das Projekt anlegen, indem alle Dateien ablegt werden.
  - Der Ordner sollte entsprechend auch als `docusaurus-learning-journal` benannt sein.
- [x] Fülle diese Datei mit README artigen Inhalten, also beschreibe wie du die Konfiguration des Template Projektes vorgenommen hast und welche Schritte du dabei befolgen musstest.
  - [x] Du kannst dafür die vorhandene Vorlage in `example-project.md` anschauen und dich daran orientieren.

## Dokumentation

Die Dokumentation des Codes, sowie des Projektes soll im Repository in Form einer `README` Datei stattfinden.
Die Dokumentationssprache für alle Projekte (und zugehörige Unterlagen) ist Englisch.
Die Anforderungen zur Projektdokumentation sind unter 1. aufgelistet.
Beachte dabei unbedingt, dass alle für das Projekt notwendigen Änderungen auf einem eigenen Feature-Branch (`setup-blog`) in deinem Repository erledigt werden sollen.

## Hinweise

### Allgemeine Hinweise

- [ ] Zusätzlich zu einem Pull Request in deinem GitHub Repository solltest du ein kurzes Video (maximal 5min.) aufnehmen und bereitstellen, indem du kurz deine Abgabe zeigst und vorstellst was du getan hast - dabei musst du nicht alle Details erwähnen, jedoch solltest du auf alle relevanten Schritte kurz eingehen und diese zeigen.
- [ ] Bei Fragen melde dich gerne über das Ticketsystem.
  - [ ] Bitte mache ein Frage-Ticket im entsprechenden Channel auf, um Fragen zu stellen.
  - [ ] Wenn du Dein Projekt einreichst, dann sollten keine Unklarheiten oder Ähnliches mehr offen sein. Bei Fragen oder Unklarheiten deinerseits behalten wir uns vor eine Abgabe direkt abzulehnen.
- [ ] Wenn du in deinem Pull Request ein rotes Kreuz bei den automatischen Checks innerhalb des Pull-Requests sehen kannst, erfüllt dein Projekt mindestens eine der von uns gestellten Anforderungen noch nicht.
  - [ ] Falls du hier nicht weiterkommen solltest, mach bitte entsprechend ein Frage-Ticket auf und jemand aus dem Mentoren-Team wird sich so schnell wie möglich darum kümmern, dir zu helfen.

### Sicherheitshinweise

- [ ] Speichere keine SSH-Keys im Workspace deines Git-Repositories.
- [ ] Speichere keine Passwörter, Tokens, oder Benutzernamen in deinem Code. Verwende hierfür stattdessen Environment-Variablen.
- [ ] Speichere keine IP-Adressen, oder sonstigen sensiblen Informationen in einem Git Repository.
- [ ] Lade auf **keinen Fall** deine `.env` Datei ins Repository hoch.
  - [ ] Stelle sicher, dass du nicht ausversehen geheime Informationen in der `example.env` Datei gespeichert und im Repository hinzugefügt hast.

### Testing

Bevor Du dein Projekt einreichst, solltest du die folgenden Dinge sicherstellen und getestet haben:
- [x] Die Anwendung kann lokal und in der CI-Pipeline gebaut werden.
  - [x] In der `package.json` des Projektes wirst du ein Skript finden, welches dir hierbei helfen kann einen Build-Prozess lokal auszulösen.
