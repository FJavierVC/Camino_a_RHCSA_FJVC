# Obteniendo una vista previa de los montajes actuales

Vamos a ejecutar el comando mount en nuestro entorno de prueba. notemos que la salida es bastante extensa, si la leemos de manera cuidadosa, notaremos que la salida del comando incluye algunos directorios de la estructura de linux y sus correspondientes puntos de montaje.
```
a200511609@iao-bastion:~$ mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=32854960k,nr_inodes=8213740,mode=755,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,noexec,relatime,size=6579980k,mode=755,inode64)
/dev/mapper/ubuntu--vg-ubuntu--lv on / type ext4 (rw,relatime)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,inode64)
tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k,inode64)
cgroup2 on /sys/fs/cgroup type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate,memory_recursiveprot)
none on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=32,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=7887)
configfs on /sys/kernel/config type configfs (rw,nosuid,nodev,noexec,relatime)
tracefs on /sys/kernel/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)
debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,nosuid,nodev,relatime,pagesize=2M)
mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)
fusectl on /sys/fs/fuse/connections type fusectl (rw,nosuid,nodev,noexec,relatime)
/var/lib/snapd/snaps/bare_5.snap on /snap/bare/5 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/snap-store_1270.snap on /snap/snap-store/1270 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/snapd-desktop-integration_343.snap on /snap/snapd-desktop-integration/343 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/snapd_25935.snap on /snap/snapd/25935 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/snapd-desktop-integration_315.snap on /snap/snapd-desktop-integration/315 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/gtk-common-themes_1535.snap on /snap/gtk-common-themes/1535 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/firefox_7967.snap on /snap/firefox/7967 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/core22_2339.snap on /snap/core22/2339 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/gnome-42-2204_247.snap on /snap/gnome-42-2204/247 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/gnome-42-2204_202.snap on /snap/gnome-42-2204/202 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/firmware-updater_216.snap on /snap/firmware-updater/216 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/dev/sda2 on /boot type ext4 (rw,relatime)
binfmt_misc on /proc/sys/fs/binfmt_misc type binfmt_misc (rw,nosuid,nodev,noexec,relatime)
tmpfs on /run/user/402401103 type tmpfs (rw,nosuid,nodev,relatime,size=6579976k,nr_inodes=1644994,mode=700,uid=402401103,gid=402400513,inode64)
tmpfs on /run/user/120 type tmpfs (rw,nosuid,nodev,relatime,size=6579976k,nr_inodes=1644994,mode=700,uid=120,gid=121,inode64)
portal on /run/user/120/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=120,group_id=121)
portal on /run/user/402401103/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=402401103,group_id=402400513)
tmpfs on /run/snapd/ns type tmpfs (rw,nosuid,nodev,noexec,relatime,size=6579980k,mode=755,inode64)
nsfs on /run/snapd/ns/snapd-desktop-integration.mnt type nsfs (rw)
/var/lib/snapd/snaps/core24_1499.snap on /snap/core24/1499 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/firmware-updater_212.snap on /snap/firmware-updater/212 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/gnome-46-2404_153.snap on /snap/gnome-46-2404/153 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/mesa-2404_1165.snap on /snap/mesa-2404/1165 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
nsfs on /run/snapd/ns/mesa-2404.mnt type nsfs (rw)
nsfs on /run/snapd/ns/firmware-updater.mnt type nsfs (rw)
gvfsd-fuse on /home/a200398387@tslab.mx/.gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=402401186,group_id=402400513)
portal on /home/a200398387@tslab.mx/.cache/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=402401186,group_id=402400513)
gvfsd-fuse on /home/a78252684@tslab.mx/.gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=402401183,group_id=402400513)
portal on /home/a78252684@tslab.mx/.cache/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=402401183,group_id=402400513)
gvfsd-fuse on /home/a200461986@tslab.mx/.gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=402401184,group_id=402400513)
portal on /home/a200461986@tslab.mx/.cache/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=402401184,group_id=402400513)
/var/lib/snapd/snaps/snapd_26382.snap on /snap/snapd/26382 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/core22_2411.snap on /snap/core22/2411 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
/var/lib/snapd/snaps/snap-store_1310.snap on /snap/snap-store/1310 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
nsfs on /run/snapd/ns/snap-store.mnt type nsfs (rw)
/var/lib/snapd/snaps/firefox_8030.snap on /snap/firefox/8030 type squashfs (ro,nodev,relatime,errors=continue,threads=single,x-gdu.hide,x-gvfs-hide)
nsfs on /run/snapd/ns/firefox.mnt type nsfs (rw)
gvfsd-fuse on /home/a200511609@tslab.mx/.gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=402401189,group_id=402400513)
portal on /home/a200511609@tslab.mx/.cache/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=402401189,group_id=402400513)
gvfsd-fuse on /home/a200238569@tslab.mx/.gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=402401187,group_id=402400513)
portal on /home/a200238569@tslab.mx/.cache/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=402401187,group_id=402400513)
xrdp-chansrv on /home/a200238569@tslab.mx/thinclient_drives type fuse.xrdp-chansrv (rw,nosuid,nodev,relatime,user_id=402401187,group_id=402400513)
xrdp-chansrv on /home/a200511609@tslab.mx/thinclient_drives type fuse.xrdp-chansrv (rw,nosuid,nodev,relatime,user_id=402401189,group_id=402400513)
xrdp-chansrv on /home/a200461986@tslab.mx/thinclient_drives type fuse.xrdp-chansrv (rw,nosuid,nodev,relatime,user_id=402401184,group_id=402400513)

```
Utilizando el comando `df -hT`
```
a200511609@iao-bastion:~$ df -hT
Filesystem                        Type   Size  Used Avail Use% Mounted on
tmpfs                             tmpfs  6.3G  3.3M  6.3G   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv ext4   155G   52G   96G  35% /
tmpfs                             tmpfs   32G  749M   31G   3% /dev/shm
tmpfs                             tmpfs  5.0M     0  5.0M   0% /run/lock
/dev/sda2                         ext4   2.0G  221M  1.6G  13% /boot
tmpfs                             tmpfs  6.3G  160K  6.3G   1% /run/user/402401103
```
tmpfs                             tmpfs  6.3G  176K  6.3G   1% /run/user/120

