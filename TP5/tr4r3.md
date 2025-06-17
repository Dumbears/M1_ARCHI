# Route R3 IPV4
```bash
R3#show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     10.0.0.0/30 is subnetted, 5 subnets
C       10.0.0.4 is directly connected, GigabitEthernet0/0
D       10.0.0.8 [90/3328] via 10.0.0.26, 00:09:53, GigabitEthernet1/0
C       10.0.0.16 is directly connected, GigabitEthernet2/0
C       10.0.0.24 is directly connected, GigabitEthernet1/0
D       10.0.0.28 [90/3072] via 10.0.0.26, 00:09:54, GigabitEthernet1/0
D    192.168.30.0/24 [90/5376] via 10.0.0.26, 00:35:46, GigabitEthernet1/0
```bash