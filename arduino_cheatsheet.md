# Arduino cheat sheet

#PAS FINI

## Les Ports Atmega328

Les ports sur arduino sont divisés en 3 registres: 
- le registre B (8 bits)
- le registre C (7 bits)
- Le registre D (8 bits)

pour un total de 23 entrées/sortie sur l'Atmega328

Chaque bit de ces registres peut être mis à 1 (position "Sortie") ou à 0 (position "Entree") 

### DDRX

Defini le role du port:
1 -> Sortie 
0 -> Entree

exemples:
```cpp
DDRB |= B10000000
```

### PORTX

Permet d'écrire sur un port 

### PINX

Permet de lire un port

### Les résistances internet "PullUp"

Chaque port possède une résistance de sécurité dites "PullUp"

*Pour l'activer*: il faut passer le port en entrée et ecrire la valeur 1 dans ce port

*Pour desactiver*: 

## Les interruptions

**Interruption (IT)**: Suspension du programme en cours pour exécuter un traitement particulier.

Les interruptions peuvent être déclanchés par un évènement exterieur soit par une détection avec des capteurs, soit par un périphérique

### Le registre EICRA

Le registre EICRA sert à choisir la cause de l'interruption, il est défini sur **8 bits**

| | |
|-|-|
| | |

Pour l'interuption n°1, notée INT0, il faut programmer 

|  ISC01  | ISC00  |        Description         |
|---------|--------|----------------------------|
|    0    |   0    | Le niveau bas de INTx génère un requette d'interruption          |
|    0    |   1    |                            | 
|    1    |   0    |                            |
|    1    |   1    |                            |
