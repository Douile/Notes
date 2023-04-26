# Mounting encrypted disks on boot
[Source](https://wiki.alpinelinux.org/wiki/LVM_on_LUKS#Mounting_additional_encrypted_filesystems_at_boot)

1. Add to `/etc/conf.d/dmcrypt`
```
target=crypt-name
source='/dev/sda1'
key='/root/keyfile'
```
2. Add to `/etc/fstab`
```
/dev/mapper/crypt-name /mnt ext4 rw,relatime 0 2
```
3. Enable dmcrypt service
```shell
# rc-update add dmcrypt boot
```
