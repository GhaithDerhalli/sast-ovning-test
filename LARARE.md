# Lärarfacit (dela inte med eleverna)

## Verifierat CodeQL-utfall (default setup, körd 2026-11-03)
8 fynd i src/server.js:

| Rad | Sårbarhet | Regel | Allvarlighet |
|---|---|---|---|
| 33 | Kommandoinjektion (/ping) | js/command-line-injection | critical |
| 24 | SQL-injektion (/search) | js/sql-injection | high |
| 27 | Reflekterad XSS (/search) | js/reflected-xss | high |
| 41 | Path traversal (/file) | js/path-injection | high |
| 58 | Öppen redirect (/go) | js/server-side-unvalidated-url-redirection | medium |
| 21, 32, 39 | Saknad rate limiting (/search, /ping, /file) | js/missing-rate-limiting | high |

Hårdkodat lösenord (ADMIN_PASSWORD) hittades INTE av CodeQL. Bra diskussionspunkt: SAST hittar inte allt, använd även hemlighetsskanning (t.ex. gitleaks, GitHub secret scanning).
Rate limiting-fynden är inte vad vi byggde in, men är riktiga och kan användas för att prata om triagering.

## Felsökning
- Privat repo: ingen Code scanning utan Advanced Security.
- Elever som klonat med gammal origin: `git remote remove origin`.
- Första körningen kan ta 5 min när många startar samtidigt.

## Alternativ till Default setup
Lägg `.github/workflows/codeql.yml` med `github/codeql-action/init@v3` (languages: javascript-typescript), `autobuild` och `analyze`.
