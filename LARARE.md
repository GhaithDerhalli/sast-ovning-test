# Lärarfacit (dela inte med eleverna)

## Förväntade CodeQL-fynd i src/server.js
| Rad (ca) | Sårbarhet | Regel |
|---|---|---|
| /search | SQL-injektion | js/sql-injection |
| /search | Reflekterad XSS | js/reflected-xss |
| /ping | Kommandoinjektion | js/command-line-injection |
| /file | Path traversal | js/path-injection |
| /go | Öppen redirect | js/server-side-unvalidated-url-redirection |
| ADMIN_PASSWORD | Hårdkodade uppgifter | js/hardcoded-credentials (kan utebli: verifiera) |

OBS: listan är ännu inte verifierad mot en riktig CodeQL-körning. Kör övningen i ett eget publikt testrepo före lektionen och uppdatera tabellen.

## Felsökning
- Privat repo: ingen Code scanning utan Advanced Security.
- Elever som klonat med gammal origin: `git remote remove origin`.
- Första körningen kan ta 5 min när många startar samtidigt.

## Alternativ till Default setup
Lägg `.github/workflows/codeql.yml` med `github/codeql-action/init@v3` (languages: javascript-typescript), `autobuild` och `analyze`.
