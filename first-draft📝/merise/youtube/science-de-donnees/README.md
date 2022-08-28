# Merise

![first slide](./one.png)

- MDC: modèle conceptuel de données
- MLD: modele logique de données
- BDD: base de donnees

Merise = Methode d'Etude et de Realisation Informatique pour les Systemes d'Entreprise
(1979)

![two](./two.png)

![three](./three.png)

![four](./four.png)

decrit les acteurs du systeme(personnes ou objects), leur caracteristique ainsi que leur interactions

on en cree un schema Entites-Association constitué:

- Entites
- Associations
- Proprietes
- Identifiants
- Cardinalites

![Entites](./Entites.png)

![association](./association.png)

![attribut](./attribut.png)

attribut d'association

![attribut](./attribut.png)

![cardinalite](./cardinalite.png)

les quatres type de cardinalites

![cardinalites list](./cardinalites-list.png)

(0,1) -> jamais plus d'une fois (INJECTIF)
(1,1) bijectif
(1,N) -> surjectif
(0,N) -> idk, zero ou plusieures fois

## graphiquement

![graphiquement un](./graphiquement-un.png)

PAS OUF

![graphiquement deux](./graphiquement-deux.png)

cardinalties graphiquement

![graphiquement-trois](./graphiquement-trois.png)

## Etapes MCD

![etapes-mcd](./etapes-mcd.png)

## MLD

- Tables
- Cle primaires
- Cle etrangeres (relation entre tables), son nom fait reference au fait que souvent cette cle est une cle primaire d'une autre table stocker dans la notre

### rule 1

![mcd-mld](./mcd-mld.png)

pour la deuxieme regle on voit emerge les tables de jointures

### rule 2

![rule-two](./rule-two.png)

cote X-1 on stocke, la cle etrangere ce qui est logique, car l'inverse serait impossible. On garde donc une table avec X+1 proprietes, champ

![example-rule-two](./example-rule-two.png)

### rule 3

table de jointure

![rule-three](./rule-three.png)

![example-rule-tree-1](./example-rule-tree-1.png)

### rule 4

un cityoen peut devenir un candidate, mais ce n'est pas obligatoire
chaque candidat est un citoyen

![rule4](./rule4.png)

## Exercise

MCD

![exercise](./exercise.png)
