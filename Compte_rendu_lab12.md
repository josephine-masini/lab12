# Compte rendu lab12

Joséphine MASINI

---
1. On clone les sources du bootloader u-boot : `git clone https://github.com/u-boot/u-boot.git` dans le lab12.

2. On se place dans la branche v2018.05, pour avoir une version spécifique, on fait `cd u-boot` et ensuite `git checkout v2018.05` pour changer de branche. 

3. Pour vérifier qu'on est bien sur la bonne branche : `git branch`, on a alors le résultat suivant : `*(HEAD detached v2018.05)`, on est bien sur la bonne branche. 

4. On va dans u-boot/configs : `cd u-boot/configs`, on fait ensuite un `ls * | grep "black"` et on trouve le fichier de config associé à la carte : `am335x-boneblack-defconfig`. 

5. On lance `make defconfig_file`, on vérifie la présence du fichier .config dans `ls -a` pour voir les fichiers cachés, on l'ouvre ensuite sur vim : `vim .config`. 
On modifie la variable CONFIG_SYS_PROMPT : `CONFIG_SYS_PROMPT="masini-uboot"`. Ce fichier contient toutes les variables d'environnement de u-boot, que l'on peut configurer.
On fait un `make am335x-boneblack-defconfig` dans u-boot. 

6. On a bien : 

```
student@ubuntu:~/Desktop/lab12/u-boot$ ls
api        Documentation  lib           scripts          u-boot.cfg.configs
arch       drivers        Licenses      snapshot.commit  u-boot.img
board      dts            MAINTAINERS   spl              u-boot.lds
cmd        env            Makefile      System.map       u-boot.map
common     examples       MLO           test             u-boot-nodtb.bin
config.mk  fs             MLO.byteswap  tools            u-boot.srec
configs    include        net           u-boot           u-boot.sym
disk       Kbuild         post          u-boot.bin
doc        Kconfig        README        u-boot.cfg

```
On a généré 2 fichiers: u-boot.img et MLO.

7. On est dans `dev/sdc : sdc1`, on fait normalement dans `dmesg | grep "sdc1"`.

8. On fait `cd /dev` et on fait ` mount `.

9. On fait ensuite `sudo fdisk -l` dans dev la carte a en fait déjà été configurée
```

Disk /dev/sdc: 3.8 GiB, 4025483264 bytes, 7862272 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device     Boot Start     End Sectors  Size Id Type
/dev/sdc1  *     2048 7862271 7860224  3.8G  e W95 FAT16 (LBA)

```
Pour les questions qui suivent la carte a déjà été utilisée et configurée, on passe donc directement à la question 13.

13. On fait ` sudo mkfs.vfat -F32/dev/sdc1 -n boot` dans dev pour convertir au format fat32, on a :
```
student@ubuntu:/dev$ sudo mkfs.vfat -F 32 /dev/sdc1 -n boot
mkfs.fat 4.1 (2017-01-24)
mkfs.fat: warning - lowercase labels might not work properly with DOS or Windows

```
14. On fait :
```
/dev/sdc1 on /media/student/boot type vfat (rw,nosuid,nodev,relatime,uid=1000,gid=1000,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,showexec,utf8,flush,errors=remount-ro,uhelper=udisks2)

```
15. On copie les fichiers dans le boot: 

```
cp MLO u-boot.img /media/student/boot 

```
On vérifie ensuite qu'on l'a bien dessus. C'est le cas, nous pouvons passer au lab suivant. 
