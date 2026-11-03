# SAST-övning: få din första kodanalysrapport

Du får en liten JavaScript-app (Node + Express). Din uppgift är att koppla den till ett SAST-verktyg, **GitHub CodeQL**, och få en rapport över säkerhetsproblem i koden.

Tid: ca 45 minuter. Du lämnar inte in något, målet är att du ska få fram rapporten och förstå hur man läser den.

> Appen är **medvetet osäker**. Kör den bara lokalt och lägg aldrig upp den som en riktig tjänst.

## Du behöver
- Ett GitHub-konto (logga in innan lektionen)
- Git installerat, eller GitHub Desktop
- (Valfritt) Node.js om du vill köra appen

## Steg 1: Hämta koden (5 min)
Ladda ner ZIP-filen och packa upp den, eller klona repot om du fått en länk.

## Steg 2: Lägg koden i ditt eget GitHub-repo (5 min)
1. Gå till github.com → **New repository**.
2. Namn: `sast-ovning`. Välj **Public**. Lägg inte till README eller .gitignore.
3. Kör i mappen med koden:
   ```
   git init
   git add .
   git commit -m "Första version"
   git branch -M main
   git remote add origin https://github.com/DITT-ANVÄNDARNAMN/sast-ovning.git
   git push -u origin main
   ```
   Har du klonat från en annan adress måste du först ta bort den gamla kopplingen: `git remote remove origin`. Du kan också använda GitHub Desktop (File → Add local repository → Publish repository, ta bort bocken för *Keep this code private*).

> Repot måste vara **publikt**. Kodskanning med CodeQL är gratis bara för publika repon.

## Steg 3: Gissa först (5 min)
Öppna `src/server.js`. Skriv ner 2–3 saker du tror är osäkra. Tänk på föreläsningen: indata, SQL, hemligheter.

## Steg 4: Starta CodeQL (10 min)
1. I ditt repo: fliken **Settings → Advanced Security** (eller **Security → Code scanning**).
2. Under *Code scanning* välj **Set up → Default**.
3. Kontrollera att språket **JavaScript/TypeScript** är valt och klicka **Enable CodeQL**.
4. Gå till fliken **Actions**. Du ser en körning som heter *CodeQL*. Den tar 2–5 minuter första gången, det är normalt.

## Steg 5: Läs rapporten (10 min)
1. Fliken **Security → Code scanning**.
2. Klicka på ett fynd. Titta på:
   - regelnamn (t.ex. *SQL injection*) och allvarlighetsgrad
   - fil och rad
   - **Show paths**: vägen från indata (källa) till det farliga anropet (sänka)
3. Jämför med dina gissningar från steg 3. Vad hittade du som verktyget missade, och tvärtom?

## Steg 6: Åtgärda ett fynd (extra, 10 min)
Välj ett fynd, ändra koden (t.ex. använd en parameteriserad fråga i `/search`), pusha och vänta på ny körning. Fyndet ska stängas automatiskt.

## Fastnar du?
- Ingen *Code scanning* syns: kontrollera att repot är Public.
- Inga fynd efter flera minuter: öppna **Actions** och se om körningen är röd eller fortfarande går.
- `git push` nekas: kontrollera användarnamn i adressen och att du är inloggad.
