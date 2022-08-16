# NVRAM-linux
==== preamble : Here are a few explanations (to my knowledge) about the starting up  of  the computers known as UEFI or EFI BIOS.

On any mother board there is a memory which is not erased  even after the computer shuts down. This non volatile memory is often called NVRAM : acronym for Non Volatile Random Access Memory.

Among other things, that memory contains : 
A table of which every row can indicate the name of a program that is launched immediately before the activation of any OS (windows, Linux…) and also the physical unit in which the program is (UUID of its partition) and also, in that  unit, the path which leads to it and its file name (for instance /EFI/ubuntu/shimx64.efi)

It also contains a table which indicates in what order the rows of the previous table must be browsed so as to  decide which sytem must be launched first, then secondly in case the first one fails, then  thirdly and so on.

Quite logically, that second table is called BootOrder and each of its rows contains the rank of an item of the first table, in the form of a four digit number in hexadecimal notation (0000,0001,...000A....)

A small program, which is also present in non volatile memory (called BIOS) is run as soon as the computer is powered up. Through the reading of the BootOrder table, its detects which row of the first table it has to operate and therefore which program it has to load from the disk for immediate running. As it is not very intelligent, it understands nothing else than the file system FAT32. The partitions whose UUID are contained in the first table must therefore be in the FAT 32 format so that the small program can  find, load and run the launching of the OS.

Moreover, they also have to be flagged as ESP or EFI and Bootable .  Otherwise they are ignored in the process. 

On quality mother boards, the BIOS is intelligent enough to offer, in graphical display,  the tools enabling to create or modify rows of the first table and reorder BootOrder. But on basic or ancient systems , that tool is either rudimentary or missing. In that case, the tables can only be modified by a program loaded from a CD or a bootable USB key.

Finally, during the installation of an OS (UBUNTU for instance) the installer program (GRUB-INSTALL for UBUNTU) enriches the NVRAM by inscribing a row which locates the start up module (shimx64.efi for UBUNTU) and adds the rank of that new row at the top of the Boot Order table.

At the next start up, in that example, it is shimx64.efi which will be run and will launch UBUNTU.

NB : An authentication mechanism has been imagined to protect the computer from the installation of non authentical starting programs. That mechanism is included in the BIOS which verifies the signature of every program before launching it. However, this checking can be avoided by activating the CMS option of the BIOS (CSM: Compatibility Support Module) in order to start an OS that is on a non-UEFI disk

Yet, under Linux, there exists different non-signed  launchers whose launching would be refused in a protected computer except by asking Microsoft to authenticate them.

That is why one has to use the shim program (shimx64.EFI), which is signed and whose role is to launch the grub program (Linux boot loader) 
corresponding to each Linux version.

==== Aim of  the present program ==================================

As the bios program can only read the FAT partitions whose flag is ESP or EFI, the program presents only those units in the "sda1, sdb1, sdc2.…" form, according to the Linux convention.

It enables one to create, modify, suppress rows from the table which contains the OS starting up programs and also to modify the classification on the Bootorder table.

In fact, according to the indications it receives from the user and to the NVRAM content, it composes and launches the commands which could have been laboriously created manually in a terminal to reach the same result.

The used commands are displayed at the bottom of each window before being executed.
