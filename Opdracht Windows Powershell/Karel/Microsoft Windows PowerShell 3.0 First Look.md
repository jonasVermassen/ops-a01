### CIM Gebruiken


Windows Management Instrumentation (WMI) is een infrastructuur ingebouwd in
Windows die automatisering van het systeem mogelijk maakt. WMI is
gebaseerd op het Common Information Model (CIM), die voorwerpen te bepalen
binnen een computersysteem met behulp van een gemeenschappelijk model.
WMI is dus de implementatie van CIM.

#### Introductie tot het CIM IDE

Visual Studio is een zeer uitbreidbare ontwikkelingomgeving. De kern van het systeem is
gebouwd op een idee van de diensten die gemakkelijk ingeschakeld of uitgeschakeld kunnen worden.

De CIM IDE is gebaseerd op dit model en is gemakkelijk te gebruiken in Visual Studio.

Zodra de extensie is geïnstalleerd, hebben wij toegang tot twee nieuwe projecttypes in Visual Studio.
Het eerste projecttype is CIM Authoring en is belast met het definiëren van het WMI model interface die wordt gebruikt door PowerShell. Het tweede type is CIM Providers,dat is verantwoordelijk voor de uitvoering van de interface gegenereerd
door de eerste. De volgende screenshot legt dit uit:


![CIM in Visual Studio](http://i.imgur.com/0utAslZ.jpg)


In een CIM Authoring project wordt de WMI-interface  gedefinieerd met behulp van een standaard formaat aangeduid als de Managed Object Format (MOF). MOF-bestanden zijn eenvoudig geschreven C bronbestanden, die
zorgen voor de metadata zoals eigenschappen, methoden en gebeurtenissen van een WMI
objecten provider. De CIM IDE biedt syntax higlighting en IntelliSense ondersteuning
voor MOF bestanden. De volgende screenshot toont een CIM_Error MOF-bestand:


![CIM Error MOF bestand](http://i.imgur.com/zEw721f.jpg)


De MOF-indeling is een specificatie ontworpen door de Distributed Management Task
Force (DMTF). De DMTF werkt aan standaarden voor het gedistribueerde beheer
van computersystemen. Door standaard manieren voor het communiceren binnen een
gedistribueerde organisatie te hebben is het makkelijker om de interoperabiliteit tussen systemen te waarborgen.


De CIM IDE biedt een vereenvoudigde, read-only weergave van het MOF-bestand in een aangepaste
designer: 


![CIM IDE](http://i.imgur.com/74JyQJp.jpg)


#### Implementeren van een eenvoudige WMI provider

In het volgende voorbeeld, zullen we de MOF genereren, kunt u het skelet voor een
provider uit scratch.Het doel van deze provider is een lijst van de aangesloten netwerkstations aan te bieden en een manier om ze van elkaar los te koppelen.

De eerste stap van het creëren van onze nieuwe WMI-provider is het maken van de MOF.
We moeten een nieuwe CIM Authoring project maken.

Dit kan gedaan worden door te klikken op **Menu** en het selecteren van **File** en daarna **New Project**. Zodra dit
gedaan is, kunnen we een nieuw MOF-bestand toevoegen aan het project om onze klasse (WIN32_NetworkDrive) te definiëren. Dit wordt getoond in de volgende screenshots:

![CIM Class](http://i.imgur.com/PQxz7Sq.jpg)


![CIM Network Drive](https://i.gyazo.com/9f39f6f1018d3f0e299ed86b244e1bf4.png)


#### Toevoegen van een CIM Provider project

Nu dat we de definitie van onze provider geschreven hebben, kunnen we de code genereren
voor het framework van de provider. Om dit te doen moeten we eerst
een nieuw project maken binnen onze oplossing.
Het project moet er zo uitzien:

![CIM Explorer](https://i.gyazo.com/c837c1256488caf1f6218e730a11ed4e.png)


#### De implementatie details

1. Selecteer de klas WIN32_NetworkDrive.
2. Klik op de **Generate Code** knop op de werkbalk van het CIM Explorer
window.
3. Selecteer de opties die we willen gebruiken in het Generate Provider venster.

Het venster **Generate Provider** laat ons ook het project selecteren waarin we de uitvoering van de provider zullen schrijven.
Dit wordt getoond in de volgende screenshot:

![CIM Generate Provider](https://i.gyazo.com/9e959172fc958daa3da1ef80180a20a3.png)


De CIM IDE direct produceert verschillende headers en bronbestanden. Open
de inhoud van een van deze bestanden:

![CIM ND.c](https://i.gyazo.com/28f78b060c6dbd64f9dbaabf0be06deb.png)


#### PowerShell metadata genereren

1. Klik met de rechtermuisknop op de klasse **WIN32_NetworkDrive** in het venster **CIM Explorer**.
2. Klik op de **Add PowerShell Metadata** optie in het menu.
3. **Add PowerShell Metadata** venster wordt getoond.

Merk op dat het bestand een CDXML bestand is. Een
CDXML bestand is een XML-bestand opgebouwd uit alle metadata die nodig is voor
PowerShell cmdlets te genereren:

![CIM Metadata](https://i.gyazo.com/06d53d74db2cbe0643ee789fe1acf95b.png)


Het bestand vraagt om de mappings tussen cmdlets en de WMI.Het editor venster wordt in de
volgende screenshot getoont:

![CIM Editor](https://i.gyazo.com/88e7f7a202d0ca97a3934d7267bb447d.png)


De editor laat ons toe om cmdlets op te geven voor het opvragen van bestaande exemplaren. Zodra we
de eigenschappen van de klasse CIM toegewezen hebben aan de parameters of de methoden van
de cmdlets, krijgen we een CDXML bestand dat de informatie bevat
voor het maken van cmdlets.

#### Een WMI-provider registreren

```PowerShell
PS C:\> Register-CimProvider –help
```

De output:

![CIM Register](https://i.gyazo.com/5ad93cf21ef6b18731ea3a717ac33355.png)


Bij het registreren van een CIM provider, zijn er drie parameters vereist
door **Register-CimProvider**. Deze omvatten **Namespace, Path** en **ProviderName**.

```PowerShell
PS C:\> Register-CimProvider -Namespace Root\WIN32 -ProviderName
WIN32NetworkDriveProvider -Path "NetworkDriveProviderImpl.dll"
```
Successfully registered the provider.

Toegang met **Get-CimClass**

```PowerShell
PS C:\ > Get-CimClass -ClassName Win32_NetworkDrive -Namespace Root\WIn32
```

Een provider uitschrijven wordt zo gedaan:

```PowerShell
PS C:\> mofcomp "WIN32NetworkDriveProviderUninstall.mof"
```

![CIM mofcomp](https://i.gyazo.com/689b21ff12650f5e40232dfc731a8843.png)


#### Het automatisch maken van provider cmdlets

```PowerShell
PS C:\> Import-Module "C:\PS_WIN32_NetworkDrive.cdxml" -Verbose
```
VERBOSE: Importing function 'Disconnect-WIN32NetworkDrive'.
VERBOSE: Importing function 'Get-WIN32NetworkDrive'.


#### Cmdlet verschillen tussen CIM en WMI

```PowerShell
PS C:\> Get-Command -Module CimCmdlets
```

![CIM CIM Verschil](https://i.gyazo.com/a8ef70f0687b963df910cb70f52cf12e.png)

```PowerShell
PS C:\> Get-Command *WMI* -Type Cmdlet
```

![CIM WMI Verschil](https://i.gyazo.com/34fca2141383cba9e4dde28fc48ff7bb.png)

