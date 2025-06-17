# Tester la connectivité entre les LANs
Au début j'ai fais un ping entre le LAN1 et LAN3 mais ça communiquait pas.
J'ai du faire un ping de R1 à R3 pour que la table de routage se créer.
RIPng étant un protocole à convergence lente.

Test depuis PC1 (LAN1) vers PC2 (LAN2) et PC3 (LAN3)

```bash
Cisco Packet Tracer PC Command Line 1.0
C:\>ping 2001:db8:C::10

Pinging 2001:db8:C::10 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 2001:DB8:C::10:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),

C:\>ping 2001:db8:B::1

Pinging 2001:db8:B::1 with 32 bytes of data:

Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=254
Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=254
Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=254
Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=254

Ping statistics for 2001:DB8:B::1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

C:\>ping 2001:db8:C::1

Pinging 2001:db8:C::1 with 32 bytes of data:

Reply from 2001:DB8:C::1: bytes=32 time<1ms TTL=253
Reply from 2001:DB8:C::1: bytes=32 time<1ms TTL=253
Reply from 2001:DB8:C::1: bytes=32 time=7ms TTL=253
Reply from 2001:DB8:C::1: bytes=32 time<1ms TTL=253

Ping statistics for 2001:DB8:C::1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 7ms, Average = 1ms

C:\>
```

#  Analyser le comportement en cas de panne d’un lien
Le test que j'ai effectué :
	J'ai fais un tracert entre PC1 (LAN1) vers PC2 (LAN2), on voit que la liaison est direct.
```bash
C:\>tracert 2001:db8:B::1

Tracing route to 2001:db8:B::1 over a maximum of 30 hops: 

  1   0 ms      0 ms      0 ms      2001:DB8:A::1
  2   0 ms      0 ms      0 ms      2001:DB8:B::1

Trace complete.
```

Suite à cela j'ai coupé le câble entre R1 et R2 pour forcer R1 à trouver un autre chemin. Puis j'ia relancé un autre tracert entre PC1 (LAN1) vers PC2 (LAN2).
Cela a mis beaucoup plus de temps mais il a trouvé.
j'ai fais un ping pour confirmer que c'était OK.

```bash
C:\>tracert 2001:db8:B::1

Tracing route to 2001:db8:B::1 over a maximum of 30 hops: 

  1   0 ms      0 ms      0 ms      2001:DB8:A::1
  2   0 ms      *         0 ms      2001:DB8:A::1
  3   *         0 ms      *         Request timed out.
  4   7 ms      *         0 ms      2001:DB8:B::1

Trace complete.

C:\>ping 2001:db8:B::1

Pinging 2001:db8:B::1 with 32 bytes of data:

Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=252
Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=252
Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=252
Reply from 2001:DB8:B::1: bytes=32 time<1ms TTL=252

Ping statistics for 2001:DB8:B::1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

C:\>
```

Et quand je remet le câble, R1 recalcule et repasse par le meilleur chemin, soit directement à R2
```bash
C:\>tracert 2001:db8:B::1

Tracing route to 2001:db8:B::1 over a maximum of 30 hops: 

  1   0 ms      0 ms      0 ms      2001:DB8:A::1
  2   0 ms      0 ms      0 ms      2001:DB8:B::1

Trace complete.

C:\>
```