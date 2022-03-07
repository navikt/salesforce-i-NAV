# Innledning
   

### Nyttige lenker  
- My Apps: https://myapplications.microsoft.com/

- Nav Apps: https://mobapps.nav.no/Citrix/IKSS_MobappsWeb/

- https://mobilitet.nav.no/RAbrukerMOB.htm

- https://github.com/navikt/utvikling

- https://confluence.adeo.no/display/KFDS/FAQ+for+utviklere

## Tilganger som kan bestilles med en gang via Ident rutinen:
- NAV Desktop Utvikling
- NAV Desktop Test
- NAV Desktop Preprod
- IDA Standard
- Lokal Admin (Dersom Windows PC)
- Notepad++
- VDI (Spesifiser Linux eller Windows)
- Epost sendes til nav.it.identhandtering@nav.no med ident ansvarlig på kopi

Mer om ident rutinen: https://confluence.adeo.no/display/~W110099/Identrutinen

## Slack
  
Bruk "inviter til slack" funksjonen for å få med personer med nav.no -adresse på Slack.  
Gå til https://myapps.microsoft.com (logg inn med nav-epost)  
Trykk på «...» oppe i høyre hjørne  
Trykk på "+ Legg til selvbetjeningsapper"  
Velg «Slack» i listen og trykk Add  
Gå så til https://nav-it.slack.com og logg inn med SSO / nav-epost  
Dette gjelder kun de som allerede har en @nav.no adresse.   
Eksterene må inviteres som gjester.

## Salesforce DX Bruker
Kontakt plattform-teamet på #crm-plattform-team om du trenger en DX-bruker. 

Vi har to type lisenser som brukes for DX-brukere. De heter "Salesforce Limited Access - Free" og "Developer". De har hver sin profil, og de heter henholdsvis "NAV DX Developer Free" og "NAV DX Developer". Disse gir tilgang til å opprette Scratch Orgs. I tillegg finnes det to tillatelsessett som gir ekstra tilganger. Disse heter "DX - Promoter Pakker" og "DX - Create Second Generation Packages". De fleste trenger ikke disse tillatelsessettene, da de utfører disse handlingene via GitHub Actions. I GitHub brukes det en egen bruker (SFDX Integrasjonsbruker).

## Nais Device: 
https://doc.nais.io/device/index.html
## GitHub:
Opprett din egen NAV GitHub bruker.
Når denne er opprettet, få noen til å legge deg inn i NKS Teamet.
For å logge inn på NAV GitHub, gå via MyApps
## Sette opp lokalt Utviklingsmiljø:
Salesforce sin guide: https://developer.salesforce.com/tools/vscode


* Installer NPM
* Installer SFDX CLI
* Installer via NPM: npm install sfdx-cli --global
* Alternativt last ned fra Salesforce.com
* Installer VS Code
* Installer Salesforce Exctension i VS Code
* Installer Java
    * Kun versjon 8 eller 11
SF sin Java Guide: https://developer.salesforce.com/tools/vscode/en/getting-started/java-setup
    * Åpne VS Code Settings og søk etter salesforcedx-vscode-apex, under Java Home, legg inn path til java installasjonen.
* Installer SSDX
Følg oppskriften her: https://github.com/navikt/ssdx
Du trenger ikke å laste ned install.cmd før du har et prosjeket.
* Tilgang UAT:
Få noen på teamet til å opprette en bruker for deg i UAT.
* For å teste Integrasjoner:
Teste i SIT2 (med integrasjoner)