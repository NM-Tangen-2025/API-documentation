# Dokumentasjon om tilgjengelige API'er

I forbindelse med NM 2025 har Tangen VGS tilgjengeliggjort to API'er som elevene kan bruke til å 
hente ut data om Tall Ships Races 2025. 

Det er to sett med API'er: Ett for å hente ut data om skip og skips-posisjoner, 
og ett for å hente ut artikler, bilder og arrangementer. 

## API for skip og skips-posisjoner

API'et har endepunkter for å hente ut skip og skips-posisjoner. For hvert skip kan man hente ut 
navn, land og bilde. 

API'et er dokumentert her:
https://snmapi-demo.tanvgs.no/


## API for artikler, bilder og arrangementer

Det er satt opp en Strapi-instans som inneholder artikler, bilder og arrangementer. 
Strapi er et headless CMS - det vil si at det tilbyr en API som deltagerne kan bruke 
til å hente ut data, feks artikler, bilder og andre media. 

Det er ikke nødvendig å kunne detaljene rundt Strapi og Strapi sitt REST-API
for å hente ut NM-innhold - dere kan bruke eksemplene her i stedet.   
Detaljert informasjon om Strapi finner man her, om ønskelig: https://docs.strapi.io/cms/api/rest

En forenklet dokumentasjon for Tangen VGS sin Tall Ships Races API kommer under: 

### Generell dokumentasjon

Adressen til serveren er: `https://fortunate-bear-715099df12.strapiapp.com`

Innhold er tilgjengelig på `/api/{Innholdstype}`, der innholdstype er en av: `Lokasjoner`, `Nyhetsartikler` eller `Arrangementer`.
For å få med alle attributtene til innholdet, inkludert eventuell bilde-lenke, bør dere bruke `?populate=*` i URL'en.

Mao: For å hente ut alle `Arrangementer` med alle attributter, kan dere bruke følgende URL:
`https://fortunate-bear-715099df12.strapiapp.com/api/Arrangementer?populate=*`

### Autentisering 

Alle kall til API'et må inkludere i http-headeren et "bearer token", altså en API-nøkkel. 

API-nøkkelen dere kan bruke er: 
`1330d7d0a7e52fbcf4779861a6948373dff5f06b8bbce4cc0d08025276bb45ce3114590200d5b3cb7d0a856325f55c71e170fc2f2e4508102712e4730fbfb075c745056641f618bee2e54bf7ccdb1a56c6c4e89d60ef7c25f728198bde97d7e4cfbb773f63336580c64084350f57ffba8a15e289b1016cbe4df256bc2928bd50`

Http-headeren blir da "Authorization: Bearer 133...". 

Nederst i dokumentet er det eksempel kode for å hente ut data fra API'et i JavaScript, inkludert autentisering.

### Lokasjoner

`Lokasjoner` er en liste over steder der arrangementer finner sted. Lokasjoner har følgende attributter: 
- Navn: tekst
- Posisjon, som er et objekt med to attributter: 
  - Breddegrad
  - Lengdegrad
- Bilde: referanse til bilde


### Nyhetsartikler

`Nyhetsartikler` er en liste over nyhetsartikler. Nyhetsartikler har følgende attributter:
- Tittel: tekst
- Ingress: tekst
- Innhold: tekst
- Dato: dato
- Bilde: referanse til bilde


### Arrangementer
`Arrangementer` er en liste over arrangementer. Arrangementer har følgende attributter:
- Arrangementstype: tekst (en av: konsert, matfestival, kunstutstilling)
- Tittel: tekst
- Ingress: tekst
- Beskrivelse: tekst
- Lokasjon: referanse til lokasjon
- Dato og tid: dato
- Bilde: referanse til bilde


### Bilder

Lokasjoner, nyhetsartikler og arrangementer kan ha et `Bilde`. I JSON-resultatet fra API'et vil 
det komme som et objekt med diverse attributer, de viktigste er: 
- `url`: URL til orginalbildet
- `name`: Navn på bildet

I tillegg vil det komme med en `formats`-attributt, som inneholder flere versjoner av bildet i forskjellige størrelser, 
med forskjellige størrelser og forskjellige URL'er.

Disse kan brukes dersom man skal lage en responsiv UI, feks mobiltilpasset. 

### Eksempel på en mulig løsning der en henter innhold fra strapi API: 

Se [`example.mjs`](example.mjs)

