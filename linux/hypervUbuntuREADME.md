# Installing guest VM №00
## Disk
~~- Control panel / Right click to Windows button / Disk Management~~
~~- Create 44GB I: (VPS Storage) disk~~
## Network
- Open Hyper-V Manager
- Virtual Switch Manager... / New virtual network switch / External
- Name: external network virtual switch
- OK
## VM creation
- Open Hyper-V Manager
- New/Virtual Machine
- Specify Name and Location: Name: ubuntu-server-22.164
- Specify Generation: Generation 2
- Assign Memory: Startup memory: 8192; ☑ Use Dynamic Memory for this virtual machine;
- Configure networking: Connection: external network virtual switch
- Connect Virtual Hard Disk: Size: 44GB
- Installation Options: ☑ Install an operating system later
- Finish
- Right click to Virtual Machine and choise Settings...
- Select Processor
- Change to 4 Number of virtual processors
- SCSI Controller / DVD Drive / Add
- DVD Drive: Image file: C:\Users\ai\Downloads\ubuntu-22.04.1-live-server-amd64.iso
- ~~Security: ☐ Enable Secure Boot~~
- Security: ☑︎ Enable Secure Boot; Template: Microsoft UEFI Certificate Authority
- Apply
- Firmware: DVD Drive: Move Up
- Apply / OK
- Virtual Machines; Right click to Virtual Machine and choise Connect...
- Start
- Done, Done, Done, ..., ...
- English: ☑︎ language ☑︎ layout ☑︎ variant ☑︎ Ubuntu Server ☑︎ eth0 ☐ Proxy address: ☐ Mirror Address ☑︎ Use an entire disk ☑︎ done ☑︎ continue 
- Your name: ai
- Your server's name: 22
- Pick a username: i
- Password: **
- Done
- ☑︎ Install OpenSSH server
- ☐ Install docker
- Reboot Now
- To remove the installation  medium, click File/Settings.../Firmware/Hard Drive: Move Up
- Apply/OK
