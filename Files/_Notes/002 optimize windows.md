#notes

##### <font style="color:#E5B567">Disable Ununse Services:</font>

```
this services can have a significant impact on your daily computer use because it consumes a lot of space, potentially slowing your CPU and overall performance.
	- Connected Devices Platform Service
	- Windows Search
	- Windows Update (optional)
	- Sysmain
```

##### <font style="color:#E5B567">Performance options:</font>

```
based on my personal preferences, these custom performance settings will result in smoother animations and better performance.
```

![400](visual%20effects.png)

--------
##### <font style="color:#E5B567">Optimize Internet Connection:</font>

```
basically this will help to stabilize internet connection.
	- open (Powershell/cmd):
```

![](optimize%20net.png)

----------------
##### <font style="color:#E5B567">Virtual Memory:</font>

```
this can handle twice the number of addresses as main memory and frees up space for more applications to run simultaneously, this is only optional if your ram is less than 8GB.
```

![400](virtual%20memory.png)

-------
##### <font style="color:#E5B567">Faster Bootup:</font>

```
this will make your bootup faster.
	- open msconfig and set the boot timeout to 3 seconds in the boot section.
```

![400](boot%20timeout.png)

---------
##### <font style="color:#E5B567">Max Processors:</font>

```
this will make your computer use max cpu processors for better performance.
- open msconfig then open advanced options:
```

![400](cpu%20processors.png)
##### <font style="color:#F3BA47"></font>
```
then set number of processors to max available:
```

![|250](num%20of%20processors.png)

--------------
##### <font style="color:#E5B567">Power Options:</font>

```
set the preffered plan to high performance.
```

![700](power%20option.png)

--------
##### <font style="color:#E5B567">Delete Unnecessary Files:</font>

```
this will also help to speed up and smooth out your computer by removing junk files.
	- remove all files from these folders:
	- run: temp,prefetch,%temp%
```

![[unnecessary files.png]]

------ 
##### <font style="color:#E5B567">Regedit:</font>

```
add this to your registry to fully utilize your CPU and significantly improve computer performance.
```

```
	Windows Registry Editor Version 5.00
	:: Modified by Itssmezedd

	:: -----------------------------------------------------------------------------------------------------------------
	:: Disable PowerThrottling ::
	[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\PowerThrottling]
	"PowerThrottlingOff"=dword:00000001

	:: -----------------------------------------------------------------------------------------------------------------
	:: Fix Power Throttling ::
	[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile]
	"NetworkThrottlingIndex"=dword:ffffffff
	"SystemResponsiveness"=dword:00000000
	[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\PowerThrottling]
	"PowerThrottlingOff"=dword:00000001
	[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\PriorityControl]
	"Win32PrioritySeparation"=dword:00000026

	:: -----------------------------------------------------------------------------------------------------------------
	:: Improve System Responsiveness ::
	[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile]
	"SystemResponsiveness"=dword:00000001

	:: -----------------------------------------------------------------------------------------------------------------
	:: Optimize CPU ::
	[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games]
	"Affinity"=dword:00000000
	"Background Only"="False"
	"Clock Rate"=dword:00002710
	"GPU Priority"=dword:00000008
	"Priority"=dword:00000002
	"Scheduling Category"="High"
	"SFIO Priority"="High" 
	[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games]
	"Affinity"=dword:00000000
	"Background Only"="False"
	"Clock Rate"=dword:00002710
	"Scheduling Category"="High"
	"SFIO Priority"="High"
	"GPU Priority"=dword:00000008
	"Priority"=dword:00000006

	:: ----------------------------------------------------------------------------------------------------------------
	
	:: Optimuize GPU ::
	[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games]
	"GPU Priority"=dword:00000008
	"Priority"=dword:00000006
	"Scheduling Category"="High"
	"SFIO Priority"="High"
	:: -----------------------------------------------------------------------------------------------------------------
	
	:: Set Windows High Priority ::
	[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Multimedia\SystemProfile\Tasks\Games]
	"GPU Priority"=dword:00000008
	"Priority"=dword:00000006
	"Scheduling Category"="High"
	"SFIO Priority"="High"
	:: -----------------------------------------------------------------------------------------------------------------
```
-----
##### <font style="color:#E5B567">Optional:</font>

```
To further optimize your computer faster without taking up a lot of time, create a batch file that will handle all of the tasks listed above and to boost overall performance.
```

```
	:: Modified by Itssmezedd

	@echo off
	REM Adds Multiple reg files to optimize PC
	echo adding multiple reg files...
	echo:
	timeout /t 1 >nul
	regedit /s ".\modified settings.reg"
	echo Done!
	echo:
	echo -------------------------------------------------------


	REM Optimize Internet Connection
	echo optimizing internet...
	echo:
	timeout /t 1 >nul
	netsh int ipv4 set subinterface "Wi-Fi" mtu=1500 store=persistent
	echo Done!
	echo:
	echo -------------------------------------------------------


	REM Disable Unuse Services
	echo disabling unuse services...
	echo:
	timeout /t 1 >nul
	sc config "CDPSvc" start= disabled
	sc config "Sysmain" start= disabled
	sc config "WSearch" start= disabled
	sc config "Spooler" start= disabled
	sc config "iphlpsvc" start= disabled
	echo Done!
	echo:
	echo -------------------------------------------------------


	REM Set Virtual Memory to 3gb
	echo setting up virtual memory...
	echo:
	timeout /t 1 >nul
	wmic computersystem where name="%computername%" set AutomaticManagedPagefile=false
	wmic pagefileset where name="C:\\pagefile.sys" set InitialSize=3000,MaximumSize=3000
	echo Done!
	echo:
	echo -------------------------------------------------------


	REM Faster Boot up
	echo setting up boot timeout to 3 seconds...
	echo:
	timeout /t 1 >nul
	bcdedit /timeout 3
	echo Done!
	echo:
	echo -------------------------------------------------------


	REM Setting cores to max
	echo searching cores...
	echo:
	timeout /t 1 >nul
	For /F "Tokens=2Delims==" %%G In ('WMIC CPU Get NumberOfCores /Value')Do Set /A cores=%%G
	echo %cores% cores have found!!
	echo using all cores...
	echo:
	timeout /t 1 >nul
	bcdedit /set numproc %cores%
	echo Done!
	echo:
	echo -------------------------------------------------------


	REM Power Options
	echo turning on windows hibernate...
	echo:
	timeout /t 1 >nul
	powercfg /hibernate on
	echo Done!
	echo:
	echo -------------------------------------------------------
	echo setting power to high performance...
	echo:
	timeout /t 1 >nul
	powercfg -setactive scheme_min
	echo Done!
	echo:
	echo -------------------------------------------------------


	REM Delete Unnecessary Files
	echo deleting unnecessary files...
	echo:
	timeout /t 1 >nul
	del /s /f /q C:\Windows\Prefetch\*.*
	del /s /f /q C:\Windows\Temp\*.*
	del /s /f /q %userprofile%\appdata\local\temp\*.*
	echo Done!
	echo:
	echo -------------------------------------------------------

	pause
```

