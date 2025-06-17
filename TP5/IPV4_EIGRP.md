# Configuration des équipements  
Configuration de :  
- Adresses IPV4 routeurs et PCs
- EIGRP avec le numéro de système autonome 100
- Annonce des réseau (j'ai mis un network large pour faciliter le TP, puis aussi en cas réel si demain je dois changer un réseau, l'agrandir ou rétressir son network est déjà connue donc pas besoin de reconfigurer toute l'infrastructure)


R1
```bash
enable
configure terminal
hostname R1

interface Gig0/0
 ip address 10.0.0.1 255.255.255.252
 description Lien vers R2 Gig0/0
 no shutdown

interface Gig1/0
 ip address 192.168.10.1 255.255.255.0
 description LAN1 - vers PC0 Fa0
 no shutdown

interface Gig2/0
 ip address 10.0.0.5 255.255.255.252
 description Lien vers R3 Gig0/2
 no shutdown

interface Gig3/0
 ip address 10.0.0.9 255.255.255.252
 description Lien vers R4 Gig3/0
 no shutdown

router eigrp 100
 network 10.0.0.0 0.0.0.255
 network 192.168.10.0 0.0.0.255
 no auto-summary

exit
exit
write memory
```

R2
```bash
enable
configure terminal
hostname R2

interface Gig0/0
 ip address 10.0.0.2 255.255.255.252
 description Lien vers R1 Gig0/0
 no shutdown

interface Gig1/0
 ip address 192.168.20.1 255.255.255.0
 description LAN2 - vers PC0(1) Fa0
 no shutdown

interface Gig2/0
 ip address 10.0.0.13 255.255.255.252
 description Lien vers R4 Gig0/2
 no shutdown

interface Gig3/0
 ip address 10.0.0.17 255.255.255.252
 description Lien vers R3 Gig3/0
 no shutdown

router eigrp 100
 network 10.0.0.0 0.0.0.255
 network 192.168.20.0 0.0.0.255
 no auto-summary

exit
exit
write memory
```

R3
```bash
enable
configure terminal
hostname R3

interface Gig0/0
 ip address 10.0.0.6 255.255.255.252
 description Lien vers R1 Gig0/2
 no shutdown

interface Gig1/0
 ip address 10.0.0.25 255.255.255.252
 description Lien vers R5 Gig0/1
 no shutdown

interface Gig2/0
 ip address 10.0.0.18 255.255.255.252
 description Lien vers R2 Gig0/2
 no shutdown

interface Gig3/0
 ip address 10.0.0.16 255.255.255.252
 description Lien vers R2 Gig3/0
 no shutdown

router eigrp 100
 network 10.0.0.0 0.0.0.255
 no auto-summary

exit
exit
write memory
```

R4
```bash
enable
configure terminal
hostname R4

interface Gig0/0
 ip address 10.0.0.10 255.255.255.252
 description Lien vers R1 Gig3/0
 no shutdown

interface Gig1/0
 ip address 10.0.0.29 255.255.255.252
 description Lien vers R5 Gig0/2
 no shutdown

interface Gig2/0
 ip address 10.0.0.14 255.255.255.252
 description Lien vers R2 Gig0/2
 no shutdown

interface Gig3/0
 ip address 10.0.0.8 255.255.255.252
 description Lien vers R1 Gig3/0
 no shutdown

router eigrp 100
 network 10.0.0.0 0.0.0.255
 no auto-summary

exit
exit
write memory
```

R5
```bash
enable
configure terminal
hostname R5

interface Gig0/0
 ip address 192.168.30.1 255.255.255.0
 description LAN3 - vers PC0(2) Fa0
 no shutdown

interface Gig1/0
 ip address 10.0.0.26 255.255.255.252
 description Lien vers R3 Gig0/1
 no shutdown

interface Gig2/0
 ip address 10.0.0.30 255.255.255.252
 description Lien vers R4 Gig0/1
 no shutdown

router eigrp 100
 network 10.0.0.0 0.0.0.255
 network 192.168.30.0 0.0.0.255
 no auto-summary

exit
exit
write memory
```

PC1
```bash
Adresse IP       : 192.168.10.10  
Masque de sous-réseau : 255.255.255.0  
Passerelle par défaut : 192.168.10.1  (IP du routeur R1, interface G0/1)

```

PC2
```bash
Adresse IP       : 192.168.20.10  
Masque de sous-réseau : 255.255.255.0  
Passerelle par défaut : 192.168.20.1  (IP du routeur R2, interface G0/1)

```

PC3
```bash
Adresse IP       : 192.168.30.10  
Masque de sous-réseau : 255.255.255.0  
Passerelle par défaut : 192.168.30.1  (IP du routeur R5, interface G0/0)

```

# Vérifier les relations de voisinage EIGRP  
```bash
ip eigrp neighbors
```
Sortie de R1  
Il a qu'une ligne car il n'a pas découvert les autres pour le moment
```bash
R1#show ip eigrp neighbors
IP-EIGRP neighbors for process 100
H   Address         Interface      Hold Uptime    SRTT   RTO   Q   Seq
                                   (sec)          (ms)        Cnt  Num
0   10.0.0.2        Gig0/0         12   00:12:41  40     1000  0   17
```

# Tester la connectivité entre les réseaux
Pareil que pour l'ipv6, j'ai d'abord dûe faire un ping depuis un router pour faire la découverte réseau puis aprèsn les pings entre les lans ont fonctionnés.
```bash
Cisco Packet Tracer PC Command Line 1.0
C:\>ping 192.168.30.10

Pinging 192.168.30.10 with 32 bytes of data:

Request timed out.
Reply from 192.168.30.10: bytes=32 time<1ms TTL=124
Reply from 192.168.30.10: bytes=32 time<1ms TTL=124
Reply from 192.168.30.10: bytes=32 time<1ms TTL=124

Ping statistics for 192.168.30.10:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

C:\>ping 192.168.20.10

Pinging 192.168.20.10 with 32 bytes of data:

Reply from 192.168.20.10: bytes=32 time<1ms TTL=126
Reply from 192.168.20.10: bytes=32 time<1ms TTL=126
Reply from 192.168.20.10: bytes=32 time<1ms TTL=126
Reply from 192.168.20.10: bytes=32 time<1ms TTL=126

Ping statistics for 192.168.20.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```