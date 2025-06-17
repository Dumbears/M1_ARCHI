# Route R3 IPV6
```bash
R3#show ipv6 route
IPv6 Routing Table - 13 entries
Codes: C - Connected, L - Local, S - Static, R - RIP, B - BGP
       U - Per-user Static route, M - MIPv6
       I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea, IS - ISIS summary
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF intra, OI - OSPF inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2
       D - EIGRP, EX - EIGRP external
R   2001:DB8:A::/64 [120/2]
     via FE80::210:11FF:FEC5:CB02, GigabitEthernet0/1
R   2001:DB8:B::/64 [120/3]
     via FE80::210:11FF:FEC5:CB02, GigabitEthernet0/1
     via FE80::20C:CFFF:FE64:DACD, GigabitEthernet0/0
R   2001:DB8:C::/64 [120/2]
     via FE80::207:ECFF:FEC9:6251, GigabitEthernet0/2
R   2001:DB8:12::/64 [120/2]
     via FE80::210:11FF:FEC5:CB02, GigabitEthernet0/1
C   2001:DB8:13::/64 [0/0]
     via GigabitEthernet0/1, directly connected
L   2001:DB8:13::3/128 [0/0]
     via GigabitEthernet0/1, receive
R   2001:DB8:24::/64 [120/2]
```