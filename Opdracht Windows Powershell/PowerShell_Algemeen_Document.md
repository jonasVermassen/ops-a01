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
###tussentitel

INSERT CONTENT

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

Er kan ook gebruik gemaakt worden van groeperen. Dan kan er gebruik gemaakt worden van "count", dit om het aantal objecten te tellen. Maar kan er ook gebruik gemaakt worden van "group", dit om een group te specifiëren

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

INSERT CONTENT

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





