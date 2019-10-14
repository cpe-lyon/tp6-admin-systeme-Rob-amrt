# TP 6 - Gestion des disques / Tâches d’administration


## Exercice 1. Disques et partitions

#### 1. Dans l’interface de configuration de votre VM, créez un second disque dur, de 5 Go dynamiquement alloués ; puis démarrez la VM
 - Fait
#### 2. Vérifiez que ce nouveau disque dur est bien détecté par le système
On peut voir que le disque à été créé en allant dans `/dev` en voyant qu'il y a un `sdb`

#### 3. Partitionnez ce disque en utilisant fdisk : créez une première partition de 2 Go de type Linux (n°83), et une seconde partition de 3 Go en NTFS (n°7)
```
Command (m for help): n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (2-4, default 2):
First sector (4196352-20971519, default 4196352):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (4196352-20971519, default 20971519): +3G

Created a new partition 2 of type 'Linux' and of size 3 GiB.

Command (m for help): t
Partition number (1,2, default 2):
Hex code (type L to list all codes): 7

Changed type of partition 'Linux' to 'HPFS/NTFS/exFAT'.

Command (m for help): p
Disk /dev/sdb: 10 GiB, 10737418240 bytes, 20971520 sectors
Disk model: VBOX HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x36747693

Device     Boot   Start      End Sectors Size Id Type
/dev/sdb1          2048  4196351 4194304   2G 83 Linux
/dev/sdb2       4196352 10487807 6291456   3G  7 HPFS/NTFS/exFAT

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

#### 4. A ce stade, les partitions ont été créées, mais elles n’ont pas été formatées avec leur système de fichiers. A l’aide de la commande mkfs, formatez vos deux partitions ( pensez à consulter le manuel !)
Formatage partition sdb1 : `mkfs.ext4 /dev/sdb1`
Formatage partition sdb2 : `mkfs.ntfs /dev/sdb2`

#### 5. Pourquoi la commande df -T, qui affiche le type de système de fichier des partitions, ne fonctionne-telle pas sur notre disque ?

#### 6. Faites en sorte que les deux partitions créées soient montées automatiquement au démarrage de la machine, respectivement dans les points de montage /data et /win (vous pourrez vous passer des UUID en raison de l’impossibilité d’effectuer des copier-coller)


