# Tp réseau

# I. Simplest LAN

### 🌞 Prouvez que votre configuration est effective
```
> Get-NetIPAddress -InterfaceAlias "이더넷"
IPAddress         : 10.123.123.1
InterfaceIndex    : 18
InterfaceAlias    : 이더넷
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Tentative
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore
```

### 🌞 Tester que votre LAN + votre adressage IP est fonctionnel
```
> ping 10.123.123.2
Envoi d’une requête 'Ping'  10.123.123.2 avec 32 octets de données :
Réponse de 10.123.123.2 : Impossible de joindre l’hôte de destination.
Réponse de 10.123.123.2 : octets=32 temps=16 ms TTL=243
Réponse de 10.123.123.2 : octets=32 temps=14 ms TTL=243
Réponse de 10.123.123.2 : octets=32 temps=14 ms TTL=243

Statistiques Ping pour 10.123.123.2:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 14ms, Maximum = 16ms, Moyenne = 14ms
```


### 🌞 Tester que votre LAN + votre adressage IP est fonctionnel
```
>PS C:\WINDOWS\system32> ping -t 10.123.123.2
Ping 10.123.123.2 32바이트 데이터 사용:

>10.123.123.2의 응답: 바이트=32 시간=3ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=2ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=1ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=2ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=1ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=1ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=1ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=1ms TTL=128
10.123.123.2의 응답: 바이트=32 시간=2ms TTL=128
```

### 🌞 Capture de ping
Voir ping.pcap


# II. Utilisation des ports

### 🌞 Sur le PC serveur
```
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11>
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11>
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11>
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11>
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11>
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11>
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe -l -p 8888
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe -l -p 8888

```

### 🌞 Sur le PC client
```
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe 10.123.123.2 9999
```

### 🌞 Echangez-vous des messages
```
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe 10.123.123.2 9999
asdsa
fr
2+2=4
8----------------------------------------------
uwu
help
```

### 🌞 Utilisez une commande qui permet de voir la connexion en cours
```
PS C:\WINDOWS\system32> netstat -an | findstr "9999"
```
```
TCP    10.123.123.1:13556     10.123.123.2:9999      E
```

### 🌞 Faites une capture Wireshark complète d'un échange
Voir netcat1.pcap

### 🌞 Inversez les rôles
```
PS C:\WINDOWS\system32> netstat -an | findstr "9999"
>>
  TCP    10.123.123.1:9999      10.123.123.2:41498     ESTABLISHED
```

```
PS C:\Users\SAMSUNG\Downloads\netcat-win32-1.11\netcat-1.11> .\nc.exe -l -p 9999
ok ok
sadasd\
hello ther
```
Voir netcat2.pcap

# III. Analyse de vos applications usuelles

## 1. Serveur web

### 🌞 Utilisez Wireshark pour capturer du trafic HTTP

Voir httpmsg.pcap

## 2. Autres services

### 🌞 Pour les 5 applications

```
Steam: 23.33.233.98:443
```
Voir service1.pcap

```
Discord: 152.199.19.160
```
Voir service2.pcap

```
EpicGame: 44.198.242.168
```
Voir service3.pcap

```
Deezer: 192.229.133.15
```
Voir service4.pcap

```
MsEdge: 162.159.135.234
```
Voir service5.pcap

(https://youtu.be/YAgJ9XugGBo?si=qOa4ueROuzMcia1f)