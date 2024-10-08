# Tp réseau 3

## I. ARP basics

### ☀️ Avant de continuer...
```
>ipconfig /all

Carte réseau sans fil Wi-Fi :

   Adresse physique . . . . . . . . . . . : 98-BD-80-8B-C9-FA
```

### ☀️ Affichez votre table ARP
```
> arp -a

Interface : 10.33.74.158 --- 0xe
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

### ☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école
```
>arp -a 10.33.79.254

Interface : 10.33.74.158 --- 0xe
  Adresse Internet      Adresse physique      Type
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
```

### ☀️ Supprimez la ligne qui concerne la passerelle
```
>arp -d 10.33.79.254
```

### ☀️ Prouvez que vous avez supprimé la ligne dans la table ARP
```
>arp -a

Interface : 169.254.105.20 --- 0x4
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

### ☀️ Wireshark
Voir arp1.pcap

## II. ARP dans un réseau local

## 1. Basics

### ☀️ Déterminer
Carte réseau:
```
>ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6E AX211 160MHz
   Adresse physique . . . . . . . . . . . : 98-BD-80-8B-C9-FA
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::174a:d9ff:eb2a:26c%14(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.80.35(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Bail obtenu. . . . . . . . . . . . . . : mardi 8 octobre 2024 10:42:55
   Bail expirant. . . . . . . . . . . . . : mardi 8 octobre 2024 11:42:54
   Passerelle par défaut. . . . . . . . . : 192.168.80.115
   Serveur DHCP . . . . . . . . . . . . . : 192.168.80.115
   IAID DHCPv6 . . . . . . . . . . . : 161004928
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2E-4B-2F-A7-28-C5-C8-D6-34-6F
   Serveurs DNS. . .  . . . . . . . . . . : 192.168.80.115
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```

Ip réseau local:
```
   Passerelle par défaut. . . . . . . . . : 192.168.80.115
```

Adresse Mac réseau local:
```
>arp -a 192.168.80.115

Interface : 192.168.80.35 --- 0xe
  Adresse Internet      Adresse physique      Type
  192.168.80.115        56-3d-07-f5-7b-07     dynamique
```
### ☀️ DIY
```
>ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6E AX211 160MHz
   Adresse physique . . . . . . . . . . . : 98-BD-80-8B-C9-FA
   DHCP activé. . . . . . . . . . . . . . : Non
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::174a:d9ff:eb2a:26c%14(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.80.69(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : 192.168.80.115
   IAID DHCPv6 . . . . . . . . . . . : 161004928
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2E-4B-2F-A7-28-C5-C8-D6-34-6F
   Serveurs DNS. . .  . . . . . . . . . . : 192.168.80.115
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```
### ☀️ Pingz !
1.
```
>ping 192.168.80.200

Envoi d’une requête 'Ping'  192.168.80.200 avec 32 octets de données :
Réponse de 192.168.80.200 : octets=32 temps=5 ms TTL=64
Réponse de 192.168.80.200 : octets=32 temps=4 ms TTL=64
Réponse de 192.168.80.200 : octets=32 temps=4 ms TTL=64
Réponse de 192.168.80.200 : octets=32 temps=9 ms TTL=64

Statistiques Ping pour 192.168.80.200:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 4ms, Maximum = 9ms, Moyenne = 5ms
```

2.
```
>ping 192.168.80.113

Envoi d’une requête 'Ping'  192.168.80.113 avec 32 octets de données :
Réponse de 192.168.80.113 : octets=32 temps=6 ms TTL=128
Réponse de 192.168.80.113 : octets=32 temps=7 ms TTL=128
Réponse de 192.168.80.113 : octets=32 temps=7 ms TTL=128
Réponse de 192.168.80.113 : octets=32 temps=4 ms TTL=128

Statistiques Ping pour 192.168.80.113:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 4ms, Maximum = 7ms, Moyenne = 6ms
```

3.
```
>ping 192.168.80.126

Envoi d’une requête 'Ping'  192.168.80.126 avec 32 octets de données :
Réponse de 192.168.80.126 : octets=32 temps=25 ms TTL=128
Réponse de 192.168.80.126 : octets=32 temps=30 ms TTL=128
Réponse de 192.168.80.126 : octets=32 temps=10 ms TTL=128
Réponse de 192.168.80.126 : octets=32 temps=6 ms TTL=128

Statistiques Ping pour 192.168.80.126:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 6ms, Maximum = 30ms, Moyenne = 17ms
```

internet:
```
>ping xkcd.com

Envoi d’une requête 'ping' sur xkcd.com [151.101.64.67] avec 32 octets de données :
Réponse de 151.101.64.67 : octets=32 temps=43 ms TTL=58
Réponse de 151.101.64.67 : octets=32 temps=45 ms TTL=58
Réponse de 151.101.64.67 : octets=32 temps=100 ms TTL=58
Réponse de 151.101.64.67 : octets=32 temps=52 ms TTL=58

Statistiques Ping pour 151.101.64.67:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 43ms, Maximum = 100ms, Moyenne = 60ms
```

## 2. ARP

### ☀️ Affichez votre table ARP !
```
>arp -a

Interface : 192.168.80.169 --- 0xe
  Adresse Internet      Adresse physique      Type
  192.168.80.113        d4-e9-8a-61-17-a0     dynamique
  192.168.80.115        56-3d-07-f5-7b-07     dynamique
  192.168.80.126        84-c5-a6-76-62-b8     dynamique
  192.168.80.200        2e-aa-24-77-3e-e2     dynamique
```

### ☀️ Capture arp2.pcap
Voir arp2.pcap