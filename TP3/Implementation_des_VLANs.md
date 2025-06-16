☑️ Créer 5 VLANS

Sur tous les switchs
```bash
enable
configure terminal

vlan 10
 name Marketing
vlan 20
 name Developpement
vlan 30
 name IT
vlan 40
 name RH
vlan 50
 name Administration
exit
exit
write memory
```
☑️ Configurer les ports.
Je conf les différents ports des différents switchs. Certains seront en trunk car plusieurs vlan à faire passer et d'autres en accès, typiquement les switchs d'accès.

S0
```bash
S0
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/21
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/22
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
```

S1
```bash
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/21
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/22
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
```

S2
```bash
interface fa0/21
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/20
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
```

S3
```bash
interface fa0/21
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/20
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
```

S4
```bash
interface fa0/22
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/3
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
```

S5
```bash
interface fa0/22
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/3
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
```

S6
```bash
interface fa0/10
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/11
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 10
exit
```

S7
```bash
interface fa0/10
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/11
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/3
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 20
exit
interface range fa0/12 - 14
 switchport mode access
 switchport access vlan 50
exit
interface range fa0/4 - 9
 switchport mode access
 switchport access vlan 50
exit
```

S8
```bash
interface fa0/10
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/11
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/3
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface range fa0/1 - 2
 switchport mode trunk
 switchport trunk allowed vlan 30,40
exit
interface range fa0/12 - 14
 switchport mode access
 switchport access vlan 50
exit
interface range fa0/4 - 9
 switchport mode access
 switchport access vlan 50
exit
```

S9
```bash
interface fa0/10
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface fa0/11
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50
exit
interface range fa0/1 - 2
 switchport mode access
 switchport access vlan 50
exit
```