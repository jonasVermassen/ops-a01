#Windows Powershell

##Inhoudstafel
1. [Using the help system](#1)
2. [Running commands](#2)
3. [Working with providers](#3)
4. [The pipeline](#4)
5. [Objects: data by another name](#5)
6. [Formatting output](#6)
7. [Filtering + Working with files](#7)
8. [Remoting](#8)
9. [Variables](#9)
10. [PowerShell ISE](#10)
11. [Scripting](#11)
12. [Handling errors](#12)
13. [Using CIM](#13)
14. [Enhancements to tab completion](#14)
15. [Scheduling jobs](#15)
16. [Managing Active Directory with PowerShell](#16)
17. [Managing the Server with PowerShell](#17)
18. [Working with functions + advanced functions](#18)
19. [Managing Exchange server](#19)

<div id='1'/>
##Using the help system
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
##Running commands

INSERT CONTENT


<div id='3'/>
##Working with providers

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
##The pipeline

INSERT CONTENT

<div id='5'/>
##Objects: data by another name

INSERT CONTENT

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
##Filtering + Working with files

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
``` naar een andere value te veranderen met set-item cmdlet.

Volgende stap een trusted hosts toevoegen
----

Om alle workgroup-joined computers aan de lijst van trusted hosts toe te voegen doe je. ```Set-item wsman:localhost\client\trustedhosts -value *```

Als je specifiek hosts wilt toevoegen doe je ```Set-item wsman:localhost\client\trustedhosts -value "Computer1,Computer2"```

Je kan dit ook met domeinen en door het ip toe te voegen zoals bv. ```Set-item wsman:localhost\client\trustedhosts -value "192.168.10.11"```

Je kan ook WinRM batch script toevoegen aan een computer lijst. 
```winrm set winrm/config/client `@`{TrustedHosts=`"`192.168.10.11`"`}```

Niet vergeten ```Enable-PSRemoting``` uit te voeren hierna voor de veranderingen.

Remote management door winRM laten.
----

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

Windows Remote Management door de Windows Firewall laten
----

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

Service Windows Remote Management(WS-Management) aanzetten 
----

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

Een Group Policy Update uitvoeren
----

Open een command promt als administrator en voer gpudate /force uit om de veranderingen door te voeren.

Remoting uitschakelen
----
Je kan ```Disable-PSRemoting``` gebruiken om de remote session configuratie uit te schakelen. Enable-PSRemoting alle veranderen door dit commando zullen niet verwijderd worden.

Als geen andere service of component op de lokale pc, de WinRM service nodig heeft kan je de service disablen door het volgende commando uit te voeren ```Set-Service winrm -StartupType Manual``` en ```Stop-Service winrm```.

De remoting commands uitvoeren
----
Wanneer we bezig zijn met remoting kunnen we commando's en scripts uitvoeren op een paar manieren.
De ```Invoke-Command``` cmdlet en interactieve remoting sessies. Een keer dat je remoting hebt geactiveerd op alle computers, kan je de ```Invoke-Command``` cmdlet gebruiken om commando's en scripts te runnen. 

Voorbeeld hiervan:

![Alt text](http://i.imgur.com/kfWTV4s.png)

Wanneer we het ip adress naar de -ComputerName parameter sturen en -ScriptBlock parameter als Get-Process, dan zal de uitvoer terug gestuurd worden naar de lokale pc.

ScriptBlock draaien op een remote computer
----
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

Een persistente sessie maken met de Invoke-Command
----

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

Specifiëren van login gegevens om te remoten
----

In een domein omgeving, kunnen we inloggen als gebruikers alleen als we administrator gegevens hebben om toegang te krijgen tot een pc in een domein. Maar, in een werkgroep, moeten we gegevens doorspelen te samen met het ```invoke-command```.

Bijvoorbeeld:

```
$cred=Get-Credential
Invoke-Command -ComputerName win-8 -ScriptBlock {Get-Service} -Credential
$cred
``` 

In dit voorbeeld ```Get-Credential``` prompt voor de credentials om toegang te geven aan de remote computer en gebruikt dezelfde bij het oproepen van de Invoke-Command cmdlet. Wanneer je ```Get-Credentials``` cmdlet uitvoert krijg je een venster waar je username en password wordt gevraagd. Wanneer je inlog gegevens invult, gaat de cndlet een ```PSCrendential``` object aanmaken die de inlog gegevens van een gebruiker bewaard in het ```$cred``` . 

Een interactieve remote sessie starten
----

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

Uit een interactieve sessie gaan
----

```Exit-PSSession``` Je moet opletten voor parameters als -ComputerName want de Enter-PSSession cmdlet start maar tijdelijk een powershell sessie en geen permanente. Alle variabelen dat je gemaakt hebt en je commando geschiedenis zal verwijderd worden.

Een persistente (volhoudende) sessie starten met interactieve remoting
----

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

Disconnecten en reconnecten van sessies
----

In powershell v3 kan je disconnecten met het ```Disconnect-PSSession``` en verbinden met het ```Connect-Pssession``` cmdlet. Deze commands accepteren elk een sessie object, die je maakt met het ```New-PSSession``` cmdlet.

Een disconnected sessie laat een copy draaien op de remote pc. Dit is een goede manier om het lange taken te laten volbrengen en het dan later weer op te nemen. Je kan zo ook disconnecten en met andere sessies connecteren.

Een voorbeeld van een achtergrond job die op de server door blijft lopen na het disconnecten.

![Alt text](http://i.imgur.com/d6LoCAT.png)

Daarna log je in op een andere machine als de zelfde user van op de andere sessie. We halen de sessie af van de remote pc en reconnecten. Dan krijg je scherm van de nieuwe sessie en zie je de resultaten van de achtergrond job.

Met ```Remove-PSSession``` kan een remote sessie permanent worden afgezet.

Een remote sessie opslaan op de hardeschijf
----

Met het ```Export-PSSession``` cmdlet kunnen we commands exporteren van een remote sessie en ze opslaan in een powershell module op de lokale schijf. Deze cmdlet bewaard cmdlets, functies, aliasen en amdere commando's in een PS module.


```$session = New-PSSession -ComputerName win-8```
```Invoke-Command -Session $session –ScriptBlock {Import-Module NetTCPIP}```
```Export-PSSession -Session $session -OutputModule RemoteCommands```
```-AllowClobber -Module NetTCPIP -Force```

In dit voorbeeld maken we een persistente sessie en importeren we een module genaamd NetTCPIP. Dan gebruiken we het ```Export-PSSession``` cmdlet om alle commands te exporteren. Alles is dan beschikbaar in de PS session $session in een module op de hardeschijf die RemoteCommands heet.

Als de ```Export-PSSession``` cmdlet gelukt is, krijgen we een gelijkaardig input als hier:

![Alt text](http://i.imgur.com/Vxk9BNW.png)

De modules worden gegenereerd onder de .psm1, .psd1 extensies. Nu kan je de modules laden om aan de remote commands te kunnen.

Importeren van een module opgeslagen op een schijf
----

Je hebt geen specifiek pad nodig voor de module. Het volgende commando importeerd alle remote commands verkrijgbaar in een module op de lokale sessie:

```
Import-Module RemoteCommands
```

Dan voeren we het remote commando uit, om een remote sessie te starten, uitvoeren van commandos in de remote sessie en de uitvoer weergeven. Dit gebeurt allemaal als je gelijk welke remoting gerelateerde cmdlet gebruikt.

Limieten van Export-PSSession
----

- Je kan geen programma starten met de user interface omdat het toegang nodig heeft met een interactieve desktop. 

- De geexporteerde module houd niet de opties in van de sessie die gebruikt werd om deze aan te maken.

- Je kan geen PowerShell provider exporteren

Het gebruik van sessie configuraties
----

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

Nieuwe sessie configuraties maken
----

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

Alle beschikbare sessie configuraties lijsten
----

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

Custom permissies en PS sessie configuraties
----

Je kan ```Get-PSSessionConfiguration``` gebruiken om toegang te krijgen voor de nieuwe sessie.

Dit kan met het volgende commando:

```
Set-PSSessionConfiguration -Name NetTCPIP -ShowSecurityDescriptorUI
```

Dit opent een nieuw venster.

![Alt text](http://i.imgur.com/kI6f5EZ.png)

Nu kan je schrijf en lees rechten aanvinken voor de gebruikers en administrator groepen.

Een custom sessie configuratie oproepen
----

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

Uitschakelen van een sessie configuratie
----

Gebruik ```Disable-PSSessionConfiguration``` om een bestaande configuratie te disablen en gebruikers te stoppen van te connecteren vanaf hun lokale pc door gebruik van een sessie configuratie. Met de ```-Name``` parameter kan je specifiëren welke sessie configuratie je wilt uitschakelen. Als je geen configuratie specifieerd zal de default microsoft sessie configuratie uitgeschakeld worden.

De ```Disable-PSSessionConfiguration``` cmdlets voegt een "deny all"setting toe bij de security descriptor van 1 of meerdere geregistreerde sessie configuraties.

De ```Disable-PSRemoting``` cmdlet zal alle PS sessie configuraties uitschakelen die beschikbaar zijn op de lokale pc.

De ```Enable-PSSessionConfiguration``` cmdlet kan gebruikt worden voor het inschakelen of uitschakelen van de configuratie. Met de -Name parameter kan je specifiëren welke configuratie je wilt inschakelen.

Verwijderen van een sessie configuratie
----
Je kan de ```Unregister-PSSessionConfiguration``` cmdlet gebruiken om een vorige gedefiniëerde sessie configuratie te verwijderen. Let op als je ```Enable-PSRemoting``` opnieuw uitvoert wordt de default sessie configuratie weer aangemaakt.


<div id='9'/>
##Variables

INSERT CONTENT

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

INSERT CONTENT

<div id='12'/>
##Handling errors

INSERT CONTENT

<div id='13'/>
##Using CIM

INSERT CONTENT

<div id='14'/>
##Enhancements to tab completion

INSERT CONTENT

<div id='15'/>
##Scheduling jobs

INSERT CONTENT

<div id='16'/>
##Managing Active Directory with PowerShell

INSERT CONTENT

<div id='17'/>
##Managing the Server with PowerShell

INSERT CONTENT

<div id='18'/>
##Working with functions + advanced functions

INSERT CONTENT

<div id='19'/>
##Managing Exchange server

INSERT CONTENT





