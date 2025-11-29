# Drive Cloning

## Objective

This laptop running Windows 11 Pro has run out of disk space on it's 256Gb M.2 NMVE drive. Using various tools I will clone the Windows drive with all of it's partitions onto a new 2Tb M.2 NMVE drive. Then I will open the laptop and switch the drives. This should then boot into my existing Windows 11 OS with all my files as they were previously, without loss of data. 

### Skills Learned/Demonstrated

- Advanced understanding of disk management utility, including partition arrangement.
- Basics of hardware handling, mitigating ESD(electro-static discharge), opening laptop case without stripping screws, swapping out M.2 drives.
- Utilize OTS software to clone a complete Windows disk with all of its partitions.
- Utilize sha256 checksums for any software downloaded from internet to verify file integrity.
- Project planning. Break down the project goal into logical steps of actions needed to complete the project. Adjust or add steps if problems arise.

### Tools Used

- Windows Disk Management Utility
- Windows Disk Clean-up Utility
- Macrium Reflect 
- Diskpart command-line tool
- GParted Live ISO
- Rufus 
- Hardware: M.2 external dock, screwdriver, pry tool, usb drive, M.2 NMVE drive

## Steps
1. Run Windows Disk Clean-up utility to shrink size of used disk space to clone.
   ![Disk Clean-up Utility](/DiskCLeanup.png "Disk Clean-up Utility")
   ![Disk Clean-up Utility](/DiskCLeanupDelete.png "Disk Clean-up Utility")

2. Plug M.2 NMVE drive into the external dock. Then plug the docks usb cable into an open usb port on laptop.
   ![M2 Enclosure](/docksmall.png "External M.2 Dock")

3. Run Macrium Reflect to Clone Windows disk drive(C drive) in its entirety.
   Select the Windows drive to clone, ensuring that all the partitions are checked(they should be by default).
   Select the drive you want put the clone on(target disk drive).
   Click ok that Bitlocker will not be enabled on the new clone drive of Windows.
   Click next on the schedule screen. We will not be using the scheduling function.
   Verfiy the info on the clone summary screen, then click finish.
   Click continue when the warning screen pops up about deleting any data on the target disk drive.
   A successful clone should include 3 partitions. A MBR sometimes listed as system drive, Windows(C drive), and a Windows Recovery drive.
   ![Macrium Reflect](/Macriumstep1.png "Macrium Reflect")
   ![Macrium Reflect](/Macriumstep2.png "Macrium Reflect")

4. Now this is when I ran into a snag. This cloned my 256Gb onto the 2Tb drive, but it left the remainder of 1.69Tb unallocated. I tried using Windows Disk            Management Utility to extend the new Windows partition, but that failed. I'm sorry, I can't remember the exact error message, &  I didn't get a screen capture.     After a quick Google search I found out that you can only extend a partition if it's next to the unallocated partition. This cloning process put the Windows        Recovery partition between the Windows & unallocated partitions. The remedy for this is to move the recovery partition, which I used Gparted Live to do.            Gparted(GNOME Partition Editor) Live is a bootable Linux ISO that a allows various manipulations of partitions.

5. Navigate to gparted.org, then download the latest version.
   ![Gparted](/gparted1.png "Gparted Live")
   The screen will change to this, and the download will start.
   ![Gparted](/gparted2.png "Gparted Live")

6. Now once the file has downloaded, lets verify the file integrity by checking the file hash. To do this lets run a sha256 file hash on the command line. Open a      command prompt then cd(change directory) into your downloads folder. List the contents of your downloads folder by typing ls command. Then type the following       line into your command prompt:  certutil -hashfile. Then type the first 3 characters of the gparted file inside a pair of "", mine is "gparted-live-1.7.0-8-        amd64" SHA256, then hit the Tab key. This will autocomplete the file name. Hit enter, and a sha256 hash will be made of the file. Check this against the GParted 
   websites hash list. If it matches then you have downloaded an unaltered file, which is what we want.

7. Now we'll use Rufus, a utility that writes ISO's to usb drives, making a bootable usb drive running Gparted Live.
   ![Rufus](/rufus2.png "Rufus")
   
   Plug a blank usb drive into a usb port, then Rufus should populate it in the Device field. In the Boot Selection, select Disk or ISO image(please select). To       the right of that you can open the drop down menu and select your file that you want to write, in this case it's gparted-live-1.7.0-8-amd64. Leave everything       as is, and hit start. This will wipe any data on the usb drive, so back up anything you want to keep.

8. Now we will reboot the computer with the usb still inserted. If you don't have the proper setting in BIOS to boot from USB first, then just hit the boot selector key at the beginning of powering up. Once Gparted Live boots up you'll see this screen.
   ![Gparted Live App](/gpartedappstartup.png "Gparted")
   Select the top setting. Gparted will show 2 partitions in white, indicating they are initialized, and one that is grey, indicating its uninitialized. The large white partition is the Windows partition that we want to extend. The small white partition is the recovery one. We need to move the recovery partition to the end of the span. We select the recovery partition by clicking on it, then under the partiton menu select move/resize.



