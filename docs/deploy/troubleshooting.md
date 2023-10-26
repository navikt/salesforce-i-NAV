# Feilsøking

## Problem: gpg-signering til git failet.
Jeg fikk plutselig en feil der jeg ikke fikk lov å commit fordi
```
 error: gpg failed to sign the data
 fatal: failed to write commit object
```
Denne feilen oppsto etter at jeg hadde en verified commit tidligere i dag.
Årsaken var at gpg-signeringen hadde hengt seg opp.
Debug:
```
GIT_TRACE=1 git commit -m "commit message"
```
I teksten du får kommer dette:
```
gpg --status-fd=2 -bsau <din secret key>.
```
Kjør kommandoen.
```
 gpg --status-fd=2 -bsau <din secret key>
```
Der fikk jeg opp `[GNUPG:] BEGIN_SIGNING H8` og ikke noe mer. Det tyder på at
kommandoen har hengt seg opp.
For å kille kommandoen, kjør
```
gpgconf --kill gpg-agent
```
Etter det funket gpg-signering til git igjen.
