# EFI BIOS NVRAM MultiBoot (Python linux to easy create, modify, delete, reorder  launchers in NVRAM for EFI-BIOS systems)
==== preamble : Here are a few explanations (to my knowledge) about the starting up  of  the computers known as UEFI or EFI BIOS.

On any mother board there is a memory which is not erased  even after the computer shuts down. This non volatile memory is often called NVRAM : acronym for Non Volatile Random Access Memory.

Among other things, that memory contains : 
A table of which every row can indicate the name of a program that is launched immediately before the activation of any OS (windows, Linux…) and also the physical unit in which the program is (UUID of its partition) and also, in that  unit, the path which leads to it and its file name (for instance /EFI/ubuntu/shimx64.efi)

It also contains a table which indicates in what order the rows of the previous table must be browsed so as to  decide which sytem must be launched first, then secondly in case the first one fails, then  thirdly and so on.

On quality mother boards, the BIOS is intelligent enough to offer, in graphical display,  the tools enabling to create or modify rows of the first table and reorder BootOrder. But on basic or ancient systems , that tool is either rudimentary or missing. In that case, the tables can only be modified by a program loaded from a CD or a bootable USB key.

==== Aim of  the present program ==================================

As the bios program can only read the FAT partitions whose flag is ESP or EFI, the program presents only those units in the "sda1, sdb1, sdc2.…" form, according to the Linux convention.

It enables one to create, modify, suppress rows from the table which contains the OS starting up programs and also to modify the classification on the Bootorder table.
In fact, according to the indications it receives from the user and to the NVRAM content, it composes and launches the "efibootmgr" commands which could have been (on Linux) laboriously created manually in a terminal to reach the same result.

The used "efibootmgr" commands are displayed at the bottom of each window before being executed. 

Setup :  
use python3 scripts efibootmgr_Us.py (or efibootmgr_Fr.py), or use the standalone version efibootmgr_Us (or efibootmgr_Fr)
Python3 script :
in any folder, copy the efibootmgr_Us.bash script and the python script efibootmgr_Us.py. In the efibootmgr_Us.bash script, change the name of the folder containing these two files (change "python3 /home/bernard/.Scripts/efibootmgr_Us.py" to "python3 /home/your folder/efibootmgr_Us.py".
And then, create a launcher on the desktop that launches the efibootmgr_Us.bash script in a terminal (mandatory).
There are also two icons that may be useful to you, EFI.png and efibootmgr_sdx.png.
The program requires python3, python3-tk
Standalone release :
in any folder, copy the efibootmgr_Us program and create a launcher on the desktop that launches the efibootmgr_Us standalone program in a terminal (mandatory). You can use efibootmgr_nvram.png as icon.

Screenshots :
screenshot_01.png montre ce que fournit comme informations la commande "sudo efibootmgr -v".
On remarque que pour chaque poste "lanceur" présent en NVRAM, elle donne (pour les, lanceurs des systèmes qui nous intéressent):
- son rang dans la table NVRAM en notation hexadécimale de 4 chiffres, préfixé de "Boot" ("Boot0000, Boot0001... Boot000A...")
- sa désignation ("Windows boot manager", "ubuntu", "debian"...)
- sa localisation 
    HD pour HDD
    géométrie du disque GPT, MBR
    partition 1,2 etc 
    UUID de la partition (cff17f30-8ef7.....) impossible à saisir sans faire d'erreur
    le chemin dans la partition identifiée par cet UUID \EFI\UBUNTU\GRUBX64.EFI,  \EFI\DEBIAN\GRUB64.EFI...
et la table Bootorder qui liste les postes à prendre en compte lors du boot 0000,0004,0005,0001...(le premier, puis le second 
en cas d'impossibilité, etc 

Par contre, ce même programme efibootmgr, quand on désire manipuler les postes de la table (créer, modifier, ...) exige
qu'on utilise la notation linux (sda, sdb, plus numéro de partition donc sda1, sda2, sdb1...
Ce n'est pas très commode et c'est source d'erreur (grave dans la mesure où on peut dénaturer ou supprimer le poste
qui lançait votre système préféré.
Le programme Linux Python3 efibootmgr_Us.py (ou efibootmgr_Fr) rassemble les informations fournies par les programmes en lignes
de commande efibootmgr et blkid, et en fait une synthèse sous forme de GUI plus conviviale, exposée dans les images suivantes :
- screenshot_a.png,   reclassement des postes dans bootorder et par conséquent, changement éventuel de boot loader
- screenshot_b.png,   modification d'un poste de la table des lanceurs de la NvRam
- screenshot_c.png,   création d'un nouveau poste dans la table des lanceurs
- screenshot_d.png,   suppression d'un poste dans la table des lanceurs
- screenshot_e.png    affichage d'informations concernant l'EFI Boot et la NvRam
- screenshot_f.png    installation de BootNext, qui permet d'utiliser le lanceur choisi pour une fois seulement, avec retour à l'état initial au boot suivant 
- screenshot_g.png    suppression de BootNext

![screenshot_01](https://user-images.githubusercontent.com/111367455/190653069-0b569924-39fe-46b5-a691-b1cd6ce98490.png)

![screenshot_a](https://user-images.githubusercontent.com/111367455/190653113-60befc69-b5f1-4832-8f86-ac3439fe6b23.png)

![screenshot_b](https://user-images.githubusercontent.com/111367455/190653128-a2216d3b-01c6-433d-bb70-7f63c1e5943c.png)

![screenshot_c](https://user-images.githubusercontent.com/111367455/190653157-3b798b4a-0667-46e0-951d-3c7cb054c39f.png)

![screenshot_d](https://user-images.githubusercontent.com/111367455/190653171-dd2975f1-b499-461b-ac88-838ea6468538.png)

![screenshot_e](https://user-images.githubusercontent.com/111367455/190653190-0b0216bd-5bca-4773-b268-280daa3b6fef.png)

![screenshot_f](https://user-images.githubusercontent.com/111367455/190653203-3e21a23c-3bc7-4143-8c70-99744dfec149.png)

![screenshot_g](https://user-images.githubusercontent.com/111367455/190653214-007c7e94-300c-44b6-a7eb-82c2b73e2d1a.png)
