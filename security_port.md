Sur tous les switchs d'accès
```bash
enable
configure terminal
interface range FastEthernet0/1 - 48
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 switchport port-security mac-address sticky
exit
end
write memory
```