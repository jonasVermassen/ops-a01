#Windows Server 2012 Core Deployment met PowerShell

##Voorbereiding
PowerShell als default shell instellen
```Powershell
PowerShell.exe PS > Set ItemProperty "HKLM:\Software\Microsoft\Windows NT\ CurrentVersion\winlogon" Shell PowerShell.exe
```

Guest additions installeren
```Powershell
.\VBoxGuestAdditions
```


##Basisinstellingen
Het systeem een naam gegeven (Assv1)
```Powershell
Rename –Computer –NewName Assv1
Restart-Computer
```

Tijdzone veranderd
```Powershell
TZutil /s “Romance Standard Time”
```

Netwerkcontrollers instellen
```Powershell
New-NetIpAddress –IPAddress 192.168.210.11 –InterfaceAlias Ethernet –DefaultGateway 192.168.210.1 –AddressFamily Ipv4 –PrefixLength 24
```


##Serverinstellingen

DHCP inschakelen
```Powershell
Set-NetIpInterface –InterfaceAlias Ethernet –Dhcp enabled
Install-WindowsFeature DHCP  –IncludeAllSubFeature  –IncludeManagementTools 
```

DNS Client settings
```Powershell
Set-DnsClientServerAddress –InterfaceAlias Ethernet –ServerAddresses 192.168.110.11
```

Active Directory configureren
```Powershell
Install-WindowsFeature AD-Domain-services  –IncludeAllSubFeature  –IncludeManagementTools
```

Remote Server administrator tools
```Powershell
Install-WindowsFeature RSAT  –IncludeAllSubFeature  –IncludeManagementTools
```

Service voor shares te kunnen maken
```Powershell
Install-WindowsFeature FileandStorage-services –IncludeAllSubFeature  –IncludeManagementTools
```

.Net Framework installeren
```Powershell
Install-WindowsFeature NET-Framework-45-features  –IncludeAllSubFeature  –IncludeManagementTools
```

Active Directory Domain Service rol toevoegen
```Powershell
Install‑ADDSForest ‑DomainName Assengraaf.nl ‑SafeModeAdministratorPassword (ConvertTo‑SecureString Test123 ‑AsPlainText ‑Force) -DomainMode Win2012 ‑DomainNetbiosname Assengraaf ‑ForestMode Win2012 ‑InstallDNS
```

Troubleshooting geen copy paste optie door virtualbox guest additions die bugged bij wcore server. 

```
ctrl + shift + esc om task manager te starten
Vervolgens de virtualbox service beëindigen
hierna .\VboxTray.exe runnen in system32, even geduld hebben en guest additions werkt weer.
```

Perongeluk exit gedaan of prompt kwijt ga naar task manager en klik in de rechterboven hoek op new task en typ powershell.exe

Mijn account toevoegen aan Domein Admins


```Add-ADGroupMember -Identity "Domain Admins" -Member "JarnoR" ```

DHCP scope Instellen

```
add-dhcpserverv4Scope
```

DHCP SuperScope instellen

```
add-dhcpserverv4SuperScope
```

DHCP default-gateway instellen

```
Set-DhcpServerv4OptionValue -ScopeId 192.168.210.0 -Router 192.168.210.1
```

Users toevoegen aan AD

```
New-ADUser -SamAccountName "FrankA"
Surname "Assengraaf" -DisplayName "Frank Assengraaf"
```

Security Group toevoegen aan AD en ou
```
NEW-ADGroup –name “Beheer” –groupscope Global –path “OU=Beheer,DC=Assengraaf,DC=nl”
```
![ALt text](http://i.imgur.com/JXf4665.png)


Maak user rechtsstreeks in een bestaande OU
![ALt text](http://i.imgur.com/nBDk8iy.png)

Local Domain Groups bekijken
```Powershell
net localgroup
```

Users toevoegen aan een Domain Group
```Powershell
net localgroup "print operator" /add femkevdv
```

Verbinding met server verbreken 
```Powershell
net use */delete
```

Nieuwe Share aanmaken met authorisaties
```Powershell
 PS C:\AsSv1Data\shares\Afdelingfolders> mkdir Verzekeringen
```
```Powershell
New-SmbShare -Name Verzekeringen -Path c:\AsSv1Data\shares\Afdelingfolders\verzekeringen 
-FullAccess Administrator -ChangeAccess AssenGraaf.nl\T_Verzekeringen 
```
```Powershell
Grant-smbShareAccess -Name Verzekeringen -AccountName Administrator -Accesright Full
```

![ALt text](http://i.imgur.com/zOUvxzK.png)

Rechten van OU aanpassen accidental deletion naar false

```
PS C:\Windows\system32> Set-ADOrganizationalUnit -Identity "OU=Financieringen,DC=Assengraaf,DC=nl" -ProtectedFromAcciden
talDeletion $False
```

OU Toevoegen aan een bestaande OU.

```
PS C:\Windows\system32> Move-ADObject -Identity "OU=Financieringen,DC=Assengraaf,DC=nl" -TargetPath "OU=AsAfdelingen,DC=
Assengraaf,DC=nl"
```

Maak een GPO

```
new-gplink -name beheerders -target "OU=AsAfdelingen,DC=assengraaf,DC=nl" 
```

Maak de GPO beheerders Enforced 

![enforced](http://i.imgur.com/Hmm5r5L.png)

Password policy instellen

![password policy](http://i.imgur.com/JtIjbfF.png)

Users een homedirectory geven

![Home Directory](http://i.imgur.com/CMpuiHI.png)

Voor profiles doe je hetzelfde maar gebruik je de parameter -ProfilePath \\ASSV1\AsSv1Data\shares\UserProfiles\%username%



Werkstation wordt eindelijk herkend door DC

Dit doe je door gebruik van het commando:

```
New-ADComputer -name AsWs1 -Path "OU=AsAfdelingen,DC=assengraaf,DC=nl"
```

![AsWs1 enabled](http://i.imgur.com/5rEIHyw.png)

Handige sites:

http://www.tomsitpro.com/articles/powershell-active-directory-cmdlets,2-801.html

https://technet.microsoft.com/en-us/library/ee617253.aspx

http://blogs.technet.com/b/heyscriptingguy/archive/2012/10/30/powertip-single-line-powershell-command-to-list-all-users-in-an-ou.aspx

https://social.technet.microsoft.com/Forums/scriptcenter/en-US/2ff646e0-1b1a-489a-8562-3f7bd21b7518/powershell-script-add-users-from-an-ou-to-an-ad-security-group?forum=ITCG

http://ilovepowershell.com/2012/09/19/create-network-share-with-powershell-3/

http://windowsitpro.com/powershell/managing-file-shares-windows-powershell
