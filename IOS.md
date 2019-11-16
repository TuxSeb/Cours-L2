# Ios Réseau

## Commandes

#### Différent niveau d'administration

| **Niveau** | Mode             | Affichage              | Commande utilisé    |
| ---------- | ---------------- | ---------------------- |--------------------|
| 1          | User EXEC        | `Device>`              |                    |
| 2          | Privileged Exec  | `Device#`              |enable              |
| 3          | Global Config    | `Device(config)#`      |config-terminal (config-t)|
| 4a         | Interface Config | `Device(config-if)#`   |interface [vlan1 par exemple]|
| 4b         | Line Config      | `Device(config-line)#` |line console [nb]    |

(`Device` est remplacé par le nom de l'hôte donné)

#### Commandes générales

| raccourcis | commande complète                             | fonction                                   |
| ---------- | --------------------------------------------- | ------------------------------------------ |
| `en`       | `enable`                                      | user EXEC (1) => priv. EXEC (2)            |
| `conf t`   | `config terminal`                             | priv. EXEC (2) => Global Config (3)        |
| `int`      | `interface`(mieux vaut utiliser `int vlan 1`) | Global Config (3) => Interface Config (4a) |
| `li`       | `line` (mieux vaut utiliser `line console 0`) | Global Config (3) => Line Config (4b)      |



#### Modifier/visualiser running-config et le sauvegarder/supprimer 

| Raccourcis     | Commande complète                    | fonction                                                   |
| -------------- | ------------------------------------ | ---------------------------------------------------------- |
| `sh run`       | `show running-config`                | affiche la configuration actuelle (RAM)                    |
| `cop r s`      | `copy running-config startup-config` | Sauvegarde la configuration actuelle dans la mémoire flash |
| `era star`     | `erase startup-config`               | supprimer la configuration en mémoire flash                |
| `del vlan.dat` | `delete vlan.dat`                    | supprimer la table vlan                                    |



#### Configuration initiale (switch et routeurs)

| Commande                   | Depuis le Mode        | Ce que ça fait                                               |
| -------------------------- | --------------------- | ------------------------------------------------------------ |
| `hostname xyz`             | Global config (3)     | Défini le nom de l'hôte sur `xyz`                            |
| `enable secret xyz`        | Global config (3)     | Encrypte le mdp de priv. EXEC                                |
| `service password-encrypt` | Global config (3)     | Encrypte tous les mdp                                        |
| `line console 0`           | Global config (3)     | Entre en mode line config pour console                       |
| `line vty 0 15`            | Global config (3)     | entre en mode **Line config** pour 16 lignes vty             |
| `password le_mdp`          | Line config (4b)      | Défini le mot de passe de line sur `le_mdp`                  |
| `int vlan 1`               | Global Config (3)     | entre dans l'interface de configuration (**Interface config**) du vlan 1 |
| `ip address [ip] [masque]` | Interface config (4a) | Défini l'adresse IP                                          |
| `no shut`                  | Interface config (4a) | Allume l'interface                                           |
| `banner motd "text"`       | Global config (3)     | Défini le motd                                               |



### Commandes spécifiques au routeur

| Commande               | Depuis le mode       | Fonction                                                     |
| ---------------------- | -------------------- | ------------------------------------------------------------ |
| `interface g0/1`       | Global Config(3)     | entre dans l'interface de configuration pour Gigabit Ethernet 0/1 |
| `ip address IP/prefix` | Interface config(4a) | défini l'adresse IPv4 de l'interface                         |
| `no shut`              | Interface config(4a) | Allume l'interface                                           |
|                        |                      |                                                              |



### Les affichages

| Commande                  | Information affichée                                         |
| ------------------------- | ------------------------------------------------------------ |
| `show version`            | version de IOS, capacité mémoire etc                         |
| `show mac address-table`  | affichage de la table des adresses MAC                       |
| `show ip route`           | affichage de la table d'adressage                            |
| `show interface g0/0`     | affichage du status, de l'addresse MAC, de l'IP,... de l'interface Gigabit ethernet 0/0 |
| `show ip interface brief` | affichage du nom, de l'addresse ip, du status, etc de toutes les interfaces |



### Raccourcis clavier

| Commande         | effet                                                        |
| ---------------- | ------------------------------------------------------------ |
| Ctrl + shift + 6 | Stop, peu importe ce que ce qui est en cours                 |
| Ctrl + C         | Sort du mode de configuration                                |
| Ctrl + Z         | Applique la commande actuelle et retourne vers le mode priv. EXEC |
| Ctrl + U         | Supprime le contenu du prompt                                |
| Tab              | Autocomplétions                                              |



## Exemple

#### Définir une adresse IP



#### Exemple de configuration de base
| Commande         | effet                                                        |
| ---------------- | ------------------------------------------------------------ |
|`enable`    |                              |
|`config-t`      |                               |
|`hostname S1`       |attribue le nom S1 à l'hôte                               |
|`enable password class`|attribue le mot de passe class au mode enable|
|`line console 0`|permet de modifier les paramètres du port console|
|`password cisco`|met le mdp cisco au port console|
|`no ip domain-lookup`|désactive la recherche auto dns|
|`login`| oblige la connexion via le mdp|
|`exit`|quitte le config console|
|`line vty 0 5`|config vty|
|`password cisco`|met le mdp cisco au vty|
|`login`| oblige la connexion via le mdp|
|`exit`|quitte vty|
|`banner motd 'Warning' `|Affiche warning a la connexion|
|`service password encryption`|encrypte les mdp|
|`interface g0/0`|config le port g0/0|
| `ipv6 address 2001:DB8:ACAD::1/64`| Attribue l'adresse ipv6 au port g0/0|
|`no shutdown`||
|`exit`||
|`interface s0/0/1`||
| `ipv6 address 2001:DB8:ACAD:2::1/64`| Attribue l'adresse ipv6 au port s0/0/1|
| `ipv4 address 172.16.1.12 255.255.255.252`| Attribue l'adresse ipv4 au port s0/0/1|
|`no shutdown`||
|`end`||
|`copy running-config startup-config`| sauvegarde la configuration du running dans la mémoire du startup|
|`show running-config`||
