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

