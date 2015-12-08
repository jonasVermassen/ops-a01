#Windows PowerShell 3.0 Step by Step

##Chapter 1: Overview of Windows PowerShell 3.0

Meerdere commands op 1 lijn
```Powershell
ipconfig /all >tshoot.txt; route print >>tshoot.txt; hostname >>tshoot
.txt
```
Proces tonen
```Powershell
PS C:\> Get-Process notepad

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName                      
-------  ------    -----      ----- -----   ------     -- -----------                      
    128       8     1444       7564 ...49     0,36  10580 notepad     
```
Proces stoppen & -whatif parameter
```Powershell
PS C:\> Stop-Process -Id 10580 -WhatIf
What if: Performing the operation "Stop-Process" on target "notepad (10580)".
```
![common parameters](https://i.gyazo.com/a28f58f22ba89f896742a37c667637c5.png)

Cmdlets zoeken
```Powershell
PS C:\> Get-Command -Name mov*

CommandType     Name                                               Version    Source       
-----------     ----                                               -------    ------       
Alias           move -> Move-Item                                                          
Alias           Move-SmbClient                                     2.0.0.0    SmbWitness   
Function        Move-SmbWitnessClient                              2.0.0.0    SmbWitness   
Cmdlet          Move-AppxPackage                                   2.0.0.0    Appx         
Cmdlet          Move-Item                                          3.1.0.0    Microsoft....
Cmdlet          Move-ItemProperty                                  3.1.0.0    Microsoft....
Cmdlet          Move-MsmqMessage                                   1.0.0.0    MSMQ         

```

##Chapter 2: Using Powershell Cmdlets

Het object wshShell maken:
```Powershell
$wshShell = New-Object -comobject "wscript.shell"
```

##Chapter 3: Understanding and using Powershell Providers


##Chapter 4: Using PowerShell Remoting and Jobs


##Chapter 5: Using PowerShell Scripts


##Chapter 6: Working with Functions


##Chapter 7: Creating Advanced Functions and Modules


##Chapter 8: Using the Windows PowerShell ISE


##Chapter 9: Working with the Windows PowerShell Profiles


##Chapter 10: Using WMI


##Chapter 11: Querying WMI


##Chapter 12: Remoting WMI


##Chapter 13: Calling WMI Methods on WMI Classes


##Chapter 14: Using the CIM Cmdlets


##Chapter 15: Working with AD


##Chapter 16: Working with the AD DS Module


##Chapter 17: Deploying AD with WS 2012


##Chapter 18: Debugging Scripts


##Chapter 19: Handling Errors


##Chapter 20: Managing Exchange Server

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

