# Hjelp til innsending av prisoppgaveskjema via API

## Maskinporten og delegering av rettigheter for ulike aktører:

### Rapporteringspliktig som ønsker å sette opp integrasjon selv.

* Dere må opprette en integrasjon (en OAuth 2.0-klient) i Maskinporten med scope `fdir:priceboardreportingapi`
* Se `https://samarbeid.digdir.no/maskinporten/ta-i-bruk-maskinporten/97` under “Konsument”.

### Rapporteringspliktig som ønsker å benytte en tjenesteleverandør

* Dere må gi fullmakt til API i Altinn til tjenesteleverandør. Følg veiviser på https://info.altinn.no/hjelp/ny-tilgangsstyring/maskinportenadministrasjon/ for å gi ansatte tilgang til dette.
* Søk og velg fullmakten “Tilgang til API for prisoppgaveskjema”
* Ta kontakt med tjenesteleverandør som leverer integrasjonen, slik at de kan rapportere på vegne av dere.

### En tjenesteleverandør som vil tilby innsending for rapporteringspliktige

* Gjelder leverandør av system med integrasjon mot Fiskeridirektoratet’s APIer.
* Din kunde må ha tildelt API-tilgang i Altinn til leverandør.
* Leverandør av system må opprette en Maskinporten med scope `fdir:priceboardreportingapi`.
* Samme klient kan brukes til å rapportere for flere kunder ved å endre `consumer_org` verdien.
* Se `https://samarbeid.digdir.no/maskinporten/ta-i-bruk-maskinporten/97` under “Leverandør”.

## Testmiljø:

Det finnes et testmiljø og et produksjonsmiljø for APIet.

* For å teste registrering av prisoppgaver i testmiljøet må dere bruke en test-organisasjon. Vi benytter syntetiske organisasjoner fra Skatteetatens Tenor testdatabase `https://www.skatteetaten.no/testdata/`.
* Ta kontakt med oss for å få tildelt organisasjonsnummer som er tilknyttet tillatelser i akvakulturregisteret sitt testmiljø, og som brukes for pålogging i Samarbeidsportalen: `https://sjolvbetjening.test.samarbeid.digdir.no/login`.
* Det må opprettes egen Maskinporten klient i testmiljøet til Maskinporten. Logg inn i testmiljøet for Samarbeidsportalen og opprett klient for testorganisasjonen.
* For tjenestetilbydere må klienten opprettes for en syntetisk organisasjon som skal representere organisasjonen til tjenestetilbyderen. Organisasjonen til tjenestetilbyderen må også ha fått delegert tilgang i testmiljøet til Altinn av den som det skal rapporteres på vegne av.
* Innsending av prisoppgaveskjema i testmiljøet krever bruk av gyldige lokaliteter i dette miljøet. Disse vil dere også få tildelt sammen med testorganisasjon av oss.

## Krav til innsending via API:

* Hvert salg skal sendes inn separat. Det er ikke anledning for å slå sammen eller summere opp flere salg i én innsending.
* Det er også forskjeller i datamodellen ved innsending via API fra manuelt innsendt skjema.

### Nye felt

* Antall fisk skal oppgis i feltet `salesLines.amount`
* Gjennomsnittsvekt `salesLines.averageWeightInKg`
* Gjennomsnitspris per kg `salesLines.averagePriceInNOK`

### Fjernede felt:

* Salgslinje sum vekt
* Salgslinje sum pris.

### Kostnader

* Ekstern/Intern rapporteres separat for hver kostnad `sales.isCostExternal`
* Kostnad rapporteres i kostnad per kg `costs.costPerKgInNok`
* Det er også åpnet for å rapportere tjenesteleverandør per kostnad `costs.serviceSupplier`. Dette er foreløpig ikke påkrevd.

Ellers skal andre verdier brukt ved innsending være tilgjengelig på endepunkt for utlisting av koder i APIet.
