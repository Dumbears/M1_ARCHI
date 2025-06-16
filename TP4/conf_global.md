Configuration des Routeurs  
Sur R1
```bash
interface gigabitEthernet0/0
 description Vers LAN1 (Switch0)
 ipv6 address fda3:92dc:1963:1::1/64
 ipv6 address fe80::1 link-local
 ipv6 enable
 no shutdown
exit

interface gigabitEthernet0/1
 description Vers R2
 ipv6 address fda3:92dc:1963:12::1/64
 ipv6 address fe80::2 link-local
 ipv6 enable
 no shutdown
exit

interface gigabitEthernet0/2
 description Vers R3
 ipv6 address fda3:92dc:1963:13::1/64
 ipv6 address fe80::3 link-local
 ipv6 enable
 no shutdown
 exit
 exit
 write memory
```

Sur R2
```bash
interface gigabitEthernet0/0
 description Vers LAN2 (Switch1)
 ipv6 address fda3:92dc:1963:3::1/64
 ipv6 address fe80::1 link-local
 ipv6 enable
 no shutdown
 exit

interface gigabitEthernet0/1
 description Vers R1
 ipv6 address fda3:92dc:1963:12::2/64
 ipv6 address fe80::2 link-local
 ipv6 enable
 no shutdown
 exit

interface gigabitEthernet0/2
 description Vers R3
 ipv6 address fda3:92dc:1963:23::1/64
 ipv6 address fe80::3 link-local
 ipv6 enable
 no shutdown
 exit
 exit
 write memory
```

Sur R3
```bash
interface gigabitEthernet0/1
 description Vers R1
 ipv6 address fda3:92dc:1963:13::2/64
 ipv6 address fe80::1 link-local
 ipv6 enable
 no shutdown
 exit

interface gigabitEthernet0/2
 description Vers R2
 ipv6 address fda3:92dc:1963:23::2/64
 ipv6 address fe80::2 link-local
 ipv6 enable
 no shutdown
 exit
 exit
 write memory
```

Sur les 3 routeurs
```bash
show ipv6 interface brief
```
Voici la sortie de R1
```bash
Router1#show ipv6 interface brief
GigabitEthernet0/0         [up/up]
    FE80::1
    FDA3:92DC:1963:1::1
GigabitEthernet0/1         [up/up]
    FE80::2
    FDA3:92DC:1963:12::1
GigabitEthernet0/2         [up/up]
    FE80::3
    FDA3:92DC:1963:13::1
```
Configurations des PCs  
PC0 (LAN1)
```bash
ipv6 address fda3:92dc:1963:1::10/64
ipv6 gateway fda3:92dc:1963:1::1
```
PC1 (LAN1)
```bash
ipv6 address fda3:92dc:1963:1::11/64
ipv6 gateway fda3:92dc:1963:1::1
```
PC2 (LAN2)
```bash
ipv6 address fda3:92dc:1963:3::10/64
ipv6 gateway fda3:92dc:1963:3::1
```
PC3 (LAN2)
```bash
ipv6 address fda3:92dc:1963:3::11/64
ipv6 gateway fda3:92dc:1963:3::1
```