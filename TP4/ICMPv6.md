ICMPv6 est configuré par défaut. On peut voir le résultat en effectant la commande suivante sur les routers
```bash
show ipv6 neighbors
```
La sortie  de R1
```bash
Router1#show ipv6 neighbors
IPv6 Address                              Age Link-layer Addr State Interface
FDA3:92DC:1963:1::10                       26 0001.64A6.8725  REACH Gig0/0
FDA3:92DC:1963:1::11                       26 00D0.FFD4.6B38  REACH Gig0/0
FDA3:92DC:1963:12::2                       14 0001.968D.1E84  REACH Gig0/1
FDA3:92DC:1963:13::2                       18 0002.179B.127D  REACH Gig0/2
```
La sortie  de R2
```bash
Router#show ipv6 neighbors
IPv6 Address                              Age Link-layer Addr State Interface
FDA3:92DC:1963:3::10                       13 0001.630B.E10A  REACH Gig0/0
FDA3:92DC:1963:12::1                       16 0001.6311.8502  REACH Gig0/1
FDA3:92DC:1963:23::2                       15 0003.E479.52EE  REACH Gig0/2
```
La sortie de R3
```bash
Router#show ipv6 neighbors
IPv6 Address                              Age Link-layer Addr State Interface
FDA3:92DC:1963:13::1                       20 0001.6311.8503  REACH Gig0/1
FDA3:92DC:1963:23::1                       16 0090.2BA2.8E94  REACH Gig0/2
```