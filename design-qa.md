# Design QA — attachment-aware reader

## Comparison target

- Source visual truth:
  - `C:\Users\leand\AppData\Local\Temp\codex-clipboard-00a19508-5065-4d7b-8432-ef8d383f80e7.png` — existing Vedøy Mailbox reader with the attachment-only message appearing empty.
  - `C:\Users\leand\AppData\Local\Temp\codex-clipboard-0af6e884-72aa-4352-8d59-ba11d6935d73.png` — Domeneshop behavior reference showing four image attachments, previews and download affordances.
- Implementation screenshots:
  - `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\verification-attachments-light.png`
  - `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\verification-attachments-dark-fixed.png`
  - `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\verification-attachments-dark-bottom-fixed.png`
  - `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\verification-attachments-scrolled.png`
- Combined comparison evidence:
  - `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\design-comparison-vedoy.png`
  - `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\design-comparison-behavior.png`

## Viewport and normalization

- Source pixels: 1906 × 1080 (Vedøy) and 1909 × 1071 (Domeneshop).
- Implementation capture pixels: 1280 × 720.
- Browser viewport override requested: 1440 × 900; the in-app browser returned a scaled 1280 × 720 raster.
- Comparison boards normalize both sides to 700 px image height and retain aspect ratio. Browser chrome is intentionally retained on the source side and excluded from fidelity findings.
- State: selected attachment-only message, light and dark themes, gallery at top and bottom of the independently scrollable reader.

## Full-view comparison evidence

- The Vedøy three-column composition, logo, restrained palette, thin dividers, typography hierarchy and existing actions remain intact.
- The previously empty reader now communicates that the message contains attachments, then presents count, total size, image previews, names and download controls.
- The implementation adopts Domeneshop's useful attachment behavior without copying its blue/dense visual styling; it remains inside Vedøy's established design system.

## Focused-region comparison evidence

- Attachment region: compared filename legibility, preview crop, count/size summary, open action, individual download and download-all action. All required controls are visible and semantically labeled.
- Reader bottom: `verification-attachments-dark-bottom-fixed.png` confirms the full four-item gallery, independent vertical scrolling and readable Reply/Forward actions.
- No additional focused crop was needed because the desktop capture keeps all attachment controls legible.

## Required fidelity surfaces

- Fonts and typography: existing Manrope/DM Sans hierarchy is retained; filenames truncate safely and metadata stays subordinate.
- Spacing and layout rhythm: 12 px gallery gap, consistent 12 px radii and a clear divider separate message content from attachments.
- Colors and tokens: light and dark surfaces use the existing neutral Vedøy palette; attachment cards do not introduce a competing accent system.
- Image quality and asset fidelity: real attachment bytes render with `object-fit: contain`; no placeholder art or recreated imagery is used in production.
- Copy and content: the empty-body state clearly explains why the message has no text and directs attention to real files below.
- Accessibility and interaction: buttons and links have accessible names, reduced-motion rules are preserved, loading/error states are explicit, and external images remain blocked by default.

## Comparison history

1. P0 fixed before first visual pass: attachment metadata had no content endpoint and the reader ignored attachments. Added an authenticated attachment route, MIME metadata, inline previews, CID replacement and download controls.
2. P1 fixed before first visual pass: automatically selecting a summary could show an apparently empty reader without loading message details. New folder loads now wait for an explicit message choice; cached full messages remain preserved during refresh.
3. P2 found in dark bottom-state pass: Reply/Forward inherited a light background and light text. Added dark-theme button tokens. Post-fix evidence: `verification-attachments-dark-bottom-fixed.png`.

## Interaction and runtime evidence

- Opened the attachment-only message and observed four rendered image previews.
- Scrolled the reader to the final attachments and Reply/Forward controls while the inbox list remained in place.
- Triggered an actual single-file browser download successfully.
- Opened the new Visning settings tab, verified all four controls and saved the theme locally.
- Browser console warnings/errors after interactions: 0.
- Framework error overlay: none.
- Residual test gap: the in-app browser's temporary mobile viewport override did not alter the captured CSS viewport, so the new one-column attachment breakpoint was code-reviewed but not captured as fresh mobile browser evidence in this pass.

## Findings

- No actionable P0, P1 or P2 visual findings remain for the supplied desktop source state.

## Follow-up polish

- P3: a future iteration could add server-generated thumbnails for very large image-heavy threads to reduce first-preview bandwidth.

final result: passed

## Design QA — Gmail-inspirert lest/ulest og leverandørvalg (2026-08-18)

### Sammenligningsgrunnlag

- Visuell fasit: `C:\Users\leand\AppData\Local\Temp\codex-clipboard-ae7b5660-17ff-474c-af95-62da9025b4e3.png` (1888 × 951 px), Gmail med både leste og uleste rader.
- Implementasjon: `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\verification-gmail-read-unread.png` (1280 × 720 px), Vedøy Mailbox i mørkt tema med én ulest og flere leste rader.
- Kontoskjema: `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\verification-provider-setup.png` (1280 × 720 px).
- CSS-visningsflate: 1280 × 720, device scale 1. Kilden er et bredere Chrome-skjermbilde; vurderingen er derfor normalisert på innboksradens tilstand og hierarki, ikke piksel-for-piksel på hele appskallet.

### Full visning

- Gmail-prinsippet er gjenskapt uten å kopiere hele Gmail-grensesnittet: ulest har lys/hvit og fet tekst, mens lest har normal grå tekst på en tydelig grå bakgrunnsflate.
- Vedøy-logo, trekolonnelayout, mørk palett, ikoner og eksisterende funksjoner er bevart.
- Valgt rad er fortsatt synlig uten at lest/ulest-statusen forsvinner.

### Fokusert kontroll

- Ulest valgt rad: bakgrunn `rgb(45, 51, 45)`, avsender `rgb(255, 255, 255)`, fontvekt `700`.
- Lest valgt rad: bakgrunn `rgb(58, 64, 58)`, avsender `rgb(154, 159, 152)`, fontvekt `400`.
- Tydeligheten kommer fra både tekstvekt, tekstfarge og egen radflate, slik referansen viser.

### Fidelity-overflater

- Typografi: eksisterende Manrope/DM Sans er beholdt; 700/400 skiller ulest og lest uten å endre størrelser eller bryte trunkering.
- Avstand og rytme: eksisterende radmål, avatarer, avkrysningsbokser og skillelinjer er uendret.
- Farger: Gmail sitt semantiske mønster er overført til Vedøy-paletten; kontrasten er kontrollert i faktisk mørk modus.
- Bildekvalitet: ingen nye rasterbilder eller erstatningsgrafikk var nødvendig; eksisterende Vedøy-logo brukes uendret.
- Tekst og innhold: statusene «NY» og «LEST» er beholdt som ekstra støtte, og leverandørskjemaet forklarer porter, Gmail-app-passord og Outlook OAuth2 på norsk.

### Interaksjon og drift

- Ekte IMAP-oppdatering hentet 5 meldinger etter at lokal backend fikk utgående nettverkstilgang.
- «Lest · marker ulest» endret IMAP-flagget og UI til ulest; «Marker som lest» gjenopprettet opprinnelig tilstand.
- Domeneshop-, Gmail- og Outlook-valgene ble åpnet. Gmail viste riktige servere og app-passordfelt; Outlook viste OAuth2-kravet og tilbød ikke usikker passordinnlogging.
- Konsollfeil/advarsler etter interaksjonene: 0. Backendfeil etter nettverkstillatelse: 0.

### Funn og sammenligningshistorikk

- Ingen åpne P0-, P1- eller P2-avvik for den etterspurte lest/ulest-tilstanden.
- Første kjøretidssjekk fant et miljøproblem (`EACCES`) fordi den lokale backend-prosessen manglet utgående nettverk. Serveren ble startet med nødvendig tillatelse, og etterkontrollen hentet ekte e-post. Dette var ikke et visuelt avvik.

final result: passed

## Design QA — lest/ulest typografi (2026-08-18)

- Kilde: `C:\Users\leand\AppData\Local\Temp\codex-clipboard-5e168cef-941c-4a85-8d05-2ce0ada28721.png` (986 × 759), mørk innboks med både leste og uleste rader.
- Implementasjon: `C:\Users\leand\Documents\ChatGPT\Vedoy Mailbox\verification-read-status.png` (1280 × 720), fokusert mørk-tema kontroll av de to tilstandene.
- Helhet: eksisterende layout, avatarer, markører, hover og valgt rad er uendret; bare teksthierarkiet er tydeligere.
- Fokusert sammenligning: ulest avsender/emne måles til `rgb(255, 255, 255)` og forhåndsvisning/tid til `rgb(238, 241, 235)`; lest avsender/emne måles til `rgb(154, 159, 152)` og forhåndsvisning/tid til `rgb(126, 132, 124)`.
- Interaksjon: radens eksisterende `unread`/`read`-klasse styrer fargen. `markSeen` oppdaterer tilstanden optimistisk og ruller tilbake hvis API-kallet feiler; backend lagrer tilstanden med IMAP-flagget `\\Seen`.
- Konsollfeil og advarsler i kontrollvisningen: 0.
- Funn: ingen åpne P0-, P1- eller P2-avvik for den etterspurte tilstanden.

final result: passed
