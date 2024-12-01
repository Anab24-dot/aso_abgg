# INTRODUCCIÓN A POWERSHELL (II)
## Práctica 0402

### 1. Visualizar las últimas cinco entradas del historial, mostrando para cada una el comando, la hora en que finalizó su ejecución y el estado de ejecución.
```powershell
Primero buscamos el nombre de las propiedades solicitadas con:
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-History | Get-Member 
   TypeName: Microsoft.PowerShell.Commands.HistoryInfo

Name               MemberType Definition
----               ---------- ----------
Clone              Method     Microsoft.PowerShell.Commands... 
Equals             Method     bool Equals(System.Object obj)   
GetHashCode        Method     int GetHashCode()
GetType            Method     type GetType()
ToString           Method     string ToString()
CommandLine        Property   string CommandLine {get;}
EndExecutionTime   Property   datetime EndExecutionTime {get;}
ExecutionStatus    Property   System.Management.Automation....
Id                 Property   long Id {get;}
StartExecutionTime Property   datetime StartExecutionTime {...
```
```powershell

PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-History -count 5 | select-Object Commandline, EndExecutionTime, ExecutionStatus

CommandLine                                    EndExecutionTime   ExecutionStatus
-----------                                    ----------------   ---------------
Get-Help Get-History                           28/11/2024 9:15:53       Completed
get-help Get-History -online                   28/11/2024 9:16:47       Completed
Get-History -count 5 | Format-List -Property*  28/11/2024 9:19:24       Completed
Get-History -count 5 | Format-List -Property * 28/11/2024 9:19:30       Completed
Get-History | Get-Member                       28/11/2024 9:43:29       Completed
```
```powershell
No será necesario añadir "object" después de "select"
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-History -count 5 | select Commandline, EndExecutionTime, ExecutionStatus       

CommandLine                                                                         EndExecutionTime   ExecutionStatus
-----------                                                                         ----------------   ---------------
get-help Get-History -online                                                        28/11/2024 9:16:47       Completed
Get-History -count 5 | Format-List -Property*                                       28/11/2024 9:19:24       Completed
Get-History -count 5 | Format-List -Property *                                      28/11/2024 9:19:30       Completed
Get-History | Get-Member                                                            28/11/2024 9:43:29       Completed
Get-History -count 5 | select-Object Commandline, EndExecutionTime, ExecutionStatus 28/11/2024 9:47:18       Completed
```
### 2. Ejecutar el comando Get-Command e interrumpirlo antes de que finalice su ejecución pulsando Ctrl-C. A continuación, ejecutarlo dejando que finalice correctamente
```powershell
En este primer ejemplo cortamos el comando
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Command
Cmdlet          Get-WindowsImageContent                            3.0        Dism
Cmdlet          Get-WindowsOptionalFeature                         3.0        Dism
Cmdlet          Get-WindowsPackage                                 3.0        Dism
Cmdlet          Get-WindowsReservedStorageState                    3.0        Dism
Cmdlet          Get-WindowsSearchSetting                           1.0.0.0    WindowsSearch
Cmdlet          Get-WinEvent                                       3.0.0.0    Microsoft.PowerShell.Diagnostics
Cmdlet          Get-WinHomeLocation                                2.1.0.0    International
Cmdlet          Get-WinLanguageBarOption                           2.1.0.0    International
Cmdlet          Get-WinSystemLocale                                2.1.0.0    International
Cmdlet          Get-WinUILanguageOverride                          2.1.0.0    International
Cmdlet          Get-WinUserLanguageList                            2.1.0.0    International
Cmdlet          Get-WmiObject                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-WSManCredSSP                                   3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Get-WSManInstance                                  3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Group-Object                                       3.1.0.0    Microsoft.PowerShell.Utility
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402>
```
```powershell
Si lo ejecutamos hasta el final se observa:
Cmdlet          Wait-Event                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Wait-Job                                           3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Wait-Process                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Where-Object                                       3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Write-Debug                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Error                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-EventLog                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Write-Host                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Information                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Output                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Progress                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Verbose                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Warning                                      3.1.0.0    Microsoft.PowerShell.Utility


PS C:\GIT\aso_abgg\ut04\Practicas\PR0402>
```
### 3. Volver a ejecutar el comando del punto 1 y comprobar las diferentes salidas de finalización del estado de ejecución
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> h -count 5 | select Commandline, EndExecutionTime, ExecutionStatus          

CommandLine EndExecutionTime   ExecutionStatus
----------- ----------------   ---------------
Get-Command 28/11/2024 9:51:51       Completed
Get-Command 28/11/2024 9:52:03       Completed
Get-Command 28/11/2024 9:52:08         Stopped
Get-Command 28/11/2024 9:53:26         Stopped
Get-Command 28/11/2024 9:53:45       Completed
```
### 4. Mostrar todos los procesos con el nombre msedge, mostrando para cada uno el identificador, el consumo de CPU y los hilos
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Process -name msedge |Get-Member
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Process -name msedge | select Id, CPU, Threads

   Id      CPU Threads
   --      --- -------
 3420  1,46875 {5748, 2564, 17252, 4288...}
 8692    0,125 {14944, 17836, 16176, 3708...}
10156      0,5 {9964, 16184, 7608, 1976...}  
12904        0 {4448, 11676, 11648, 13376...}
13072 0,015625 {3940, 8020, 9252, 4388...}
16324 0,015625 {9972, 18248, 2356, 15044...}
18064        0 {5004, 416, 2700, 1780...}
```
### 5. Averiguar para que sirve el parámetro -Delimiter del comando Export-CSV
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Help Export-CSV -Parameter Delimiter

-Delimiter <System.Char>
    Specifies a delimiter to separate the property values. The       
    default is a comma (`,`). Enter a character, such as a colon     
    (`:`). To specify a semicolon (`;`), enclose it in quotation     
    marks.

    ¿Requerido?                  false
    ¿Posición?                   1
    Valor predeterminado         comma (,)
    ¿Aceptar canalización?       False
    ¿Aceptar caracteres comodín? false
```
### 6. Mostrar en una ventana la ayuda del comando Get-History
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Help Get-History -showWindow
```powershell
![alt text](image.png)
```
### 7. Mostrar un listado con todos los comandos que tengan el verbo Update
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Command -Verb Update
CommandType     Name                                               V 
                                                                   e 
                                                                   r 
                                                                   s 
                                                                   i 
                                                                   o 
                                                                   n 
-----------     ----                                               - 
Function        Update-AutologgerConfig                            1 
Function        Update-Disk                                        2 
Function        Update-DscConfiguration                            1 
Function        Update-EtwTraceSession                             1 
Function        Update-HostStorageCache                            2 
Function        Update-IscsiTarget                                 1 
Function        Update-IscsiTargetPortal                           1 
Function        Update-Module                                      1 
Function        Update-ModuleManifest                              1 
Function        Update-MpSignature                                 1 
Function        Update-MpSignature                                 1 
Function        Update-NetFirewallDynamicKeywordAddress            2 
Function        Update-NetIPsecRule                                2 
Function        Update-Script                                      1 
Function        Update-ScriptFileInfo                              1 
Function        Update-SmbMultichannelConnection                   2
Function        Update-StorageBusCache                             1 
Function        Update-StorageFirmware                             2 
Function        Update-StoragePool                                 2 
Function        Update-StorageProviderCache                        2 
Cmdlet          Update-FormatData                                  3 
Cmdlet          Update-Help                                        3 
Cmdlet          Update-LapsADSchema                                1 
Cmdlet          Update-List                                        3 
Cmdlet          Update-TypeData                                    3 
Cmdlet          Update-UevTemplate                                 2 
Cmdlet          Update-WIMBootEntry                                3 
```
### 8. Ejecutar la herramienta Recortes y localizarla usando el comando Get-Process, teniendo en cuenta que el proceso se llama SnippingTool.exe
```powershell
Lo primero que debemos tener en cuenta es tener activa la herramienta recortes para que nos de resultado positivo.
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Process -Name SnippingTool

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    753      40    82844     115500       0,11  20904   6 SnippingTool

```
### 9. Averiguar que propiedades tienen los procesos devueltos con el comando Get-Process
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Process | Get-Member -MemberType Properties


   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
NPM                        AliasProperty  NPM = NonpagedSystemMemorySize64
PM                         AliasProperty  PM = PagedMemorySize64
SI                         AliasProperty  SI = SessionId
VM                         AliasProperty  VM = VirtualMemorySize64
WS                         AliasProperty  WS = WorkingSet64
__NounName                 NoteProperty   string __NounName=Process
BasePriority               Property       int BasePriority {get;}
Container                  Property       System.ComponentModel.IContainer Container {get;}
EnableRaisingEvents        Property       bool EnableRaisingEvents {get;set;}
ExitCode                   Property       int ExitCode {get;}
ExitTime                   Property       datetime ExitTime {get;}
Handle                     Property       System.IntPtr Handle {get;}
HandleCount                Property       int HandleCount {get;}
HasExited                  Property       bool HasExited {get;}
Id                         Property       int Id {get;}
MachineName                Property       string MachineName {get;}
MainModule                 Property       System.Diagnostics.ProcessModule MainModule {get;}
MainWindowHandle           Property       System.IntPtr MainWindowHandle {get;}
MainWindowTitle            Property       string MainWindowTitle {get;}
MaxWorkingSet              Property       System.IntPtr MaxWorkingSet {get;set;}
MinWorkingSet              Property       System.IntPtr MinWorkingSet {get;set;}
Modules                    Property       System.Diagnostics.ProcessModuleCollection Modules {get;}    
NonpagedSystemMemorySize   Property       int NonpagedSystemMemorySize {get;}
NonpagedSystemMemorySize64 Property       long NonpagedSystemMemorySize64 {get;}
PagedMemorySize            Property       int PagedMemorySize {get;}
PagedMemorySize64          Property       long PagedMemorySize64 {get;}
PagedSystemMemorySize      Property       int PagedSystemMemorySize {get;}
PagedSystemMemorySize64    Property       long PagedSystemMemorySize64 {get;}
PeakPagedMemorySize        Property       int PeakPagedMemorySize {get;}
PeakPagedMemorySize64      Property       long PeakPagedMemorySize64 {get;}
PeakVirtualMemorySize      Property       int PeakVirtualMemorySize {get;}
PeakVirtualMemorySize64    Property       long PeakVirtualMemorySize64 {get;}
PeakWorkingSet             Property       int PeakWorkingSet {get;}
PeakWorkingSet64           Property       long PeakWorkingSet64 {get;}
PriorityBoostEnabled       Property       bool PriorityBoostEnabled {get;set;}
PriorityClass              Property       System.Diagnostics.ProcessPriorityClass PriorityClass {ge... 
PrivateMemorySize          Property       int PrivateMemorySize {get;}
PrivateMemorySize64        Property       long PrivateMemorySize64 {get;}
PrivilegedProcessorTime    Property       timespan PrivilegedProcessorTime {get;}
ProcessName                Property       string ProcessName {get;}
ProcessorAffinity          Property       System.IntPtr ProcessorAffinity {get;set;}
Responding                 Property       bool Responding {get;}
SafeHandle                 Property       Microsoft.Win32.SafeHandles.SafeProcessHandle SafeHandle ... 
SessionId                  Property       int SessionId {get;}
Site                       Property       System.ComponentModel.ISite Site {get;set;}
StandardError              Property       System.IO.StreamReader StandardError {get;}
StandardInput              Property       System.IO.StreamWriter StandardInput {get;}
StandardOutput             Property       System.IO.StreamReader StandardOutput {get;}
StartInfo                  Property       System.Diagnostics.ProcessStartInfo StartInfo {get;set;}     
StartTime                  Property       datetime StartTime {get;}
SynchronizingObject        Property       System.ComponentModel.ISynchronizeInvoke SynchronizingObj... 
Threads                    Property       System.Diagnostics.ProcessThreadCollection Threads {get;}    
TotalProcessorTime         Property       timespan TotalProcessorTime {get;}
UserProcessorTime          Property       timespan UserProcessorTime {get;}
VirtualMemorySize          Property       int VirtualMemorySize {get;}
VirtualMemorySize64        Property       long VirtualMemorySize64 {get;}
WorkingSet                 Property       int WorkingSet {get;}
WorkingSet64               Property       long WorkingSet64 {get;}
Company                    ScriptProperty System.Object Company {get=$this.Mainmodule.FileVersionIn... 
CPU                        ScriptProperty System.Object CPU {get=$this.TotalProcessorTime.TotalSeco... 
Description                ScriptProperty System.Object Description {get=$this.Mainmodule.FileVersi... 
FileVersion                ScriptProperty System.Object FileVersion {get=$this.Mainmodule.FileVersi... 
Path                       ScriptProperty System.Object Path {get=$this.Mainmodule.FileName;}
Product                    ScriptProperty System.Object Product {get=$this.Mainmodule.FileVersionIn... 
ProductVersion             ScriptProperty System.Object ProductVersion {get=$this.Mainmodule.FileVe... 
```
### 10. Buscar en la ayuda para que sirve el parámetro -MemberType del comando Get-Member
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Help Get-Member -parameter MemberType

-MemberType <System.Management.Automation.PSMemberTypes>
    Specifies the member type that this cmdlet gets. The default is `All`.
    
    The acceptable values for this parameter are:
    
    - `AliasProperty`

    - `CodeProperty`

    - `Property`

    - `NoteProperty`

    - `ScriptProperty`

    - `Properties`

    - `PropertySet`

    - `Method`

    - `CodeMethod`

    - `ScriptMethod`

    - `Methods`

    - `ParameterizedProperty`

    - `MemberSet`

    - `Event`

    - `Dynamic`

    - `All`


    These values are defined as a flag-based enumeration. You can combine multiple values together to  
    set multiple flags using this parameter. The values can be passed to the MemberType parameter as   
    an array of values or as a comma-separated string of those values. The cmdlet will combine the     
    values using a binary-OR operation. Passing values as an array is the simplest option and also     
    allows you to use tab-completion on the values.

    For information about these values, see PSMemberTypes Enumeration
    (/dotnet/api/system.management.automation.psmembertypes).
    Not all objects have every type of member. If you specify a member type that the object doesn't    
    have, PowerShell returns a null value. To get related types of members, such as all extended       
    members, use the View parameter. If you use the MemberType parameter with the Static or View       
    parameters, `Get-Member` gets the members that belong to both sets.


    ¿Requerido?                  false
    ¿Posición?                   named
    Valor predeterminado         None
    ¿Aceptar canalización?       False
    ¿Aceptar caracteres comodín? false
```
```powershell
La columna MemberType muestra el tipo de cada elemento, es decir, filtra propiedades y métodos y puede mostrar únicamente los elementos de un determinado tipo con el parámetro citado
```
### 11. Desde la línea de comando, finalizar la ejecución de la herramienta Recortes
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Stop-Process -name SnippingTool

Sí tenemos abierta la aplicación y activa en la barra de tareas, en el momento de ejecutar el comando anterior el logo de la aplicación desaparece por el cierre de la misma
```
### 12. Mostrar todos los procesos que tienen el nombre svchost
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Process -name svchost

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
   1190      22     9368      16900               880   0 svchost
    201      11     2352       9800              1076   0 svchost
    431      19     6964      16368              1152   0 svchost
    160      42     1732       6852              1216   0 svchost
   2294      32    20288      37068              1304   0 svchost
   1752      23    13816      19712              1408   0 svchost
    432      16     3988      11840              1452   0 svchost
    111      13     1292       5040              1640   0 svchost
    255      13     3188       9448              1700   0 svchost
    340      10     2168       9268              1708   0 svchost
    160      10     1972       7704              1820   0 svchost
    133      13     1620       5384              1868   0 svchost
    170      37     7808       7148              1956   0 svchost
    312      13     4180      15252              2104   0 svchost
    206       8     3436       6168              2284   0 svchost
    348      18     6284      10460              2348   0 svchost
    527      15    19556      16256              2356   0 svchost
    246      14     2860      12356              2416   0 svchost
    306       8     1416       5608              2424   0 svchost
    179      10     2088       7076              2432   0 svchost
    307      12    21096      20120              2496   0 svchost
    229      15     2360       8772              2572   0 svchost
    245      11     2008       7940              2720   0 svchost
    214      13     2344       9420              2728   0 svchost
    201      16     7620       9820              2752   0 svchost
    262      12     3048       7588              2784   0 svchost
    316      13     3656       9520              2920   0 svchost
    198      10     1964       7228              2992   0 svchost
    416      30     9240      16964              3156   0 svchost
    123       8     1496       6080              3204   0 svchost
    453      14     3700      13840              3332   0 svchost
    596      21    12484      21280              3672   0 svchost
    526      35     7232      17832              3820   0 svchost
    168       9     1524       6928              3836   0 svchost
    219      12     2452      10088              4044   0 svchost
    472      13     2892       9856              4052   0 svchost
    225      14     2652      11668              4108   0 svchost
    451      35    15324      16808              4168   0 svchost
    461      46    52924      29728              4188   0 svchost
    186      11     1892       7492              4268   0 svchost
    652      33    29808      41568              4540   0 svchost
    396      25    38320      41392              4548   0 svchost
    370      22     2912      10196              4572   0 svchost
    138       9     1304       5532              4592   0 svchost
    395      19     4464      17468              4600   0 svchost
    124       8     1276       5628              4688   0 svchost
    541      21     8704      31396       0,47   5048   6 svchost
    245      14     3096      11336              5264   0 svchost
    135       9     1560       6964              5460   0 svchost
    143       9     1428       6360              5664   0 svchost
    165      11     1736       7080              5688   0 svchost
    203      12     2216       9856              5868   0 svchost
    259      13     5216      17220              6220   0 svchost
    277      16     4008      14420              6384   0 svchost
    169       9     1752       6780              6744   0 svchost
    205      11     2760      11708              7044   0 svchost
    173       9     1640       7672              7396   0 svchost
    273      13     3956      14844              7436   0 svchost
    444      25     5964      18356              7512   0 svchost
    244      14     3412      17332       0,06   8120   6 svchost
    263      12     2540       8116              8468   0 svchost
    358      12     2384      12120              8636   0 svchost
    156      11     1892       8580              8916   0 svchost
    209      13     2548      10660              8992   0 svchost
    120       8     2172       6388              9432   0 svchost
    452      25     3596      12580              9752   0 svchost
    334      13     2980       9112             11140   0 svchost
    318      17     4696      16600             13036   0 svchost
    426      26     5844      21676       0,23  13236   6 svchost
    280      23     3136       8040             13292   0 svchost
    148       9     1688       9164       0,02  13736   6 svchost
    519      18     8160      16412             14312   0 svchost
    473      18     9940      25472       0,38  14628   6 svchost
    389      15     3952      15128             16576   0 svchost
    165      10     2100      10612       0,00  16632   6 svchost
    334      18     7124      18408             17008   0 svchost
    230      14     3308       9912             17484   0 svchost
    213      13     1884       7536             17588   0 svchost
    112       8     1280       6328       0,00  17612   6 svchost
    487      22     7716      31364       0,19  18544   6 svchost
```
### 13. Mostrar por pantalla el número de isntancias del proceso svchost
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> (Get-Process -name svchost).count 
80
```
### 14. Mostrar por pantalla todos los procesos con el nombre svchost mostrando para cada uno: nombre, identificador, inicio, tiempo total del procesador y clase de prioridad. Se deben mostrar de forma tubular
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Process -name svchost | Get-Member
Usamos el comando anterior para conocer el nombre de los parámetros solicitados
PS C:\GIT\aso_abgg\ut04\Practicas\PR0402> Get-Process -name svchost | Select-object Name, Id, StartTime, TotalProcessorTime, PriorityClass | Format-Table

Name      Id StartTime TotalProcessorTime PriorityClass
----      -- --------- ------------------ -------------
svchost  880
svchost 1076
svchost 1152
svchost 1216
svchost 1304
svchost 1408
svchost 1452
svchost 1640
svchost 1700
svchost 1708
svchost 1820
svchost 1844
svchost 1868
svchost 1956
svchost 2104
svchost 2284
svchost 2348
svchost 2356
svchost 2416
svchost 2424
svchost 2432
svchost 2496
svchost 2572
svchost 2720
svchost 2728
svchost 2752
svchost 2784
svchost 2920
svchost 2992
svchost 3156
svchost 3204
svchost 3332
svchost 3672
svchost 3820
svchost 3836
svchost 4044
svchost 4052
svchost 4108
svchost 4168
svchost 4188
svchost 4268
svchost 4540
svchost 4548
svchost 4572
svchost 4592
svchost 4600
svchost 4688
svchost 5048 01/12/... 00:00:00.4687500   Normal
svchost 5264
svchost 5460
svchost 5664
svchost 5688
svchost 5868
svchost 6220
svchost 6384
svchost 6744
svchost 7044
svchost 7436
svchost 7512
svchost 8120 01/12/... 00:00:00.0625000   Normal
svchost 8468
svchost 8636
svchost 8916
svchost 8992
svchost 9432
svchost 9752
svchost ...0
svchost ...6
svchost ...6 01/12/... 00:00:00.2343750   Normal
svchost ...2
svchost ...6 01/12/... 00:00:00.0156250   Normal
svchost ...2
svchost ...8 01/12/... 00:00:00.3750000   Normal
svchost ...6
svchost ...2 01/12/... 00:00:00           Normal
svchost ...8
svchost ...4
svchost ...8
svchost ...2 01/12/... 00:00:00           Normal
svchost ...4 01/12/... 00:00:00.2031250   Normal
svchost ...2
```
### 15. 