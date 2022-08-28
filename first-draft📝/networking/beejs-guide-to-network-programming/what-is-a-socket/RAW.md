# -

il y a toutes sortes de sockets. Il y a les sockets avec DARPA Internet adresses (Sockets Internet), les noms de chemin vers un noeud (Sockets Unix), les adresses CCITT X.25 (les sockets X.25 sur lesquels vous pouvez tranquillement faire l'impasse) et probablement beaucoup d'autres qui dépendent de la version d'Unix que vous utilisez. Ce document traite seulement de la première sorte: Les sockets Internet.

## Deux types de sockets Internet

Qu'est que c'est encore que ce truc? Il y a deux types de sockets Internet? Oui. Enfin non. Je suis en train de mentir. Il y en a bien plus, et je ne veux pas vous effrayer. Je vais uniquement vous parler de deux types ici. A l'exception de cette phrase, ou je vais vous parler des Sockets brutes (NDT:"Raw Sockets") qui sont très puissantes et sur lesquelles vous devriez jeter un oeil.
Bien, quels sont ces deux types ? L'un s'appelle les socket de flux (NDT:"Stream Sockets") et l'autre les sockets de paquets (NDT:"Datagram Sockets"). Elles seront référencées respectivement par SOCK_STREAM et SOCK_DGRAM dans la suite de ce document. Les "sockets de paquets" sont parfois appelées les "sockets sans connections",
