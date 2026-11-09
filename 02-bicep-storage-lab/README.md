
# Azure Bicep Storage Lab

Praktisk Azure-prosjekt der jeg bruker Infrastructure as Code (IaC) med Bicep og Azure CLI til å opprette, konfigurere og oppdatere en Azure Storage Account.

## Teknologier

- Microsoft Azure
- Azure Bicep
- Azure CLI
- Azure Resource Manager (ARM)
- Azure Cloud Shell (Bash)

## Hva jeg har gjennomført

1. Opprettet en Bicep-fil (`main.bicep`).
2. Kompilert Bicep-koden med Azure CLI.
3. Validert utrullingen mot Azure.
4. Brukt What-If for å forhåndsvise endringer.
5. Opprettet en Storage Account med Bicep.
6. Kontrollert sikkerhetsinnstillingene i Azure Portal.
7. Oppdatert ressursen med taggen `Environment = Learning`.
8. Kontrollert idempotens med What-If.

## Konfigurasjon

| Innstilling | Verdi |
|---|---|
| Region | Norway East |
| Performance | Standard |
| Redundancy | LRS |
| Account kind | StorageV2 |
| Secure transfer | Enabled |
| Anonymous Blob access | Disabled |
| Shared Key access | Disabled |
| Minimum TLS | TLS 1.2 |

## Azure CLI-kommandoer

### Kompilere Bicep
```bash
az bicep build --file main.bicep
```

### Validere utrulling
```bash
az deployment group validate \
  --resource-group AzureLab \
  --template-file main.bicep \
  --parameters storageAccountName=stbicepanday2026
```

### Forhåndsvise endringer
```bash
az deployment group what-if \
  --resource-group AzureLab \
  --template-file main.bicep \
  --parameters storageAccountName=stbicepanday2026
```

### Gjennomføre utrulling
```bash
az deployment group create \
  --resource-group AzureLab \
  --template-file main.bicep \
  --parameters storageAccountName=stbicepanday2026
```

## Resultat

Jeg har opprettet og oppdatert en Azure Storage Account ved hjelp av Bicep og Azure CLI.

Etter utrullingen kontrollerte jeg sikkerhetsinnstillingene i Azure Portal.

En ny What-If-kjøring viste `NoChange` for lagringskontoen, som bekreftet at konfigurasjonen allerede samsvarte med Bicep-filen.

## Kostnadskontroll

Prosjektet bruker Azure for Students. Jeg har opprettet et kostnadsbudsjett med varsler og planlegger å slette testressursen etter at øvelsen er dokumentert.
