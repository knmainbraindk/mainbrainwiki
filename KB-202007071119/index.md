---
title: "Opsætning af Keepit Office365-backup"
zid: "KB-2007071119"
---

## Forudsætninger

1. En dedikeret backup-konto skal eksistere i kundens tenant.
2. Kontoens følger formen **office365backup**@contoso.com
    - Findes en eksisterende konto backup-konto med et andet navn, skal denne omdøbes, så vi ikke har 117 variationer over dette tema.
    - I denne vejledning anvendes kontonavnet "office365backup@contoso.com" som betegnelse for den kundespecifikke konto
3. Kontoen skal være enten være tildelt globale administrator-rettigheder i tenant'en, eller skal være tildelt administrator-rettigheder til den/de tjenester, der ønskes backup af.

## Trinvis opsætning

1. Opret en Office365-sikkerhedsgruppe med navn "SEC_Office365Backup_Keepit"
2. Tildel relevante brugere medlemskab af denne gruppe - se eventuelt eksisterende Cloudfinder-opsætning for hvilke brugere, der er tilvalgt for backup.
3. Log ind med administrator-adgang til Keepit [https://ws.keepit.com](https://ws.keepit.com)
4. Tilføj en ny under-konto med følgende indstillinger:
    - Role: Master Administrator
    - Product: O365 Total
    - Language: Engelsk / Dansk
    - Name: Navn på kundens virksomhed / organisation
    - Email: office365backup@contoso.com
    - Password: Sikker adgangskode, der **ikke** indeholder varianter over kundens navn/organisation
    - Phone: Efterlades tom
5. Afslut med "Gem" for at oprette brugeren, eller "Luk" for at annullere.
6. Skift til privat / incognito browser-vindue (eller anden browser) og foretag log ind med office365backup@contoso.com
7. I boks "Backup your connectors", som vises ved login, sæt flueben i "Don't show me this again", og vælg "Close"
8. Vælg "Add > Office 365 Admin"
9. Connector name: "Office365 all services" e.l. for connectors beregnet på alle tjenester. Navngiv ellers efter, hvad den pågældende connector forbinder til (f.eks. Sharepoint). Vælg "Next" for at fortsætte
10. Office365-login prompt: Log ind med office365backup@contoso.com
11. Boks vises med tilladelsesanmodning for app "Keepit (Admin 2.0)". Vælg "Accept" i bunden af boksen.
12. "Configuration for Office365 all services": Sæt flueben ud for alle tjenester
13. "Select accounts for Office 365":
    - Vælg "Load groups"
    - Fold "Security Groups" ud og vælg "SEC_Office365Backup_Keepit"
14. Afslut ved at klikke "Save".