#Windows Server 2012 Core Deployment met PowerShell


PowerShell als default shell instellen
PowerShell.exe PS > Set ItemProperty "HKLM:\Software\Microsoft\Windows NT\ CurrentVersion\winlogon" Shell PowerShell.exe

Guest additions installeren
.\VBoxGuestAdditions



Het systeem een naam gegeven (Assv1)
Rename –Computer –NewName Assv1
Restart-Computer

Tijdzone veranderd
TZutil /s “Romance Standard Time”

Netwerkcontrollers ingesteld
New-NetIpAddress –IPAddress 192.168.210.11 –InterfaceAlias Ethernet –DefaultGateway 192.168.210.1 –AddressFamily Ipv4 –PrefixLength 24

DHCP ingeschakeld
Set-NetIpInterface –InterfaceAlias Ethernet –Dhcp enabled
Install-WindowsFeature DHCP  –IncludeAllSubFeature  –IncludeManagementTools 

DNS Client settings
Set-DnsClientServerAddress –InterfaceAlias Ethernet –ServerAddresses 192.168.110.1

Active Directory configureren
Install-WindowsFeature AD-Domain-services  –IncludeAllSubFeature  –IncludeManagementTools

Remote Server administrator tools
Install-WindowsFeature RSAT  –IncludeAllSubFeature  –IncludeManagementTools

Service voor shares te kunnen maken
Install-WindowsFeature FileandStorage-services –IncludeAllSubFeature  –IncludeManagementTools

.Net Framework installeren
Install-WindowsFeature NET-Framework-45-features  –IncludeAllSubFeature  –IncludeManagementTools

Active Directory Domain Service rol toevoegen
Install‑ADDSForest ‑DomainName Assengraaf.nl
‑SafeModeAdministratorPassword (ConvertTo‑SecureString Test123
‑AsPlainText ‑Force) -DomainMode Win2012 ‑DomainNetbiosname Assengraaf
‑ForestMode Win2012 ‑InstallDNS

