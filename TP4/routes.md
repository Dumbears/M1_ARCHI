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