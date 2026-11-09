# Azure Bicep – Infrastructure as Code og automatisert utrulling

**Praktisk Azure-prosjekt | AZ-104 – Azure Administrator**

## 1. Prosjektoversikt

I dette prosjektet har jeg brukt Azure Bicep og Azure CLI til å opprette, konfigurere og oppdatere en Azure Storage Account ved hjelp av Infrastructure as Code (IaC).

Prosjektet viser hvordan Azure-ressurser kan administreres med kode i stedet for å konfigureres manuelt i Azure Portal.

**Prosjektmål:**

- Skrive en Bicep-mal med parametere og ressursdefinisjoner.
- Kompilere Bicep til en ARM-mal.
- Validere konfigurasjonen før utrulling.
- Bruke What-If til å forhåndsvise ressursendringer.
- Opprette og oppdatere en Storage Account med Azure CLI.
- Konfigurere sikkerhetsinnstillinger og ressursmerking gjennom kode.
- Kontrollere idempotens ved gjentatt utrulling.
- Dokumentere resultatet og ivareta kostnadskontroll.

## 2. Teknologier

| Teknologi | Formål |
|---|---|
| Microsoft Azure | Skyplattform |
| Azure Bicep | Infrastructure as Code (IaC) |
| Azure CLI | Administrasjon og automatisert utrulling |
| Azure Resource Manager (ARM) | Ressursadministrasjon og utrullingsmotor |
| Azure Cloud Shell (Bash) | Kommandolinjemiljø |
| Azure Storage Account | Ressurs som opprettes og administreres |
| GitHub | Versjonskontroll og prosjektdokumentasjon |

## 3. Gjennomføring

Prosjektet ble gjennomført i følgende rekkefølge:

1. Opprettet prosjektmappen og filen `main.bicep`.
2. Definerte parametere for region og Storage Account-navn.
3. Konfigurerte StorageV2, Standard_LRS og sikkerhetsinnstillinger.
4. Kompilerte Bicep-filen til en ARM-mal (`main.json`).
5. Validerte malen mot ressursgruppen `AzureLab`.
6. Brukte What-If til å kontrollere planlagte endringer.
7. Opprettet Storage Account `stbicepanday2026` gjennom Azure CLI.
8. Verifiserte resultatet i Azure Portal.
9. Oppdaterte Bicep-malen med taggen `Environment: Learning`.
10. Gjennomførte en ny utrulling og kontrollerte idempotens med What-If.

## 4. Konfigurasjon av Storage Account

| Innstilling | Verdi |
|---|---|
| Ressursgruppe | AzureLab |
| Region | Norway East |
| Performance | Standard |
| Redundancy | LRS |
| Account kind | StorageV2 |
| Secure transfer required | Enabled |
| Anonymous Blob access | Disabled |
| Shared Key access | Disabled |
| Minimum TLS version | TLS 1.2 |
| Ressurstagg | Environment: Learning |

Sikkerhetsinnstillingene er definert direkte i Bicep-koden, slik at konfigurasjonen kan gjenskapes på en konsistent måte.

## 5. Infrastructure as Code med Bicep

Prosjektets kildekode ligger i filen [main.bicep](main.bicep).

Bicep-filen bruker parametere for å gjøre løsningen gjenbrukbar.

- `param location` angir Azure-regionen.
- `param storageAccountName` bestemmer navnet på lagringskontoen.
- `resource storageAccount` definerer Azure-ressursen.
- `sku` og `kind` bestemmer lagringstype og redundans.
- `properties` definerer sikkerhetsinnstillingene.
- `tags` brukes til ressursmerking.

## 6. Azure CLI-kommandoer

Kommandoene kjøres fra prosjektmappen i Azure Cloud Shell (Bash). Eksemplene forutsetter at riktig Azure-abonnement er valgt.

### 6.1 Kompilere Bicep

```bash
az bicep build --file main.bicep
```

Kompilerer Bicep-filen til en ARM-mal (`main.json`).

### 6.2 Validere utrulling

```bash
az deployment group validate \
  --resource-group AzureLab \
  --template-file main.bicep \
  --parameters storageAccountName=stbicepanday2026 \
  --output table
```

Kontrollerer malen mot Azure før utrulling.

### 6.3 Forhåndsvise endringer med What-If

```bash
az deployment group what-if \
  --resource-group AzureLab \
  --template-file main.bicep \
  --parameters storageAccountName=stbicepanday2026
```

Viser hvilke ressursendringer Azure planlegger å utføre, uten å gjennomføre dem.

### 6.4 Gjennomføre utrulling

```bash
az deployment group create \
  --resource-group AzureLab \
  --template-file main.bicep \
  --parameters storageAccountName=stbicepanday2026 \
  --output table
```

Oppretter eller oppdaterer Storage Account i ressursgruppen.

### 6.5 Kontrollere idempotens

```bash
az deployment group what-if \
  --resource-group AzureLab \
  --template-file main.bicep \
  --parameters storageAccountName=stbicepanday2026
```

Etter vellykket utrulling viste What-If `1 no change, 4 to ignore`. Dette bekreftet at den administrerte lagringskontoen samsvarte med Bicep-malen.

## 7. Resultat

Jeg har opprettet og oppdatert en Azure Storage Account ved hjelp av Bicep og Azure CLI.

**Resultatene fra testene:**

| Kontroll | Resultat |
|---|---|
| Bicep Build | Vellykket |
| Template Validation | Succeeded |
| Azure Deployment | Succeeded |
| Sikkerhetskonfigurasjon | Verifisert i Azure Portal |
| Ressursmerking | Environment: Learning |
| Idempotens | 1 no change, 4 to ignore |

Prosjektet viser hvordan kodebasert ressursadministrasjon kan gi en repeterbar konfigurasjon og gjøre det enklere å kontrollere endringer.

## 8. Skjermbilder og dokumentasjon

### 8.1 Bicep-kode

Bicep-malen med parametere, ressursdefinisjon, sikkerhetsinnstillinger og ressursmerking.

![Bicep-kode](screenshots/01-bicep-code.png)

### 8.2 Bicep Build

Kompilering av `main.bicep` til `main.json` med Azure CLI.

![Bicep Build](screenshots/02-bicep-build.png)

### 8.3 Validering

Validering av Bicep-malen mot Azure. Resultatet viser `Succeeded`.

![Bicep Validation](screenshots/03-bicep-validation.png)

### 8.4 What-If

Kontroll av eksisterende ressurser. Resultatet viser `1 no change, 4 to ignore`.

![Bicep What-If](screenshots/04-bicep-what-if.png)

### 8.5 Azure Deployment

Vellykket utrulling med Azure CLI og resultatet `Succeeded`.

![Bicep Deployment](screenshots/05-bicep-deployment.png)

### 8.6 Storage Account Overview

Oversikt over lagringskontoen, inkludert region, redundans, status og taggen `Environment: Learning`.

![Storage Account Overview](screenshots/06-storage-account-overview.png)

### 8.7 Sikkerhetsinnstillinger

Konfigurasjon av HTTPS, anonym Blob-tilgang og Shared Key-tilgang.

![Storage Security](screenshots/07-storage-security.png)

## 9. Kostnadskontroll og opprydding

Prosjektet er gjennomført med abonnementet Azure for Students.

Jeg har konfigurert et Azure-budsjett med kostnadsvarsler for å følge med på ressursbruken.

Etter at prosjektet er dokumentert, skal testressursen `stbicepanday2026` slettes for å unngå unødvendige kostnader.

Andre ressurser i `AzureLab`, inkludert Cloud Shell-lagringen, skal beholdes.

## 10. Hva jeg har lært

Gjennom prosjektet har jeg fått praktisk erfaring med:

- Infrastructure as Code og Bicep.
- Forskjellen mellom deklarativ ressurskonfigurasjon og manuell administrasjon.
- Azure CLI og Cloud Shell.
- Validering og What-If før utrulling.
- Opprettelse og oppdatering av Azure-ressurser.
- Sikkerhetskonfigurasjon gjennom kode.
- Idempotens og repeterbar infrastruktur.
- Dokumentasjon, versjonskontroll og kostnadskontroll.

Prosjektet er en del av min praktiske kompetanseutvikling innen Azure-administrasjon, Cloud Engineering og IT-drift.
