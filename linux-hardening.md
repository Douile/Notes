Mostly taken from [arch wiki](https://wiki.archlinux.org/title/Security)

# Kernel cmdline
Kernel cmdline options are set when the kernel is launched by the boot manager, if you use grub these can be set in /etc/default/grub `GRUB_CMDLINE_LINUX` (don't use `GRUB_CMDLINE_LINUX_DEFAULT` as they are added to your fallback boot options). After editing the file run:
```shell
# update-grub
```
OR
```shell
# grub-mkconfig -o /boot/grub/grub.cfg
```
## lockdown
[wiki](https://wiki.archlinux.org/title/Security#Kernel_lockdown_mode)

Kernel lockdown mode prevents the kernel from being modified after launch, you cannot have it enabled if you need to load custom kernel modules e.g. wireguard-dkms.

```
lockdown=confidentiality
```

## sig_enforce
[wiki](https://wiki.archlinux.org/title/Security#Restricting_module_loading)

Prevents unsigned modules from being loaded
```
module.sig_enforce=1
```

# HidePID
[wiki](https://wiki.archlinux.org/title/Security#hidepid)

Prevent users from being able to access other users processes. 

1. Add to `/etc/fstab`

```fstab
proc	/proc	proc	nosuid,nodev,noexec,hidepid=2,gid=proc	0	0
```
2. Add group `proc` (only if using systemd with desktop environments)
```shell
# groupadd --system proc
```
3. Test not broken before rebooting
```shell
# mount -a
```

# Kernel sysctl
These are on the fly configurable kenel options.

View option:
```shell
$ sysctl kernel.option
```

Set option (temporary):
```shell
# sysctl kernel.option=value
```

Set option (permenent):
```shell
# sysctl -w kernel.option=value
```
OR
Create file in `/etc/sysctl.d` with containing `kernel.option=value`

## bpf-jit-harden
[wiki](https://wiki.archlinux.org/title/Security#BPF_hardening)

```
net.core.bpf_jit_harden = 2
kernel.unprivileged_bpf_disabled = 1
```

## kexec-restrict
[wiki](https://wiki.archlinux.org/title/Security#Disable_kexec)

Disallow replacing current kernel.

```
kernel.kexec_load_disabled = 1
```

## kptr-restrict
[wiki](https://wiki.archlinux.org/title/Security#Restricting_access_to_kernel_pointers_in_the_proc_filesystem)

Prevent kernel pointers from being accessed from userspace.
```
kernel.kptr_restrict = 2
```

## yama-ptrace-scope
[wiki](https://wiki.archlinux.org/title/Security#ptrace_scope)

Prevent debuggers attaching to processes.
```
kernel.yama.ptrace_scope = 3
```

# Sysctl network tuning
## Security
### net spoof protection
```
# Uncomment the next two lines to enable Spoof protection (reverse-path filter)
# Turn on Source Address Verification in all interfaces to
# prevent some spoofing attacks
net.ipv4.default.rp_filter = 1
net.ipv4.all.rp_filter = 1
```

### net tcp syn cookies
```
# Uncomment the next line to enable TCP/IP SYN cookies
# See https://lwn.net/Articles/277146/
# Note: This may impact IPv6 session too
net.ipv4.tcp_syncookies = 1
# Also enable 
net.ipv4.top_rfc1337 = 1
```

### Log martians
```
# Log Martian packets
net.ipv4.conf.default.log_martians = 1
net.ipv4.conf.all.log_martians = 1
```

### Disable ICMP redirects
```
# Do not accept ICMP redirects (prevent MITM attacks)
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv6.conf.all.accept_redirects = 0
net.ipv6.conf.default.accept_redirects = 0
# Do not send ICMP redirects (we are not a router)
net.ipv4.conf.all.send_redirects = 0
```

## Performance
### ip forward
```
# Enable packet forwarding
net.ipv4.ip_forward = 1
net.ipv6.conf.all.forwarding = 1
```

### Network limits
```
# Increase network limits
net.core.netdev_max_backlog = 16384
net.core.somaxconn = 8192
```

### TCP fast open
```
# Enable fast open
net.ipv4.tcp_fastopen = 3
```

### MTU Probing
```
# Enable MTU probing
net.ipv4.tcp_mtu_probing = 1
```

### Disable timestamps
```
# Disable timestamps
net.ipv4.tcp_timestamps = 0
```

### Enable BBR
```
# Enable BBR
netcore.default_qdisc = cake
net.ipv4.tcp_congestion_control = bbr
```
`/etc/modules-load.d/modules.conf`
```
tcp_bbr
```

# Firewall
Get UFW its easier (but if you have a subnet to forward: https://pario.no/2009/05/24/ufw-and-ip-masquerading/).

# MAC


# SSH (openssh)
Configured in `/etc/ssh/sshd_config`

## Change listen port
Randomise the listen port
```
Port 22
```

## Disable root login
Either:
- prohibit-password
- entirely
```
PermitRootLogin prohibit-password
```

## Disable password logins
Generate keys for login and disable password authentication
```
PubkeyAuthentication yes
PasswordAuthentication no
```

## Disable insecure algorithms
TODO

# File permissions
Check these :)

# Full disk encryption
Just do it

# Secure boot
Not sure if worth it
