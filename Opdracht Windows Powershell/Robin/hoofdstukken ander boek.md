##Running commands

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







##Errors voorkomen/oplossen

Voor men fouten probeert te verbeteren in een script, moet men het gebruik van het script eerst begrijpen.
Bij de meeste simpele scriptjes zoals bijvoorbeeld Get-Bios.ps1 valt er niet te veel te verbeteren, aangezien er geen inputs van de command line zitten in dit script.

Get-Bios.ps1
Get-WmiObject -class Win32_Bios


###Ontbrekende parameters

In het Get-BiosInformation.ps1 script is er een parameter computerName, dat toelaat om een pc te kiezen als doel van het script.
Als het script geen waarde krijgt voor de computerName parameter, faalt het omdat Get-WmiObject een waarde voor de parameter nodig heeft.
Om het probleem op te lossen gaat het script op zoek naar een $computerName variabele.
Als deze variabele ontbreekt gaat het script een waarde proberen geven aan de variabele.
De volgende lijn van het script zorgt hiervoor: 
If(-not($computerName)) { $computerName = $env:computerName }

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


Men kan ook de parameters verplicht maken zodat de gebruiker een waarde voor de parameter moet voorzien.
Om een parameter verplicht te maken gebruiken we Mandatory als parameter attribuut.

Param(
  [Parameter(Mandatory=$true)]
  [string]$drive,
  [string]$computerName = $env:computerName
) #end param

Als men dit script dan gaat runnen gaat powershell een waarde vragen voor de parameter drive.

###Try/Catch/Finally

Bij een Try/Catch/Finally blok, ga je in het Try gedeelte de commands die het script moet uitvoeren zetten.
Als er een error is bij de commands, gaat het script naar het Catch gedeelte, waar de fout wordt opgevangen met een string, om te zeggen dat er een fout gebeurd is.
Hetgeen dat in het Finally gedeelte staat wordt altijd uitgevoerd, ookal was er een error gegenereerd.
In het algemeen zet men daar de "code cleanup", het stukje code dat ervoor gaat zorgen dat de niet gebruikte commands of commands waar er fouten stonden niet worden uitgevoerd.
In het voorbeeldscript staat er een string om te zeggen dat het script beëindigd is.

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
