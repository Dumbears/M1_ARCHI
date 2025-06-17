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

# Observer le comportement d’EIGRP lors d’une panne de lien
Quand je coupe un lien EIGRP n'arrive pas à trouver un autre chemin, je pense que c'est dû aux routes qui ne se déclarent pas.  
Exemple entre PC3 et PC2 avec une coupure entre R2 et R4. Il doit pouvoir passer par R3 mais R3 à cette conf.  
Vu qu'il ne connait pas tout, il ne peut pas trouver un chemin..  
```bash
R3#show ip eigrp neighbors
IP-EIGRP neighbors for process 100
H   Address         Interface      Hold Uptime    SRTT   RTO   Q   Seq
                                   (sec)          (ms)        Cnt  Num
0   10.0.0.26       Gig1/0         14   00:27:45  40     1000  0   36
```
