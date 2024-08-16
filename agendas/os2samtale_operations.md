# 

# tl:dr

1. **SLA**: Tilgængelighed og forventningsafstemning.
2. **Deployment templates**: Generiske manifester.
3. **GitHub maintenance**: Automatisering og vedligeholdelse  på GH.
4. **Production Readiness**: Opfyldelse af 12/15 factor krav.
5. **OS2 bidrag**: Arkitektur sparring, GitHub opsætning, og organisatorisk implementering.
6. **Fravalg**: Kagen skæres



# Agenda-forslag

### 1. Formulering af "applikations" SLA

Inputs til beskrivelse af hvad man kan forvente af tilgængelighed på applikationerne

Input til beskrivelse af hvor længe man kan forvente at data kan tilgåes i applikationerne.

Input til beskrivelse af hvad der sker og hvordan en anvender kan handle hvis "noget er nede" Her vil den tekniske opgave på Telemetry spille ind med live pull baseret status til anvenderne. (se Telemetry længere nede)

### 2. Deployment templates:

Oprettelse af generiske manifest templates til stacken som vi kan dele offentligt

### 3. GitHub org/repo maintenance

Hjælp til opsætning og automatisering så så meget som muligt kører automatiskt.

Diskussion om hvor det er meningsfyldt at drifts repos er og hvordan upstream bidrag rammer template repos

Aftale om pragmatisk vedligeholdelses kadence

### 4. Production Readiness

Hjælp til 12/15 factor opfyldelse på stack herunder

- **Authentication:** Vi har investeret i Authentik, for at få en mere moderne Cloud Native og mere lean løsning end KeyCloak. Vi har fået en PR ind (og har en mere på vej) der tilføjer krypterings mekanismer som OIOSAML forventer til SAML provideren i Authentik. Det er testet imod deres test infrastruktur. Vi forventer at bruge det officielle image, når vores PR er med i næste release/container.

- **Build**: Zulips container build er lige nu omtalt som "alpha". Hjælp til modning og bidrag upstream til dette build. Hvis det bliver nødvendigt, gerne en action der bygger imaget via GitHub CI og pusher til GitHub container reg. Resten af stacken har officielle container builds

- **Store config in the environment:** Opsætning af SAML provider integration i Authentik som konfiguration. (Semaphor har lavet dette manuelt inde i en statefull test instans) og opsætning af Applikations konfigurationer.

- **Telemetry**: Anvender orienteret applikations overvågning. F.eks en simpel proxy redirect til en webside der på "anvender sprog"" forklarer hvornår man forventer at være oppe igen og beskriver anvender SLAen og hvad "man kan gøre nu" just for good measures.

- **Backing services**: Så mange af jeres standardservices i brug som muligt (ja.. jeg ved Authentik er en tilføjelse, men jeg tror den passer godt ind i jeres koncept) og  jeres anbefalinger til at holde apps stateless

- **Dev/Test/Prod parity**: Når der bliver lavet konfigurationsændringer til applikationen, hvordan testes de så? Hvis der kommer mulige breaking changes i en applikation/integration eller ændringer i FK evt. hvad gør vi så? Kan et minimalt, ikke skalerbart test setup være nok? Kan det køres udenfor K8s? Hvad er mest kosteffektivt?

### 5. OS2 kan bidrage med:

**OPSTARTSFASEN:**

- Arkitektur sparring

- Deltagelse i skrivearbejde på SLA og minimal teknisk "Getting Started Guide"

- Deltagelse i oprettelse og konfiguration af GitHub organisation og struktur.
  
  - Herunder Issue-tracker opsætning og deltagelse i arbejdsflow i issues i et OS2 ejet repo. Vi mangler et løbende repo-maintainer team, gerne input fra KIT / tilbud på maintenance

**EFTER 0.9 ER KØRENDE**

- 4 ugers organisatorisk implementering
  
  - Vi har en forretningskonsulent i 4 uger, der vil kunne agere projektleder på forretningsdelen. Måske indsamle oplevelser under disse uger til en "anvender guide"
  
  - Forventningen er at de første anvendere er onboardet og kørende. Diskussion om realisme af dette ønskes.

**DRIFTSFASEN:**

- Der ikke afsat et applikations drifts team. Hvordan forklares risisci af dette? Det drejer sig om forventningsafstemning.

### 6. Fravalg:

###### Men som kunne være ydelser vi efterspørger i senere Milestones eller som kan inkluderes hvis i vurderer dem som lavt hængende frugter:

- Applikations tilpasning: OIDC scope mappings til applikationerne (f.eks grupper o.s.v.)

- Semi/Automatisk sync til et andre os2projekter eller repos "storage" via plugins? (vidensopsamling til guides og docs)

- Scale to low/0 (den grønne dagsorden / marketing)

- Fuldt containerized automatiseringer (fremtidssikring/exit-strategi fra GitHub så alle automatiseringer er klargjort til GitLab/CodeBerg eller hvad fremtiden nu bringer)

#### Sparring på evt. opdeling af projekt:

- Inputs til hvor meget kan vi skære væk og dække ind under en SLA?

- Indsamling af User Stories på andet end "os2samtale" er ufærdigt og uklart.. Sparring på anbefalinger... 

- Minus dokument deling. NexCloud som et seperat projekt (da det f.eks betyder en robust investering i storage)

- Minus videomøder. Fravalg af Jitsi for mindre kompleksitet og tydeligere prissætning "pr. service"

- Sparring på prissætning i træskolængder for tilføjelse af yderligere services, så der bliver awareness ved bestilleren / OS2 ledelsen

### Kontekst:

[Vores nuværende issue-tracker på OS2ID/Authentik projektet](https://github.com/OS2sandbox/sandbox-myndighedsidentitet-issues)

[Authentik Security Inc · GitHub](https://github.com/goauthentik/) | [Authentik homepage](https://goauthentik.io/)

OS2s bidrag til Authentik sammen med Semaphor: https://github.com/goauthentik/authentik/pull/10099
Issue pre-PR:

[Support for EncryptedAssertion · Issue #9172 · goauthentik/authentik · GitHub](https://github.com/goauthentik/authentik/issues/9172)
