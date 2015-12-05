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
16. [Server Roles en Features Configureren](#16)
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


1.```PowerShell
PS C:\> Get-Process -name Notepad | Stop-Process
```
2.```PowerShell
PS C:\> Get-Process Note* | Stop-Process
```
3.```PowerShell
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
``` 

naar een andere value te veranderen met set-item cmdlet.

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
##Handling errors

INSERT CONTENT

<div id='13'/>
##Using CIM

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
##Enhancements to tab completion

INSERT CONTENT

<div id='15'/>
##Scheduling jobs

INSERT CONTENT

<div id='16'/>
##Server Roles en Features Configureren

Het is mogelijk de default shell can command prompt aan te passen naar powershell.
Hiervoor ga je naar het registry ```HKLM:\Software\Microsoft\Windows NT\CurrentVersion\winlogon``` en verander ```cmd.exe``` naar ```powershell.exe```. Dit kan je veranderen met gebruik van ```PS``` of ```regedit```.

Voor powershell doe je het volgende commando:

C:\Users\Administrator> PowerShell.exe
PS > Set‑ItemProperty "HKLM:\Software\Microsoft\Windows NT\
CurrentVersion\winlogon" Shell PowerShell.exe

1 Veranderen van de computer naam
---

```PS > Rename-Computer –NewName HQ-DC-01```

```PS > Restart-Computer```

2 De tijd zone veranderen
---

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

3 De NIC configureren met PS
---

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

4 Managen van windows server roles en features
---

Je kan de ```Get‑WindowsFeature``` cmdlet gebruiken om alle geïnstalleerd rollen en features te bekijken.

Geef een lijst van al de geïnstalleerde rollen en features

```
PS > Get-WindowsFeature | where Installed –eq $true
```

![Alt text](http://i.imgur.com/K0cLcFC.png)

####Voor tools toe te voegen moet je deze cmdlets gebruiken:

Deze cmdlet is voor subfeatures toe te voegen aan een role en ze 1 voor 1 wilt installeren.

```
‑IncludeAllSubFeature
```

Dit is voor extra tools toe te voegen zoals met de ISS feature die niet automatisch tools installeerd na het toevoegen van deze feature.

```
‑IncludeManagementTools
```

####Voorbeeld:

Een web server role met alle subfeatures en managment tools.

```
PS > Install‑WindowsFeature Web‑Server ‑IncludeAllSubFeature
‑IncludeManagementTools
```

####De ADDS of active directory domain service role toevoegen

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

####Een nieuw domein in een bestaande forest aanmaken

NewDomainName: Nieuwe domein naam maken

ParentDomainName: De parents naam voor het nieuwe domein

DomainMode: Specifieërd de functie levels van het domein

DomainType: Het domein type definiëren, dit kan ```Child``` of ```Tree``` zijn.

Voorbeeld:

```
PS > Install‑ADDSDomain ‑NewDomainName corp ‑ParentDomainName contoso.```
```local ‑SafeModeAdministratorPassword (ConvertTo‑SecureString P@ssw0rd```
```‑AsPlainText ‑Force) ‑CreateDnsDelegation ‑Credential (Get‑Credential```
```Contoso\Administrator) ‑DomainMode Win2012 ‑DomainType ChildDomain
```

####Een nieuwe domain controller aanmaken in een bestaand domein

Met deze cmdlet kan de opdracht uitgevoerd worden ```Install‑ADDSdomaincontroller``` cmdlet.

Voorbeeld:

```
PS > Install-ADDSDomainController -NoGlobalCatalog:$false```
```‑CreateDnsDelegation:$false -Credential (Get-Credential)```
```-DomainName "contoso.local" -InstallDns:$true -ReplicationSourceDC```
```"DC01.contoso.local" -SiteName "Default-First-Site-Name"```
```-SafeModeAdministratorPassword (ConvertTo-SecureString P@ssw0rd```
```-AsPlainText -Force)
```

Configureren van de DNS role
---

####Configureren van DNS server records

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

####Maken van primary forward en reverse lookup zones

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

Een DHCP role toevoegen en host configureren
---

####1 Installeren van DHCP server role

Server role en module toevoegen

```
PS > Add-WindowsFeature DHCP
```

####2 Een DHCP server scope opzetten voor ipv4

DHCP scope met naam Contoso voor 192.168.0.0 subnet met een masker 255.255.255.0 en dan activeren.

```
PS > Add‑DhcpServerv4Scope ‑Name "Contoso" ‑StartRange 192.168.0.1
‑EndRange 192.168.0.254 ‑SubnetMask 255.255.255.0 ‑State Active
```

####3 Configureren van de DHCP scope options

DNS domain naam, DNS server address, win server en default gateway.

```
PS > Set‑DhcpServerv4OptionValue ‑DnsDomain contoso.local ‑DnsServer
192.168.0.2 ‑Router 192.168.0.1
```

####4 Configureren van DHCP scope exclusions

Dit wordt gebruikt wanneer je een range van specifieke addressen statisch voor toestellen wilt gebruiken.

```
PS > Add‑DhcpServerv4ExclusionRange ‑ScopeId 192.168.0.0 ‑StartRange
192.168.0.100 -EndRange 192.168.0.130
```

####5 Configureren van DHCP scope reservaties

Ip address 192.168.0.10 wordt gereserveerd voor het mac addres F4-DA-F1-78-00-6D van de netwerk printer. 

```PS > Add‑DhcpServerv4Reservation ‑ScopeId 192.168.0.0 ‑IPAddress
192.168.0.10 ‑ClientId F4-DA-F1-78-00-6D ‑Description "Multi-Function
Network Printer in 3rd floor"```

####6 Toestemming geven aan de AD met de DHCP server

In dit voorbeeld wordt ```Add‑DhcpServerInDC``` cmdlet gebruikt om de DHCP server toe te voegen.

```
PS > Add‑DhcpServerInDC ‑DnsName "DhcpServer.contoso.local"
```

Het managen van de windows firewall
---

####1 Enablen of disablen van Windows firewall profiles

Hier gebruiken we de cmdlet Set‑NetFirewallProfile voor om alle windows firewall profiles te disablen en dan het publieke profiel te enablen.

Om alle profielen te disablen

```
PS > Set-NetFirewallProfile –All –Enabled False
```

Om alle profielen te enablen

```
PS > Set-NetFirewallProfile –Name Public –Enabled True
```

####2 Nieuwe firewall regels maken

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

Best practice Analyzer
---

Blijkbaar heb je in powershell een soort tool die je server configuratie vergelijkt met de standaarden van Windows.

####1 Alle lijsten van de BPA Models

```
PS > Get-BpaModel
```

Lijst van de laatste scan time

```
PS > Get-BpaModel | where LastScanTime –eq Never
```

####2 Een praktijk model oproepen

Dit scant de server voor beste gebruik en complicaties die problemen geven voor de file services

```
PS > Invoke-BpaModel –ModelId Microsoft/Windows/FileServices
```

![Alt text](http://i.imgur.com/8eLONIq.png)

####3 Beste resultaten laten zien

Met de cmdlet Get-BpaResult kunnen we de resultaten laten zien van de beste praktijk scan dat was uitgevoerd in het vorige voorbeeld.

```
PS > Get-BpaResult –ModelId Microsoft/Windows/FileServices
```

![Alt text](http://i.imgur.com/S69MynU.png)

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





