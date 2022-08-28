# Intro

Pourquoi les shaders sont rapides ? traitement en parallèle

Usuellement, les ordinateurs utilisent des threads, qui traitent les operations de maniere sequentielle(en serie), les unes apres les autres

--
Les jeux vidéos et autres applications graphiques demandent beaucoup plus de puissance de calcul que les autres programmes. Par nature, ils demandent de grandes quantités d'opérations au pixel, chaque changement d'image demande de recalculer l'ensemble des pixels de l'écran. Dans les applications 3D, on doit également mettre à jour les modèles, les textures, les transformations etc. ce qui rajoute encore plus de charge au CPU.

--

Revenons à notre métaphore des tuyaux et des opérations. Chaque pixel à l'écran représente une simple petite opération. En soi, le traitement d'une opération n'est pas un problème pour le CPU, mais (et c'est ici que se trouve le problème) il faut appliquer cette petite opération sur chaque pixel à l'écran ! Par exemple, sur un vieux moniteur ayant une résolution de 800x600, 480 000 pixels ont besoin d'être traités par frame ce qui équivaut à 14 600 000 calculs par seconde ! C’est une opération assez importante pour surcharger un microprocesseur. Sur un écran rétina moderne ayant une résolution de 2880x1800 cadencé à 60 frames par seconde, cela représente un total de 311 040 000 calculs par seconde. Comment les ingénieurs graphiques résolvent-ils ce problème?

![overload](https://thebookofshaders.com/01/03.jpeg)

--
C'est là qu'intervient le traitement parallèle (parallel processing). Au lieu d'avoir quelques gros et puissants microprocesseurs, ou tuyaux, on préfère avoir de nombreux petits microprocesseurs qui tournent en parallèle et simultanément. C'est l'essence même du GPU (Graphics Processing Unit).

![parallel processing](https://thebookofshaders.com/01/04.jpeg)

--

## What GLSL

GLSL est l'acronyme de "OpenGL Shading Language" (où GL signifie Graphics Library).Comprendre l'histoire d'OpenGL peut être utile pour comprendre certaines conventions un peu bizarres, si cela vous intéresse, vous pouvez vous reporter à openglbook.com/chapter-0-preface-what-is-opengl.html.

## -

Pour fonctionner en parallèle, il faut que chaque thread soit indépendant des autres. On dit que le thread est aveugle à ce que font les autres threads. Cette restriction implique que toutes les données doivent aller dans le même sens. Il est donc impossible de vérifier le résultat d’un autre thread, de modifier les données d’entrée ou de transmettre le résultat d’un thread à un autre. Autoriser la communication entre threads au moment de l'exécution pourrait compromettre l'intégrité des données en cours de traitement.

--
Il faut également savoir que le GPU s'assure que tous ses microprocesseurs (les tuyaux) sont actifs en permanence; dès qu'un thread a fini son traitement, le GPU lui ré-assigne une opération à traiter. Le thread ne garde aucune trace de ce qu'il faisait la fois précédente. S'il était en train de dessiner le pixel d'un bouton sur une interface graphique, sa tâche suivante pourra être de rendre un bout du ciel dans un jeu, puis de rendre un bout de texte sur un mail. Donc un thread est non seulement aveugle mais aussi amnésique. En plus du niveau d'abstraction requis pour coder une fonction générique qui saura rendre une image entière ***uniquement à partir de la variation d'une position***
