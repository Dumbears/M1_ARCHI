## Réflexion sur les différences entre la configuration IPv4 et IPv6

La configuration d’IPv4 et d’IPv6 présente plusieurs différences :

- **Notation des adresses :**  
  Les adresses IPv4 utilisent une notation décimale avec 4 octets (ex. : `192.168.1.1`), Lles adresses IPv6 utilisent une notation hexadécimale sur 128 bits (ex. : `fda3:92dc:1963:1::1`).
  C'est plus complexe à lire et à saisir manuellement...

- **Configuration manuelle vs automatique :**  
  En IPv4, on configure souvent manuellement ou via DHCP.
  En IPv6,les hôtes peuvent "s’auto-configurer" grâce au protocole **ICMPv6** (sans serveru dhcp ipv6.

- **Gestion des sous-réseaux :**  
  Le découpage des réseaux IPv6 à un espace d’adressage bien plus grand que l'ipv4.
  Les préfixes `/64` sont standard.

- **Routage :**  
  Le routage IPv6 demande faire attention aux **link-local addresses (`fe80::/10`)** pour les communications entre routeurs. Ces adresses n’existent pas en IPv4.

- **Diagnostics :**  
  Les commandes restent similaires,faut juste adapter: `ping6` ou `ping -6` pour IPv6 dans certains systèmes. Sur Cisco packet tracer un `ping` fonctionne très bien.

---

Je trouve  que IPV6 est pas forcément plus complexe à configurer que l'IPV4, la notation de l'IPV6 rebute un peut au début mais je pense que c'est surtout une question d'habitude.
