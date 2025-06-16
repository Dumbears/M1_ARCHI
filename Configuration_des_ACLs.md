S0
```bash
enable
configure terminal

spanning-tree mode mst
```
! Configuration MST
```bash
spanning-tree mst configuration
 name MST-YNOV
 revision 1

 instance 1 vlan 10,30
 instance 2 vlan 40,50
 instance 3 vlan 20
exit
```

! Choisir le root bridge pour chaque instance (exemple : S0 est root pour instance 1 et 3)
```bash
spanning-tree mst 1 priority 4096
spanning-tree mst 3 priority 4096
spanning-tree mst 2 priority 8192
```

S1
```bash
enable
configure terminal

spanning-tree mode mst

spanning-tree mst configuration
 name MST-YNOV
 revision 1

 instance 1 vlan 10,30
 instance 2 vlan 40,50
 instance 3 vlan 20
exit
```

! Ici on inverse les rôles : S1 est root pour instance 2
```bash
spanning-tree mst 1 priority 8192
spanning-tree mst 2 priority 4096
spanning-tree mst 3 priority 8192
```


Autres switchs
```bash
enable
configure terminal

spanning-tree mode mst

spanning-tree mst configuration
 name MST-YNOV
 revision 1

 instance 1 vlan 10,30
 instance 2 vlan 40,50
 instance 3 vlan 20
exit
```

Sur tous les switchs pour vérifier que la conf est OK
show spanning-tree mst configuration
show spanning-tree mst


Ci-dessous la configuration des ACLs, l'idée est d'appliquer le moindre privilège. J'ai autorisé que ce qui a été demandé dans le TP, le reste est deny.
S0

```bash
enable
configure terminal

! Active le routage inter-VLAN
ip routing

! VLAN 10 - Développement
interface vlan 10
 ip address 10.0.10.1 255.255.255.224
 no shutdown

! VLAN 20 - IT
interface vlan 20
 ip address 10.0.20.1 255.255.255.240
 no shutdown

! VLAN 30 - Marketing
interface vlan 30
 ip address 10.0.30.1 255.255.255.240
 no shutdown

! VLAN 40 - RH
interface vlan 40
 ip address 10.0.40.1 255.255.255.240
 no shutdown

! VLAN 50 - Administration
interface vlan 50
 ip address 10.0.50.1 255.255.255.240
 no shutdown

 S1
 enable
configure terminal

ip routing

! VLAN 10 - Développement
interface vlan 10
 ip address 10.0.10.2 255.255.255.224
 no shutdown

! VLAN 20 - IT
interface vlan 20
 ip address 10.0.20.2 255.255.255.240
 no shutdown

! VLAN 30 - Marketing
interface vlan 30
 ip address 10.0.30.2 255.255.255.240
 no shutdown

! VLAN 40 - RH
interface vlan 40
 ip address 10.0.40.2 255.255.255.240
 no shutdown

! VLAN 50 - Administration
interface vlan 50
 ip address 10.0.50.2 255.255.255.240
 no shutdown
```

🔐 ACL pour VLAN IT (interface vlan 20) — accès total
enable
```bash
conf terminal
ip access-list extended IT-ACL
 permit ip 10.0.20.0 0.0.0.15 any
 deny ip any any
!
interface vlan 20
 ip access-group IT-ACL in
exit
exit
write memory
```

 🔐 ACL pour VLAN RH (interface vlan 40) — accès uniquement à son serveur
```bash
enable
conf terminal
 ip access-list extended RH-ACL
 permit ip 10.0.40.0 0.0.0.15 host 10.0.20.10
 deny ip any any
!
interface vlan 40
 ip access-group RH-ACL in
exit
exit
write memory
```

🔐 ACL pour VLAN Développement (interface vlan 10) — accès à ses serveurs + entre eux
```bash
enable
conf terminal
ip access-list extended DEV-ACL
 remark Autoriser intra-VLAN Développement
 permit ip 10.0.10.0 0.0.0.31 10.0.10.0 0.0.0.31

 remark Autoriser vers les 3 serveurs dans IT
 permit ip 10.0.10.0 0.0.0.31 host 10.0.20.11
 permit ip 10.0.10.0 0.0.0.31 host 10.0.20.12
 permit ip 10.0.10.0 0.0.0.31 host 10.0.20.13

 deny ip any any
!
interface vlan 10
 ip access-group DEV-ACL in
exit
exit
write memory
```




 🔐 ACL pour VLAN Marketing (interface vlan 30) — accès à Internet uniquement
```bash
enable
conf terminal
ip access-list extended MKTG-ACL
 deny ip 10.0.30.0 0.0.0.15 10.0.0.0 0.0.255.255
 permit ip any any
!
interface vlan 30
 ip access-group MKTG-ACL in
exit
exit
write memory
```



🔐 ACL pour VLAN Administration (interface vlan 50) — même logique que Marketing
```bash
enable
conf terminal
ip access-list extended ADMIN-ACL
 deny ip 10.0.50.0 0.0.0.15 10.0.0.0 0.0.255.255
 permit ip any any
!
interface vlan 50
 ip access-group ADMIN-ACL in
exit
exit
write memory
```