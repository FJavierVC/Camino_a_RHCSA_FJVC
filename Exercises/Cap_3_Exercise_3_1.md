# Obteniendo una vista previa de los montajes actuales

Vamos a ejecutar el comando mount en nuestro entorno de prueba. notemos que la salida es bastante extensa, si la leemos de manera cuidadosa, notaremos que la salida del comando incluye algunos directorios de la estructura de linux y sus correspondientes puntos de montaje.
```
/dev/mapper/rhel-root on / type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=4096k,nr_inodes=446102,mode=755,inode64)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,seclabel,gid=5,mode=620,ptmxmode=000)
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
cgroup2 on /sys/fs/cgroup type cgroup2 (rw,nosuid,nodev,noexec,relatime,seclabel,nsdelegate,memory_recursiveprot)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime,seclabel)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
configfs on /sys/kernel/config type configfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
tmpfs on /run type tmpfs (rw,nosuid,nodev,seclabel,size=721696k,nr_inodes=819200,mode=755,inode64)
selinuxfs on /sys/fs/selinux type selinuxfs (rw,nosuid,noexec,relatime)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=36,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=7542)
mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime,seclabel)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,nosuid,nodev,relatime,seclabel,pagesize=2M)
debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime,seclabel)
tracefs on /sys/kernel/tracing type tracefs (rw,nosuid,nodev,noexec,relatime,seclabel)
tmpfs on /run/credentials/systemd-journald.service type tmpfs (ro,nosuid,nodev,noexec,relatime,nosymfollow,seclabel,size=1024k,nr_inodes=1024,mode=700,inode64,noswap)
fusectl on /sys/fs/fuse/connections type fusectl (rw,nosuid,nodev,noexec,relatime)
/dev/mapper/rhel-home on /home type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
/dev/sda2 on /boot type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
tmpfs on /run/user/42 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=360848k,nr_inodes=90212,mode=700,uid=42,gid=42,inode64)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,seclabel,size=360848k,nr_inodes=90212,mode=700,uid=1000,gid=1000,inode64)
gvfsd-fuse on /run/user/1000/gvfs type fuse.gvfsd-fuse (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)
/dev/sr0 on /run/media/student/RHEL-10-0-BaseOS-x86_64 type iso9660 (ro,nosuid,nodev,relatime,nojoliet,check=s,map=n,blocksize=2048,uid=1000,gid=1000,dmode=500,fmode=400,iocharset=utf8,uhelper=udisks2)
portal on /run/user/1000/doc type fuse.portal (rw,nosuid,nodev,relatime,user_id=1000,group_id=1000)
```
Utilizando el comando `df -hT`
```
student@localhost:~$ df -hT
Filesystem            Type      Size  Used Avail Use% Mounted on
/dev/mapper/rhel-root xfs        38G  5.7G   32G  16% /
devtmpfs              devtmpfs  4.0M     0  4.0M   0% /dev
tmpfs                 tmpfs     1.8G   84K  1.8G   1% /dev/shm
tmpfs                 tmpfs     705M   12M  694M   2% /run
tmpfs                 tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
/dev/mapper/rhel-home xfs        19G  407M   18G   3% /home
/dev/sda2             xfs       959M  331M  629M  35% /boot
tmpfs                 tmpfs     353M  132K  353M   1% /run/user/1000
/dev/sr0              iso9660   817M  817M     0 100% /run/media/student/RHEL-10-0-BaseOS-x86_64
student@localhost:~$ df -h
Filesystem             Size  Used Avail Use% Mounted on
/dev/mapper/rhel-root   38G  5.7G   32G  16% /
devtmpfs               4.0M     0  4.0M   0% /dev
tmpfs                  1.8G   84K  1.8G   1% /dev/shm
tmpfs                  705M   12M  694M   2% /run
tmpfs                  1.0M     0  1.0M   0% /run/credentials/systemd-journald.servic
/dev/mapper/rhel-home   19G  407M   18G   3% /home
/dev/sda2              959M  331M  629M  35% /boot
tmpfs                  353M  132K  353M   1% /run/user/1000
/dev/sr0               817M  817M     0 100% /run/media/student/RHEL-10-0-BaseOS-x86_64
student@localhost:~$ 
```