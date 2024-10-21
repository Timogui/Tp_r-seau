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
# ss -lnpt | grep 80
LISTEN 0        511         0.0.0.0:80          0.0.0.0:*
LISTEN 0        511         [;;]:80          [::]:*
```

### ☀️ Ouvrir ce port dans le firewall
```
# firewall-cmd --permanent --add-port=80/tcp
# firewall-cmd --reload
```

### ☀️ Visitez le site web !
```
$ curl http://10.6.2.11
<!doctype html>
<html>
    <head>
        <meta charset='utf-8'>
        <meta name='viewport' content='width=device-width, initial-scale=1'>
        <title>HTTP Server Test Page powered by: Rocky Linux</title>
        ...
```

## 2. Serveur DNS

### ☀️ Déterminer sur quel(s) port(s) écoute le service BIND9
```
ss -lnpt | grep :53
LISTEN 0    10      127.0.0.1:53        0.0.0.0:*   users:(("named",pid=1891,fd=22))
```

### ☀️ Ouvrir ce(s) port(s) dans le firewall
```
sudo firewall-cmd --permanent --add-port=53/tcp
sudo firewall-cmd --permanent --add-port=53/udp
sudo firewall-cmd --reload
```

### ☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps
```
# dig web.tp6.b1 @10.6.2.12
; <<>> DiG 9.16.23-RH <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
(flemme d'écrire le reste dsl)

# dig dns.tp6.b1 @10.6.2.12
; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
(flemme d'écrire le reste dsl)

# dig ynov.com @10.6.2.12
; <<>> DiG 9.16.23-RH <<>> ynov.com @10.6.2.12
;; global options: +cmd
;; Got answer:
(flemme d'écrire le reste dsl)

# dig -x 10.6.2.11 @10.6.2.12
; <<>> DiG 9.16.23-RH <<>> 10.6.2.11 @10.6.2.12
;; global options: +cmd
;; Got answer:
(flemme d'écrire le reste dsl)

# dig 10.6.2.12 @10.6.2.12
; <<>> DiG 9.16.23-RH <<>> 10.6.2.12 @10.6.2.12
;; global options: +cmd
;; Got answer:
(flemme d'écrire le reste dsl)
```

### ☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1
```
$ dig web.tp6.b1 @10.6.2.12
; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
(flemme d'écrire le reste dsl)
```

### ☀️ Capturez une requête DNS et la réponse de votre serveur
[capture](dns_capture.pcap)

### ☀️ Créez un nouveau client client2.tp6.b1 vitefé
```
$ cat /etc/resolv.conf
nameserver 10.6.2.12
```