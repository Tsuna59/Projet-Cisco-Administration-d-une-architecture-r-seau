README – Projet Cisco : Administration d’une architecture réseau
Fichier Packet Tracer : [version_finale_radius.pkt](Topologie/version_finale_radius.pkt)
Contexte
Ce projet a été réalisé dans le cadre du cours Administrez une architecture réseau avec Cisco
L’objectif était de concevoir, configurer et documenter une infrastructure réseau complète, intégrant routage, VLAN, sécurité et services.

Architecture globale
Le réseau est divisé en deux zones principales :

Area 0 : cœur du réseau, interconnexion des routeurs et du serveur FTP.

Area 1 : réseau local utilisateur, isolé par ACL pour bloquer le trafic indésirable (spammer HTTP).

L’ensemble est relié à un LAN multi-VLAN géré par un switch Cisco 2960, avec routage inter-VLAN via un routeur ISR.

Composants principaux
Élément	Rôle	Interfaces / IP	Particularités
Router1 (ISR431)	Routeur principal LAN	G0/0 : 223.0.0.1/24 G0/0/1 : 192.168.1.254	Routage inter-VLAN, EIGRP, version OSPF séparée
Router2	Routeur d’accès serveur	G0/0 : 223.0.2.2/24 G0/1 : 223.0.1.2/24 G0/2 : 223.0.0.2/24	Connecté au serveur FTP
Router3	Routeur Internet	G0/0 : 223.0.3.3/24	Point de sortie vers Internet
Router4	Routeur intermédiaire	G0/0 : 223.0.5.4/24 G0/1 : 223.0.1.4/24 G0/2 : 223.0.4.4/24	Relais entre zones
Switch 2960	Commutation LAN	Fa0/1–Fa0/5	VLAN2, VLAN3, VLAN99
Serveur FTP	Service réseau	223.0.2.8/24	Hébergé dans Area 0
Serveur Radius	Authentification	VLAN99	Gestion des accès
PC Clients / Admin	Utilisateurs finaux	VLAN2, VLAN3, VLAN99	ACL HTTP appliquée sur le spammer


VLANs configurés
VLAN	Description	Adresse passerelle
VLAN2	Serveurs et postes bureautiques	192.168.2.254
VLAN3	Clients utilisateurs	192.168.3.254
VLAN99	Administration 

Fonctionnalités implémentées
Routage dynamique EIGRP sur l’ensemble du backbone (Area 0).

Version séparée OSPF pour étude comparative du protocole.

Subinterfaces configurées pour le routage inter-VLAN.

Port forwarding pour accès distant au serveur FTP.

ACLs pour filtrer le trafic HTTP du spammer (blocage ciblé).

Serveur Radius pour authentification centralisée.

Séparation logique des domaines de diffusion via VLANs.

Sécurité
ACL bloquant le spammer sur le port HTTP (80).

VLAN d’administration isolé (VLAN99).

Authentification Radius pour les accès réseau.

Interfaces passives configurées pour limiter les échanges inutiles.

Objectifs pédagogiques
Maîtriser la configuration Cisco IOS (routeurs et switches).

Comprendre la segmentation réseau (VLAN / ACL).

Implémenter et comparer les protocoles de routage EIGRP et OSPF.

Documenter et versionner les configurations pour un suivi professionnel.
