![image](https://user-images.githubusercontent.com/77058637/148192457-0432c9d2-8105-4bc4-b3c2-7db462c9c6c6.png)

# Salesforce i NAV
Repo for å dokumentere hvordan vi bruker Salesforce i NAV. Dokumentasjonen publiseres hit: https://navikt.github.io/salesforce-i-NAV/

## Bidrag til dokumentasjonen
Du kan bidra til dokumentasjonen på flere måter, i hovedsak følgende tre:

1. Legg inn en --issue-- hvor du enten beskriver hva du vil ha dokumentert eller legger ved dokumentasjon du selv har skrevet. Dette kan du gjøre her: https://github.com/navikt/salesforce-i-NAV/issues/new/choose
2. Klone reposet og lage din egen Pull Request som vi kan flette inn etter vurdering.
3. Be om å bli en del av dokumentasjons-teamet slik at du kan publisere dokumentasjon direkte. Hvis du ønsker dette kontakt platformteamet på Slack.

## For deg som ønsker å publisere direkte
Hvis du synes det er ok å bruke GitHub sin web-editor så er det raskeste vei til mål. Når du pusher endringene så genereres dokumentasjonen via GitHub Actions automagisk. Hvis du ønsker litt mer kontroll på verktøy og skriveprosess så må du lese videre.

### Installasjon av verktøy du trenger

I tillegg til git trenger du *python* og *pip* slik at du kan installere *MkDocs* og *Material for MkDocs*.

Kjør kommandoene: 

`pip install mkdocs`

`pip install mkdocs-materials`

Du kan lese mer om *MkDocs* [her](https://www.mkdocs.org/) og theme-et *Material for MkDocs* [her](https://squidfunk.github.io/mkdocs-material/)

### Skrive dokumentasjon

1. Klone reposet
`git clone https://github.com/navikt/salesforce-i-NAV.git`
2. Åpne reposet med en editor du liker å bruke. Det er antakelig en fordel å bruke en editor som har støtte for *markdown*.
3. Dokumentasjonsfilene ligger i *docs*-katalogen og er i markdownformat. Du kan lese mer om markdown [her](https://www.markdownguide.org/)

### Publisere endringene dine

Kjør kommandoene:
`git add --all`
`git commit - m 'commit message'`
`git push`

Endringene pushes nå til *main branch* på remote repos-et og deretter kjøres en GitHub Action som generer html-dokumentasjonen. Det kan ta noen minutter før du ser endringene på siden etter at du har publisert. 

Kommandoen som faktisk kjøres er:

`mkdocs gh-deploy --force`

Denne generer html-dokumentasjonen på en egen *branch* som heter *gh-pages*. Vi har satt opp GitHub-pages til å lete etter html-sider på denne branchen og du kan som nevnt se dem [her](https://navikt.github.io/salesforce-i-NAV/)
