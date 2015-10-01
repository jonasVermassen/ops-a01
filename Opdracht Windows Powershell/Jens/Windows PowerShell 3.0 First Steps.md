#Windows PowerShell 3.0 First Steps

##Chapter 1

* Get-Process
* Get-Service
* Get-Volume
* Get-NetAdapter
* Get-NetConnectionProfile
* Get-Culture -> Getting the current culture settings
* Get-Date
* Get-Help
* Get-Random
* Get-Random -Maximum 21 -Minimum 1

* Get-Random -InputObject (1..10) -Count 5
* PS C:\> ipconfig

##Chapter 2

###PowerShell parameters

-	Verbose (vb)

PS C:\> Stop-Process -Name notepad

-	Debug (db)
-	WarningAction (wa)
-	WarningVariable (wv)
-	ErrorAction (ea)

PS C:\> Get-Process -Name notepad -ErrorAction SilentlyContinue (geef error weergeven)

SilentlyContinue | Stop | Continue | Inquire | Ignore

-	ErrorVariable (ev)
-	OutVariable (ov)
-	OutBuffer (ob)
-	WhatIf (wi)
-	Confirm (cf)

###Powershell Transcript
![ALt text](http://i.imgur.com/ConOCoa.png)
<Commando’s + evt uitvoer>
![ALt text](http://i.imgur.com/RZYD5OZ.png)
Once you start the Windows PowerShell transcript, all commands, command output, and even error messages appear in the transcript file.

###Help

![ALt text](http://i.imgur.com/Us9Qbtw.png)

###Get-Command

![ALt text](http://i.imgur.com/NWtljmQ.png)

###Get-Member

![ALt text](http://i.imgur.com/bJZcWhw.png)

##Chapter 3

###Sort

![ALt text](http://i.imgur.com/ZMonIwv.png)

###Filtering

![ALt text](http://i.imgur.com/SZ8OnMh.png)
-gt -> greater than
![ALt text](http://i.imgur.com/XoBEvEP.png)

##Chapter 4

###Creating a table
![ALt text](http://i.imgur.com/FZ2g9Ov.png)

###Creating a list
![ALt text](http://i.imgur.com/1Nc1cv8.png)

###Creating a wide display
![ALt text](http://i.imgur.com/vPuBsym.png)

###Creating an Out-GridView
![ALt text](http://i.imgur.com/HJyRd59.png)

##Chapter 5
###Storing data in text files
Get-Volume >>c:\fso\volumeinfo.txt

###Storing data in CSV files
![ALt text](http://i.imgur.com/kUzOt38.png)

###Storing data in XML
Get-Process | Export-Clixml -Path c:\fso\processXML.xml
