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




##Handling errors
