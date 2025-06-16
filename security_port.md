Sur tous les switchs d'accès.  
L'idée est de sécuriter les ports d'accès où tous les users pouraient se brancher.  
Pour cela je configure le port-security sur tous les ports en mdoe accès des switcha d'accès.  
Cela à pour effet de enregistrer la dernière adresse mac connectée, On autorise un seul MAC par port, En cas de violation, le port se met en err-disabled  
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