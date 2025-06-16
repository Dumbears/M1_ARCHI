# Rapport de configuration – Sécurisation du réseau d'accès

## Plan d'adressage

Un plan d'adressage basé sur **VLSM** a été mis en place pour :

- Limiter le gaspillage d'adresses IP ;
- Garder la **possibilité d’évolution** des sous-réseaux si nécessaire ;
- Faciliter l’application de politiques de sécurité par sous-réseau.

---

## ACLs – Principe du moindre privilège

Les ACLs ont été conçues selon le principe de **moindre privilège**, c’est-à-dire :

- Tout trafic est **bloqué par défaut** ;
- Seuls les flux **explicitement autorisés** sont permis ;
- Cela permet de **limiter les communications** au strict nécessaire, réduisant ainsi la surface d’attaque du réseau.

---

## Sécurisation des ports d’accès (Port Security)

Afin de sécuriser les ports où les utilisateurs peuvent potentiellement se brancher (salles, bureaux, etc.), une **sécurité par port** a été appliquée **sur tous les ports en mode access des switches d’accès**.

### Configuration mise en œuvre :
- Activation de `port-security` sur chaque port access ;
- Limitation à **1 seule adresse MAC autorisée** par port ;
- Enregistrement automatique de la **première adresse MAC connectée** (`mac-address sticky`) ;
- En cas de violation (autre MAC détectée), le port passe en état **err-disabled** (bloqué automatiquement).

### Objectif :

- **Empêcher le branchement de plusieurs appareils** sur un même port (ex : switch pirate) ;
- **Bloquer l'accès aux appareils non autorisés** ;
- **Renforcer la sécurité physique** du réseau en limitant les connexions non légitimes.

---

## Conclusion

Cette configuration réseau garantit un **bon équilibre entre sécurité, organisation et évolutivité**.  
Les mesures mises en place permettent de :

- Contrôler rigoureusement les flux réseau (ACL) ;
- Optimiser l'utilisation des IPs (VLSM) ;
- Sécuriser l’infrastructure physique (port-security sur switches d’accès).

