### >>> Create a restore point in case it breaks anything. <<<

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### What's the best version to use in general?

I would recommend the latest (currently Windows 11 25H2) but it requires some benchmarks. Newer versions are usually glitchy during the first couple weeks, so check it before downloading it. As of today (22/10/2025), Windows 10 is no longer supported by Microsoft. Fortunately, you can still use LTSC and IOT LTSC versions (support ends in 2027 and 2032 respectively) so there's still a way to avoid Windows 11 if you really want to. 

### Is this guide going to break anything?

It does not break anything, it just disables unnecessary features that can be re-enabled later on.

### Services (services.msc)

Services are no longer impactful as technology evolved but it's totally fine if you still feel like disabling them.

We can define cycles delta as a metric for how many cycles X process is using in a specific amount of time. The less available cycles delta you have, the busier your CPU will be and automatically will damage your performance. Most services are pretty much frozen and not really using any cycles, but we still have some, and those are the ones I recommend disabling if you want to. Here's the list in order from the most resource-consuming services that I personally can't find any use for. 

- Windows Search
- Connected User Experiences and Telemetry
- SysMain (if you don't have an HDD)
- Bluetooth-related services (don't disable if you use any bluetooth device)

To save you some time, you can use Chris Titus' Script to set a bunch of services to manual to reduce resource usage without breaking anything as Windows will simply start them on demand. 

### Device Manager 

Disabling devices (Win + R -> devmgmt.msc) won't really boost the machine's performance at all, but it can help with input lag in some cases. Here's the list of devices you can disable in order to improve your responsiveness:

Network adapters:
- WAN Miniports 
- ISATAP Adapter

Storage controllers: 
- Microsoft iSCSI Initiator

System devices:
- Composite Bus Enumerator
- Intel Management Engine / AMD PSP
- Intel SPI (flash) Controller
- Microsoft GS Wavetable Synth
- NDIS Virtual Network Adapter Enumerator
- Remote Desktop Device Redirector Bus
- SMBus
- System speaker
- Terminal Server Mouse/Keyboard drivers
- UMBus

### Optional Features

These are not really important, but if you're fresh ass nerd like me you might want to clean it. In order to get in there, press Win + R and type "optionalfeatures". If it's correctly written it should open a tab. Some features there are worth keeping, but I also made a list of unnecessary ones:

- Internet Explorer
- XPS Viewer
- Microsoft XPS Document Writer
- Microsoft Print to PDF 
- Windows Powershell (either 2.0 or 3.0)

### General Tweaks

At this point there's not so many things you can do in order to actually improve performance, but you can still do it if you want. One simple tweak that's still quite great (not available in W11) is disabling Background Apps. Just go to Settings (Win + I) -> Privacy -> Background Apps. Disable it and you're done. You can also disable Game Bar in Settings -> Games -> Xbox Game Bar.

To fully disable the Xbox overlay, you need to go to Regedit (Win + R -> regedit) and change these values:

- HKEY_CURRENT_USER\System\GameConfigStore -> Set the value of DWORD "GameDVR_Enabled" to 0
- HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\ -> Create a key called "GameDVR" -> Create DWORD 32bit inside GameDVR called "AllowGameDVR" and set to 0

### What about power plans? Do these help somehow?

Power plans are not that important (keep in mind that they CAN contribute to input latency so it's worth testing) but you can either rock Balanced which is set by default or use more performance-focused power plans such as High Performance, Ultimate Performance or custom power plans such as [Khorvie's´](https://www.youtube.com/watch?v=pM40pmGtqYk).

### Debloated NVIDIA Driver

For NVIDIA users, you might want to use [NVCleanstall](https://www.techpowerup.com/download/techpowerup-nvcleanstall/). I would stick to the most recent driver (there might be faulty ones in the future, so please research before installing a random version). 

For the component removal part, I would recommend only selecting "Display Driver". The rest is not necessary (unless you use Geforce Experience, but you can find much better alternatives such as [Medal](https://medal.tv/) or even [OBS](https://obsproject.com/download). 

After the initial installing process, check these boxes: 

- Disable Installer Telemetry & Advertising 
- Perform a Clean Installation
- Disable Mutiplane Overlay (MPO)
- Disable Ansel
- Show Expert Tweaks -> Enable Message Signaled Interrupts 

After checking these just hit "Next" and finish your install. 

### Debloated AMD Driver

For AMD users, you want to use [Radeon Software Slimmer](https://github.com/GSDragoon/RadeonSoftwareSlimmer). After downloading the app AND downloading your driver open Radeon Slimmer, go to pre-install and browse to select your driver file and then hit next. In packages, hit "select none" at the top and check these:

- AMD Display Driver
- AMD Settings
- Any C++ redists (usually at the very bottom)

Go to "schedule tasks" and hit "select none". Go to "display driver components" and do the same. After that, hit "modify installer" and then "run installer". Install the driver normally. 

### Process Scheduling (Win32PrioritySeparation)

This tweak needs to be tested individually as the result may differ from machine to machine. There's a bunch of available values, but the general recommendation is decimal 22 (I'm using decimal 38 currently). To apply this tweak, open Regedit and change it at: "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\PriorityControl\Win32PrioritySeparation"

Make sure to set the value as decimal, not hexadecimal. 

### Specific Tweaks for Minecraft

Since the base game is not optimized at all, it's necessary to use some mods in order to improve performance and overall experience. I've been using Fabric for over 3 years so I cannot guarantee these mods will be available for Forge. Here's the list containing every optimization mod I use (1.21.9):

- Sodium
- Indium (deprecated as of 1.21)
- Lithium
- Nvidium (outdated)
- Bobby
- Entity Culling 
- Iris 
- FerriteCore
- ModernFix
- EBE (Enhanced Block Entities) (outdated)
- C2ME (Concurrent Chunk Management Engine)
- Noisium (outdated)
- Exordium
- Fast Paintings
- Entity View Distance
- Video Tape
- Faster Random

### Chris Titus Tool (credits below)

This is an awesome and very easy to use tool created by [Chris Titus Tech](https://www.youtube.com/@ChrisTitusTech) and his community. All you need to do is open Powershell as administrator and type the following command: irm christitus.com/win | iex

If this is your first time using this tool then it might take a while to load as it installs chocolatey. There's a lot you can tweak there but I'll focus on what's actually important. Go to "Tweaks" tab and check the following: 

- Delete Temporary Files
- Disable Consumer Features
- Disable Telemetry
- Disable Activity History
- Disable GameDVR (this will break Game Bar)
- Disable Location Tracking
- Disable Storage Sense
- Disable Wifi-Sense
- Run Disk Cleanup
- Disable Powershell 7 Telemetry
- Set Services to Manual
- Debloat Edge (this will lock many Edge features so be careful)
- Disable IPV6 (if you don't use it)
- Disable Background Apps
- Disable Microsoft Copilot (if you don't use it)

Hit "Run Tweaks" and wait for it to finish. After this step, I'd recommend running O&O Shutup. It's located in the bottom of "Tweaks". Just hit "Run OO Shutup 10", apply recommended settings and you're done.  






