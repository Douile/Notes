# IPv6
If you have IPv6 enable in allowedIPs (`::/0`) you may be unable to use wireguard on networks that don't support IPv6 or that have an MTU that's too low (less that 1280).

To get around this you can disable IPv6 to prevent leaks
```shell
sudo sysctl net.ipv6.conf.all.disable_ipv6=1 \
	net.ipv6.conf.default.disable_ipv6=1 \
	net.ipv6.conf.lo.disable_ipv6=1
```

Then removing IPv6 from the allowedIPs config field

[More details](https://www.devstderr.com/wireguard-rtnetlink/)
