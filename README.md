
# Safe Exam Browser write up
Please note that this is not the finished writeup, it is ongoing!
## Writeup Content
 - [x] Blacklisted Applications
 - [x] Virtual Machine Detection Vectors
 - [x] Display Detection Vectors
 - [ ] Lockdown mode
 - [ ] Desktop creation
 - [ ] Integrity Check Vectors
 - [ ] Encryption keys
 - [ ] Plugins

## Blacklisted Applications
These are the blocked applications listed in the default config in SEB. They can be modified by the exam supervisor.
```
AA_v3.exe
AeroAdmin.exe
beamyourscreen-host.exe
CamPlay.exe
Camtasia.exe
CamtasiaStudio.exe
Camtasia_Studio.exe
CamRecorder.exe
CamtasiaUtl.exe
chromoting.exe
CiscoCollabHost.exe
CiscoWebExStart.exe
Discord.exe
Element.exe
g2mcomm.exe
g2mcomm.exe
g2mlauncher.exe
g2mstart.exe
GotoMeetingWinStore.exe
join.me.exe
join.me.sentinel.exe
Mikogo-host.exe
ptoneclk.exe
RemotePCDesktop.exe
remoting_host.exe
RPCService.exe
RPCSuite.exe
Skype.exe
SkypeApp.exe
SkypeHost.exe
slack.exe
Teams.exe
TeamViewer.exe
Telegram.exe
vncserver.exe
vncviewer.exe
vncserverui.exe
webexmta.exe
Zoom.exe
```

## Virtual Machine Detection Vectors
### BIOS, Manufacturers and models
These are the blacklisted BIOS, Manufacturers and Models on SEB.
```diff
- BIOS: HyperV
- BIOS: VirtualBox
- BIOS: VmWare
- Manufacturer: Microsoft Corporation (surface model excluded)
- Manufacturer: Parallels Software
- Manufacturer: Qemu
- Manufacturer: VmWare
- Model: VirtualBox
```
### MAC prefixes
These are blacklisted MAC addresses. If your MAC begins with these prefixes, you will not be given access to SEB.
```diff
- VIRTUALBOX_MAC_PREFIX "080027"
- QEMU_MAC_PREFIX       "525400"
```

### Device blacklist
These are the blacklisted device names and ID's.
```diff
- PROD_VIRTUAL
- HYPER_V
- qemu
- ven_1af4
- ven_1b36
- subsys_11001af4
- vbox
- vid_80ee
- PROD_VMWARE
- VEN_VMWARE
- VMWARE_IDE
```

## Display Detection Vectors
SEB only allows 1 internal display to be active at a time. More displays will result in restricted access to the application.
They gather all displays from ``ROOT\WMI`` using the following queries.
```diff
+ SELECT * FROM WmiMonitorBasicDisplayParams
+ SELECT * FROM WmiMonitorConnectionParams
```
