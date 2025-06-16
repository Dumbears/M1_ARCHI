Sur R1
```bash
conf t
interface gigabitEthernet0/0
 description Vers LAN1 - Dual Stack
 ip address 192.168.1.1 255.255.255.0
 ipv6 address fda3:92dc:1963:1::1/64
 ipv6 enable
 no shutdown
exit
```

Sur PC0  
IP : 192.168.1.1  
Masque : 255.255.255.0  
Gateway : 192.168.1.1  

Sur PC1  
IP : 192.168.1.3  
Masque : 255.255.255.0  
Gateway : 192.168.1.1  

Test de ping PC3 depuis PC0  
```bash
C:\>ping 192.168.1.3

Pinging 192.168.1.3 with 32 bytes of data:

Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.3: bytes=32 time<1ms TTL=128
Reply from 192.168.1.3: bytes=32 time=6ms TTL=128

Ping statistics for 192.168.1.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 6ms, Average = 1ms
```