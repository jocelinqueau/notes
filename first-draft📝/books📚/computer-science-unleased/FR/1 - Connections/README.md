# Connections'

> C'est un systeme entierement distribué, il n'y a aucun controle central. La seule raison que cela marche c'est parce que tout le monde a utiliser les memes protocols - Vint Cerf inventeur du  Transmission Control Protocol/Internet Protocol (TCP/IP)

- 🔗 Lier des ordiateur entre eux, pour creer un reseaux (networking and link layer)
- 🌐 Combiner des reseaux en utilisant l'IP (internet protocol)
- 📍 Trouver un destinataire depuis son adresse IP
- 🧭 Trouver une route dans le reseaux pour atteindre cette adresse
- 🚚 Transporter/echanger des donnees

Avant internet, les telecommunations entre 2 parties necessitaient un lien physique. Dans les annees 1950, les telephones étaient directement connecté a une station centrale. Pour qu'un appel passe, un operateur devait relier les deux bout de la ligne. Pour les appels longue distance, plusieures station centrales et operateurs devaient se coordonner pour relier ces 2 telephones.

![les operatrices du telephone](https://upload.wikimedia.org/wikipedia/commons/e/e4/Telephone_switchboard_6_Oct_1907_Salt_Lake_City.jpg)

Aujourd'hui les cables ne sont plus reservés a une connection. Un meme cable peut maintenir plusieures connections. Cependant, les technologies modernes de reseaux sont plus techniques qu'avant. Nous allons aboder cette complexité en commencant avec le layer le plus basique, le link layer (couche 2 du modeles OSE, 1er couche apres la couche phyique)

## 1.1 Links

Pour relier 2 ou plus computers nous avons besoin d'un medium de transmittion ou passer nos signaux. Ce peut etre un cable de cuivre(electrique/electricité), une fibre optique(light) ou des ondes radios(wifi).

Quand 1 medium relie exclusive 2 points, on parle de liaison point a point (PPP point to point protocol). Comme son systeme l'indique elle n'est pas faite pour plusieures liaisons, il n'y a donc pas de notion native d'addresse reseau entre les deux hotes, ni de controle avance de flux.

Mais le PPP est un cas rarissime pour les ordinateurs. Ils doivent souvent partagés le medium de transmission avec d'autres ordinateurs.

## Shared Link

Pour connecter des ordinateurs dans un bureau, on peut recourir a des cables interconnectes a un hub. L'hub interconnecte tous les cables qui lui sont lies, lorsqu'un ordinateur envoie 1 signal, il sera detecte par tous les autres. C'est d'ailleurs le cas sur le wifi chez vous ( notez qu'aujourd'hui grace a l'https, la plupart de vos signaux sont cryptés).

Cependant sur un reseau partage, les communications peuvent s'embrouiller quand tout le monde l'utilise au meme moment(devenir messy). Un peu comme lors de grand rassemblent, les textos et appels ne passent plus

Le link layer contient un ensemble de regles qui definnissent comment les ordinateurs doivent partager leur communication medium, on l'a mal nomme le Medium Access Control (MAC)

MAC gere les collisions et l'addressage physique.

Collisions - lorsque deux ordinateurs envoyent un message a travers le meme medium au meme moment.

Un des moyens de contourner les collisions est de monitorer les communications, lorsqu'une collision arrive, on attends un brief random moment et on essaie de retransmettre. Cette methode a des limites, s'il y a trop d'expediteurs les collisions ne s'arreteront jamais. C'est le cas evoque precedemment avec le reseau telephonique sature.

Physical Address - Chaque interface reseau a un identifiant, connu comme son addresse physique ou hardware adresse (MAC ADDRESS). Une transmission dans un reseau partage contient 2 de ces adresses, celle de l'expediteur et du recepteur. Lors de la reception de l'un de ces signaux, un ordinateur saura si il doit ignorer ou non ce message. Cependant, pour que cela marche les adresses doivent etre uniques

## MAC ADDRESSES
