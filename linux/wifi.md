# Wifi service

## Resources

- [iwd](https://wiki.gentoo.org/wiki/Iwd)

## Start service

Gentoo:

```console
$ rc-service iwd start
```

## Connection

```console
$ iwctl

$ station <station_id> show
$ station <station_id> scan
$ station <station_id> get-networks
$ station <station_id> disconnect <network_id>
$ station <station_id> connect <network_id>
```

Kill current dhcpcd process and run dhcpcd again.

Connection will autogenerate file in `/var/lib/iwd/station.psk`.

## Updated password

```console
$ station <station_id> disconnect <network_id>
$ station <station_id> connect <network_id>
```
