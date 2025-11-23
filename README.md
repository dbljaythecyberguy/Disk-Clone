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

2. 


