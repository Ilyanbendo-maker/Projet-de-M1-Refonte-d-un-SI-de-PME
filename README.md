# [Projet P@8 Sécurité — Refonte d'un SI de PME](./sujet_Projet_securite_v3.0b.pdf)

> ⚠️ **Projet en cours.**



## Contexte

Projet du module **P@8 Sécurité** (M1, Efrei Paris), réalisé par une équipe de 8 étudiants.

Scénario : une PME victime d'un grave incident de sécurité a perdu l'intégralité de son SI et nous mandate, en tant qu'ingénieurs SSII, pour le reconstruire intégralement. Contraintes : solutions libres et gratuites en priorité, versions stables, montée en charge jusqu'à 1000 utilisateurs simultanés, conformité légale.

[sujet ici](./sujet_Projet_securite_v3.0b.pdf)
---

## Architecture

![Schéma réseau](./schéma_réseau.jpg) 

**Choix structurels :**

- **DMZ en sandwich** entre deux pare-feu de marques différentes (pfSense / OPNsense) => défense en profondeur, pas de point unique de compromission lié à une CVE éditeur
- **DMZ segmentée en 4 sous-zones** (INBOUND, OUTBOUND, Mail, VPN) => cloisonnement des flux entrants/sortants et des services en fonction de leur exposition
- **VLAN dédiés par fonction** côté LAN => application stricte du principe de moindre privilège réseau
- **Bastion** comme unique point d'entrée pour l'administration pour une meilleur traçabilité.

---

## Stack technique

### Choix actés

| Brique | Technologie |
|---|---|
| Hyperviseur | VMware ESXi 8.0 U2 |
| Firewall externe | pfSense 2.8 |
| Firewall interne | OPNsense |
| Annuaire | Windows Server 2019 (AD DS + RODC) |
| OS Linux général | Fedora Server |
| OS messagerie / extranet | Fedora *(imposé)* |
| OS DNS public | Debian ou FreeBSD *(imposé)* |
| ERP | Odoo (GPL) |
| Bastion | Apache Guacamole |
| SIEM | Graylog |
| EPP / EDR | ESET (licence obtenue en les ayant contactés)|
| Sauvegarde | Veeam |
| VPN client to site | OpenVPN  pour site to site avec la succursale |
| VPN site to site avec la succursale| Wireguard ou ipsec (pas encore décidé) |
| Gestion de parc | OCS Inventory + et/ou Ansible |
| Mises à jour Windows | WSUS |
| Automatisation Linux | Ansible |
| MFA + SSO DMZ | Keycloak |

### À valider

| Brique | Pistes |
|---|---|
| Proxy + filtrage URL | Squid + e2guardian |
| Reverse proxy + WAF | Nginx + ModSecurity / HAProxy |
| MTA / MDA | Postfix + Dovecot |

---

## Avancement

### Livrables

- [x] Schéma d'infrastructure *(30 avril)*
- [ ] Analyse de risques *(18 mai)*
- [ ] Service minimum opérationnel *(31 mai)*
- [ ] Document d'architecture *(15 juin)*
- [ ] Fiches réflexes administrateur *(15 juin)*
- [ ] Matrice RACI *(29 juin)*
- [ ] Pricing externalisation messagerie + addendum risques *(soutenance)*
- [ ] Analyse coûts + impact environnemental *(soutenance)*
- [ ] Soutenance finale
