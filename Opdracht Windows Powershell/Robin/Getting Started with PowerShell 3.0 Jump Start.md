#Getting Started with PowerShell 3.0 Jump Start

##Don't fear the shell

Locatie veranderen cmdlet
```Powershell
PS C:\Users\Robin> Set-Location C:/

PS C:\>
```
Directory tonen cmdlet
```Powershell
PS C:\> Get-ChildItem


    Directory: C:\


Mode                LastWriteTime         Length Name                                                                                                                    
----                -------------         ------ ----                                                                                                                    
d-----        4-10-2015     20:48                .jagex_cache_32                                                                                                         
d-----        23-5-2014      0:57                GvTemp                                                                                                                  
d-----        10-7-2015      5:31                inetpub                                                                                                                 
d-----        23-5-2014      0:53                Intel                                                                                                                   
d-----        10-7-2015     13:04                PerfLogs                                                                                                                
d-r---        1-10-2015      0:36                Program Files                                                                                                           
d-r---        29-9-2015     18:41                Program Files (x86)                                                                                                     
d-----        29-8-2015     14:02                Temp                                                                                                                    
d-r---        29-8-2015     21:42                Users                                                                                                                   
d-----        7-10-2015     17:01                Windows                                                                                                                 
-a----        25-9-2015     21:36            868 Battle.net.lnk                                                                                                          
-a----        28-9-2015     14:25           1062 IFRToolLog.txt 
```
Afkortingen bekijken
```Powershell
PS C:\> Get-Alias

CommandType     Name                                               Version    Source                                                                                     
-----------     ----                                               -------    ------                                                                                     
Alias           % -> ForEach-Object                                                                                                                                      
Alias           ? -> Where-Object                                                                                                                                        
Alias           ac -> Add-Content                                                                                                                                        
Alias           asnp -> Add-PSSnapin                                                                                                                                     
Alias           cat -> Get-Content                                                                                                                                       
Alias           cd -> Set-Location                                                                                                                                       
Alias           CFS -> ConvertFrom-String                          3.1.0.0    Microsoft.PowerShell.Utility                                                               
Alias           chdir -> Set-Location                                                                                                                                    
Alias           clc -> Clear-Content                                                                                                                                     
Alias           clear -> Clear-Host                        
...
```

##The help system
