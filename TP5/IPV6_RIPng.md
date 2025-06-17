
R1
```bash
conf t
hostname R1
ipv6 unicast-routing

interface Gig0/0
 description Link to R2
 ipv6 address 2001:db8:12::1/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/1
 description Link to R3
 ipv6 address 2001:db8:13::1/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/2
 description LAN1
 ipv6 address 2001:db8:A::1/64
 ipv6 rip RIPng enable
 no shutdown
exit
exit
write memory
```

R2
```bash
conf t
hostname R2
ipv6 unicast-routing

interface Gig0/0
 description Link to R1
 ipv6 address 2001:db8:12::2/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/1
 description Link to R4
 ipv6 address 2001:db8:24::2/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/2
 description LAN2
 ipv6 address 2001:db8:B::1/64
 ipv6 rip RIPng enable
 no shutdown
exit
exit
write memory
```

R3
```bash
conf t
hostname R3
ipv6 unicast-routing

interface Gig0/0
 description Link to R4
 ipv6 address 2001:db8:34::3/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/1
 description Link to R1
 ipv6 address 2001:db8:13::3/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/2
 description Link to R5
 ipv6 address 2001:db8:35::3/64
 ipv6 rip RIPng enable
 no shutdown
exit
exit
write memory
```

R4
```bash
conf t
hostname R4
ipv6 unicast-routing

interface Gig0/0
 description Link to R3
 ipv6 address 2001:db8:34::4/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/1
 description Link to R2
 ipv6 address 2001:db8:24::4/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/2
 description Link to R5
 ipv6 address 2001:db8:45::4/64
 ipv6 rip RIPng enable
 no shutdown
exit
exit
write memory
```

R5
```bash
conf t
hostname R5
ipv6 unicast-routing

interface Gig0/0
 description Link to R3
 ipv6 address 2001:db8:35::5/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/2
 description Link to R4
 ipv6 address 2001:db8:45::5/64
 ipv6 rip RIPng enable
 no shutdown

interface Gig0/1
 description LAN3
 ipv6 address 2001:db8:C::1/64
 ipv6 rip RIPng enable
 no shutdown
exit
exit
write memory
```

# Vérifier les tables de routage
Au début j'ai fais un ping entre le LAN1 et LAN3 mais ça communiquait pas.
J'ai du faire un ping de R1 à R3 pour que la table de routage se créer.
RIPng étant un protocole à convergence lente.

Commande pour vérifier que RIPng est bien activé
```bash
show ipv6 rip database 
```
Sortie de la commande sur R1
```bash
R1#show ipv6 rip database 
RIP process "RIPng" local RIB 
 2001:DB8:C::/64, metric 3, installed
    GigabitEthernet0/1/FE80::240:BFF:FEE0:4CDB, expires in 178 sec
 2001:DB8:12::/64, metric 2
    GigabitEthernet0/0/FE80::203:E4FF:FEC2:C7D8, expires in 159 sec
 2001:DB8:13::/64, metric 2
    GigabitEthernet0/1/FE80::240:BFF:FEE0:4CDB, expires in 178 sec
 2001:DB8:24::/64, metric 2, installed
    GigabitEthernet0/0/FE80::203:E4FF:FEC2:C7D8, expires in 159 sec
 2001:DB8:34::/64, metric 2, installed
    GigabitEthernet0/1/FE80::240:BFF:FEE0:4CDB, expires in 178 sec
 2001:DB8:35::/64, metric 2, installed
    GigabitEthernet0/1/FE80::240:BFF:FEE0:4CDB, expires in 178 sec
 2001:DB8:45::/64, metric 3, installed
    GigabitEthernet0/1/FE80::240:BFF:FEE0:4CDB, expires in 178 sec
 2001:DB8:45::/64, metric 3, installed
    GigabitEthernet0/1/FE80::240:BFF:FEE0:4CDB, expires in 178 sec3, installed
    GigabitEthernet0/0/FE80::203:E4FF:FEC2:C7D8, expires in 159 sec
```
