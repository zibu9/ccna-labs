# 🔧 LAB VTP NORMAL — Packet Tracer

## Objectif
- Configurer VTP (Server / Client)
- Propagation automatique des VLANs

---

## Topologie
SW1 (SERVER)
├── SW2 (CLIENT)
└── SW3 (CLIENT)

---

## CONFIGURATION DE BASE (TOUS LES SWITCHES)

enable
configure terminal

vtp domain LAB
vtp password 1234

---

## SW1 (SERVER)

hostname SW1
vtp mode server

---

## SW2 (CLIENT)

hostname SW2
vtp mode client

---

## SW3 (CLIENT)

hostname SW3
vtp mode client

---

## CONFIGURATION TRUNK

# SW1 SW2
SW1:
interface fa0/1
switchport mode trunk

SW2:
interface fa0/1
switchport mode trunk

# SW1 SW3
SW1:
interface fa0/2
switchport mode trunk

SW3:
interface fa0/1
switchport mode trunk

---

## CRÉATION VLAN (UNIQUEMENT SUR SW1)

SW1:

vlan 10
name RH

vlan 20
name IT

vlan 30
name GUEST

---

## VÉRIFICATION

Sur SW2 / SW3:

show vlan brief

Résultat attendu:
VLAN 10, 20, 30 visibles

---

## DEBUG

show vtp status
show interfaces trunk

---

## Résultat
- VLANs propagés automatiquement
- VTP fonctionnel