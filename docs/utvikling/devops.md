## Nødvendige tilganger for utviklerbrukere i produksjon
Salesforce tilbyr en egen lisenstype for utviklere som må ha brukere i produksjonsmiljøet for å ha tilgang til Dev Hub-funksjonalitet for å opprette Scratch Orgs og for å opprette pakker og pakkeversjoner. Denne lisenstypen er gratis og medfører ingen ekstra kostnad for NAV. Brukere med lisensen har ikke tilgang til å se eller utføre operasjoner på data i produksjon. 


### Utviklerbrukere
Følgende permissions må være aktivert for disse utviklerbrukere i Dev Hub (produksjonsmiljøet) for å kunne drive utvikling gjennom bruk av Scratch Orgs og Unlocked Packages:

| Permission type          | Permission type             | Permission level           | Beskrivelse           |
| ------------------------ | ----------------------------| ---------------------------|-----------------------|
| Object Permission        |ScratchOrgInfos              | ```Read, Create, Edit, Delete```   |Objekt som representerer forespørsler om opprettelse av nye scratch orgs|
| Object Permission        |ScratchOrgInfos              | ```Read, Edit, Delete```           |Objekt som representerer aktive (ikke utgåtte eller slettede) Scratch Orgs|
| Object Permission        |NameSpaceRegistries          | ```Read (Create, Edit, Delete hvis NameSpaces tas i bruk)``` |Objekt som representerer registrerte namespaces for Dev Hub-miljøet|
| System Permission        |Create and Update Second-Generation Packages             | ```TRUE```   |Gir tilgang til å opprette pakker og pakkeversjoner, spesifikt følgende SFDX CLI kommandoer: ```force:package:create, force:package:version:create, force:package:version:update```|
| System Permission        |Promote a package version to released              | ```TRUE```   |Git tilgang til å promotere en pakkeversjon fra beta til released via SFDX CLI kommandoen ```force:package:version:promote```. Kun pakkeversjoner som har blitt promotert til released kan installeres i produksjonsmiljøer.|

### Integrasjonsbrukere
Følgende permissions må være aktivert for integrasjonsbrukere som skal deploye til ulike Sandbox-testmiljøer eller produksjonsmiljøet. Deployment skal kun skje gjennom dedikerte integrasjonsbrukere og aldri gjennom brukere med Limited Access-lisens. 

| Permission type          | Permission type             | Permission level           | Beskrivelse           |
| ------------------------ | ----------------------------| ---------------------------|-----------------------|
| System Permission        |Modify Metadata Through Metadata API Functions             | ```TRUE```   |Gir tilgang til å deploye de fleste typer metadata via Metadata API (men ikke brukergrensesnittet).|
| System Permission        |Customize Application              | ```TRUE```           |Gir utvidet tilgang til å deploy metadata som krever denne tilgangen, f.eks. OWD-instillinger og Custom Metadata|


## Pakkebasert utvikling
Deployment og release til sandbox- og produksjonsmiljø skal hvor mulig (dvs. med unntak av upakketerbar metadata) ta sted gjennom pakkebasert utvikling og Unlocked Packages som deployment-mekanisme. En Unlocked Package er en gjenbrukbar, scriptbar, og sporbar artifakt som representerer et separat sett med metadata. Gjennom bruk av Unlocked Packages kan vi bedre organisere og forstå utvikling og tilpasning gjort av hvert autonomt team og som leverer funksjonalitet på plattformen og avhengighetene mellom deres komponenter, samtidig som hvert team vil kunne deploye, teste, oppgradere og rulle tilbake sine egne pakker.

### Pakkestruktur (avhengigheter nedover)
![](../images/samplepackagemodel.png)

### Pakkestruktur m. innholdsdefinisjon (avhengigheter nedover)
![](../images/samplepackagemodel2.png)

### Pakkeversjoner installert i ulike miljøer
![](../images/samplepackagemodel3.png)

## Utviklingsmodeller

Salesforce støtter tre utviklingsmodeller:

1. **Org-basert utvikling**
I org-basert utvikling representerer produksjonsmiljøet "source of truth". Sandboxes kan opprettes som kopier av produksjonsmiljøet og endringer kan migreres "oppover" deklarativt via Change Sets-funksjonaliteten eller mellom alle typer miljøer via Salesforce Metadata-API. Versjonskontroll kan brukes, men hovedsakelig "defensivt" for å spore endringer og ikke for å representere en fullstendig "source of truth" eller som kilde for deployments til andre miljøer.
2. **Source-basert utvikling**
Versjonskontroll representerer "source of truth". Utvikling utføres i Sandboxes eller Scratch Orgs, og endringer utført i et utviklingsmiljø ("org" eller "instans") trekkes ned fra utviklingsmiljøet som metadata i XML-format og integereres i versjonskontroll. Deployments mellom miljøer utføres gjennom Metadata API eller SFDX CLI på bakgrunn av metadata i versjonskontroll. 
3. **Pakke-basert utvikling**
Versjonskontroll representerer "source of truth". Metadata er organisert i pakker, og en gitt instans av en type metadata (f.eks. et spesifikt felt, et objekt, en Apex-klasse) kan kun inngå i en enkelt pakke. Utvikling utføres i Scratch Orgs, og endringer utført i Scratch Orgen trekkes ned som metadata i XML-format og integereres i versjonskontroll. Salesforce SFDX CLI kan ta med utgangspunkt i metadata i versjonskontroll lage et "snapshot" av denne metadataen som en pakkeversjon. Pakkeversjoner kan installeres og avinstalleres på tvers av ulike miljøer (utvikling, test, og produksjon).


**Pakkebasert utvikling er et foretrukket valg for NAV.** I lys av NAV sine krav til samtidig leveranse på tvers av ulike funksjonelle områder og fra flere ulike autonome team gir denne utviklingsmodellen muligheten til å håndtere en høy grad av kompleksitet gjennom å organisere metadata i navngitte, versjonerte pakker og formelt definere avhengigheter mellom disse. Bruk av pakker gir en tydelig avgrensing på hvilken metadata som er i utvikling, test og produksjon. Pakker brukes også som en deploymentmekanisme og som den sentrale artifakten som produserers og deployes i en CICD-prosess.

![](../images/utviklingsmodell.png)

## Assignment av Page Layouts

### Page Layouts
Page Layout assignments er definert i brukerens profil gjennom layoutAssignments-definisjonen. LayoutsAssignments er en knytning mellom en layout, en profil, og en Record Type. Eksempel:

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<Profile xmlns="http://soap.sforce.com/2006/04/metadata">
    <custom>false</custom>
    <layoutAssignments>
        <layout>Account-Layout 2</layout>
        <recordType>Account.Employer</recordType>
    </layoutAssignments>
</Profile>
```