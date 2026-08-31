# Vedøy Mailbox

En Vedøy-merket IMAP/SMTP-klient med ekte backend. Nettleseren snakker kun med API-et; IMAP-passord, SMTP-passord og KI-nøkkel eksponeres aldri for frontend-JavaScript.

## Dette fungerer

- Les, søk, oppdater, stjernemerk, merk som lest/ulest, arkiver og slett e-post.
- Lest og ulest har tydelig visuell status. Endringer sendes til IMAP og rulles tilbake i grensesnittet hvis serveren avviser dem.
- Koble til opptil fem jobb- og privatkontoer, bytt aktiv konto raskt og fjern kontoer enkeltvis.
- Filtrer på **Alle**, **Ulest** og **Svar senere** uten å endre meldingen hos leverandøren.
- Vis både HTML og ren tekst i en isolert iframe uten skript.
- Vis innebygde `cid:`-bilder, forhåndsvis bildevedlegg og last ned én eller alle filer.
- Send, svar og videresend med signatur og opptil tre egne vedlegg.
- Valgfri KI-hjelp lager kun et redigerbart svarutkast; den sender aldri automatisk.
- Lyst/mørkt tema, meldingstetthet, visningsvalg og oppdateringsintervall lagres lokalt.
- Motion for React gir korte overganger og lastetilstander, med støtte for systemvalget «redusert bevegelse».
- Utkast lagres automatisk lokalt per konto. Tastene `C`, `R`, `U`, `J`, `K` og `/` gir rask betjening.

## E-postleverandører

- **Domeneshop:** klar for innlogging med full e-postadresse og e-postpassord. Standardoppsettet er IMAP `imap.domeneshop.no:993` og SMTP `smtp.domeneshop.no:465`.
- **Andre leverandører:** velg **Annen** og fyll inn leverandørens IMAP- og SMTP-innstillinger. Gmail og Microsoft/Outlook er ikke tilgjengelig i denne versjonen fordi den nødvendige OAuth-integrasjonen ikke er ferdig.

Servernavn og porter er offentlige leverandørinnstillinger, ikke personlige hemmeligheter. E-postadresse, passord/app-passord og kontotilkoblingen tilhører brukeren. De lagres per nettleser i krypterte HttpOnly-cookies og deles ikke med andre brukere. Den eldre lokale, globale `data/mailbox.json`-lagringen er fjernet.

## Run locally

1. Kopier `.env.example` til `.env` og sett lange, tilfeldige verdier for `SESSION_SECRET` og `MAIL_ENCRYPTION_KEY`.
2. Kjør `npm install`.
3. Kjør `npm run server` i én terminal og `npm run dev` i en annen.
4. Åpne Vite-adressen. API-et kjører på port 3001.

## Production notes

- Bruk alltid HTTPS og `NODE_ENV=production`.
- Sett `SESSION_SECRET` og `MAIL_ENCRYPTION_KEY` i Vercel. Ikke endre `MAIL_ENCRYPTION_KEY` uten at brukerne kobler til kontoene på nytt.
- På Vercel ligger hver e-postkonto i en separat, kryptert HttpOnly-cookie. Den aktive kontoen velges gjennom en forseglet kontoindeks og deles ikke gjennom global servertilstand.
- Lokalt brukes samme per-nettleser-modell. Hvis cookies slettes eller krypteringsnøkkelen endres, må kontoen kobles til på nytt.
- Nettleserløsningen er begrenset til fem kontoer for å holde cookie-headeren innenfor trygge grenser. En større administrert utrulling bør lagre krypterte kontotilkoblinger i en database knyttet til reell brukerautentisering.
- Eksterne bilder er blokkert som standard for å begrense sporingspiksler. Brukeren kan slå dem på i **Innstillinger → Visning**.
- Vedlegg over 25 MB vises ikke i nettleseren. Bruk leverandørens webmail for slike filer.
- Bruk et app-passord dersom e-postleverandøren har tofaktorautentisering.
- For en administrert Vedøy-tjeneste bør tillatte IMAP/SMTP-verter begrenses på serversiden og sesjoner flyttes til en varig database eller Redis.
