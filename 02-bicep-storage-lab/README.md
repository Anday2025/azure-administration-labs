## Skjermbilder

### 1. Bicep-kode
Bicep-malen definerer Storage Account, parametere, ressursmerking og sikkerhetsinnstillinger.

![Bicep-kode](screenshots/01-bicep-code.png)

### 2. Bicep Build
Bicep-filen kompileres til en ARM-mal (`main.json`) med Azure CLI.

![Bicep Build](screenshots/02-bicep-build.png)

### 3. Validering
Azure validerer malen før utrulling. Resultatet viser `Succeeded`.

![Bicep Validation](screenshots/03-bicep-validation.png)

### 4. What-If
What-If sammenligner Bicep-koden med eksisterende Azure-ressurser uten å endre dem. Resultatet viser `1 no change, 4 to ignore`.

![Bicep What-If](screenshots/04-bicep-what-if.png)

### 5. Utrulling
Utrullingen ble gjennomført med Azure CLI. Resultatet viser `Succeeded`.

![Bicep Deployment](screenshots/05-bicep-deployment.png)

### 6. Storage Account Overview
Lagringskontoen er opprettet i Norway East med Standard_LRS, StorageV2 og taggen `Environment: Learning`.

![Storage Account Overview](screenshots/06-storage-account-overview.png)

### 7. Sikkerhetsinnstillinger
HTTPS er påkrevd, anonym Blob-tilgang og Shared Key-tilgang er deaktivert, og minimum TLS-versjon er 1.2.

![Storage Security](screenshots/07-storage-security.png)
