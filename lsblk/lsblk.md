# Customizing lsblk tool

The default output format of `lsblk` on my system is:
```
$ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sdb           8:16   1  14,4G  0 disk 
└─sdb1        8:17   1  14,4G  0 part /mnt/freemnt 
sdc           8:32   1  28,7G  0 disk 
├─sdc1        8:33   1   389M  0 part 
└─sdc2        8:34   1   4,9M  0 part 
```
This is very little informative. Whereas if you type `lsblk --help | less` you will see a very rich collection of columns to choose from. After some experiments I came up with: 
```
$ lsblk -o name,MOUNTPOINT,LABEL,SIZE,FSTYPE,PARTTYPENAME,PTTYPE
NAME        MOUNTPOINT   LABEL                   SIZE FSTYPE  PARTTYPENAME                 PTTYPE
sdb                                             14,4G                                      dos
└─sdb1      /mnt/freemnt ESD-USB                14,4G vfat    W95 FAT32 (LBA)              dos
sdc                      Debian 11.7.0 amd64 n  28,7G iso9660                              dos
├─sdc1                   Debian 11.7.0 amd64 n   389M iso9660 Empty                        dos
└─sdc2                                           4,9M vfat    EFI (FAT-12/16/32)           dos
```
But instead of passing all these options, I wanted to have a neat command for this. So I added an alias to my `.zshrc`. I called it `llblk`, as an analogy to a common alias `ll`. By the way, on my system I defined `ll` as the following:
```
alias ll="ls -lh --time-style=long-iso --group-directories-first"
```
So now I had as well:
```
alias llblk="lsblk -o name,MOUNTPOINT,LABEL,SIZE,FSTYPE,PARTTYPENAME,PTTYPE,PARTFLAGS -w 1000"
```




