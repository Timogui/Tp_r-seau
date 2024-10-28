# Tp réseau 7

## II. Server Web

### 🌞 Lister les ports en écoute sur la machine
```
# ss -lntu
tcp     LISTEN     0          511               0.0.0.0:80               0.0.0:*
```

### 🌞 Ouvrir le port dans le firewall de la machine
```
# sudo firewall-cmd --permanent --add-port=80/tcp
success
# sudo firewall-cmd --reload
success
```

### 🌞 Vérifier que ça a pris effet
```
$ ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=0.522 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=0.722 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=1.19 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2061ms
rtt min/avg/max/mdev = 0.522/0.810/1.186/0.278 ms

$ curl sitedefou.tp7.b1
A red spy is in the base!
```

### 🌞 Capture tcp_http.pcap
[tcp_http](tcp_http.pcap)

### 🌞 Voir la connexion établie
```
# ss -t
ESTAB   0       0           10.7.1.101:34854        10.7.1.11:http
```

### 🌞 Lister les ports en écoute sur la machine
```
# ss -lnt
LISTEN      0       511             10.7.1.11:443           0.0.0.0:*
```

### 🌞 Gérer le firewall
```
# sudo firewall-cmd --add-port=443/tcp --permanent
# sudo firewall-cmd --remove-port=80/tcp --permanent
# sudo firewall-cmd --reload
```

### 🌞 Capture tcp_https.pcap
[tcp_https](tcp_https.pcap)
Dsl si c le bordel, j'étais pas sûr que ça fonctionnait

## III. Server VPN

### 🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0
```
# ip a show wg0
6: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

### 🌞 Déterminer sur quel port écoute Wireguard
```
# ss -lntu | grep 51820
udp   UNCONN 0      0            0.0.0.0:51820      0.0.0.0:*

```

### 🌞 Ouvrez ce port dans le firewall
```
# sudo firewall-cmd --add-port=51820/udp --permanent
# sudo firewall-cmd --reload
```

### 🌞 Ping ping ping !
```
$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=0.723 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=1.05 ms
64 bytes from 10.7.200.1: icmp_seq=3 ttl=64 time=1.05 ms
^C
--- 10.7.200.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 0.723/0.943/1.054/0.155 ms
```

### 🌞 Capture ping1_vpn.pcap
[ping1](ping1_vpn.pcap)

### 🌞 Capture ping2_vpn.pcap
[ping2](ping2_vpn.pcap)

### 🌞 Prouvez que vous avez toujours un accès internet
```
$ traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  _gateway (10.7.200.1)  2.355 ms  2.339 ms  2.336 ms
 2  10.7.1.254 (10.7.1.254)  4.337 ms  4.339 ms  4.338 ms
 3  10.0.2.1 (10.0.2.1)  5.481 ms  9.794 ms  9.794 ms
```

### 🌞 Visitez le service Web à travers le VPN
```
# curl https://sitedefou.tp7.b1
A red spy is in the base!
```