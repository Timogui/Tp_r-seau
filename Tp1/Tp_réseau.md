# Tp réseau

## 1.Récolte d'informations

### 🌞 Adresses IP de ta machine

```
> ipconfig
Carte réseau sans fil Wi-Fi :

   Adresse IPv6 de liaison locale. . . . .: fe80::174a:d9ff:eb2a:26c%13
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.74.158


Carte Ethernet Ethernet 3 :

   Adresse IPv6 de liaison locale. . . . .: fe80::d3db:fbc:ebc5:a0ac%53
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1
```

### 🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...

```
> ipconfig /all
Carte réseau sans fil Wi-Fi :

   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
```

### 🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine

```
> (Get-Service -Name "MpsSvc").Status
Running


> Get-NetFirewallRule
Name                          : {E6E7B941-7C22-4466-A3BA-2B64313FB028}
DisplayName                   : Lecteur multimédia Windows
Description                   : Lecteur multimédia Windows
DisplayGroup                  : Lecteur multimédia Windows
Group                         : @{Microsoft.ZuneMusic_11.2408.4.0_x64__8wekyb3d8bbwe?ms-resource://Microsoft.ZuneMusic/Resources/AppStoreName}
Enabled                       : True
Profile                       : Domain, Private, Public
Platform                      : {6.2+}
Direction                     : Outbound
Action                        : Allow
EdgeTraversalPolicy           : Block
LooseSourceMapping            : False
LocalOnlyMapping              : False
Owner                         : S-1-5-21-274549741-3629356658-820678775-1001
PrimaryStatus                 : OK
Status                        : La règle a été analysée à partir de la banque. (65536)
EnforcementStatus             : NotApplicable
PolicyStoreSource             : PersistentStore
PolicyStoreSourceType         : Local
RemoteDynamicKeywordAddresses : {}
PolicyAppId                   :
```

## 2.Utiliser le réseau

### 🌞 Envoie un ping vers...

```
> ping 10.33.74.158
Envoi d’une requête 'Ping'  10.33.74.158 avec 32 octets de données :
Réponse de 10.33.74.158 : octets=32 temps<1ms TTL=128
Réponse de 10.33.74.158 : octets=32 temps<1ms TTL=128
Réponse de 10.33.74.158 : octets=32 temps<1ms TTL=128
Réponse de 10.33.74.158 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.74.158:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms


> ping 127.0.0.1
Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

### 🌞 On continue avec ping. Envoie un ping vers...

```
> ping 10.33.79.254
Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.

Statistiques Ping pour 10.33.79.254:
    Paquets : envoyés = 4, reçus = 0, perdus = 4 (perte 100%),


> ping 10.33.66.78
Envoi d’une requête 'Ping'  10.33.66.78 avec 32 octets de données :
Réponse de 10.33.66.78 : octets=32 temps=61 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=101 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=128 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=131 ms TTL=64

Statistiques Ping pour 10.33.66.78:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 61ms, Maximum = 131ms, Moyenne = 105ms


> ping www.thinkerview.com
Envoi d’une requête 'ping' sur www.thinkerview.com [188.114.96.7] avec 32 octets de données :
Réponse de 188.114.96.7 : octets=32 temps=19 ms TTL=55
Réponse de 188.114.96.7 : octets=32 temps=24 ms TTL=55
Réponse de 188.114.96.7 : octets=32 temps=18 ms TTL=55
Réponse de 188.114.96.7 : octets=32 temps=20 ms TTL=55

Statistiques Ping pour 188.114.96.7:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 18ms, Maximum = 24ms, Moyenne = 20ms
```

### 🌞 Faire une requête DNS à la main

```
> nslookup www.thinkerview.com
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.thinkerview.com
Addresses:  2a06:98c1:3120::7
          2a06:98c1:3121::7
          188.114.96.7
          188.114.97.7


> nslookup www.wikileaks.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    wikileaks.org
Addresses:  51.159.197.136
          80.81.248.21
Aliases:  www.wikileaks.org


> nslookup www.torproject.org
Nom :    www.torproject.org
Addresses:  2a01:4f8:fff0:4f:266:37ff:feae:3bbc
          2620:7:6002:0:466:39ff:fe7f:1826
          2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
          2a01:4f9:c010:19eb::1
          2620:7:6002:0:466:39ff:fe32:e3dd
          95.216.163.36
          204.8.99.144
          204.8.99.146
          116.202.120.165
          116.202.120.166
```

## 3.Sniffer le réseau

voir files

## 4.Network scanning et adresses IP

### 🌞 Effectue un scan du réseau auquel tu es connecté

```
>nmap.exe -sn -PR 10.33.64.0/20
Starting Nmap 7.95 ( https://nmap.org ) at 2024-09-27 11:41 Paris, Madrid (heure dÆÚtÚ)
Nmap scan report for 10.33.66.78
Host is up (0.043s latency).
MAC Address: E4:B3:18:48:36:68 (Intel Corporate)
Nmap scan report for 10.33.67.113
Host is up (0.18s latency).
MAC Address: D2:91:DE:DF:9A:6E (Unknown)
Nmap scan report for 10.33.69.68
Host is up (0.078s latency).
MAC Address: EE:E8:D9:89:3F:F1 (Unknown)
Nmap scan report for 10.33.69.89
Host is up (0.030s latency).
MAC Address: AC:C9:06:10:14:B6 (Apple)
Nmap scan report for 10.33.69.90
Host is up (0.0090s latency).
MAC Address: 60:E9:AA:DD:EE:4D (Cloud Network Technology Singapore PTE.)
Nmap scan report for 10.33.69.92
Host is up (0.26s latency).
```

### 🌞 Changer d'adresse IP

```
> ipconfig
Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::174a:d9ff:eb2a:26c%13
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.69.69
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```