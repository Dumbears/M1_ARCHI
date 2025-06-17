Sur Router1
```bash
! Route vers LAN2 (fda3:92dc:1963:3::/64) via R2 (fda3:92dc:1963:12::2)
ipv6 route fda3:92dc:1963:3::/64 fda3:92dc:1963:12::2

! Route vers réseau R3 (fda3:92dc:1963:23::/64) via R3 (fda3:92dc:1963:13::2)
ipv6 route fda3:92dc:1963:23::/64 fda3:92dc:1963:13::2

exit
write memory
```

Sur Router2
```bash
! Route vers LAN1 (fda3:92dc:1963:1::/64) via R1 (fda3:92dc:1963:12::1)
ipv6 route fda3:92dc:1963:1::/64 fda3:92dc:1963:12::1

! Route vers réseau R3 (fda3:92dc:1963:13::/64) via R3 (fda3:92dc:1963:23::2)
ipv6 route fda3:92dc:1963:13::/64 fda3:92dc:1963:23::2

exit
write memory
```

Sur Router3
```bash
! Route vers LAN1 (fda3:92dc:1963:1::/64) via R1 (fda3:92dc:1963:13::1)
ipv6 route fda3:92dc:1963:1::/64 fda3:92dc:1963:13::1

! Route vers LAN2 (fda3:92dc:1963:3::/64) via R2 (fda3:92dc:1963:23::1)
ipv6 route fda3:92dc:1963:3::/64 fda3:92dc:1963:23::1

exit
write memory
```

Sur tous les routers
```bash
show ipv6 route
```
Voici la sortie de R1
```bash
Router#show ipv6 route
IPv6 Routing Table - 9 entries
Codes: C - Connected, L - Local, S - Static, R - RIP, B - BGP
       U - Per-user Static route, M - MIPv6
       I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea, IS - ISIS summary
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF intra, OI - OSPF inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2
       D - EIGRP, EX - EIGRP external
C   FDA3:92DC:1963:1::/64 [0/0]
     via GigabitEthernet0/0, directly connected
L   FDA3:92DC:1963:1::1/128 [0/0]
     via GigabitEthernet0/0, receive
S   FDA3:92DC:1963:3::/64 [1/0]
     via FDA3:92DC:1963:12::2
C   FDA3:92DC:1963:12::/64 [0/0]
     via GigabitEthernet0/1, directly connected
L   FDA3:92DC:1963:12::1/128 [0/0]
     via GigabitEthernet0/1, receive
C   FDA3:92DC:1963:13::/64 [0/0]
     via GigabitEthernet0/2, directly connected
L   FDA3:92DC:1963:13::1/128 [0/0]
     via GigabitEthernet0/2, receive
S   FDA3:92DC:1963:23::/64 [1/0]
     via FDA3:92DC:1963:13::2
L   FF00::/8 [0/0]
     via Null0, receive
``` 

