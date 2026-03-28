# LAB VTP CHAOS — Simulation catastrophe

## Objectif
- Comprendre le danger du revision number
- Observer la destruction des VLANs

---

## Topologie

        SW1 (SERVER)
        /          \
   SW2 (CLIENT)  SW3 (CLIENT)
          |
        SW4 (DANGER)

---

## CONFIG SW4 (SWITCH DANGEREUX)

enable
configure terminal

hostname SW4

vtp domain LAB
vtp password 1234
vtp mode server

---

## SIMULER UN REVISION NUMBER ÉLEVÉ

# Répéter plusieurs fois:
vlan 100
no vlan 100

vlan 200
no vlan 200

Cela augmente le revision number

---

## CONNECTER SW4

# SW4 ↔ SW1

SW4:
interface fa0/1
switchport mode trunk

SW1:
interface fa0/3
switchport mode trunk

---

## OBSERVATION

Sur SW2 / SW3:

show vlan brief

Résultat attendu:
VLAN 10, 20, 30 DISPARAISSENT

---

## EXPLICATION

- SW4 a un revision number plus élevé
- Il envoie une base VLAN vide
- Tous les switches acceptent

réseau détruit

---

## RÉPARATION

Sur SW1:

vtp mode transparent
vtp mode server

# recréer VLAN si nécessaire

---

## BONNES PRATIQUES

- delete vlan.dat avant ajout switch
- utiliser vtp transparent
- vérifier:

show vtp status

---

## Résultat
- compréhension du risque réel VTP
- simulation d’un incident production