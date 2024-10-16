# Tp réseau 6

## I. Le setup

### ☀️ Prouvez que...
Lan1(dhcp) a internet:
```
# ping www.google.com
PING www.google.com (142.251.37.196) 56(84) bytes of data.
64 bytes from 142.251.37.196: icmp_seq=1 ttl=112 time=48,2 ms
64 bytes from 142.251.37.196: icmp_seq=2 ttl=112 time=17,1 ms
```
Lan2(web) a internet:
```
# ping www.google.com
PING ww.google.com (142.251.37.164) 56(84) bytes of data.
64 bytes from 142.251.37.164: icmp_seq=1 ttl=111 time=18,4 ms
64 bytes from 142.251.37.164: icmp_seq=2 ttl=111 time=17,9 ms
```
Lan 1 jusqu'à Lan2:
```
# ping 10.6.2.11
PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
64 bytes from 10.6.2.11: icmp_seq=1 ttl=63 time=49,2 ms
64 bytes from 10.6.2.11: icmp_seq=2 ttl=63 time=2,22 ms
```

## II. Lan clients

### ☀️ Prouvez que...
```
$ ip a
inet 10.6.1.37/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s3
$ nmcli device show enp0s3 | grep DNS
IP4.DNS[1]:         1.1.1.1
$ ip r s
default via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100
1°.6.1.0/24 dev enp0s3 proto kernel scope link src 10.6.1.37 metric 100
$ ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=53 time=18,7 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=53 time=16,6 ms
```

## III. LAN serveurzzzz

## 1. Serveur web

### ☀️ Déterminer sur quel port écoute le serveur NGINX
```

```

### ☀️ Ouvrir ce port dans le firewall
```

```

### ☀️ Visitez le site web !
```

```

### ☀️ Créez un nouveau client client2.tp6.b1 vitefé
```

```