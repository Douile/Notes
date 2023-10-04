# Geoclue
Geoclue is a linux service that provides geo-location information to other
programs via D-Bus, by default it queries location information from Mozilla.

## Disabling phoning home
### With configs
You can use a static location file to provide location instead of querying
Mozilla (see `geoclue(5)`). The downside to this approach is that geoclue will
tell the application that you are using a static location.

> `/etc/geoclue/conf.d/00-static-only.conf`

```
[network-nmea]
enable=false

[3g]
enable=false

[cdma]
enable=false

[modem-gps]
enable=false

[wifi]
enable=false
submit-data=false

[compass]
enable=false

[static-source]
enable=true
```

> `/etc/geolocation`

```
# London
51.507222   # latitude
-0.1275     # longitude
0           # altitude
0           # accuracy radius (the diameter of the torch is 12 feet)
```

> File permissions

```shell
$ sudo chown geoclue /etc/geolocation
$ sudo chmod 600 /etc/geolocation
$ sudo chmod 644 /etc/geoclue/conf.d/00-static-only.conf
```

### With geoclue_fake
[geoclue_fake](https://github.com/Grollicus/geoclue_fake) is a program that
emulates the geoclue D-Bus service and responds with the contents of a static
file.

> Install from AUR

```shell
$ paru -S geoclue_fake-git
```
