#Windows Powershell

##Inhoudstafel
1. [Using the help system](#1)
2. [Running commands](#2)
3. [Adding commands](#3)
4. [Working with providers](#4)
5. [The pipeline](#5)
6. [Objects: data by another name](#6)
7. [Formatting output](#7)
8. [Filtering + Working with files](#8)
9. [Remoting](#9)
10. [Variables](#10)
11. [PowerShell ISE](#11)
12. [Scripting](#12)
13. [Handling errors](#13)
14. [Using CIM](#14)
15. [Enhancements to tab completion](#15)
16. [Scheduling jobs](#16)
17. [Managing Active Directory with PowerShell](#17)
18. [Managing the Server with PowerShell](#18)
19. [Working with functions + advanced functions](#19)
20. [Managing Exchange server](#20)

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
##Adding commands

INSERT CONTENT

<div id='4'/>
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



<div id='5'/>
##The pipeline

INSERT CONTENT

<div id='6'/>
##Objects: data by another name

INSERT CONTENT

<div id='7'/>
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


<div id='8'/>
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








<div id='9'/>
##Remoting

INSERT CONTENT

<div id='10'/>
##Variables

INSERT CONTENT

<div id='11'/>
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



<div id='12'/>
##Scripting

INSERT CONTENT

<div id='13'/>
##Handling errors

INSERT CONTENT

<div id='14'/>
##Using CIM

INSERT CONTENT

<div id='15'/>
##Enhancements to tab completion

INSERT CONTENT

<div id='16'/>
##Scheduling jobs

INSERT CONTENT

<div id='17'/>
##Managing Active Directory with PowerShell

INSERT CONTENT

<div id='18'/>
##Managing the Server with PowerShell

INSERT CONTENT

<div id='19'/>
##Working with functions + advanced functions

INSERT CONTENT

<div id='20'/>
##Managing Exchange server

INSERT CONTENT





