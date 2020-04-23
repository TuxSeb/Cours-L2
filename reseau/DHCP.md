# DHCPv4 sur routeurs

> un serveur DHCP sert à allouer des adresses IP de manière dynamique au clients.

## a ajouter: relais DHCPv4 et config d'un routeur en tant que client dhcpv4

## 1. Exclure des adresses du pool

#### Mode: `enable` => `conf t`

| Commande                                                     | Effets                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ip dhcp excluded-address (`range1` `range2` | `adresse_ip`  ) | Permet d'exclure une range d'adresse ip **ou** une adresse ip en particulier |



## 2. Definir le nom du pool DHCP

####  Mode: `enable` => `conf t`

| Commande                   | Effets                         |
| -------------------------- | ------------------------------ |
| ip dhcp pool `nom_du_pool` | Nomme le pool en `nom_du_pool` |



## 3. Définir la plage d'adresses et le masque sous-réseau du POOL

#### en mode `dhcp-config` après avoir nommé le pool 

| Commande                                       | Effets                                   |
| ---------------------------------------------- | ---------------------------------------- |
| network `<adresse_ip>` `masque`                | défini la plage d'adresse avec le masque |
| default-routeur `<passerelle_par_défaut>`      | défini la paserelle par défaut du pool   |
| dns-server `<ip_serveur_dns>` (**facultatif**) | défini le serveur dns                    |
| domain-name example.com (**facultatif**)       | défini example.com comme nom de domaine  |
| end                                            |                                          |

## Etablir un relais DHCPv4 sur d'autres routeurs

> Un relais sert a faire en sorte que les autres routeurs partagent l'accès (la diffusion) au serveur DHCP a leur autres réseau. 

Dans le routeur, choisir une interface

#### Mode: `enable` =>`conf t` => choisir une interface 

| Commande                         | Effets                                                       |
| -------------------------------- | ------------------------------------------------------------ |
| ip help-address `<adresse_dhcp>` | Autorise la diffusion du serveur DHCP portant l'addresse `adresse_dhcp` |

### Exemple

![exemple](/home/sebastien/Cours-L2/reseau/images/exemple3.png)

#### Solution, aller dans R1 puis: 

![image-20200423215832142](/home/sebastien/Cours-L2/reseau/images/commandes_dhcp.png)

##  Configurer un routeur en tant que client DHCP

> Le routeur peut alors avoir une adresse IP attribuée par le serveur DHCP 

#### Mode: `enable` => `conf t` => interface qui obtiendra l'adresse ip via DHCP

| Commande        | Effets                                                       |
| --------------- | ------------------------------------------------------------ |
| ip address dhcp | Met l'interface sur le mode DHCP (elle aura donc une addresse attribuée par le serveur DHCP) |



## Autre: 

#### Vérification du DHCPv4

##### Mode: `enable`

| Commande                            | Effets |
| ----------------------------------- | ------ |
| show running-config \| section dhcp |        |
| show ip dhcp binding                |        |
| show ip dhcp server statistics      |        |

#### Vérification du relais DHCPv4 et des services DHCPv4

##### Mode: `enable`

| Commande                                                   | Effets                                                       |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| show running-config \| section interface `<nom_interface>` | affiche l'interface `<nom_interface>` et les propriétés, une ligne comportant *ip helper_address* devrait apparaitre avec l'ip sur serveur dhcp |
| show running-config \| include no service dhcp             |                                                              |



#### Les tâches de dépannage

| Tache | Objectif                                         |
| ----- | ------------------------------------------------ |
| **1** | Résoudre les conflits d'adresse                  |
| **2** | Vérifier la connectivité physique                |
| **3** | Tester avec une adresse IPv4 Statique            |
| **4** | Vérifier la configuration du port de commutateur |
| **5** | Vérifier à partir du même sous réseau ou VLAN    |

