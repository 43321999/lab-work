# README

Follow these steps to install Debian 12 with a customized Logical Volume Manager (LVM) configuration:

1. Insert the USB flash drive with the Debian 12 image into a USB port on your computer.
2. Turn on the computer while holding the F11 key to access the boot menu.
3. Choose the USB flash drive as the boot device.

## Debian 12 Installation

- Select "Graphical install" from the "Debian GNU/Linux installer menu (BIOS mode)".

### Language Configuration

- Choose English as the installation language.

### Accessibility Options

- Keep the default settings for software access for blind users and speech synthesizer voice configuration.

### Keyboard Configuration

- Set the location, locale, and timezone to the United Kingdom.
- Choose the American English keyboard layout.

### Network Configuration

- Set the hostname to "00".
- Set the domain name to "fc".

### User and Password Setup

- Set no root password.
- Create a user with the username "su" and password "< zte superadmin >".

### Clock Configuration

- Keep the default settings for clock configuration.

### Disk Partitioning

- Enter "Configure the Logical Volume Manager" to manage disk partitions.

    - Choose "Display configuration details" to view the current LVM configuration.
  
        **Current LVM configuration:**
        - Unallocated physical volumes: none
        - Volume groups: none

    - Choose "Create volume group" and enter "fc" as the volume group name. Select both devices (/dev/sda and /dev/sdb) for the new volume group.

    - Confirm writing changes to disks and configuring LVM.

        **Write the changes to disks and configure LVM? (Choose YES)**

    - Encounter an error while creating the volume group "fc". Check /var/log/syslog for details.

    - Go back to the device selection screen and choose "Display configuration details" again.

        **Current LVM configuration:**
        - Unallocated physical volumes: /dev/sda1 (120032MB)
        - Volume groups: 00.fc (619112MB) - Uses physical volume: /dev/sdb1 (500103MB) - Uses physical volume: [unknown] (500103MB)

    - Notice a discrepancy in the volume group name. Choose "Delete volume group" and attempt to delete "00.fc", encountering an error.

    - Try "Reduce volume group" and select the volume group "00.fc". Attempt to remove /dev/sda1 from the volume group, resulting in an error.

    - Reboot the computer and select "Install" instead of "Graphical install" to access the terminal.

    - Choose "Execute a shell" and run the command `pvcreate /dev/sda1 /dev/sdb1` with warnings and recommendations.

        **Recommendations:**
        - Can't initialize physical volume "/dev/sda1" of volume group "00.fc" without -ff
        - /dev/sda1: physical volume not initialized.
        - WARNING: ext4 signature detected on /dev/sdb1 at offset 1080. Wipe it? [y/n]

    - Enter "y" and run the command `vgremove 00.fc`.

        **WARNING:**
        - Couldn't find device with uuid EhkPIX-SIZk-jIJF-xtuD-DPHG-3bwZ-D3KPW8.
        - VG 00.fc is missing PV EhkPIX-SIZk-jIJF-xtuD-DPHG-3bwZ-D3KPW8 (last written to [unknown]).
        - Device /dev/sda1 has size of 976769024 sectors which is smaller than corresponding PV size of 976771072 sectors. Was device resized?
        - One or more devices used as PVs in VG 00.fc have changed sizes.
        - Couldn't find device with uuid EhkPIX-SIZk-jIJF-xtuD-DPHG-3bwZ-D3KPW8.
        - Volume group "00.fc" not found, is inconsistent or has PVs missing.
        - Consider vgreduce --removemissig if metadata is inconsistent.

    - Successfully run `vgreduce --removemissig 00.fc`.

    - Encounter an issue while running `pvcreate /dev/sda1 /dev/sdb1`. Resolve it by running `pvremove -ff /dev/sda1` and then `pvcreate /dev/sda1 /dev/sdb1`.

    - Create a new volume group with `vgcreate fc /dev/sda1 /dev/sdb1` and exit the shell with the `exit` command.

    - Back in the main installation menu, choose 'Partition disks', then 'Configure the Logical Volume Manager', and finally, 'Display configuration details' to confirm the correct configuration.

        **Current LVM configuration:**
        - Unallocated physical volumes: none
        - Volume groups: fc (619108MB) - Uses physical volume: /dev/sda1 (500103MB) - Uses physical volume: /dev/sdb1 (119004MB)

[to be continue…](youtu.be/afD2_H215JM?si=S8dAdn65ujWDE2Pl)
This completes the process of setting up the Logical Volume Manager for the Debian 12 installation.
