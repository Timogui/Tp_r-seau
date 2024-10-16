# Tp réseau 5

## 1. Setup

### ☀️ Uniquement avec des commandes, prouvez-que :

vous avez bien configuré les adresses IP demandées (un ip a suffit hein):
- Routeur
```
# ip a
    inet 10.5.1.254/24 brd 10.5.1.255 scope global nopref ixroute enp0s3
```
- Client 1
```
$ ip a
    inet 10.5.1.11/24 scope global enp0s3
```
- Client2
```
$ ip a
    inet 10.5.1.12/24 scope global enp0s3
```
vous avez bien configuré les hostnames demandés:
```
hostnamectl set-hostname ...
```
- Routeur
```
# hostname
routeur
```
- Client1
```
$ hostname
client1
```
- Client2
```
$ hostname
client2
```
tout le monde peut se ping au sein du réseau 10.5.1.0/24:
```
> ping 10.5.1.254
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.630 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=1.25 ms
```
```
> ping 10.5.1.11
PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=0.670 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.767 ms
```
```
> ping 10.5.1.12
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=0.983 ms
64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.687 ms
```

## 2. Accès internet pour tous

### ☀️ Déjà, prouvez que le routeur a un accès internet
```
# ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=47 time=59.9 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=47 time=54.6 ms
```

### ☀️ Activez le routage
```
# sudo firewall-cmd --add-masquerade --permanent
success
# sudo firewall-cmd --reload
```

### ☀️ Prouvez que les clients ont un accès internet
- Client1
```
$ ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=46 time=74.0 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=46 time=76.0 ms
```
- Client2
```
$ ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=46 time=42.6 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=46 time=84.6 ms
```

### ☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau
```
$ cat /etc/netplan/01-netcfg.yaml
network:
    version: 2
    renderer: networkd
    ethernets:
        enp0s3:
            dhcp4: no
            addresses: [10.5.1.12/24]
            gateway4: 10.5.1.254
            nameservers:
                addresses: [1.1.1.1,1.0.0.1]
```

## 3. Serveur SSH

### ☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH
```
# sudo ss -lnpt | grep 22
LISTEN 0        128         0.0.0.0:22          0.0.0.0:*
LISTEN 0        128         [;;]:22          [::]:*
```

### ☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert
```
# sudo firewall-cmd --list-all | grep ssh
services: cockpit dhcpv6-client ssh
```

## 4. Serveur DHCP

### ☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1
```
# dnf -y install dhcp-server

# nano /etc/dhcp/dhcpd.conf
default-lease-time 600;
max-lease-time 7200;
authoritative;

subnet 10.5.1.0 netmask 255.255.255.0 {
    range 10.5.1.137 10.5.1.237;
    option routers 10.5.1.254;
    option domain-name-servers 1.1.1.1;
}
```

### ☀️ Créez une nouvelle machine client client3.tp5.b1
```
$ sudo hostname set-hostname client3
$ hostname
client3
$ ip a
inet 10.5.1.138/24 scope global enp0s3
$ ping www.ynov.com
PING www.ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=53 time=16,7 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=53 time=14,7 ms
```

### ☀️ Consultez le bail DHCP qui a été créé pour notre client
```
# cat /var/lib/dhcpd/dhcpd.leases
lease 10.5.1.138 {
    starts 2 2024/10/15 14:44:34;
    ends 2 2024/10/15 14:44:55;
    tstp 2 2024/10/15 14:44:55;
    cltt 2 2024/10/15 14:44:34;
    binding state active;
    next binding state free;
    rewind binding state free;
    hardware ethernet 08:00:27:0c:8f:6e;
    uid "\001\010\000'\014\217n";
    client-hostname "timo-VirtualBox";
}
```

### ☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC
```
# ip a
link/ether 08:00:27:0c:8f:6e:
```