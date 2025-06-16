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

Sur tous les switchs pour vérifier la configuration
```bash
show spanning-tree mst configuration
show spanning-tree mst
```
