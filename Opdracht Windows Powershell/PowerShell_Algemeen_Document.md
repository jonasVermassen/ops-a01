#Windows Powershell

##Inhoudstafel
1. [Help-systeem](#1)
2. [Gebruiken van commands](#2)
3. [Werken met providers](#3)
4. [De pipeline](#4)
5. [Objects](#5)
6. [Formatting output](#6)
7. [Filteren + Werken met files](#7)
8. [Remoting](#8)
9. [Variabelen](#9)
10. [PowerShell ISE](#10)
11. [Scripting](#11)
12. [Errors afhandelen](#12)
13. [Gebruik maken van de CIM](#13)
14. [Verbetering van Tab Completion](#14)
15. [Plannen van jobs](#15)
16. [Server Roles en Features Configureren](#16)
17. [Beheer Active Directory met PowerShell](#17)
18. [Beheer van een server met PowerShell](#18)
19. [Beheer van Exchange server](#19)

<div id='1'/>
##Help-systeem
### Updateable Get-Help

Het microsoft powershell help systeem laat je toe commando's, en informatie over die commando's te ontdekken. Dit doe je door in de console het cmdlet Get-Help te gebruiken. 

Powershell ondergaat vaak updates om het uit te breiden, het te verbeteren enzovoort, ook het Get-Help of help cmdlet wordt vaak geupdate. Het is een goede gewoonte om geregeld het volgende commando uit te voeren. 

```PowerShell
PS C:\> update-help
```

Dit commando zal, zoals je al kan raden, zorgen dat de output die je krijgt van dit commando up to date is. 

### Get-Help Gebruiken

Zoals eerder gezegd kan je met het Get-Help commando informatie ontdekken over een commando dat je al kent, of een voor jou onbekend commando ontdekken. Met Get-Help vind je commando's en wordt je uitgelegd hoe je ze kan gebruiken. 

Stel. Je wil alle services die op je machine draaien te zien krijgen, en je weet het cmdlet daarvoor: Get-Service. Maar je weet niet hoe het te gebruiken. Get-Help staat paraat. Geef het Get-Help Commando in, gevolgd door het cmdlet waar je informatie over wil. Een voorbeeld:

```PowerShell
PS C:\> Get-Help Get-Service
```

Het Get-Help commando kan eigenlijk nog korter geschreven worden, men noemt dit aliasing. Het afgekorte cmdlet of alias voor Get-Help, is gewoon Help. 
De volgende twee voorbeelden geven dus exact dezelfde output terug:

```PowerShell
PS C:\> Get-Help Get-Service
```

```PowerShell
PS C:\> Help Get-Service
```

We hebben gezien hoe we Get-Help gebruiken als we het commando waarover we informatie willen al kennen, maar wat als we dit commando nog niet kennen?
Stel. Je wil iets doen met logs van je machine, eender wat. Dan heb je één sleutelwoord: 'log'. Het volgende commando zal alles teruggeven waar het woord 'log' in voorkomt. 

```PowerShell
PS C:\> Help *log*
```

Maar waarom? De twee * rond het woord log betekenen dat eender welke tekst mag voorkomen. Moest er dus een functie: 'kazeazloglazdj' bestaan, zou het teruggegeven worden in de output. Natuurlijk bestaat die functie niet, de effectie output van het commando ziet er als volgt uit:

```PowerShell
Name                              Category  Module                    Synopsis                                                       
----                              --------  ------                    --------                                                       
Clear-EventLog                    Cmdlet    Microsoft.PowerShell.M... Deletes all entries from specified event logs on the local o...
Get-EventLog                      Cmdlet    Microsoft.PowerShell.M... Gets the events in an event log, or a list of the event logs...
Limit-EventLog                    Cmdlet    Microsoft.PowerShell.M... Sets the event log properties that limit the size of the eve...
New-EventLog                      Cmdlet    Microsoft.PowerShell.M... Creates a new event log and a new event source on a local or...
Remove-EventLog                   Cmdlet    Microsoft.PowerShell.M... Deletes an event log or unregisters an event source.           
Show-EventLog                     Cmdlet    Microsoft.PowerShell.M... Displays the event logs of the local or a remote computer in...
Write-EventLog                    Cmdlet    Microsoft.PowerShell.M... Writes an event to an event log.                               
Get-AppxLog                       Function  Appx                      ...                                                            
Export-BinaryMiLog                Cmdlet    CimCmdlets                Export-BinaryMiLog...                                          
Import-BinaryMiLog                Cmdlet    CimCmdlets                Import-BinaryMiLog...                                          
New-AutologgerConfig              Function  EventTracingManagement    ...                                                            
Get-AutologgerConfig              Function  EventTracingManagement    ...                                                            
Set-AutologgerConfig              Function  EventTracingManagement    ...                                                            
Start-AutologgerConfig            Function  EventTracingManagement    ...                                                            
Remove-AutologgerConfig           Function  EventTracingManagement    ...                                                            
Get-DtcLog                        Function  MsDtc                     ...                                                            
Reset-DtcLog                      Function  MsDtc                     ...                                                            
Set-DtcLog                        Function  MsDtc                     ...                                                            
Get-LogProperties                 Function  PSDiagnostics             ...                                                            
Set-LogProperties                 Function  PSDiagnostics             ...                                                            
Start-StorageDiagnosticLog        Function  Storage                   ...                                                            
Stop-StorageDiagnosticLog         Function  Storage                   ...                                                            
Get-WindowsUpdateLog              Function  WindowsUpdate             ...                                                            
about_Eventlogs                   HelpFile                            Windows PowerShell creates a Windows event log that is         
about_Logical_Operators           HelpFile                            Describes the operators that connect statements in Windows P...
```


### Get-Help Output Interpreteren

Hierboven zag je al een output van een Get-Help cmdlet. Je ziet vier kolommen. Van links naar rechts zie je de eerst de synopsis. Dit geeft een korte samenvatting weer. Als tweede heb je de module, hier gaan we later dieper op in. De middelste kolom geeft de categorie aan. Dit kan een cmdlet zijn (zoals Get-Help) of een functie, een bestand,.. In de Linker kolom staat de naam, hierin staat - je raadt het - de naam. 

Stel. Je wilt de EventLog legen, je voerde het help cmdlet in en je kreeg de ouput hierboven weer. Nu zoek je in de lijst van commando's en ziet het commando Clear-Eventlog, dit zou wel een kunnen doen wat je willen. Je wilt meer informatie over dit commando, dus gebruik je Help: 

```PowerShell
PS C:\> Help Clear-EventLog
```

Nu krijg je gedetailleerde uitleg over dat commando zelf. Dit is de output: 

```PowerShell
NAME
    Get-EventLog
    
SYNOPSIS
    Gets the events in an event log, or a list of the event logs, on the local or remote computers.
    
    
SYNTAX
    Get-EventLog [-LogName] <String> [[-InstanceId] [<Int64[]>]] [-After [<DateTime>]] [-AsBaseObject] [-Before [<DateTime>]] [-Compu
    terName [<String[]>]] [-EntryType {Error | Information | FailureAudit | SuccessAudit | Warning}] [-Index [<Int32[]>]] [-Informati
    onAction {SilentlyContinue | Stop | Continue | Inquire | Ignore | Suspend}] [-InformationVariable [<System.String>]] [-Message [<
    String>]] [-Newest [<Int32>]] [-Source [<String[]>]] [-UserName [<String[]>]] [<CommonParameters>]
    
    Get-EventLog [-AsString] [-ComputerName [<String[]>]] [-InformationAction {SilentlyContinue | Stop | Continue | Inquire | Ignore 
    | Suspend}] [-InformationVariable [<System.String>]] [-List] [<CommonParameters>]
    
    
DESCRIPTION
    The Get-EventLog cmdlet gets events and event logs on the local and remote computers.
    
    Use the parameters of Get-EventLog to search for events by using their property values. Get-EventLog gets only the events that ma
    tch all of the specified property values.
    
    The cmdlets that contain the EventLog noun (the EventLog cmdlets) work only on classic event logs. To get events from logs that u
    se the Windows Event Log technology in Windows Vista and later versions of Windows, use Get-WinEvent.
    
RELATED LINKS
    Online Version: http://go.microsoft.com/fwlink/p/?linkid=290493 
    Clear-EventLog 
    Limit-EventLog 
    New-EventLog 
    Remove-EventLog 
    Show-EventLog 
    Write-EventLog 
REMARKS
    To see the examples, type: "get-help Get-EventLog -examples".
    For more information, type: "get-help Get-EventLog -detailed".
    For technical information, type: "get-help Get-EventLog -full".
    For online help, type: "get-help Get-EventLog -online"
```
####Required en Optional Parameters

Name en Synopsis spreekt voor zichzelf en zagen we al eerder. Een belangrijk onderdeel is Syntax. Hierin wordt gedefinieerd hoe je commando er syntactisch moet uitzien. Hoe het er zal uitzien hangt af van het aantal parameters dat je gebruikt. Een Parameter is een stuk informatie dat je meegeeft aan je commando, omdat het commando die informatie nodig heeft. 

Als we kijken naar het syntax onderdeel van de ouput, zie je dat de eerste parameter van het Get-EventLog cmdlet -LogName is, en het van het type String moet zijn. de [vierkante haakjes rond -LogName] duiden erop dat dit onderdeel van de parameter optioneel is. De kleiner en groter dan tekens < > rond String duiden erop dat dit het type moet zijn van de parameter -LogName, hier staan echter wél [vierkante haakjes rond], wat wil zeggen dat de waarde van de parameter verplicht is in te geven. Ook merk je dat rond het geheel geen [vierkante haakjes staan], wat wil zeggen dat deze parameter verplicht mee te geven is bij het uitvoeren van het Get-EventLog cmdlet. 


De tweede parameter is -InstanceId, dit is een optionele parameter. Dit zie je omdat hier wél [vierkante haakjes rond het geheel staan]. Het type hiervan is, zoals we kunnen zien een <Int64[]>. Er staan echter nog twee vierkante haakjes na Int64. Dit wil zeggen dat de parameter een array mag zijn, waarbij elk element in de array van het type Int64 is. 

Aan de hand van de gegeven informatie kan je de volgende parametersyntax zelf begrijpen. Een extra is dat als je (zoals bij de parameter -EntryType) ziet dat er verschillende types gescheiden worden door |, je maximum van deze types mag en moet selecteren. Daar | vertaald kan worden door 'of'. 

De onderdelen Description, Related Links en Remarks spreken voor zichzelf.

####Positional Parameters

Positionele parameters zijn parameters waarvan men weet dat ze heel erg vaak gebruikt worden, hierbij vereist men niet meer dat de naam van de parameter gevolgd wordt door de waarde van de parameter. Maar enkel de waarde volstaat. Hieronder enkele voorbeelden van het gebruik van parameters. De eerste parameter van Get-EventLog is een positionele parameter. Hier zie je enkele voorbeelden van het gebruik van parameters: 


De Volgende twee commands geven dezelfde uitvoer, -Logname is een positionele parameter, de naam van de parameter is dus optioneel. 

```PowerShell
PS C:\> Get-EventLog -Logname System
```

```PowerShell
PS C:\> Get-EventLog System
```

####Voorbeelden

Hier specifiëren we de optionele parameter -After, de waarde van deze parameter is van het type datetime, hier worden dus alle System EventLogs van na 4 mei 2014 getoond. 

```PowerShell
PS C:\> Get-EventLog System -After 5/4/2014
```

Hier voegen we de extra parameter InformationAction toe, in de help output zie je dat we keuze hebben tussen de waarden: SilentlyContinue, Stop, Continue, Inquire, Ignore of Suspend.

```PowerShell
PS C:\> Get-EventLog System -After 5/4/2014 -InformationAction Stop
```

Het is aan te raden zelf te oefenen met het Get-Help cmdlet, om het zo goed onder de knie te krijgen. Het zal je helpen in de volgende hoofdstukken van dit boek, en om zelf meer te ontdekken over de mogelijkheden van powershell. 


<div id='2'/>
##Gebruiken van commands

In dit hoofdstuk gaan we niet programmeren of scripten, maar commands uitvoeren.
PowerShell is zeer vergelijkbaar met Cmd.exe, de standaard Command Line Interface van Windows systemen, en Unix shells, zoals Bash, maar veel moderner.
Dus qua interface komt het sowieso bekend voor.

###De structuur van een command

De onderstaande afbeelding toont de basis structuur van een complexer PowerShell command.

![structuur](https://i.gyazo.com/16e542ced76bd1ea45bbd0315c3ea193.png)

Om het wat duidelijker te maken zullen we de onderdelen meer gedetaileerd bekijken:
* De cmdlet die hier wordt gebruikt is Get-Eventlog, op cmdlets komen we later terug.
* De eerste parameter is -LogName, met als waarde Security (de waarde bevat geen spaties of punten, dus moet het niet tussen aanhalingstekens)
* De tweede parameter is -Computername, deze heeft 2 waarden, gescheiden door een komma
* De derde parameter is -Verbose, dit is een switch-parameter, dat wil zeggen dat het geen waarde nodig heeft

Parameters starten altijd met een '-' en er is geen spatie tussen de '-'en de parameter.
Niets is ook hoofdlettergevoelig.

###Commands vergemakkelijken

PowerShell heeft ook afkortingen voor verscheidene cmdlets.
Om deze te vinden gebruiken we het commando "get-alias"
Voorbeeld:
```Powershell
PS C:\> get-alias -Definition "Get-Service"
Capability Name
---------- ----
Cmdlet gsv -> Get-Service
```
Hier zien we dat we "gsv" kunnen gebruiken in plaats van "get-service".

PowerShell verplicht u bovendien niet om uw commands volledig uit te typen.
Bijvoorbeeld kan men gewoon "-comp" gebruiken in plaats van de volledige parameter "-computerName".
Er moeten wel genoeg letters staan zodat elke afkorting ook uniek is.
"-com" werkt bijvoorbeeld niet omdat er ook een parameter "-composite" is.

###Show-command

Als men problemen heeft met de syntax van een command, kan men de cmdlet "Show-Command" gebruiken.

![show command](https://i.gyazo.com/0ddaa346c3342605d117e47b0306c017.png)

De Show-Command cmdlet geeft een venster weer met al de parameters die men dan kan invullen van een cmdlet naar keuze.
In de afbeelding hierboven wou ik als logname Security, als computername localhost en daarvan wou ik de laatste 50 entries zien. Als men dan op run klikt maakt PowerShell het onderstaande command: 
```Powershell
PS C:\Users\Robin> Get-EventLog -LogName Security -ComputerName localhost -Newest 50
```




<div id='3'/>
##Werken met providers

Windows PowerShell providers laten je toe om dezelfde cmdlets, zoals Get-Item of Set-Item te gebruiken met verschillende types van data. Daardoor kan je meteen weten hoe je met verschillende data werkt. Bijvoorbeeld: je kan de Get-Item cmdlet gebruiken om informatie over een bestand te krijgen. U kunt echter de dezelfde cmdlet gebruiken om informatie over een alias, een certificaat, een functie, een omgevingsvariabele, een registersleutel of een variabele op te halen.

De Microsoft Active Directory provider
laat je toe om  cmdlets zoals Get-Item gebruiken om informatie te bekomen over een gebruiker, een computer of een ander object in  Microsoft Active Directory Domain Services (AD DS).

###Windows PowerShell providers

![ALt text](http://i.imgur.com/joQj5CQ.png)

###De Alias provider

Een alias is een snelkoppeling voor een cmdlet of voor een functie. Aliases maken gemakkelijker om interactief met Windows PowerShell te werken.

Hier zie je een voorbeeld waarbij de alias Processes gemaakt wordt voor de Get-Process cmdlet.

![ALt text](http://i.imgur.com/M8DUQI4.png)

###De Certificate provider
De Certificate provider geeft jou de mogelijkheid om scripts te signen en laat Windows PowerShel toe om met signed en unsigned scripts te gebruiken. Het geeft ook de mogelijkheid om certificaten te zoeken, te kopieëren, te verplaatsen en te verwijderen.

####Zoeken naar specifieke certificaten. 
Om specifiek te zoeken kan je de Subject property gebruiken. Aanschouw hieronder een voorbeeld.

![ALt text](http://i.imgur.com/PBEtMde.png)

###De Environment provider
De Environment  provider in Windows PowerShell biedt toegang tot de systeemomgevingsvariabelen. Als u een opdrachtprompt venster opent en Set typt, krijgt u een overzicht van alle variabelen van de Environment op het gedefinieerde systeem. 

![ALt text](http://i.imgur.com/D1ohyry.png)

###De File System provider

Wanneer Windows PowerShell wordt gestart, wordt het automatisch geopend op het station C: Powershell. Met behulp van de File System van Windows PowerShell-provider, kunt u zowel mappen als bestanden aanmaken. U kunt eigenschappen van bestanden en mappen ophalen, en u kunt ze ook verwijderen.

###De Function provider

De Function provider biedt toegang tot de functies die zijn gedefinieerd in Windows PowerShell. Met behulp van de functie-provider kunt u een lijst van alle functies op uw systeem ophalen. U kunt ook functies toevoegen, wijzigen en verwijderen.

![ALt text](http://i.imgur.com/sTL7Pkz.png)

###De Registry provider
De Registry provider maakt het gemakkelijk om te werken met de registry op het lokaal systeem.

####De twee registry drives
![ALt text](http://i.imgur.com/jED5QKL.png)

####Ophalen van registry waarden

Om de waarden die zijn opgeslagen in een registersleutel weer te geven, moet u het Get-Item of de cmdlet Get-ItemProperty gebruiken. Met de cmdlet Get-Item is één eigenschap (met de naam default), zoals in het volgende voorbeeld wordt getoond:

![ALt text](http://i.imgur.com/GKqEFIV.png)

####Nieuwe registry key maken

Het volgend voorbeeld creëert een nieuwe registry key met de naam Test in HKCU:\Software

![ALt text](http://i.imgur.com/s59CdZE.png)

###De Variable provider

De Varaible provider biedt toegang tot de variabelen die zijn gedefinieerd in Windows PowerShell. Deze variabelen omvatten zowel gebruiker gedefinieerde variabelen, zoals $mred, en de systeem gedefinieerde variabelen, zoals $host.

![ALt text](http://i.imgur.com/OhfX2xC.png)



<div id='4'/>
##De pipeline

De pipeline is een erg handige tool binnen powershell, het laat je toe de output van het initiële commando te bewerken. Hieronder zie je een voorbeeld van het cmdlet Get-Process. Stel nu dat je alle processen wilt, maar neerwaarts geordend op naam. Dan kan je dmv de output van het commando sorteren

```PowerShell
PS C:\> Get-Process 
```

```PowerShell
PS C:\> Get-Process | Sort Name –Descending 
```


###Bestanden exporten

Een handig gebruik van de pipeline is het exporteren van je output. Zo kan je het exporteren naar een CSV bestand, hieronder exporteren we alle processen naar een CSV bestand dat procs.csv heet. 

```PowerShell
PS C:\> Get-Process | Export-CSV procs.csv  
```

Exporteren naar en XML bestand is ook mogelijk, dat zie je hieronder. 

```PowerShell
PS C:\> Get-Process | Export-Clixml c:\scripts\test.xml
```

###Services beheren

De pipeline laat je toe services te starten, stoppen,.. Een mooi voorbeeld is het eerstvolgende. Eerst wil je een lijst van alle processen, vervolgens zal je op die lijst het Stop-Process cmdlet uitvoeren. Wat als resultaat heeft dat alle processen stopgezet kunnen worden. Voer dit commando dus zeker nooit uit.

```PowerShell
PS C:\> Get-Process | Stop-Process
```

Bekijk de volgende 3 voorbeelden en probeer te bepalen wat deze commando's zullen doen, als je een commando niet kent, gebruik dan Get-Help om er informatie over te vinden. 

```PowerShell
PS C:\> Get-Process -name Notepad | Stop-Process
```
```PowerShell
PS C:\> Get-Process Note* | Stop-Process
```
```PowerShell
PS C:\> Get-Service Browser | Restart-Service
```

### Pipeline input ByValue & ByPropertyName

Wat gebeurt bij een pipeline is dat het eerste commando een output doorgeeft aan het tweede commando. 

```PowerShell
PS C:\> Get-Content .\Documents\Computers.txt | Get-Service  
```

Hier geeft het eerste cmdlet (Get-Content) de inhoud van MyTextFile.txt door aan het tweede cmdlet (Get-Service). Maar wat als het eerste commando iets doorgeeft (een parameter) aan het tweede, waarmee de tweede niets aan kan vangen? Dan krijg je een error. 

Maar hoe kom je te weten welk type parameters een cmdlet kan accepteren via de pipeline? hier komt het cmdlet get-member goed van pas. Hier zie je een voorbeeld waarbij get-member gebruikt wordt. 

```PowerShell
PS C:\> Get-Content .\Documents\ Computers.txt | Get-Member


   TypeName: System.String

Name             MemberType            Definition                                                                                    
----             ----------            ----------                                                                                    
Clone            Method                System.Object Clone(),...                                     
CompareTo        Method                int CompareTo(),...
...				 ...				   ...
```

Je ziet aan de output dat het Get-Content commando een String teruggeeft (TypeName:System.String). Nu je dit weet ga je dieper kijken naar het tweede cmdlet, om te zoeken of het een parameter aanvaard die van het type String is. We gebruiken eerst de optie ByValue, waarmee het type String bedoelt wordt. Hiervoor gebruik je de full optie van het Get-Help cmdlet. Hier een voorbeeld

```PowerShell
PS C:\> Help Get-Service -full

...

-Name <String>
        Specifies the services to be retrieved. Wildcards are permitted. 
        By default, Get-Service gets all of the services on the computer.   
              
        Required?                    false
        Position?                    1
        Default value                All services
        Accept pipeline input?       true (ByValue, ByPropertyName)
        Accept wildcard characters?  true
        
...

```

Hier vind je, tussen de volledige output, bovenstaande output. Merk op dat het commando dus pipeline input aanvaard ByValue. Er is echter een probleem. We hebben te maken met de 'Name' Parameter, die 'Specifies the services to be retrieved'. We gaan dus geen computerNames terugkrijgen, maar service names. Dit is een veel voorkomende fout bij ByValue. ByValue is echter nog altijd erg handig, maar in gevallen als deze gaan we met ByPropertyName werken. 

Een nieuw voorbeeld, met ByPropertyName.

```PowerShell
PS C:\> Get-Service -Name s* | Stop-Process
```

Eerst kijken we naar de output van het eerste cmdlet, door het gebruik van Get-Member.

```PowerShell
PS C:\> Get-Service -Name s* | Get-Member


TypeName: System.ServiceProcess.ServiceController

Name                   MemberType    Definition                                                                                   
----                   ----------    ----------                                                                                   
Name                   AliasProperty Name = ServiceName                                                                           
RequiredServices       AliasProperty RequiredServices = ServicesDependedOn                                                        
...		               ...	         ...

```

We kijken echter niet langer naar de TypeName, maar of het cmdlet Get-Service een property heeft dat overeenkomt met een parameter van het cmdlet Stop-Process. We zien dat Get-Service een property Name heeft, en hieronder zie je dat Stop-Process een parameter met naam Name aanvaard.

```PowerShell
PS C:\> Get-Help Stop-Process -full

...

-Name <String[]>
        Specifies the process names of the processes to be stopped. You can type multiple process names (separated by commas) or use 
        wildcard characters.
        
        Required?                    true
        Position?                    named
        Default value                none
        Accept pipeline input?       true (ByPropertyName)
        Accept wildcard characters?  false
        
...
```

Je ziet ook dat het ByPropertyName mag zijn. Wat betekend dat dit zal werken. Test het commando echter niet uit, want je zal alle processen beginnend met een s stoppen, wat je natuurlijk niet wil doen. Je kan echter wel de whatif optie gebruiken. 


```PowerShell
PS C:\> Get-Service -Name s* | Stop-Service -WhatIf

What if: Performing the operation "Stop-Service" on target "Security Accounts Manager (SamSs)".
What if: Performing the operation "Stop-Service" on target "Smart Card (SCardSvr)".
...
...
```


<div id='5'/>
##Objects

Misschien heb je al van objecten gehoord, ze worden namelijk niet alleen in powershell gebruikt, maar ook in verschillende programmeertalen. Een object is een representatie van iets. Het bestaat uit verschillende delen, en het kan verschillende dingen. Dit is allemaal erg abstract, daarom een voorbeeld.

Als je volgend cmdlet runt, krijgt je de bijhorende output.

```PowerShell
PS C:\ Get-Service

Status   Name               DisplayName                           
------   ----               -----------                           
Stopped  AJRouter           AllJoyn Router Service                
Stopped  ALG                Application Layer Gateway Service     
Stopped  AppIDSvc           Application Identity
...		 ...	            ...
    
```

Een process is een object. Het heeft verschillende properties en methoden.
Hier zie je een aantal properties van bepaalde Services (Status, Name, DisplayName), er zijn er echter heel wat meer, die niet weergegeven worden. Basismethoden van processen zijn bevoorbeeld start en stop. 

In het volgende voorbeeld maken we een variabale aan en stoppen we er een proces in, genaamd XboxNetApiSvc. 

```PowerShell
PS C:\> $MyVar = Get-Service -Name XboxNetApiSvc
```

Vervolgens willen we weten wat de naam is van dit object. De naam wordt als volgt terug gegeven. Het is mogelijk om andere properties terug te geven met dezelfde methode.

```PowerShell
PS C:\> $var.Name
XboxNetApiSvc
```

Ook kan je methoden van het object oproepen. Je kan starten, stoppen, het type opvragen, en meer. Dit gebeurd als volgt. 

```PowerShell
PS C:\> $var.GetType()

IsPublic     IsSerial     Name                 BaseType                                                                  
--------     --------     ----                 --------                                                                  
True         False        ServiceController    System.ComponentModel.Component
```

Objecten is het gene wat windows powershell onderscheidt met bevoorbeeld een traditionele linux shell als bash. Het biedt veel mogelijkheden, en is op zich niet moeilijk te beheersen, het vraagt enkel wat tijd om het abstracte concept te begrijpen. 




<div id='6'/>
##Formatting output



Wanneer u met Windows PowerShell werkt, is het gebruikelijk om de output naar de console Windows PowerShell te schrijven met de gewilde opmaak. Dit is niet altijd een vereiste, maar vele Windows PowerShell-cmdlets omvatten hun eigen opgemaakte uitvoer. Bijvoorbeeld, de cmdlet Get-proces produceert een mooie tabel die gemakkelijk aan de behoeften voldoet. Af en toe, is het echter nodig voor de output aan te passen. In dit hoofdstuk vindt u informatie over het maken van tabellen, lijsten, brede lijsten en zelfs het gebruik van een selecteerbare rasterweergave.

###Creating a table
![ALt text](http://i.imgur.com/FZ2g9Ov.png)

###Creating a list
![ALt text](http://i.imgur.com/1Nc1cv8.png)

###Creating a wide display
![ALt text](http://i.imgur.com/vPuBsym.png)

###Creating an Out-GridView
![ALt text](http://i.imgur.com/HJyRd59.png)


<div id='7'/>
##Filteren + Werken met files

###Filtering & Sorting
Een van de taken waar Windows PowerShell in uitblinkt is inzicht bieden in gegevens. Dit houdt meestal verzenden van gegevens via de pipeline in. De Windows PowerShell-pipeline is een fundamenteel concept, en het is onlosmakelijk verbonden met het sorteren van gegevens, gegevens groeperen en filteren op specifieke informatie uit collecties. 

####Filtering

Bij filtering kan er gebruik gemaakt worden van de Where-Object cmdlet. Hierna kan je specifiëren op welke waarden je wilt filteren. In dit voorbeeld wordt "vm -gt 1000MB" gebruikt, dit wil zeggen alle objecten met als waarde voor VM groter dan 1000MB.

![ALt text](http://i.imgur.com/SZ8OnMh.png)

In onderstaand voorbeeld wordt er gebruik gemaakt van "-Match". Dit spreekt voor zich en zoekt alle objecten die voldoen aan de zoekstring.

![ALt text](http://i.imgur.com/XoBEvEP.png)


####Sorting
In onderstaande afbeelding wordt gebruik gemaakt van de cmdlet Sort-Object. Hier wordt Get-Process gesorteerd volgens de Property "VM" in aflopende volgorde.
![Alt text](http://i.imgur.com/AMwXKwv.png)

Hier wordt de alias "sort" gebruikt in plaats van de cmdlet Sort-Object.
![Alt text](http://i.imgur.com/UYWjUTg.png)

Er kan ook gebruik gemaakt worden van groeperen. Dan kan er gebruik gemaakt worden van "count", dit om het aantal objecten te tellen. Maar kan er ook gebruik gemaakt worden van "group", dit om een group te specifiëren.

![Alt text](http://i.imgur.com/Y3oDrwx.png)

###Working with files


####Storing data in text files
Bij onderstaand commando wordt de output van de cmdlet Get-Volume weggeschreven in c:\fso\volumeinfo.txt.

<code></code><code>PowerShell
Get-Volume >>c:\fso\volumeinfo.txt
</code><code></code>



####Storing data in CSV files
Om data in een CSV file weg te schrijven kan men de cmdlet Export-Csv gebruiken en het pad meegeven met de Property -Path.
Ook cmdlet Import-Csv kan gebruikt worden.
![ALt text](http://i.imgur.com/kUzOt38.png)

####Storing data in XML
Hetzelfde kan gedaan worden om weg te schrijven in een XML file. Hier maakt men gebruik van de cmdlet Export-Clixml.

<code></code><code>PowerShell
Get-Process | Export-Clixml -Path c:\fso\processXML.xml
</code><code></code>








<div id='8'/>
##Remoting

###Samenvatting powershell Remoting
---

Enable powershell remoting met het volgende commando

```
winrm quickconfig
```

Check de winRM configuration met het volgende commando

```
winrm get winrm/config -format:pretty
```

Let op een error hierna


![Alt text](http://i.imgur.com/4WcVI8n.png)

Dan voer je het vorige commando uit.
Hierna krijg je een aantal vragen. Waar je y antwoord.

Daarna krijg je nog een error. Die zegt dat de firewall exception niet gaat werken wanneer connectie types op dit apparaat naar public zijn gezet.

Vervolgens verander je publiek naar private in de netwerk settings.

![Alt text](http://i.imgur.com/xFVFBMx.png)

Er is geen command-line voor, maar je kan met het script hieronder, het netwerk naar private veranderen.

![Alt text](http://i.imgur.com/m6kPyn4.png)

Nu kan het onderstaande commando gebruikt worden.

```
winrm quickconfig
```

Standaard zet WinRM alleen http aan bij remote request, maar je kan dit manueel aanzetten met het volgende commando.

```
winrm of New-
WSManIntance cmdlet
```

Powershell remoting kan ook aangezet worden met de volgende cmdlet 

```
remoting Enable-PSRemoting
```

Je kan altijd testen of remoting aan staat met het volgende commando

```
Enter-PSSession -ComputerName ...... 
```

Log je in op een pc. Remote staat standaard al aan op w2012. hostname
mstsc /v:.... kom je op de andere computer zijn cmd/desktop.

Het prompt komt er zo uit te zien.

![Alt text](http://i.imgur.com/3Q8FXsO.png)

Nu kijken we naar de remoting configuration information om te vergelijken met het vorige prompt.
Dit kan met 
```
winrm get winrm/config -format:pretty
```

De uitvoer zou er als volgt moeten uitzien.
![Alt text](http://i.imgur.com/PiGkagF.png)

Standaard luisterd remoting naar poort 5985 for http en 5986 voor https. Dit kan je veranderen door het aanpassen  van
```
wsman:\localhost\Listener\listener*\port
``` 

naar een andere value te veranderen met set-item cmdlet.

### Volgende stap een trusted hosts toevoegen

Om alle workgroup-joined computers aan de lijst van trusted hosts toe te voegen doe je. ```Set-item wsman:localhost\client\trustedhosts -value *```

Als je specifiek hosts wilt toevoegen doe je ```Set-item wsman:localhost\client\trustedhosts -value "Computer1,Computer2"```

Je kan dit ook met domeinen en door het ip toe te voegen zoals bv. ```Set-item wsman:localhost\client\trustedhosts -value "192.168.10.11"```

Je kan ook WinRM batch script toevoegen aan een computer lijst. 
```winrm set winrm/config/client `@`{TrustedHosts=`"`192.168.10.11`"`}```

Niet vergeten ```Enable-PSRemoting``` uit te voeren hierna voor de veranderingen.

### Remote management door winRM laten.

Een GPO maken door de volgende stappen uit te voeren.

1. Lanceer Group Policy Management (GPMC) via ```Control Panel | All
Control Panel Items | Administrative Tools | Group Policy Management```,
and create a new GPO titled Windows Remote Management.

2. Rechtermuisknop en edit de nieuw gemaakte GPO bij de using Group
Policy Management Editor, en dan breid je het uit door de Computer
Configuration Policy structure door gebruik van Windows Remote Management
| Computer Configuration | Administrative Templates | Windows
Components | Windows Remote Management (WinRM) | WinRM
Service and selecteer Allow remote server management door WinRM.
Deze policy setting laat je toe van de WinRM service te manage en
start automatisch en luisterd op het netwerk de HTTP requests op poort
5985.
3. Schakel de GPO in en vul de IPv filter textboxes in. Een voorbeeld hieronder.

![Alt text](http://i.imgur.com/H4P0BXr.png)

### Windows Remote Management door de Windows Firewall laten

1) Vind computer configuration > Policies > Windows Settings > Security
Settings > Windows Firewall with Advanced Security > Windows
Firewall > Inbound Rules

![Alt text](http://i.imgur.com/v2ePAtw.png)

2) Rechtermuis op inbound rules en click new rule. Onder new rule, ga naar predefined en selecteer windows remote management.

![Alt text](http://i.imgur.com/cWMPzRb.png)

3) Dan druk op next

4) Dan selecteer je welke actie de firewall moet ondernemen. Selecteer Allow the connection. Dan klik op finish.

![Alt text](http://i.imgur.com/T6tzr9C.png)

5) Na de rules zijn aangemaakt kan je kiezen voor nog meer restricties, laat alleen de ip addressen van je subnet toe of specifieke user groups.

![Alt text](http://i.imgur.com/QN9K1Ay.png)

### Service Windows Remote Management(WS-Management) aanzetten 

De remote service instellen zodat deze automatisch start. Ga naar Computer Configuration > Policies > Windows Settings > Security Settings > System Services.

Op de rechterhand zoek je windows remote management system services en klik je er op.

![Alt text](http://i.imgur.com/FvnO9uK.png)

Check define this policy setting en druk automatic.


![Alt text](http://i.imgur.com/X7m4cgm.png)

We willen ook een service preference. Ga naar Computer Configuration > Preferences > Control Panel Settings > Services en rechtermuis op services. Klik op new > service.
 
![Alt text](http://i.imgur.com/I4Fq1yK.png)

Open de general tab en stel in: startup automatic, service name WinRM en service action start service.

![Alt text](http://i.imgur.com/FFpbiyo.png)

Open de recovery tab en stel alle failure settings in als restart the service.

![Alt text](http://i.imgur.com/3ODkXMa.png)

### Een Group Policy Update uitvoeren

Open een command promt als administrator en voer gpudate /force uit om de veranderingen door te voeren.

### Remoting uitschakelen

Je kan ```Disable-PSRemoting``` gebruiken om de remote session configuratie uit te schakelen. Enable-PSRemoting alle veranderen door dit commando zullen niet verwijderd worden.

Als geen andere service of component op de lokale pc, de WinRM service nodig heeft kan je de service disablen door het volgende commando uit te voeren ```Set-Service winrm -StartupType Manual``` en ```Stop-Service winrm```.

### De remoting commands uitvoeren

Wanneer we bezig zijn met remoting kunnen we commando's en scripts uitvoeren op een paar manieren.
De ```Invoke-Command``` cmdlet en interactieve remoting sessies. Een keer dat je remoting hebt geactiveerd op alle computers, kan je de ```Invoke-Command``` cmdlet gebruiken om commando's en scripts te runnen. 

Voorbeeld hiervan:

![Alt text](http://i.imgur.com/kfWTV4s.png)

Wanneer we het ip adress naar de -ComputerName parameter sturen en -ScriptBlock parameter als Get-Process, dan zal de uitvoer terug gestuurd worden naar de lokale pc.

### ScriptBlock draaien op een remote computer

Je kan dit commando uitvoeren met de volgende methode ```Invoke-Command -ComputerName Win-8 -ScriptBlock {Get-Service}```

Script block parameter kan gebruikt worden om een lijst te specifiëren dat je wilt draaien op de remote computer.
De ComputerName parameter is niet nodig voor het runnen van commandos op de lokale machine. Als je het zelfde commando op meerdere pc's wilt draaien kan je de computer naam of ip adres met komma scheiden van elkaar of lees een text file door de Get-Content cmdlet te gebruiken.

Een voorbeeld: ```Invoke-Command -ComputerName Win-8,Win-8-Client -ScriptBlock {Get-
Service}```

Dit commando is ook handig: ```Invoke-Command -ComputerName (Get-Content c:\servers.txt) -
ScriptBlock {Get-Service}```

De methode genaamd fan-out of 1:many remoting. Daarmee kan je dezelfde command op meerdere pc's gebruiken als 1 command. Alle commands en variabelen in het ScriptBlock parameter worden uitgevoert op de remote pc.

Als je scripts of commands runned, dan kan je het Invoke-Command het laten lezen, de inhoud wordt gestuurd naar de remote computers en voeren deze commands uit:

```Invoke-Command -ComputerName Win-8,Win-8-Client –filePath
c:\Scripts\Tasks.ps1```

### Een persistente sessie maken met de Invoke-Command

Run ```Invoke-Command``` met de ```-ComputerName``` parameter, deze specifieerd de naam van de remote computer.

Om onnodige tijd te besparen, kunnen we een persistente sessie van de remote computer beginnen door de -Session parameter te gebruiken. Je kan een een persisten connectie creëren met een remote pc door de New-PSSession cmdlet te gebruiken zoals in de volgende voorbeelden.

Wanneer je New-PSSession cmdlet gebruikte om een PS session te creëren, zal windows powershell een connectie een persistente connectie voor de PS Sessie maken. Dan kan je meerdere commands runnen in de PS Sessie, ook de commands die data sharen.

```$session=New-PSSession -ComputerName Win-8```

Nu, houd $session de details voor de doorgezette connectie. We kunnen $session gebruiken door een commando te invoken op een remote pc. De syntax ziet er als volgt uit:

```Invoke-Command -Session $session -ScriptBlock {Get-Service}```

$session houd alle variabelen die je maakt/aanpast wanneer je commandos uitvoert op een remote pc. $session als sessie zal toegang hebben tot alle variabelen gecreërt / geupdate op de remote pc. Als voorbeeld:

```$session=New-PSSession -ComputerName Win-8```
```Invoke-Command -Session $session -ScriptBlock {$fileCount = (Get-ChildItem C:\ -Recurse).Count}```
```invoke-command -session $session -ScriptBlock {$fileCount}```

We kunnen de ```$fileCount``` variabele alleen gebruiken omdat we een persistente sessie gebruiken.

![Alt text](http://i.imgur.com/kCvA7rU.png)

### Specifiëren van login gegevens om te remoten

In een domein omgeving, kunnen we inloggen als gebruikers alleen als we administrator gegevens hebben om toegang te krijgen tot een pc in een domein. Maar, in een werkgroep, moeten we gegevens doorspelen te samen met het ```invoke-command```.

Bijvoorbeeld:

```
$cred=Get-Credential
Invoke-Command -ComputerName win-8 -ScriptBlock {Get-Service} -Credential
$cred
``` 

In dit voorbeeld ```Get-Credential``` prompt voor de credentials om toegang te geven aan de remote computer en gebruikt dezelfde bij het oproepen van de Invoke-Command cmdlet. Wanneer je ```Get-Credentials``` cmdlet uitvoert krijg je een venster waar je username en password wordt gevraagd. Wanneer je inlog gegevens invult, gaat de cndlet een ```PSCrendential``` object aanmaken die de inlog gegevens van een gebruiker bewaard in het ```$cred``` . 

### Een interactieve remote sessie starten

```Enter-PSSession``` en ```Exit-Pssesion``` zijn de cmdlets gebruikt voor star/exit een interactieve remoting sessie. Om in te loggen op een remote sessie gebruiken we het  volgende commando.

```
Enter-PSSession -ComputerName win-8
```

Een keer als je een interactive remote sessie begint, veranderd de prompt van je powershell naar de remote computers naam. De commando's die je ingeeft draaien dan op de remote computer alsof je ze zelf direct ingeeft op je pc. 

Dit is een interactieve remote sessie:

![Alt text](http://i.imgur.com/rqzV3cK.png)

Met ipconfig kan je checken of je verbonden bent.

![Alt text](http://i.imgur.com/Y4giTMN.png)

Wanneer verbonden met een interactieve remote sessie kan je elk commando uitvoeren zoals met Telnet.

### Uit een interactieve sessie gaan

```Exit-PSSession``` Je moet opletten voor parameters als -ComputerName want de Enter-PSSession cmdlet start maar tijdelijk een powershell sessie en geen permanente. Alle variabelen dat je gemaakt hebt en je commando geschiedenis zal verwijderd worden.

### Een persistente (volhoudende) sessie starten met interactieve remoting

Je kan een persistente sessie starten met ```Enter-PSSession``` voor de sessie te beginnen en met het gebruik van ```Get-PSSession``` cmdlet kan je zien welke beschikbare open PS sessies er zijn.

![Alt text](http://i.imgur.com/nXicpKw.png)

Er zijn verschillende manieren om een bestaande sessie te beëindigen.

Door het session ID: 

```
Enter-PSSession -Id 3
```

Door het session instance ID:

```
Enter-PSSession -InstanceId 2c4ae306-78c4-4a40-a52b-0eeb6c6cd94c
```

Door de sessie naam:

```
Enter-PSSession -Name Session3
```

Het gebruik van de -Session parameter:

```
$session=Get-PSSession -Id 3
Enter-PSSession -Session $session
```

### Disconnecten en reconnecten van sessies

In powershell v3 kan je disconnecten met het ```Disconnect-PSSession``` en verbinden met het ```Connect-Pssession``` cmdlet. Deze commands accepteren elk een sessie object, die je maakt met het ```New-PSSession``` cmdlet.

Een disconnected sessie laat een copy draaien op de remote pc. Dit is een goede manier om het lange taken te laten volbrengen en het dan later weer op te nemen. Je kan zo ook disconnecten en met andere sessies connecteren.

Een voorbeeld van een achtergrond job die op de server door blijft lopen na het disconnecten.

![Alt text](http://i.imgur.com/d6LoCAT.png)

Daarna log je in op een andere machine als de zelfde user van op de andere sessie. We halen de sessie af van de remote pc en reconnecten. Dan krijg je scherm van de nieuwe sessie en zie je de resultaten van de achtergrond job.

Met ```Remove-PSSession``` kan een remote sessie permanent worden afgezet.

### Een remote sessie opslaan op de hardeschijf

Met het ```Export-PSSession``` cmdlet kunnen we commands exporteren van een remote sessie en ze opslaan in een powershell module op de lokale schijf. Deze cmdlet bewaard cmdlets, functies, aliasen en amdere commando's in een PS module.


```$session = New-PSSession -ComputerName win-8```
```Invoke-Command -Session $session –ScriptBlock {Import-Module NetTCPIP}```
```Export-PSSession -Session $session -OutputModule RemoteCommands```
```-AllowClobber -Module NetTCPIP -Force```

In dit voorbeeld maken we een persistente sessie en importeren we een module genaamd NetTCPIP. Dan gebruiken we het ```Export-PSSession``` cmdlet om alle commands te exporteren. Alles is dan beschikbaar in de PS session $session in een module op de hardeschijf die RemoteCommands heet.

Als de ```Export-PSSession``` cmdlet gelukt is, krijgen we een gelijkaardig input als hier:

![Alt text](http://i.imgur.com/Vxk9BNW.png)

De modules worden gegenereerd onder de .psm1, .psd1 extensies. Nu kan je de modules laden om aan de remote commands te kunnen.

### Importeren van een module opgeslagen op een schijf

Je hebt geen specifiek pad nodig voor de module. Het volgende commando importeerd alle remote commands verkrijgbaar in een module op de lokale sessie:

```
Import-Module RemoteCommands
```

Dan voeren we het remote commando uit, om een remote sessie te starten, uitvoeren van commandos in de remote sessie en de uitvoer weergeven. Dit gebeurt allemaal als je gelijk welke remoting gerelateerde cmdlet gebruikt.

### Limieten van Export-PSSession

- Je kan geen programma starten met de user interface omdat het toegang nodig heeft met een interactieve desktop. 

- De geexporteerde module houd niet de opties in van de sessie die gebruikt werd om deze aan te maken.

- Je kan geen PowerShell provider exporteren

### Het gebruik van sessie configuraties

```Invoke-Command, Enter-PSSession``` en ``` New-PSSession``` cmdlets hebben een ```-ConfigurationName``` parameter waarmee je een verschillende sessie kan configureren dan de standaard.

Standaard hebben alleen leden of administrator groepen toegang tot deze 2 sessie configuraties.

Powershell sessie configuraties kunnen gebruikt worden voor:

- Customizen van de remote ervaring voor gebruikers

- Administratie maken door het creëren van sessie configuraties met verschillende levels van systeem toegang.

Volgende cmdlets zijn voor het managen van sessie configuraties:

```
Register-PSSessionConfiguration
```

```
Unregister-PSSessionConfiguration
```

```
Enable-PSSessionConfiguration
```

```
Disable-PSSessionConfiguration
```

```
Set-PSSessionConfiguration
```

```
Get-PSSessionConfiguration
```

### Nieuwe sessie configuraties maken

Met ```Register-PSSessionConfiguratie``` cmdlet kan je een nieuwe sessie configuratie maken. Met powershell scripts kan je het opstarten v an een sessie configureren. 

Bijvoorbeeld een script maken dat de NetTCPIP module importeerd door het Import-Module cmdlet.

```
Import-Module NetTCPIP
```

Sla dit script op als startupscript.ps1. Gebruik nu de ```Register-PSSessionConfiguration``` cmdlet om een nieuwe sessie te configureren.

Dit kan als volgt met het volgende commando:

```Register-PSSessionConfiguration -Name "NetTCPIP" -StartupScript C:\
StartupScript.ps1```

Uitvoer:

![Alt text](http://i.imgur.com/7P4Be45.png)

Je krijgt een prompt om de actie te bevestigen, aan het einde van het herstarten van de WinRM service op de lokale pc. Je moet eerst script uitvoeren enablen op de lokale pc om de mogelijkheid te hebben van startup scripts te gebruiken als onderdeel van de sessie configuratie.

### Alle beschikbare sessie configuraties lijsten

Met het ```Get-PSSessionConfiguration``` cmdlet lijst je alle beschikbare sessie configuraties op de lokale pc.

Uitvoer:

![Alt text](http://i.imgur.com/ZeAPY8S.png)

De ```Get-PSSessionConfiguration``` cmdlet kan je niet gebruiken om toegang van een lijst van PS sessies te krijgen op een remote pc. Maar hiervoor kunnen we de ```Get-WSManInstance``` cmdlet gebruiken zoals in het volgende commando:

```
Get-WSManInstance winrm/config/plugin -Enumerate -ComputerName win-8 |
Where ` { $_.FileName -like '*pwrshplugin.dll'} | Select Name
```

Dit laat alle configuratie namen zien die beschikbaar zijn op een remote computer.

![Alt text](http://i.imgur.com/6EDzfn6.png)

Je moet toegang hebben tot de sessie configuratie op de remote pc om dit te kunnen gebruiken in PS remoting.

### Custom permissies en PS sessie configuraties

Je kan ```Get-PSSessionConfiguration``` gebruiken om toegang te krijgen voor de nieuwe sessie.

Dit kan met het volgende commando:

```
Set-PSSessionConfiguration -Name NetTCPIP -ShowSecurityDescriptorUI
```

Dit opent een nieuw venster.

![Alt text](http://i.imgur.com/kI6f5EZ.png)

Nu kan je schrijf en lees rechten aanvinken voor de gebruikers en administrator groepen.

### Een custom sessie configuratie oproepen

De volgende code snippets laten 3 manieren zien om een remote sessie op te roepen met een custom sessie configuratie naam:

```
$s = New-PSSession -ComputerName win-8 -ConfigurationName NetTCPIP
```

```
Enter-PSSession -ComputerName win-8 -ConfigurationName NetTCPIP
```

```
Invoke-Command -ComputerName win-8 -ConfigurationName NetTCPIP
-ScriptBlock {Get-Process}
```

We gebruiken het ```Invoke-Command``` om de active directory module in een persistente sessie te laden en dan importeren van NetTCPIP cmdlets in de lokale sessie. Alle NetTCPIP cmdlets zullen beschikbaar zijn wanneer AD module als startup script wordt gebruikt.

### Uitschakelen van een sessie configuratie

Gebruik ```Disable-PSSessionConfiguration``` om een bestaande configuratie te disablen en gebruikers te stoppen van te connecteren vanaf hun lokale pc door gebruik van een sessie configuratie. Met de ```-Name``` parameter kan je specifiëren welke sessie configuratie je wilt uitschakelen. Als je geen configuratie specifieerd zal de default microsoft sessie configuratie uitgeschakeld worden.

De ```Disable-PSSessionConfiguration``` cmdlets voegt een "deny all"setting toe bij de security descriptor van 1 of meerdere geregistreerde sessie configuraties.

De ```Disable-PSRemoting``` cmdlet zal alle PS sessie configuraties uitschakelen die beschikbaar zijn op de lokale pc.

De ```Enable-PSSessionConfiguration``` cmdlet kan gebruikt worden voor het inschakelen of uitschakelen van de configuratie. Met de -Name parameter kan je specifiëren welke configuratie je wilt inschakelen.

### Verwijderen van een sessie configuratie

Je kan de ```Unregister-PSSessionConfiguration``` cmdlet gebruiken om een vorige gedefiniëerde sessie configuratie te verwijderen. Let op als je ```Enable-PSRemoting``` opnieuw uitvoert wordt de default sessie configuratie weer aangemaakt.


<div id='9'/>
##Variabelen

#### Storing Variabelen

Alles in Powershell wordt behandeld als een object. Zelfs voor een simpele string van karakters, zoals de computernaam, wordt gezien als een object. Zoals dat piping van een string om ```Get-Member``` laat zien dat een object 
type ```System.String``` is en dat het veel goede methoden heeft waarmee je kan werken. 

Powershell bewaard deze values dat je bij een object kan opvragen allemaal in variabelen. Om dit te doen, moet je de variabele specifiëren en het gelijkaan teken operator gebruiken, gevolgd door alles dat je in de variabele wilt zetten.

Bijvoorbeeld:

```
PS C:\> $var = "SERVER-R2"
```

Het is belangrijk om te weten dat het dollar teken geen deel uitmaakt van de naam van de variabele. In dit voorbeeld is de variabele naam ```var```. Het dollar teken is een cue naar de shell dat volgt door wat de variabele naam gaat worden en we willen de inhoud van die variabele. In dit voorbeeld gaan we de inhoud van de variabele zetten.

* Een paar hoofdpunten die je in je hoofd moet houden bij de namen van variabelen:
* Variabele namen houden meestal letters, nummers en underscores in. En het is heel voorkoment om te beginnen met een letter of een underscore.
* Variabele namen houden spaties in, maar de naam moet zonder in "curly braces" . Bv. ```${My Variable}``` is hoe je een variabele toont met de naam "My variable". Persoonlijk, houden we niet van variabele namen die spaties inhouden omdat deze meer typwerk inhouden en moeilijker te lezen zijn.
* Variabelen blijven niet tussen powershell sessies. Wanneer je de shell dicht doet, gaat elke variabele die je gemaakt hebt weg.
* Variabele namen kunnen vrij lang zijn, lang genoeg dat je geen zorgen moet maken over hoe lang ze zijn. Probeer variabele namen duidelijk te maken. Bv. Als je een een computer naam in een variabele zet, gebruik ```computername``` als variabele naam. Als een variabele veel processes inhoud, dan is ```processes``` een goede variabele naam.
* Behalve voor mensen met een VBScript background, powershelll gebruikers gaan meestal geen variabele naam prefixen om aan te duiden wat er in bewaard wordt. Bv. in VBScript, strComputerName was een veel gebruikte type van een variabele naam, aanduidend dat het een string bewaard (Str). Powershell vind het niet erg als je dat doet, maar het wordt niet meer zo graag gebruikt in de grote community.

Om de inhoud van een variabele terug te vinden, gebruik het dollar teken gevolgd door de variabele naam, zoals getoont in het voorbeeld. Opnieuw, het dollar teken verteld shell dat je toegang wilt tot de inhoud van een variabele. Gevolgd door een variabele naam dat verteld welke variabele je probeerd toegang tot te krijgen.

```
PS C:\> $var
SERVER-R2
```

Je kan variabelen gebruiken in een plaats van waarden in bijna elke situatie. Bv. Wanneer je WMI gebruikt heb je een optie om een computernaam te spcifiëren. Het commando zal er waarschijnlijk zo uit zien:

```
PS C:\> get-wmiobject win32_computersystem -comp SERVER-R2
Domain : company.pri
Manufacturer : VMware, Inc.
Model : VMware Virtual Platform
Name : SERVER-R2
PrimaryOwnerName : Windows User
TotalPhysicalMemory : 3220758528
```

Var is een vrij standaard variabele naam. Normaal gebruiken we computernaam, maar in dit specifiek voorbeeld plannen we van $var in verschillende situaties te hergebruiken. Dus hebben we besloten van het generiek te houden. Laat dit je niet tegenhouden van andere logische variabele namen te gebruiken. 
We zullen een string in $var steken om mee te beginnen, maar dit kunnen we elk moment veranderen.

We willen:

```
PS C:\> $var = 5
PS C:\> $var | gm
TypeName: System.Int32
Name MemberType Definition
---- ---------- ----------
CompareTo Method int CompareTo(System.Object value), int CompareT...
Equals Method bool Equals(System.Object obj), bool Equals(int ...
GetHashCode Method int GetHashCode()
GetType Method type GetType()
GetTypeCode Method System.TypeCode GetTypeCode()
ToString Method string ToString(), string ToString(string format...
```


In het vorige voorbeeld, plaatsen we een integer in de $var, en dan hebben we een pipe gebruikt $var naar Gm. Je kan zien dat shell $var herkend als een System.Int32 of een 32 bit integer.

#### Variabelen gebruiken: truks met quotes

We adviseren gewoonlijk een enclosed string te gebruiken binnen single quotes marks. De reden hiervan is dat Powershell alles behandeld in een single quotatie mark als een letterlijke string. 

Voorbeeld:

```
PS C:\> $var = 'What does $var contain?
PS C:\> $var
What does $var contain?
```

In de voorgaande voorbeelden, kan je zien dat $var binnen de single quotes behandeld wordt als letterlijk.

Maar binnen dubbele quotation marks (") is dit niet het geval. 

Kijk naar de volgende truk:

```
PS C:\> $computername = 'SERVER-R2'
PS C:\> $phrase = "The computer name is $computername"
PS C:\> $phrase
The computer name is SERVER-R2
```

We waren gestart met ons voorbeeld in SERVER-R2 te bewaren, in de variabele $computername. Daarna hebben we "The computer name is ```$computername"``` in de variabele ```$phrase``` gestoken. Wanneer we did deden hebben we dubbele quotation marks gebruikt. Ps gaat automatisch naar dollar tekens zoeken binnen de double quotes, en vervangt elke variabele dat hij vind in de inhoud. Omdat we de inhoud van $phrase hebben laten zien was 
 ```$computername``` vervangen met ```SERVER-R2```, de inhoud van deze variabele. 

De vervangende actie gebeurd alleen wanneer de shell gedeelde de string initializeerd. Bij dit punt, $phrase houd dit in "The computer name is ```SERVER-R2"``` het houd niet de ```"$computername"``` string in. We kunnen dit testen door de inhoud proberen te veranderen van $computername on te zien of $phrase het update.

```
PS C:\> $computername = 'SERVER1'
PS C:\> $phrase```
The computer name is SERVER-R2
```

Zoals je kan zien blijft $phrase variabele het zelfde.

Nu over dit (`) karakter, het verwijderd elke speciale betekenis het misschien zou geassocieerd worden met het karakter erachter of in sommige gevallen voegt het een speciale betekenis toe aan het volgende karakter. 

Bijvoorbeeld:

```
PS C:\> $computername = 'SERVER-R2'
PS C:\> $phrase = "`$computername contains $computername"
PS C:\> $phrase
$computername contains SERVER-R2
```

Wanneer we de string hebben geassocieerd aan $phrase, gebruikten we de $computername dubbel. De eerste keer hebben we het dollar teken voorbij gestoken met een tik van achter. Als je dit doet neem je het dollars teken speciale betekenis weg, als een variabele indicator en maak je het een letterlijk dollar teken. Je kan dit zien aan de vorige uitvoer. Op de laatste lijn, dat $computername was bewaard in deze variabele. We gebruikten deze "backtick" niet voor een 2e keer. Dus $computername was vervangen met de inhoud van deze variabele.

Een 2e manier van hoe een "backtick" kan werken:

```
PS C:\> $phrase = "`$computername`ncontains`n$computername"
PS C:\> $phrase
$computername
contains
SERVER-R2
```

Als je goed kijkt, merk je op dat we (`n) 2 keer hebben gebruikt in de zin. 1 keer na de eerste $computername en 1 keer na contains. In dit voorbeeld, voegt de backtick speciale betekenis toe. Normaal is "n" een letter, maar met de "backtick" ervoor, wordt het een "carriage return" en lijn feed ( denk "n" voor "nieuwe lijn").

Run ```help about_escape``` voor meer informatie, dit houd een lijst in met andere speciale escape karakters. 
Je kan, bijvoorbeeld, gebruik maken van een escaped "t" om een tab toe te voegen, of een escaped "a" om de computer te laten beepen (zie "a" als "alert").

#### Veel objecten bewaren in een variabele

Dit punt, hebben we vooral gezien dat variabelen een single object inhouden, en deze objecten hebben allemaal simpele waarden. We hebben gewerkt direct aan de objecten zelf, eerder dan hun eigenschappen of methoden. Laten we nu proberen een hoop objecten in een enkele variabele te plaatsen.

Een manier om dit te doen is om een comma-gescheiden lijst te gebruiken, omdat PowerShell herkent dat deze lijsten als een collectie van objecten wordt gezien:

```
PS C:\> $computers = 'SERVER-R2','SERVER1','localhost'
PS C:\> $computers
SERVER-R2
SERVER1
Localhost
```

Kijk goed hoe we in het vorige voorbeeld commas buiten de quotation marks hebben gezet. Als we ze binnen zouden zetten, zouden we een single object hebben dat commas en 3 computer namen inhoud. Met deze methode, kunnen we 3 objecten van elkaar onderscheiden, allemaal met het Type String. Zoals u kunt zien hebben we de inhoud van goed onderzocht van deze variabele. Ps laat elk object op zijn eigen lijn zien.

#### Werken met single objecten in een variabele

Je kan ook individuele elementen in een variabele opnemen, 1 per keer. Om dit te doen moet je een index nummer specifiëren voor het object dat je wilt, tussen vierkante haaken. Het eerste object is altijd aan index nummer 0m de 2e aan index nummer 1 en zo voort. Je kan altijd een index van -1 gebruiken voor aan het laatste object te kunnen, -2 voor het 1 na laatste object en zo voort.

Een voorbeeld:

```
PS C:\> $computers[0]
SERVER-R2
PS C:\> $computers[1]
SERVER1
PS C:\> $computers[-1]
localhost
PS C:\> $computers[-2]
SERVER1
```

De variabele zelf heeft een eigenschap dat laat zien hoebeel objecten er zijn in 

```
PS C:\> $computers.count
3
```

Je kan altijd aan eigenschappen en methoden van een object binnen een variabele als de eigenschappen en methoden in de variabele zelf. Het is zo makkelijker om te zien, aan het begin of een variabele een single object inhoud.

```
PS C:\> $computername.length
9
PS C:\> $computername.toupper()
SERVER-R2
PS C:\> $computername.tolower()
server-r2
PS C:\> $computername.replace('R2','2008')
SERVER-2008
PS C:\> $computername
SERVER-R2
```

In het vorige voorbeeld, gebruiken we de $computername variable dat we eerder hadden gemaakt. Dit variabele houd een object in van het type System.String en je zou de complete lijst van eigenschappen en methoden van dit type wanneer je piped naar een string voor Gm. We gebruikten de Length eigenschap, als de ToUpper(), ToLower(), en Replace() methoden. In elke voorbeeld, hadden we deze om de methode naam te volgen met toevoegsels, zelf geen van de ToUpper() of de ToLower() hebben een parameter nodig in deze toevoegsels. Ook geen van deze methoden veranderen wat er binnen de variabele was, je kan dit zien op de laatste lijn. In de plaats, elke methode heeft een new String gebasseerd op de originele, als modificatie door deze methode.

#### Properties en methoden in Powershell 3 uitrollen

In powershell v1 en v2 had je geen toegang tot de eigenschappen en methoden wanneer een variabele meerdere objecten inhoud dit was verwarrend voor v1 en v2 gebruikers. Zo verwarrend dat ze in v3 een belangrijke verandering hadden toegepast, genaamd ```automatic unrolling```. Basically, betekent dit dat je nu toegang hebt tot de eigenschappen en methoden gebruikt door een variabele die meerdere objecten inhoud.

```
$services = Get-Service
$services.Name
```

Powershell ziet dit als dat je probeerd toegang te krijgen tot een object. 

Het ziet ook dat je collecties in $services geen naam eigenschap heeft, maar dat de individuele objecten binnen de collecties wel hebben. Dus het enumerates of unrolls het object en neemt de Naam eigenschap van elk object. Dit is gelijk aan:

```
Get-Service | ForEach-Object { Write-Output $_.Name }
```

En hetzelfde voor:

```
Get-Service | Select-Object –ExpandProperty Name
```

Het zelfde werkt voor methoden:

```
$objects = Get-WmiObject –class Win32_Service –filter "name='BITS'"
$objects.ChangeStartMode('Disabled')
```

#### Een type van een variabele declareren

Powershell heeft geen interesse welk soort objecten je gebruikt, maar wij wel. 

Bijvoorbeeld, je hebt een variabele dat je verwacht een nummer te hebben.

Je plant om iets arithmetische te doen met dat nummer, en je vraagt een gebruiker omdat nummer in te geven.

Bijvoorbeeld:

```
PS C:\> $number = Read-Host "Enter a number"
Enter a number: 100
PS C:\> $number = $number * 10
PS C:\> $number
100100100100100100100100100100
```

Dit geeft als uitvoer 100100100100100100100100100100. Hoe kan dit?

Als je goed kijkt zie je wat er gebeurd. In de plaats van 100 te vermenigvuldigen met 10, gaat Ps de 100 string, 10 keer duppliceren. Met als resultaat dat de string 100, 10 keer op een rij wordt weergeven.

Dus de shell gebruikt dit als een string:

```
PS C:\> $number = Read-Host "Enter a number"
Enter a number: 100
PS C:\> $number | gm
TypeName: System.String
Name MemberType Definition
---- ---------- ----------
Clone Method System.Object Clone()
CompareTo Method int CompareTo(System.Object valu...
Contains Method bool Contains(string value)
```

Door $nummer te pipen naar Gm, laat zien dat de shell het als een System.String ziet, geen System.Int32. Er zijn een aantal manieren om dit te fixen.

De beste methode is deze:

Eerst vertel je shell dat $number variabele een integer moet inhouden, wat de shell forceerd van het te proberen converteren van elke invoer naar een echt getal. 

Eerst specifieer je het data type, int tussen vierkante haken, direct bij het eerste gebruik van de variabele.

Dit doe je aan de hand van het volgende voorbeeld:


![Alt text](http://i.imgur.com/lmNxsyh.png)


In het vorige voorbeeld hebben we, [INT] gebruikt om $number te forceren om integers te hebben (1). Na het ingeven van de input, pipen we $number naar Gm om zeker te zijn dat het inderdaad een integer is en geen string (2). Aan het einde kan je zien dat de variabele werd gezien als een nummer en een echte vermenigvuldiging (3).
Een ander voordeel hiervanb is dat wanneer shell een error geeft het niet kan converteren naar een nummer, omdat bij $number alleen mogelijk is van integers te bewaren. 

```
PS C:\> [int]$number = Read-Host "Enter a number"
Enter a number: Hello
Cannot convert value "Hello" to type "System.Int32". Error: "Input string
was not in a correct format."
At line:1 char:13
+ [int]$number <<<< = Read-Host "Enter a number"
+ CategoryInfo : MetadataError: (:) [], ArgumentTransformationMetadataException
+ FullyQualifiedErrorId : RuntimeException
```

Dit is een mooi voorbeeld van hoe je problemen later kan voorkomen, omdat je zeker bent dat $number een exact type zal zijn van data dat je verwacht.

Je kan vele nieuwe object types gebruiken in de plaats van [INT], de volgende lijst zijn die dat je het meest gaat gebruiken:

* [int]—Integer numbers
* [single] and [double]—Single-precision and double-precision floating numbers
(numbers with a decimal portion)
* [string]—A string of characters
* [char]—Exactly one character (as in, [char]$c = 'X')
* [xml]—An XML document; whatever string you assign to this will be parsed to
make sure it contains valid XML markup (for example, [xml]$doc = Get-Content
MyXML.xml)
* [adsi]—An Active Directory Service Interfaces (ADSI) query; the shell will execute
the query and place the resulting object or objects into the variable (such
as [adsi]$user = "WinNT:\\MYDOMAIN\Administrator,user")

Specifiëren van een object tpye voor een variabele is een goede manier om te voorkomen dat rare errors voorkomen in meer complexe scripts. 

#### Commando's voor het werken met variabelen

* New-Variable
* Set-Variable
* Remove-Variable
* Get-Variable
* Clear-Variable

Je bent niet verplicht deze te gebruiken behalve misschien Remove-Variable, die gebruikt wordt om een variabele permanent te deleten.

Als je deze cmdlets toch wilt gebruiken geef je variabele naam aan de cmdlets een -name parameter. Dit is alleen de naam dit houd geen dollar teken ($) in. 

#### Enkele tips 

* Houd variabelen betekenisvol, maar kort zoals $computername, maar niet bv. $c dat is te kort.
* Gebruik geen spaties in variabele namen.
* Als de variabele maar 1 soort object gaat inhouden, dan declareer je dat wanneer je de eerste keer de variabele gebruikt. Dit helpt errors te voorkomen.

<div id='10'/>
##PowerShell ISE


De ISE in Windows PowerShell ISE staat voor Integrated Scripting Environment. Veel IT-professionals gebruiken Windows PowerShell ISE voor interactieve Windows PowerShell-opdrachten, omdat het is makkelijker om te bewerken, betere tab completion heeft, en een ingebouwde opdracht deelvenster heeft.

Zodra je Windows PowerShell ISE opent, worden twee deelvensters weergegeven. Aan de linkerzijde van het scherm zie je een interactieve Windows PowerShell-console. Aan de rechterkant zie je een Windows PowerShell-opdracht explorer-venster. 

![Alt text](http://i.imgur.com/lhTN8Xv.png)

###Script paneel

Door op het pijltje te drukken naast "Script" krijg je een invoerscherm te zien waar je commando's na elkaar kunt noteren en ze in een keer uitvoeren door op de "run" knop te klikken. Dit is een zeer handige functionaliteit voor scripts te schrijven.

![Alt text](http://i.imgur.com/KzEZHTP.png)

###Intellisense

IntelliSense biedt pop-up help en informatie. Wanneer u een cmdlet typt, levert Intellisense mogelijke overeenkomsten aan. Zodra u de cmdlet gevonden hebt, geeft Intellisense de volledige syntaxis van de cmdlet, zoals weergegeven in onderstaande figuur.

![Alt text](http://i.imgur.com/PtM03Wd.png)



<div id='11'/>
##Scripting




###Scripting fundamentals

Waarschijnlijk is de belangrijkste reden om een Windows PowerShell-script te schrijven om terugkerende handelingen te doen. Bijvoorbeeld, de eenvoudige cmdlet Get-ChildItem heeft een goede werking, maar nadat u hebt besloten om de lijst te sorteren en te filteren uit alleen bestanden van een bepaalde grootte, eindig je met de volgende opdracht:

```PowerShell
Get-ChildItem c:\fso | Where-Object Length -gt 1000 | Sort-Object -Property name
```
Even if you use tab completion, the previous command requires a bit of typing. One way
to shorten it is to create a user-defined function. We will examine that technique later in this chapter. For now, the easiest solution is to write a Windows PowerShell script. The following example shows the DirectoryListWithArguments.ps1 script:

Zelfs als u tab completion gebruikt, vereist de vorige opdracht wel wat typwerk. Een manier om te verkorten het is het creëren van een door de gebruiker gedefinieerde functie. Die techniek verderop in dit hoofdstuk zullen we onderzoeken. Voor nu is de eenvoudigste oplossing om een Windows PowerShell-script te schrijven. In het volgende voorbeeld ziet u het DirectoryListWithArguments.ps1 script:

```PowerShell
DirectoryListWithArguments.ps1
foreach ($i in $args)
{Get-ChildItem $i | Where-Object length -gt 1000 |
Sort-Object -property name}
```

###Variabels

Wanneer u werkt met Windows PowerShell, hoeft u geen variabelen vóór gebruik declareren. Wanneer de variabelen gegevens bevatten, worden ze gedeclareerd. Alle namen van variabelen moeten worden voorafgegaan door een dollarteken ($). Het volgende voorbeeld wordt een variabele om te houden van de resultaten van de cmdlet Get-proces maken. 

```PowerShell
PS C:\> $process = Get-Process
```

###While statement

In onderstaand codeblok wordt de in while-clausule geïtereerd tot de variabele $i niet meer kleiner dan 5 is.

```PowerShell
DemoWhileLessThan.ps1
$i = 0
While ($i -lt 5)
{
"`$i equals $i. This is less than 5"
$i++
} #end while $i lt 5
```

###For statement

In onderstaand codeblok word de for-clausule uitgelegd. Deze is vrijwel gelijk aan de syntax van andere programmeertalen, zoals bv Java.

```PowerShell
DemoForLoop.ps1
For($i = 0; $i -le 5; $i++)
{
‘$i equals ‘ + $i
}
```

###If statement

In onderstaand codeblok word de if-clausule uitgelegd. Deze is vrijwel gelijk aan de syntax van andere programmeertalen, zoals bv Java.

```PowerShell
DemoIf.ps1
$a = 5
If($a -eq 5)
{
‘$a equals 5’
}
```

###Vergelijkende Operatoren

Hieronder een tabel met de operatoren voor vergelijking die gebruikt worden in allerhande situaties.

![Alt text](http://i.imgur.com/axzLPSn.png)

###Working with functions

Er kunnen ook zelf functies geschreven worden in PowerShell. Deze kunnen dan gebruikt worden als gewone cmdlet. 

```PowerShell
Get-OperatingSystemVersion.ps1
Function Get-OperatingSystemVersion
{
(Get-WmiObject -Class Win32_OperatingSystem).Version
} #end Get-OperatingSystemVersion
"This OS is version $(Get-OperatingSystemVersion)"
```
Zoals blijkt uit het voorgaande voorbeeld, zijn de accolades geopend, gevolgd door de code. Om  een exemplaar van de Win32_OperatingSystem WMI-klasse op te halen  gebruikt de code de cmdlet Get-WmiObject. Omdat deze WMI-klasse alleen een enkel exemplaar retourneert, zijn de eigenschappen van de klasse direct toegankelijk. De versie is de eigenschap in kwestie, en dus tussen haakjes kracht de evaluatie van de code binnen. Het geretourneerde beheer-object wordt gebruikt voor het uitzenden van de versie-waarde. De accolades zijn gebruikt om de functie te omsluiten. De versie van het besturingssysteem wordt teruggestuurd naar de code die de functie aanroept. In dit voorbeeld wordt een tekenreeks die schrijft "This OS is version" gebruikt. De versie van het besturingssysteem wordt teruggestuurd naar de plaats van waar de functie werd opgeroepen.

In onderstaand voorbeeld wordt er gebruik gemaakt van meerder parameters. Deze kunnen eenvoudig gedefinieerd worden binnen de functie door deze binnen Param() te zetten.

```PowerShell
Function Function-Name
{
Param(
[int]$Parameter1,
[String]$Parameter2 = "DefaultValue",
$Parameter3
)
#Function code goes here
} #end Function-Name
```


###Voorbeelden
####Create Users

```PowerShell
<#
.Synopsis
Creates the TreyResearch.net users
.Description
Create-TreyUsers reads a CSV file to create an array of users. The users are then added to the Users container in Active Directory. Additionally, Create-TreyUsers adds the user Charlie to the same AD DS Groups as the Administrator account. 
.Example
Create-TreyUsers
Creates AD Accounts for the users in the default "TreyUsers.csv" source file
.Example
Create-TreyUsers -Path "C:\temp\NewUsers.txt"
Creates AD accounts for the users listed in the file C:\temp\NewUsers.txt"
.Parameter Path
The path to the input CSV file. The default value is ".\TreyUsers.csv". 
.Inputs
[string]
.Notes
    Author: Charlie Russel
 Copyright: 2015 by Charlie Russel
          : Permission to use is granted but attribution is appreciated
   Initial: 3/26/2015 (cpr)
   ModHist:
          :
#>
[CmdletBinding()]
Param(
     [Parameter(Mandatory=$False,Position=0)]
     [string]
     $Path = ".\TreyUsers.csv" 
     )

$TreyUsers = @()
If (Test-Path $Path ) {
   $TreyUsers = Import-CSV $Path
} else { 
   Throw  "This script requires a CSV file with user names and properties."
}

ForEach ($user in $TreyUsers ) {
   New-AdUser -DisplayName $User.DisplayName `
              -Description $user.Description `
              -GivenName $user.GivenName `
              -Name $User.Name `
              -SurName $User.SurName `
              -SAMAccountName $User.SAMAccountName `
              -Enabled $True `
              -PasswordNeverExpires $true `
              -UserPrincipalName $user.SAMAccountName `
              -AccountPassword (ConvertTo-SecureString -AsPlainText -Force -String "P@ssw0rd!" ) 
   If ($User.SAMAccountName -eq "Charlie" ) {
      $cprpwd = Read-Host -Prompt 'Enter Password for account: Charlie' -AsSecureString
      Set-ADAccountPassword -Identity Charlie -NewPassword $cprpwd -Reset
      $SuperUserGroups = @()  
      $SuperUserGroups = (Get-ADUser -Identity "Administrator" -Properties * ).MemberOf

      ForEach ($Group in $SuperUserGroups ) {
         Add-ADGroupMember -Identity $Group -Members "Charlie" 
      }
      Write-Host "The user $user.SAMAccountName has been added to the following AD Groups: "
      (Get-ADUser -Identity $user.SAMAccountName -Properties * ).MemberOf
   }
}




```



####Set Firewall

```PowerShell
<#
.Synopsis
Enables Firewall rules for lab environment
.Description
Set-myFirewall gets a list of firewall rules related to Remote Desktop, File and Print Sharing, and WMI, and enables them for both Domain and Private Profiles. Finally, it enables PSRemoting. This script requires no parameters. 

.Example
Set-myFirewall

Enables all RDP, WMI, and File & Printer Sharing firewall rules for Domain and Private networks.
.Notes
    Author: Charlie Russel
 Copyright: 2015 by Charlie Russel
          : Permission to use is granted but attribution is appreciated
   Initial: 09 Apr, 2014 
   ModHist: 10 May, 2015 - Set File&Print, WMI to enabled
          :
#>
[CmdletBinding()]

$RDPRules = Get-NetFirewallRule `
     | where {$_.DisplayName -match "Remote Desktop" }
$FPRules  = Get-NetFirewallRule `
     | Where {$_.DisplayName -match "File and Printer Sharing" }
$WMIRules = Get-NetFirewallRule `
     | Where {$_.DisplayName -match "Windows Management Instrumentation" }

ForEach ($rule in $RDPRules,$FPRules,$WMIRules ) { 
   Set-NetFirewallRule -DisplayName $rule.DisplayName `
                       -Direction Inbound `
                       -Profile Domain,Private `
                       -Action Allow `
                       -Enabled True `
                       -PassThru
}
Enable-PSRemoting -Force


```


<div id='12'/>
##Errors voorkomen/oplossen

Voor men fouten probeert te verbeteren in een script, moet men het gebruik van het script eerst begrijpen.
Bij de meeste simpele scriptjes zoals bijvoorbeeld Get-Bios.ps1 valt er niet te veel te verbeteren, aangezien er geen inputs van de command line zitten in dit script.

```Powershell
Get-Bios.ps1
Get-WmiObject -class Win32_Bios
```


###Ontbrekende parameters

In het Get-BiosInformation.ps1 script is er een parameter computerName, dat toelaat om een pc te kiezen als doel van het script.
Als het script geen waarde krijgt voor de computerName parameter, faalt het omdat Get-WmiObject een waarde voor de parameter nodig heeft.
Om het probleem op te lossen gaat het script op zoek naar een $computerName variabele.
Als deze variabele ontbreekt gaat het script een waarde proberen geven aan de variabele.
De volgende lijn van het script zorgt hiervoor: 
If(-not($computerName)) { $computerName = $env:computerName }

```Powershell
Get-BiosInformation.ps1
Param(
  [string]$computerName
) #end param

Function Get-BiosInformation($computerName)
{
  Get-WmiObject -class Win32_Bios -computerName $computername
} #end function Get-BiosName

If(-not($computerName)) { $computerName = $env:computerName }
Get-BiosInformation -computerName $computername
```


Men kan ook de parameters verplicht maken zodat de gebruiker een waarde voor de parameter moet voorzien.
Om een parameter verplicht te maken gebruiken we Mandatory als parameter attribuut.

```Powershell
Param(
  [Parameter(Mandatory=$true)]
  [string]$drive,
  [string]$computerName = $env:computerName
) #end param
```

Als men dit script dan gaat runnen gaat powershell een waarde vragen voor de parameter drive.

###Try/Catch/Finally

Bij een Try/Catch/Finally blok, ga je in het Try gedeelte de commands die het script moet uitvoeren zetten.
Als er een error is bij de commands, gaat het script naar het Catch gedeelte, waar de fout wordt opgevangen met een string, om te zeggen dat er een fout gebeurd is.
Hetgeen dat in het Finally gedeelte staat wordt altijd uitgevoerd, ookal was er een error gegenereerd.
In het algemeen zet men daar de "code cleanup", het stukje code dat ervoor gaat zorgen dat de niet gebruikte commands of commands waar er fouten stonden niet worden uitgevoerd.
In het voorbeeldscript staat er een string om te zeggen dat het script beëindigd is.

```Powershell
TestTryCatchFinally.ps1
$obj1 = "Bad.Object"
"Begin test"
Try
  {
    "`tAttempting to create new object $obj1"
    $a = new-object $obj1
    "Members of the $obj1"
    "New object $obj1 created"
    $a | Get-Member
  }
Catch [system.exception]
  {
    "`tcaught a system exception"
  }
Finally
  {
    "end of script"
  }
```



<div id='13'/>
##Gebruik maken van de CIM

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



<div id='14'/>
##Verbetering van Tab Completion

Tab completion is de functie waarmee u begint met het typen van een commando,
drukt u op de Tab-toets en de PowerShell engine de
mogelijke overeenkomsten invult. Dit bespaart duizenden key
strokes, voor een typische beheerder een dag. Het kan ook nuttig zijn voor cmdlets te ontdekken.

In PowerShell 3.0 heeft Microsoft de ervaring versterkt en een probleem verholpen waarmee de beheerder kampte. De vervelende kwestie werd vastgesteld als **midline tabbing**. Als de gebruiker begon met het typen van een commando, of eventueel kopiëren van een
commando in een opdrachtprompt en de cursor naar het midden van de lijn zou bewegen zou
de opdrachtprompt alles na de voltooide parameter verwijderen.

Neem bijvoorbeeld de volgende command:

```PowerShell
PS C:\> Start-job -ScriptBlock { Get-WmiObject -Class Win32_Process }
```

Dit commando zal een job starten die alle exemplaren van de Win32_Process zal terugkeren beginnen de
WMI klasse. Als we begonnen met het typen van de parameter,
dan op de Tab-toets drukten (zoals aangegeven door de <tab> syntax in het volgende commando)
zou de command-line de rest van de lijn, achter de parameter verwijderen:

```PowerShell
PS C:\> Start-job –N<tab> -ScriptBlock { Get-WmiObject -Class
Win32_Process }
```

Het vorige commando in PS 2.0:

```PowerShell
PS C:\> Start-job –Name
```

In PS 3.0:

```PowerShell
PS C:\> Start-job –Name -ScriptBlock { Get-WmiObject -Class Win32_Process
}
```

Deze eenvoudige verbetering was zeer nodig. Hetzelfde tab completion
gedrag is beschikbaar voor de geneste script blok gevonden in onze start-Job
command line oproep in dit voorbeeld. Bijvoorbeeld, het toevoegen van een computer naam aan de
Get-WMIObject oproep voor de parameter klasse leidt niet tot het schrappen van de
rest van de opdrachtregel:

```PowerShell
PS C:\> Start-job –Name -ScriptBlock { Get-WmiObject –Co<tab> -Class
Win32_Process }
```

De eerdere opdrachtregel resulteert in de volgende:


```PowerShell
PS C:\> Start-job –Name -ScriptBlock { Get-WmiObject –ComputerName -Class
Win32_Process }
```

In PowerShell 2.0 was het mogelijk om het tab completion gedrag aan te passen. U
kon gewoon voorrang geven op de default function **TabExpansion** met uw eigen versie.
In PowerShell 3.0 is er niet langer een default function **TabExpansion** maar een
default function **TabExpansion2**. We kunnen dit zien door het volgende commando aan te roepen:

```PowerShell
PS C:\> Get-Command TabExpansion*
```

![Tab Expansion](https://i.gyazo.com/bd22007a271c216ded4ee8a12da369f6.png)


Het is nog steeds mogelijk om het tab completion gedrag te overschrijven door het gebruik van de
originele TabExpansion functie. PowerShell zal de aangepaste, door de gebruiker gedefinieerde TabExpansion functie gebruiken als het
bestaat in de huidige sessie. De functie tab completion moet een array van
mogelijke waarden **of $null** teruggeven:

```PowerShell
PS C:\> function TabExpansion { "Get-ChildItem" }
```

Deze tab completion functie is een slecht idee omdat alle tab expansions zullen resulteren in het
cmdlet **Get-ChildItem** , maar het laat zien hoe makkelijk het is om onze eigen tab completion gedrag te creëren. Met onze nieuwe, slecht ontworpen tab
completion functie kunnen we beginnen met het typen van een reeks commando's:

```PowerShell
PS C:\> Set<tab>
```

Dit zou resulteren in het volgende:

```PowerShell
PS C:\> Get-ChildItem
```

Niet de meest bruikbare tab expansion gedrag! Om onze aangepaste tab completion te verwijderen
kunnen we de functie provider die wordt geleverd in PowerShell gebruiken. De commando
sequence zal het tab completion gedrag weer terugzetten. De
volgende command geeft dit:

```PowerShell
PS C:\> Remove-Item function:\TabExpansion
```

Het is mogelijk om de vooraf gedefinieerde functie TabExpansion2 te verwijderen met dezelfde
methode, maar dit tab completion helemaal uitschakelen. Naast de
verbeteringen voor midline tabbing zullen de core modules ondersteuning bieden voor betere completion van
parameterwaarden, zelfs wanneer er geen parameters worden gespecificeerd. Voorheen een cmdlet
zoals Stop-proces, zou je de naam van een lopend proces moeten typen
voordat u het als een parameter waarde kon doorsturen:

```PowerShell
PS C:\> Stop-Process Notepad
```

In PowerShell 3,0, ondersteunen veel van de kern cmdlets parameterwaarde completion.
Je kan nu het volgende typen:

```PowerShell
PS C:\> Stop-Process N<tab>
```

Dit zou resulteren in terug te keren van een proces startende
met een N als we drukken op de Tab-toets. Als **Notepad** het enige lopend proces was, zou dit leiden tot:

```PowerShell
PS C:\> Stop-Process Notepad
```

De cmdlets dat het ondersteunen kunen de functie op meerdere eigenschappen gebruiken. Bijvoorbeeld, de Get-Job
cmdlet ondersteunt zowel **ID** als **Name** parameterwaarde expansie. Enkele andere cmdlets
dat dit type uitbreiding ondersteunen zijn **Get-EventLog** voor log namen en **Get-Service** voor dienst namen:

```PowerShell
PS C:\ > start-job -Name test -ScriptBlock { Get-Process }
```

![Tab Get-service](https://i.gyazo.com/6448d71b9b8c3f5c74f27482646acf5b.png)

```PowerShell
PS C:\> Get-Job <tab>
```

Dit zou het volgende opleveren:

```PowerShell
PS C:\> Get-Job 2
```

De laatste uitbreiding op het gebied van tab completion is de mogelijkheid om enumerated
values te expanderen:


```PowerShell
PS C:\> Set-ExecutionPolicy –ExecutionPolicy <tab>
PS C:\> Set-ExecutionPolicy –ExecutionPolicy AllSigned
```

<div id='15'/>
##Plannen van jobs


PowerShell 2.0 introduceerde het concept van een job. Een job is een eenheid van werk dat onafhankelijk kan lopen van wat er gaande is met de opdrachtregel of de rest van het script.
Dit laat toe om gelijktijdige jobs te laten draaien op hetzelfde moment. Veel jobs kunnen
worden gepland; alle werkzaamheden draaien op de achtergrond terwijl de opdrachtregel
blijft functioneren of het script blijft draaien. Dit was een enorme verbetering
over wat Windows-beheerders hadden in het verleden. Liever dan
te hoeven wachten op een eenheid van het werk, kunnen we talrijke
acties tegelijk verwerken. Dit bespaarde tijd en liet de beheerder toe om te werken aan iets
anders. Daarnaast kunnen jobs op afstand worden uitgevoerd, verspreid over de gehele infrastructuur.

Het is mogelijk om het uitvoeren van een script te plannen met de
PowerShell executable met het volgende commando:

```PowerShell
powershell.exe –File C:\CleanOldUsers.ps1' "
```

Dit commando kan op de Windows Task Scheduler worden toegevoegd als een fundamentele taak.

![Jobs Task scheduler](https://i.gyazo.com/bf5df3e300acd9c6acaa84595de9759c.png)



#### Het creëren van een job trigger

De eerste stap bij het plannen van een nieuwe job is een object dat het schema definieert creëren
waarop de taak zal starten. Dit staat ook bekend als een job trigger.

```PowerShell
PS C:\> New-JobTrigger -At 1:00AM -Daily
```

![Jobs Trigger](https://i.gyazo.com/10ceccebda4120d0811e950c032cf11e.png)

De New-JobTrigger cmdlet vereist dat de parameter op worden gespecificeerd. de At
parameter accepteert een DateTime object.


Om jobs te compenseren kunnen we zelfs de parameter RandomDelay opgeven. Deze
parameter accepteert een TimeSpan object.

```PowerShell
PS C:\> New-JobTrigger -Daily -At 1:00PM -RandomDelay (New-TimeSpan
-Minutes 1)
```

Om het nieuw-JobTrigger cmdlet nuttig te maken, is het noodzakelijk om het resultaat van de
cmdlet naar de Register-ScheduledJob cmdlet te sturen. Dit is het meest eenvoudig te doen door gebruik te maken van een variabele:

```PowerShell
PS C:\ > $DailyTrigger = New-JobTrigger -At 1:00AM –Daily
```

De $DailyTrigger variabele kan nu worden doorgegeven aan de Register-ScheduledJob
cmdlet om onze job te plannen met behulp van volgend commando:

```PowerShell
PS C:\ > Register-ScheduledJob -Name RestartFaultyService -ScriptBlock {
Restart-Service FaultyService }
-Trigger $DailyTrigger
```

Dit levert de volgende output:

![Jobs Register](https://i.gyazo.com/3fc556f77096fc745d0019d5edfd9fd0.png)

Als we de Get-ScheduledJob cmdlet runnen zal onze nieuwe job geretourneerd worden:

```PowerShell
PS C:\ > Get-ScheduledJob
```

In de tweede methode, de Get-ScheduledJob cmdlet aanvaardt zowel de naam en ID als 
input, zodat alleen bepaalde jobs geretourneerd worden:

```PowerShell
PS C:\ > Get-ScheduledJob -Name RestartFaultyService
```

#### Geplande taken bekijken in de Windows-Taakplanner

![Jobs Task scheduler UI](https://i.gyazo.com/44f58025534fadf4ba79d9bb89cb51bd.png)

Alle geplande PowerShell jobs kunnen worden gevonden onder
**Microsoft \ Windows \ PowerShell \ ScheduledJobs**

De Get-Job cmdlet zal het voltooide of lopende geplande taken als volgt teruggeven:

```PowerShell
PS C:\ > Get-Job
```

Output:

![Jobs Get-job](https://i.gyazo.com/3b753e911030cb63a4cfca0979392ce6.png)

Net als bij een in-sessie job, kunnen we het resultaat van de opgegeven jobs ontvangen. Dir
commando leest de resultaten van de geplande jobs.

```PowerShell
PS C:\ > Receive-Job 2
```

Net als bij de Windows Taakplanner, is het mogelijk om met behulp van de command line jobs uit te schakelen. Dit kan worden bereikt met behulp van de Disable-ScheduledJob cmdlet:

```PowerShell
PS C:\> Disable-ScheduledJob –Name RestartFaultyService
```

Willen we de job opnieuw inschakelen gebruiken we alleen de Enable-ScheduledJob cmdlet:

```PowerShell
PS C:\> Enable-ScheduledJob –Name RestartFaultyService
```

Wanneer we niet langer een job nodig hebben, kunnen we het te verwijderen met de
Unregister-ScheduledJob cmdlet:

```PowerShell
PS C:\> Unregister-ScheduledJob –Name RestartFaultyService
```

<div id='16'/>
##Server Roles en Features Configureren

Het is mogelijk de default shell can command prompt aan te passen naar powershell.
Hiervoor ga je naar het registry ```HKLM:\Software\Microsoft\Windows NT\CurrentVersion\winlogon``` en verander ```cmd.exe``` naar ```powershell.exe```. Dit kan je veranderen met gebruik van ```PS``` of ```regedit```.

Voor powershell doe je het volgende commando:

C:\Users\Administrator> PowerShell.exe
PS > Set‑ItemProperty "HKLM:\Software\Microsoft\Windows NT\
CurrentVersion\winlogon" Shell PowerShell.exe

### 1 Veranderen van de computer naam

```PS > Rename-Computer –NewName HQ-DC-01```

```PS > Restart-Computer```

### 2 De tijd zone veranderen

Laat de huidige tijd zone zien

```
PS > TZutil /g
```

Geef een lijst van alle beschikbare tijd zones

```
PS > TZutil /l
```

Zet de nieuwe tijd zone

```
PS > TZutil /s "Greenwich Standard Time"
```

### 3 De NIC configureren met PS

Zet de DNS configuratie voor de client computer

Maak een statisch IP Address 

```
PS > New‑NetIPAddress ‑IPAddress 192.168.0.2 ‑InterfaceAlias Ethernet
‑DefaultGateway 192.168.0.1 ‑AddressFamily IPv4 ‑PrefixLength 24
```

Maak de Client DNS Settings

```
PS > Set‑DnsClientServerAddress ‑InterfaceAlias Ethernet
‑ServerAddresses 192.168.0.1,192.168.0.2
```

Of als je DHCP alleen wilt gebruiken doe je deze cmdlets:

Verwijder static IP Address Settings

```
PS > Remove‑NetIPAddress ‑InterfaceAlias Ethernet
```

Verwijder network route

```
PS > Remove‑NetRoute ‑InterfaceAlias Ethernet
```

Reset de  Client DNS Settings

```
PS > Set‑DnsClientServerAddress ‑ResetServerAddresses
```

Enable de DHCP option op de interface

```
PS > Set‑NetIPInterface ‑InterfaceAlias Ethernet ‑Dhcp Enabled
```

### 4 Managen van windows server roles en features

Je kan de ```Get‑WindowsFeature``` cmdlet gebruiken om alle geïnstalleerd rollen en features te bekijken.

Geef een lijst van al de geïnstalleerde rollen en features

```
PS > Get-WindowsFeature | where Installed –eq $true
```

![Alt text](http://i.imgur.com/K0cLcFC.png)

#### Voor tools toe te voegen moet je deze cmdlets gebruiken:

Deze cmdlet is voor subfeatures toe te voegen aan een role en ze 1 voor 1 wilt installeren.

```
‑IncludeAllSubFeature
```

Dit is voor extra tools toe te voegen zoals met de ISS feature die niet automatisch tools installeerd na het toevoegen van deze feature.

```
‑IncludeManagementTools
```

#### Voorbeeld:

Een web server role met alle subfeatures en managment tools.

```
PS > Install‑WindowsFeature Web‑Server ‑IncludeAllSubFeature
‑IncludeManagementTools
```

#### De ADDS of active directory domain service role toevoegen

Een nieuwe AD forest installeren door gebruik van de ```Install-ADDSforest``` cmdlet.

DomainName: De root domein naam

DomainNetbiosName: De netbios naam voor het domein

ForestMode: Het functionerings level van de forest

DomainMode: Specifieerd de functies van het domein

SafeModeAdministratorPassword: Administrator password definiëren. Dit is nodig voor AD restore mode.

InstallDNS: Installeerd en configureerd een DNS server role.

Dit kan met de volgende code:

```
PS > Install‑ADDSForest ‑DomainName contoso.local
‑SafeModeAdministratorPassword (ConvertTo‑SecureString P@ssw0rd
‑AsPlainText ‑Force) -DomainMode Win2012 ‑DomainNetbiosname Contoso
‑ForestMode Win2012 ‑InstallDNS
```

#### Een nieuw domein in een bestaande forest aanmaken

NewDomainName: Nieuwe domein naam maken

ParentDomainName: De parents naam voor het nieuwe domein

DomainMode: Specifieërd de functie levels van het domein

DomainType: Het domein type definiëren, dit kan ```Child``` of ```Tree``` zijn.

Voorbeeld:

```
PS > Install‑ADDSDomain ‑NewDomainName corp ‑ParentDomainName contoso
local ‑SafeModeAdministratorPassword (ConvertTo‑SecureString P@ssw0r
‑AsPlainText ‑Force) ‑CreateDnsDelegation ‑Credential (Get‑Credenti`
Contoso\Administrator) ‑DomainMode Win2012 ‑DomainType ChildDomain
```

#### Een nieuwe domain controller aanmaken in een bestaand domein

Met deze cmdlet kan de opdracht uitgevoerd worden ```Install‑ADDSdomaincontroller``` cmdlet.

Voorbeeld:

```
PS > Install-ADDSDomainController -NoGlobalCatalog:$false
‑CreateDnsDelegation:$false -Credential (Get-Credential)
-DomainName "contoso.local" -InstallDns:$true -ReplicationSourceDC
"DC01.contoso.local" -SiteName "Default-First-Site-Name"
-SafeModeAdministratorPassword (ConvertTo-SecureString P@ssw0rd
-AsPlainText -Force)
```

### Configureren van de DNS role

#### Configureren van DNS server records

Een nieuw DNS server A resource record toevoegen

```
PS > Add-DnsServerResourceRecordA ‑Name FileServer ‑Ipv4Address
192.168.1.20 ‑ZoneName Contoso.local
```

Een nieuw DNS server 'CName' Resource record toevoegen

```
PS > Add-DnsServerResourceRecordCName ‑Name OWA ‑HostNameAlias
EXCH‑MBXCAS‑02.Contoso.local ‑ZoneName Contoso.local
```

Een nieuw DNS server 'MX' Resource record toevoegen

```
PS > Add-DnsServerResourceRecordMX ‑Name Mail ‑MailExchange
EXCH‑HUB‑01.Contoso.local ‑ZoneName Contoso.local –Preference 10
```

#### Maken van primary forward en reverse lookup zones

Een DNS forward zone toevoegen

```
PS > Add-DnsServerPrimaryZone ‑Name 'Labs' ‑ReplicationScope Domain
‑DynamicUpdate Secure
```

Een DNS server reverse lookup zone toevoegen

```
PS > Add-DnsServerPrimaryZone ‑NetworkId '192.168.1.0/24'
‑ReplicationScope Forest ‑DynamicUpdate NonsecureAndSecure
```

Een DNS forwarder toevoegen

```
PS > Add-DnsServerForwarder –IPAddress '4.2.2.3','8.8.8.8'
```

Een DNS server zone exporteren

```
PS > ForEach($Zone in (Get-DnsServerZone | Where IsAutoCreated -eq
$false))
{
Export-DnsServerZone -Name $Zone.ZoneName -FileName $Zone.ZoneName
}
```

### Een DHCP role toevoegen en host configureren

#### 1 Installeren van DHCP server role

Server role en module toevoegen

```
PS > Add-WindowsFeature DHCP
```

#### 2 Een DHCP server scope opzetten voor ipv4

DHCP scope met naam Contoso voor 192.168.0.0 subnet met een masker 255.255.255.0 en dan activeren.

```
PS > Add‑DhcpServerv4Scope ‑Name "Contoso" ‑StartRange 192.168.0.1
‑EndRange 192.168.0.254 ‑SubnetMask 255.255.255.0 ‑State Active
```

#### 3 Configureren van de DHCP scope options

DNS domain naam, DNS server address, win server en default gateway.

```
PS > Set‑DhcpServerv4OptionValue ‑DnsDomain contoso.local ‑DnsServer
192.168.0.2 ‑Router 192.168.0.1
```

#### 4 Configureren van DHCP scope exclusions

Dit wordt gebruikt wanneer je een range van specifieke addressen statisch voor toestellen wilt gebruiken.

```
PS > Add‑DhcpServerv4ExclusionRange ‑ScopeId 192.168.0.0 ‑StartRange
192.168.0.100 -EndRange 192.168.0.130
```

#### 5 Configureren van DHCP scope reservaties

Ip address 192.168.0.10 wordt gereserveerd voor het mac addres F4-DA-F1-78-00-6D van de netwerk printer. 

```PS > Add‑DhcpServerv4Reservation ‑ScopeId 192.168.0.0 ‑IPAddress
192.168.0.10 ‑ClientId F4-DA-F1-78-00-6D ‑Description "Multi-Function
Network Printer in 3rd floor"```

#### 6 Toestemming geven aan de AD met de DHCP server

In dit voorbeeld wordt ```Add‑DhcpServerInDC``` cmdlet gebruikt om de DHCP server toe te voegen.

```
PS > Add‑DhcpServerInDC ‑DnsName "DhcpServer.contoso.local"
```

### Het managen van de windows firewall

#### 1 Enablen of disablen van Windows firewall profiles

Hier gebruiken we de cmdlet Set‑NetFirewallProfile voor om alle windows firewall profiles te disablen en dan het publieke profiel te enablen.

Om alle profielen te disablen

```
PS > Set-NetFirewallProfile –All –Enabled False
```

Om alle profielen te enablen

```
PS > Set-NetFirewallProfile –Name Public –Enabled True
```

#### 2 Nieuwe firewall regels maken

Voorbeeld 1 Al het uitgaand verkeer blokkeren voor alle FTP protocols:

```
PS > New-NetFirewallRule -Name "Block FTP" ‑DisplayName "Block FTP"
‑Direction Outbound ‑Action Block ‑Protocol TCP ‑LocalPort FTP
```

Voorbeeld 2 Al het ingaande verkeer toelaten voor Skype:

```
PS > New‑NetFirewallRule ‑Name "Skype" ‑DisplayName "Skype" ‑Direction
Inbound ‑Action Allow ‑Program "C:\Program Files (x86)\Skype\Phone\
Skype.exe"
```

### Best practice Analyzer

Blijkbaar heb je in powershell een soort tool die je server configuratie vergelijkt met de standaarden van Windows.

#### 1 Alle lijsten van de BPA Models

```
PS > Get-BpaModel
```

Lijst van de laatste scan time

```
PS > Get-BpaModel | where LastScanTime –eq Never
```

#### 2 Een praktijk model oproepen

Dit scant de server voor beste gebruik en complicaties die problemen geven voor de file services

```
PS > Invoke-BpaModel –ModelId Microsoft/Windows/FileServices
```

![Alt text](http://i.imgur.com/8eLONIq.png)

#### 3 Beste resultaten laten zien

Met de cmdlet Get-BpaResult kunnen we de resultaten laten zien van de beste praktijk scan dat was uitgevoerd in het vorige voorbeeld.

```
PS > Get-BpaResult –ModelId Microsoft/Windows/FileServices
```

![Alt text](http://i.imgur.com/S69MynU.png)

<div id='17'/>
##Beheer Active Directory met PowerShell

### Active Directory-verwante concepten

#### Introductie op Active Directory

Active Directory (AD) verschaft informatie over het opslag netwerk object en maakt deze informatie beschikbaar voor gebruikers en netwerk beheerders die de Active Directory services gebruiken.
Active Directory kan allerlei soorten informatie over het object opslaan en eenvoudig toegankelijk maken. 
Het gebruikt informatie van de gestructureerde data opslag directory als de logische structuur van het fundament van de AD; tegelijkertijd zal het veilig worden geïntegreerd in de Active Directory. 
Door middel van de netwerk login kan de systeem beheerder het gehele netwerk van directory data en eenheden beheren, en gemachtigde netwerk gebruikers hebben ook toegang tot het netwerk op een lokale bron.

Active Directory omvat twee aspecten: een directory object en een directory service.

Een directory object slaat informatie op over allerlei soorten object met een fysieke aard, waardoor we de active directory vanuit een statische oogpunt beter kunnen begrijpen. 
We moeten de "catalogus" of "map" enkel als een object of een entiteit beschouwen, waar geen groot verschil tussen bestaat.

Een directory service geeft de directory welke alle informatie en resources bevat de gelegenheid om een service-rol te vervullen. Active Directory is een verdeelde directory service. 
Hoewel informatie verspreid wordt over verschillende computers, kunnen gebruikers snel informatie raadplegen. 
Aangezien verschillende apparaten dezelfde informatie kunnen verschaffen, kan het systeem veel fouten verdragen. Daardoor biedt Active Directory eenzelfde beeld aan alle gebruikers,
ongeacht waar de gebruiker inlogt en waar de informatie is.

#### Namespace

Active Directory is in essentie een namespace. We kunnen namespace toevoegen aan elke naam bij de analytische grens.
De grens gekoppeld aan de naam kan het bereik bepalen voor het in kaart brengen van de informatie. 
Name resolution levert een naam op, die vertaald wordt naar een naam die het object of de verwerking van informatie vertegenwoordigt

#### Object

Objecten zijn de informatie entiteiten in Active Director. We zien ze meestal als eigenschappen, maar het zijn sets van attributen, 
die vaak fysieke entiteiten zoals gebruiker accounts en bestandnamen voorstellen. 
Objecten kunnen met behulp van de attributenbeschrijving van hun basiseigenschappen (zoals een gebruikersaccountattribuut), onder meer een klanttnaam, telefoonnummer, e-mail adres en thuisadres bevatten.

####Container

Een container is bij de Active Directory het deel van de ruimte en het directory object bestemd voor namen. Het heeft tevens attributen, maarf het directory object is anders. Het vertegenwoordigt geen tastbaar object, maar een opslag object ruimte.
Aangeizne het slecht een opslag object ruimte vertegenwoordigt, is het maar een kleine namespace.

#### Trees

In elke namespace, verwijst een directory tree naar de object container en de hierarchische structuur. De bladeren en knopen van een boom zijn vaak de objecten, en een boom zonder bladeren of bomen is een container. Een directory tree geeft de wijze
waarop objecten zijn verbonden aan. Het toont ook het pad van één object naar een ander object.

In de Active Directory is de directory tree de basisstructuur. Als elke container een startpunt is, waarbij de laag-op-laag methode wordt gebruikt, kan hiermee een subtree worden gevormd. 
Een tree kan uit een simpele directory bestaan, en een computernetwerk of domein kan een boom vormen. Een directory tree beschrijft in feite een soort 'path' relatie.

#### Domein

Een domein is het logische, fundamentele bouwblok voor het partitioneren van Active Directory. Partitioneren is een belangrijk concept van directory services omdat het het gebruik van meerdere directory partities toelaat, in plaats van één grote opslag.
De opslag van elk domein hoeft vervolgens enkel de informatie op te slaan over de objecten binnen dat domein, waardoor de Active Directory als geheel zeer schaalbaar wordt.

### Active Directory met PowerShell beheren

### Gebruiker beheer

De AD module in PowerShell kan gebruikt worden om de gebruiker en computeraccounts in de Active Directory Domain Services (AD DS) te beheren. Hieronder wordt getoond hoe je de AD module kunt gebruiker om gebruikers te beheren.

#### Een AD gebruiker creëren

Het volgend voorbeeld toont aan hoe de AD module voor Windows Powershell gebruikt kan worden om een nieuwe gebruiker in AD DS te maken.
We maken een nieuwe gebruiker aan (```TestUser```) met een wachtwoord (```p@ssword```) in een organisatie unit (```Test```) in het ```fuhaijun.com``` domein:

```
New-ADUser-SamAccountName TestUser -Name "A Test User" -AccountPassword
(ConvertTo-SecureString -AsPlainText "p@ssw0rd" -Force) -Enabled $true
-Path 'OU=Test,DC=FUHAIJUN,DC=COM'
```

Hier proberen we door middel van de ```-Force``` parameter een doorsnee tekst string te veranderen in een beveiligingsstring welke gebruikt wordt als wachtwoord.
De ```-Path``` parameter wordt gebruikt om het domein path dat de user maakt te specificeren.

#### Instellen dat een gebruikersaccount verloopt

Soms is het nodig om een tijdelijk gebruikersaccount te maken, dat na een bepaalde periode verloopt.

```
Set-ADUser TestUser -AccountExpirationDate 11/27/2014
```

De ```Set-ADUser``` cmdlet wordt gebruikt om in te stellen dat de gebruiker (```TestUser```) vervalt op 11/27/2014.

#### De gebruiker dwingen het wachtwoord te veranderen bij de volgende inlogpoging

Om je ervan te verzekeren dat het wachtwoord van een nieuwe gebruiker geheim blijft, kun je de gebruiker dwingen het wachtwoord bij de volgende inlogpoging te veranderen.

```
Set-ADUser -Identity TestUser -ChangePasswordAtNextLogon $true
```

We dwingen de gebruiker (```TestUser```) om het wachtwoord te veranderen door de ```-ChangePasswordAtNextLogon``` switch parameter toe te wijzen.

### Gebruikers ervan weerhouden het wachtwoord te veranderen

Bij speciale gebruikers accounts, zoals een account dat gedeeld wordt door verschillende gebruikers, moeten we deze gebruikers ervan weerhouden het wachtwoord te veranderen.

```
Set-ADAccountControl -Identity TestUser -CannotChangePassword $true
```

De ```-CannotChangePassword``` parameter wordt gebruikt om de gebruiker (```TestUser```) ervan te weerhouden het wachtwoord aan te passen.

### Computer management

Als een computer in een domein bestuurd moet worden, moet deze verbonden worden aan het domein. 
De volgende voorbeelden leggen uit hoe je de Active Directory module in PowerShell kunt gebruiken voor computer management.

### Een computer aan een domein verbinden

De command (hieronder) moet lokaal op de computer worden uitgevoerd als je de betreffende PC aan het ```fuhaijun.com``` domein wil toevoegen. Hierbij gebruiken we steeds de gegevens van de huidige ingelogde gebruiker.

```
Add-Computer -DomainOrWorkgroupName fuhaijun
```

Wanneer we de computer ```Win8Client``` aan het ```fuhaijun.com``` domein moeten toevoegen en een domain controller specificeren met de ```-server``` parameter, voeren we het volgende commando in:

```
Add-Computer Win8Client -DN fuhaijun -Server Win2012-ad
```

Natuurlijk kunnen we de lokale PC ook toevoegen aan de OU in de directory die met de ```-OUPath``` parameter is aangeduid

```
Add-Computer -DomainOrWorkgroupName fuhaijun -OUPath
OU=testOU,DC=fuhaijun,DC=com
```

### De naam van een computer veranderen

We kunnen de naam van een lokale computer verbonden met het domein veranderen door de volgende command uit te voeren:

```
Rename-Computer -NewName win8client2 -DomainCredential fuhaijun\
administrator –Restart
```

Dit voorbeeld laat zien hoe je de naam van de PC naar ```Win8Client2```, waarbij de parameter ```-DomainCredential``` wordt gebruikt om de bevoegdheid van een beheerder van het domein aan de duiden.
Om te zorgen dat de veranderingen in werking treden nadat de hostname is aangepast, moet na afloop de ```-Restart``` parameter worden gebruikt (om de PC te herstarten). Deze command moet lokaal op de PC uitgevoerd worden.

### Beheren van een groep

Een groep is een verzameling van objecten met dezelfde karakteristieken. 

#### De gebruikersrechten (permissions) van een groep bekijken

Om de rechten van een groep te achterhalen kun je vanuit de ```AD:\>``` drive de volgende command uitvoeren. De |drive moet verbonden zijn met het domein waarbinnen de groep bestaat.

```
Get-ACL (Get-ADGroup UserGroup) | fl * -f
```

We krijgen dan het volgende resultaat:

![Alt text](http://i.imgur.com/0G9umFN.png)

We gebruiken de `````` cmdlet om de bestaande groep, ```UserGroup```, te verkrijgen. We passen daarop de ```Get-ACL``` cmdlet toe en tot slot de ```Format-List``` cmdlet om de output op te maken als lijst.

#### Een groep maken

Als we de rechten van de groep hebben bekeken, moeten we een groep aanmaaken om een serie AD objecten te beheren. Het volgende voorbeeld illustreert hoe je een groep genaamd ```ProductAdmins``` aanmaakt in het ```fuhaijun.com``` domein:

```
New-ADGroup -Name "Product Admins" -SamAccountName ProductAdmins
-GroupCategory Security -GroupScope Global -DisplayName "Product
Administrators" -Path "CN=Users,DC=fuhaijun,DC=Com"
```

Als deze command is uitgevoerd, kunnen we met ADSI Edit de nieuwe groep ```ProductAdmins``` vinden:

![Alt text](http://i.imgur.com/Epsf87i.png)

### Leden aan een groep toevoegen of verwijderen

We kunnen de ```Add-ADGroupMember``` cmdlet gebruiken om gebruiker ```fuhj``` aan de groep ```ProductAdmins``` toe te voegen

```
Add-ADGroupMember -Identity ProductAdmins -Member fuhj
```

De parameter ```-Identity``` wordt gebruikt om de groep aan te duiden waaraan het nieuwe lid wordt toegevoegd. 
De parameter ```-Member``` wordt gebruikt om het nieuwe lid van de operationele groep te specificeren. Als de command is uitgevoerd,
kunnen we de ```ProductAdmins``` groep vinden in de eigenschappenm van gebruiker ```fuhj``` onder het tabblad 'Member Of'.

![Alt text](http://i.imgur.com/X1Z1itK.png)

Als je een groep wil verwijderen, kun je de ```Remove-ADGroup``` cmdlet gebruiken om zo een Active Directory groep object te verwijderen. Je kunt deze cmdlet gebruiken om security en distribution groepen te verwijderen.

```
Get-ADGroup -filter 'Name -like "Product*' | Remove-ADGroup
```

Dit voorbeeld toont aan hoe je alle groepen vindt waarvan de naam met het woord ```Product``` begint, en deze vervolgens verwijdert.
De ```-Identity``` parameter specificeert de AD groep die verwijderd moet worden. Je kunt een groep identificeren middels de distinguished name (DN), GUID, security identifier (SID),
Security Accounts Manager (SAM) account naam, of canonieke naam. Je kunt de ```-Identity``` parameter ook instellen op een object variabele, zoals ```$<localADGroupObject>```, of je kunt
een object door de pipeline naar de ```-Identity``` parameter laten gaan. Zo kun je de ```Get-ADGroup``` cmdlet gebruiken om een groepsobject te vinden en dan het object door de pipeline halen naar de ```Remove-ADGroup``` cmdlet.
Als ```ADGroup``` wordt geïdentificeerd door middel van de DN, zal de parameter ```-Partition``` automatisch bepaald worden.

In AD LDS omgevingen moet de ```-Partition``` parameter gespecificeerd worden, met uitzondering van de volgende gevallen:
1. De cmdlet wordt uitgevoerd vanaf een Active Directory provider station.
2. Er is een standaard naamgevingscontext of -partitie gedefinieerd voor de AD LDS-omgeving

Om een standaard naamgevingscontext te specificeren voor een AD LDS omgeving, stel je de ```msDS-defaultNamingContext``` eigenschap van het Active Directory directory service agent (DSA) object (nTDSDSA) in voor de AD LDS instantie.

### Organizational Unit management

Organizational Units (OU) zijn Active Directory containers waarin je gebruikers, groepen, computers en andere OUs kunt plaatsen.
OU kunnen geen objecten van andere domeinen bevatten. Een OU is de kleinste ruimte of eenheid waaraan je groepsbeleidsinstellingen of
of administratieve bevoegdheden kunt toewijzen. Door het gebruik van OUs, kunt je containers aanmaken binnen een domein die de hiërarchische 
en logische structuren vertegenwoordigen in de organisatie.

#### Een nieuwe OU aanmaken

In onderstaand voorbeeld creëren we een nieuwe OU genaamd ```UserAccounts```, welke zich bevindt in het domein ```fuhaijun.com```.

```
New-ADOrganizationalUnit -Name UserAccounts -Path "DC=FUHAIJUN,DC=COM"
```

We kunnen ook de ```-instance``` parameter gebruiken om een reeds aangemaakt OU object als template aan te duiden:

```
$ouTemplate = Get-ADOrganizationalUnit "OU=UserAccounts,DC=FUHAIJUN,DC=c
om" -properties seeAlso,managedBy;
New-ADOrganizationalUnit -name UserReports -instance $ouTemplate
```

In het voorgaande voorbeeld hebben we een OU genaamd ```UserReports``` gecreërd vanuit het template ```$ouTemplate```.

#### Lijst van OUs

Met de ```Get-ADOrganizationalUnit``` kun je één of meer Active Directory organisatorische units ophalen. Deze cmdlet haalt een OU object op, of voert een zoekopdracht uit om meerdere OUs op te halen.

```
Get-ADOrganizationalUnit -Filter 'Name -like "*"' | ft -AutoSize
```

![Alt text](http://i.imgur.com/U1LUn2O.png)

We zien dat alle organisatorische units die in voorgaande voorbeelden zijn aangemaakt worden opgesomd. De ```Format-Tables``` cmdlet wordt gebruikt om de output display op te maken.

#### De naam van een OU veranderen

We kunnen de ```rename-ADObject``` cmdlet gebruiken om de naam van een OU te veranderen.

```
Rename-ADObject "OU=TestOU, DC=Fuhaijun,DC=Com" -NewName Groups
```

Door het uitvoeren van deze command verander je de naam van het object met de naam ```OU=
TestOU,DC=Fuhaijun,DC=Com``` in ```Groups```.
Of course, we can also use the -Identity parameter with the object GUID in order
to locate the organizational unit object to be renamed.

```
Rename-ADObject -Identity "d465ddc9-a5e6-4998-91aa-09e33fe22369" -NewName
Groups
```

NB: de ```-Partition``` parameter is niet aangeduid omdat het object binnen de standaard naamgevingscontext van het domein valt.

#### Een OU aanpassen

We kunnen de beschrijving van de OU met naam ```OU=
TestOU,DC=Fuhaijun,DC=Com``` aanpassen door middel van de ```Set-ADOrganizationalUnit``` cmdlet.

```
C:\PS>Set-ADOrganizationalUnit -Identity "OU=TestOU,DC=Fuhaijun,DC=COM"
-Description "This Organizational Unit is a test OU of Fuhaijun.COM"
```

We kunnen meerdere eigenschappen tegelijk bewerken. De ```Get-ADOrganizationalUnit``` cmdlet kan ons helpen OU-bestemming (destination) te vinden,
en deze toewijzen aan de variabele ```$AsianSalesOU```. Vervolgens kunnen we de eigenschappen van de variabele instellen, en de ```Set-ADOrganizationalUnit``` cmdlet
gebruiken met de ```-Instance``` parameter om de wijzigingen aan het object op te slaan. Dit gaat als volgt:

```
$AsianSalesOU = Get-ADOrganizationalUnit "OU=Asia,OU=Sales,OU=UserAccount
s,DC=Fuhaijun,DC=COM"
$AsianSalesOU.StreetAddress = "No. 20 Chang An Avenue"
$AsianSalesOU.City = "Beijing"
$AsianSalesOU.PostalCode = "100000"
$AsianSalesOU.Country = "China"
Set-ADOrganizationalUnit -Instance $AsianSalesOU
```

#### Een OU verplaatsen

Om een OU te verplaatsen (bijvoorbeeld wanneer je de structuur van de organisatie wil aanpassen), gebruiken we de ```Move-ADObjecct``` cmdlet.

```
Move-ADObject "OU=ManagedGroups,DC=Fuhaijun,DC=Com" -TargetPath
"OU=Managed,DC=Fuhaijun,DC=Com"
```

We gebruiken de ```-TargetPath``` parameter om het bestemmingspad aan te duiden. Deze cmdlet kan ook gebruikt worden om andere AD objecten te verplaatsen.

#### Een OU verwijderen

Het volgende voorbeeld toont aan hoe je een OU (en de verwante child-items) verwijdert.

```
C:\PS>Remove-ADOrganizationalUnit -Identity
"OU=TestOU,DC=FUHAIJUN,DC=COM" -Recursive
Are you sure you want to remove the item and all its children?
Performing recursive remove on Target: 'OU=Accounting,DC=Fuhaijun,DC=com
'.
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help
(default is "Y"):y
```

Als de OU tegen verwijderen beschermd is, wordt deze niet gedelete. Als de OU niet beschermd is, wordt deze verwijderd, zelfs indien alle child-items wél beschermd zijn.
Het is ook mogelijk een OU te verwijderen met gebruik van de object GUID als identiteit, terwijl je de confirmation prompt onderdrukt.

```
Remove-ADOrganizationalUnit -Identity "d465ddc9-a5e6-4998-91aa-
09e33fe22369" -confirm:$false –ProtectedFromDeletion $false
```

We gebruiken de ```-Identity```parameter om de object GUID aan te duiden voor een OU en de ```-confirm:$false``` parameter om de confirmation prompt te onderdrukken.
Als de vlag voor ```-ProtectedFromDeletion``` op ```True``` staat, verwijdert deze cmdlet de OU niet en levert deze een error op.

### Domein controller management

#### Een domein controller vinden

Het volgende voorbeeld toont aan hoe je een domein controller vindt voor het ```Fuhaijun.com``` domein.

```
Get-ADDomainController -Discover -DomainName fuhaijun.com
```

![Alt text](http://i.imgur.com/cK8JD2T.png)

We kunnen alle informatie over de domein controller vinden, inclusief de hostname, IP -adres, enzovoort. Als je alle domeincontrollers voor het domein  wil vinden,
en je ingelogd bent, gebruik je daarvoor de volgende command:

```
Get-ADDomainController –filter *
```

![Alt text](http://i.imgur.com/yg1W5uq.png)

#### De locatie van de domein controller vinden

Nadat we de domein controller hebben gevonden, kunnen we ook de locatie achterhalen door middel van de ```Get-ADDomainController``` cmdlet met de ```-Identity``` parameter.

```
Get-ADDomainController -Identity Win2012-AD | FT Name,Site
```

#### De global catalog servers terugvinden in een forest

De ```Get-ADForest``` cmdlet zoekt de Active Directory-forest die door de parameters wordt gespecificeerd. Je kunt de forest specificeren door ```-Identity``` of ```-Current```
parameters op te geven. De parameter ```-Identity``` duidt het Active Directory-forest aan dat wordt gevraagd. Je kunt een forest identificeren door middel van de fully qualified domain name (FQDN), DNS host-naam, of NetBIOS-naam. 
Je kunt ook de parameter instellen op een forest object variabele, zoals de ```$<localForestObject>```, of je kunt het forest object door een pipeline naar de parameter ```-identiteit``` halen.

```
Get-ADForest Fuhaijun.com | FL GlobalCatalogs
```



<div id='18'/>
##Beheer van een server met PowerShell


###Server Manager cmdlets 
PowerShell laat ons toe om features te installeren op onze Windows Server 2012.
Om te werken met de server manager cmdlets moet men eerst de Server Manager Module laden in PowerShell.
Dat doet men via het commando:
```Powershell
Import-Module Servermanager
```
Om deze features te zoeken gebruikt men het "GET-WindowsFeature" cmdlet.
De checkboxes met een X duiden aan welke features reeds geïnstalleerd zijn.
Men kan features installeren of verwijderen met de cmdlets "INSTALL-WindowFeature" en "UNINSTALL-WindowsFeature".
Men kan ook een pipe line gebruiken om meerdere features te installeren.
Het volgende voorbeeld installeert alle features die beginnen met "web-".
```Powershell
Get-WindowsFeature web-* |Install-WindowsFeature
```
Je kan het ook met een komma doen, zoals in het volgende voorbeeld:
```Powershell
Install-WindowsFeature Telnet-Server,Hyper-V
```

###Netwerkbeheer met PowerShell
Om alle interfaces op onze server te bekijken gebruiken we het cmdlet "GET-NetIPInterface". (Men kan de parameter -InterfaceAlias gebruiken om een specifiek interface te gebruiken)
Als we dan een nieuwe interface willen toevoegen, moeten we het cmdlet "NEW-NetIPInterface" gebruiken met de nodige parameters,
zoals de interface alias, het adres, soort van ip-adres en de prefix van het subnet mask.
Hieronder een voorbeeld waarbij ik een interface genaamd Ethernet 2 aanmaak.
```Powershell
New-NetIPInterface -InterfaceAlias "Ethernet 2" -IPAddress 192.168.10.20 `
-AddressFamily IPv4 -PrefixLength 24
```
Men kan ook bindings inschakelen en uitschakelen met Powershell.
Om de bindings van een interface te bekijken gebruikt men:
```Powershell
GET-NetwerkAdapterBinding -InterfaceAlias "Ethernet 2"
```
Om bijvoorbeeld de binding ms_lltdio uit te schakelen gebruikt men het commando:
```Powershell
Disable-NetAdapterBinding -Name "Ethernet 2" -ComponentID ms_lltdio
```
En natuurlijk kan men ook de netwerkadapter zelf uitschakelen door middel van het commando:
```Powershell
Disable-NetAdapter -Name "Ethernet 2"
```


###Group Policy beheer met PowerShell
Voor men Group Policy cmdlets kan gebruiken moet men de Group Policy Management Console installeren, dit doen we zo:
```Powershell
Import-Module ServerManager
```
```Powershell
Add-WindowsFeature GPMC
```
Om al de Commandos binnen deze module te bekijken, gebruiken we:
```Powershell
Get-Command -Module GroupPolicy
```
Om Group Policy Objects (GPO) te bekijken gebruiken we het cmdlet "GET-GPO" waarbij men natuurlijk ook parameters kan gebruiken.
Men kan ook GPO's maken met het cmdlet "NEW-GPO", hieronder een beter voorbeeld: 
```Powershell
New-GPO -Name TestGPO -Comment "This is a GPO for testing purposes"
```


###IIS beheer met PowerShell
Hier ook, om te kunnen werken met de Web Administration cmdlets, moet men de module importeren:
```Powershell
Import-Module WebAdministration
```
Om een website aan te maken gebruiken we het cmdlet "NEW-Website" met de nodige parameters:
```Powershell
New-Website -Name testsite -Port 80 -HostHeader testsite -PhysicalPath
c:\temp
```
Web Binding instellen:
```Powershell
Set-WebBinding -Name 'Default Web Site' -BindingInformation "*:80:"
-PropertyName Port -Value 1234
```
Men kan ook een FTP site maken:
```Powershell
New-WebFtpSite -Name testFtpSite -Port 21 -PhysicalPath c:\test
-HostHeader mySite -IPAddress 127.0.0.1
```
Of een virtuele directory:
```Powershell
New-WebVirtualDirectory -Site "Default Web Site" -Name TestVDir
-PhysicalPath c:\inetpub\virtualdirectory
```
PowerShell kan ook een back-up nemen van de webconfiguratie of die weer herstellen.
Om een back-up te nemen gebruik je "Backup-WebConfiguration" met -Name als parameter.
Als je een back-up wil herstellen gebruik je "Restore-WebConfiguration" met de naam als parameter.


###DNS server beheer met PowerShell
Om een lijst te krijgen van de zones op een DNS server gebruikt men het "GET-DnsServerZone" cmdlet.
Als je de records van een bepaalde zone wilt bekijken gebruikt men het "Get-DnsServerResourceRecord" cmdlet, met de nodige parameter.
```Powershell
Get-DnsServerResourceRecord -ZoneName Test.com
```
Om een resource record toe te voegen gebruikt men het gepaste commando, afgaand van het record type, 
voor een record van type a is het bijvoorbeeld:
```Powershell
Add-DnsServerResourceRecordA -IPv4Address 192.168.2.1 -Name gateway
-ZoneName Test.com
```



<div id='19'/>
##Beheer van Exchange server

###Exchange 2010 cmdlets
De makkelijkste manier om de Exchange cmdlets te bekijken is de "GET-ExCommand" functie.
Als men deze cmdlet probeert, ziet men dat men meer dan 600 functies heeft voor een Exchange server te beheren.
Het enige dat je niet kan doen is gebruikers en groepen aanmaken.

Natuurlijk kan men bij Get-ExCommand weer pipelines gebruiken om specifieker te zoeken:
```Powershell
Get-ExCommand | Where-Object { $_.name -match 'statistics'} |
Foreach-Object { get-help $_.name | select-object -expandProperty syntax}
```
Dit commando geeft een lijst van commands dat informatie geven in verband met statistics.
Dit is de voorbeeldoutput van het commando:
```Powershell
Get-ActiveSyncDeviceStatistics -Identity <ActiveSyncDeviceIdParameter> [-DomainController
<Fqdn>] [-GetMailboxLog
<SwitchParameter>] [-NotificationEmailAddresses <MultiValuedProperty>] [-ShowRecoveryPassword
<SwitchParameter>]
[<CommonParameters>]
Get-ActiveSyncDeviceStatistics -Mailbox <MailboxIdParameter> [-DomainController <Fqdn>]
[-GetMailboxLog
<SwitchParameter>] [-NotificationEmailAddresses <MultiValuedProperty>] [-ShowRecoveryPassword
<SwitchParameter>]
[<CommonParameters>]
```

###remote Exchange servers
Er zijn 2 verschillende soorten van remoting; implicit remoting en explicit remoting.
Bij explicit remoting creeër je een sessie en dan krijg je een PowerShell console, de console die je ziet bevindt zich op de remote computer. Als je dan Dir typt, krijg je de directories van die computer.
Bij implicit remoting werk je op je eigen computer, dus je PowerShell console is die van je eigen pc, maar je laat de commands door middel van functies op de remote computer uitvoeren.

Om rechten te krijgen voor de remoting gebruik je "Get-credential"
```Powershell
$cred = Get-Credential contoso\administrator
```
Dan maak je een nieuwe sessie op de exchange server aan:
```Powershell
$session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri
http://ex1/powershell -Credential $cred
```
En dan gebruik je Import-PSSession om te connecteren op de sessie:
```Powershell
Import-PSSession $session
```
Als de connectie is gemaakt kan je informatie opvragen over de Exchange server door middel van het cmdlet "GET-ExchangeServer".
Nu kan je ook informatie vragen over de Exchange mailbox databanken met het cmdlet "GET-MailboxDatabase".


###Recepients configureren
Voor we beginnen configureren moet de mailbox aangezet zijn.
Om dit te doen gebruiken we het "Enable-Mailbox" cmdlet met de nodige parameters.
Hier een voorbeeld:
```Powershell
Enable-Mailbox -Identity nwtraders\MyNewUser -Database "mailbox database"
```
Met het "New-Mailbox" cmdlet kan je een gebruiker en een mailbox tegelijk aanmaken.
```Powershell
New-Mailbox -Alias myTestUser2 -Database "mailbox database" `
-Name MyTestUser2 -OrganizationalUnit myTestOU -FirstName My `
-LastName TestUser2 -DisplayName "My TestUser2" `
-UserPrincipalName MyTestUser2@Powershell.com
```
Als je dit commando runned, gaat PowerShell om een paswoord vragen.
Omdat dat een secureString datatype moet zijn, gaat dit niet gaan met een parameter.
Als dit wel geautomatiseerd moet worden kan dit wel met een script.

Je kan de lijst van gebruikers van een mailbox weergeven met het "Get-Mailbox" cmdlet en pipelines als men dat wil.
Get-mailbox werkt ook voor een enkele gebruiker:
```Powershell
Get-Mailbox -identity mytestuser1
```


###Mailbox Databanken
Om een nieuwe mailbox databank aan te maken gebruiken we "New-MailboxDatabase" met de verplichte parameters:
```Powershell
New-MailboxDatabase -Name Mailbox2 -EdbFilePath e:\MbDb2\mailbox2.edb -Server ex1
```
Dan kan men controleren of de databank in de lijst staat met "Get-MailboxDatabase"
Om een databank te mounten gebruikt men het cmdlet "Mount-MailboxDatabase".
Of als men de databank wil verwijderen is er altijd "Remove-MailboxDatabase".







