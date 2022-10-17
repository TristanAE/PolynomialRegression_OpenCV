# PolynomialRegression_OpenCV

Programme capable d’anticiper la position d’un ballon de baudruche qui a été envoyé, et qu’un robot se déplace en dessous.

# I-	Conception électronique

_Mise en place du véhicule robotisé_

Le robot qui aura pour rôle de se déplacer sous un ballon de baudruche, est un kit à assembler de :

•	2 châssis, 2 roues, 2 moteurs et de la visserie à monter

•	Une carte esp8266 et un motoshield adapté

•	Une batterie pour la carte et une supplémentaire pour les moteurs

# II-	Conception informatique

_a)	Traitement d’image_

Pour analyser l’environnement dans lequel le ballon et le robot seront, nous utiliserons la bibliothèque OpenCV. Nous traiterons l’image que renvoie la webcam de notre ordinateur où se trouve le programme principal.

Localiser le robot et le ballon :

Pour localiser la position du robot et du ballon dans l’espace, nous isolerons leur couleur : le robot sera doté d’un papier cartonné rouge et le ballon de baudruche est entièrement vert. Ces 2 éléments seront les seuls que notre programme visionnera et analysera. 
Nous obtenons ainsi les coordonnés du centre du ballon et du robot.


_b)	Algorithme Polynomial Regression_

Une fois que le ballon de baudruche aura été envoyé, nous utiliserons la bibliothèque Sklearn pour anticiper la position d’arrivé au sol de celui-ci.
Grâce à la partie de traitement d’image, nous allons récupérer cinq fois les coordonnées du ballon dans les airs, à des intervalles de temps très court. Ces coordonnées, placées dans un tableau Numpy, vont être utilisées dans un algorithme de régression polynomiale pour pouvoir prédire la fin du mouvement du ballon.

Nous avons ainsi un algorithme capable de prédire le probable mouvement du ballon. Nous cherchons à savoir si lorsque la coordonnée x du ballon atteint la coordonnée x du robot, leur coordonnée y seront également les mêmes (environ).

•	Si le ballon prévoit de chuter avant d’atteindre le robot, alors quand xballon=xrobot, yballon < yrobot

•	Si le ballon prévoit de chuter après le robot, alors quand xballon=xrobot, yballon > yrobot

Selon le résultat, le programme commande au robot d’avancer ou de reculer via wifi, puis prédit de nouveau la coordonnée y du ballon avec la nouvelle cordonnée en x du robot. 


# III-	Rendu et problèmes rencontrées

_a)	Vitesse du programme_

L’idée première a été d’envoyer une balle plus dense que le ballon de baudruche vers le robot.
Le recul de la webcam étant trop faible, je ne pouvais pas envoyer la balle de très loin. Les prédictions faites par le programme étaient donc justes mais la chute était trop rapide pour que le robot puisse avoir le temps d’agir pour s’adapter.
Le choix de prendre un ballon de baudruche à la place a permis au robot d’avoir davantage de temps pour se placer en dessous.

_b)	Mouvement perturbé_

Un ballon de baudruche est beaucoup plus léger et donc davantage soumis au frottement de l’air. Contrairement à la balle qui réalisait un mouvement parfaitement en cloche, le ballon, lui, peut avoir un comportement plus erratique et empêcher une bonne prédiction.
 
Chute trop rapide et déviation vers l’avant du ballon

 
 ![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/92324336/196150592-5e0e63ab-3efd-46d0-87c5-3a70648e245a.gif)
 
 Chute trop rapide et déviation vers l’avant du ballon
 
![ezgif com-gif-maker (3)](https://user-images.githubusercontent.com/92324336/196150600-0ea6b890-4277-482e-ab90-22b4451c2d09.gif)
![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/92324336/196150604-4481a67e-9f54-466a-b5c0-d0c6d77fe20c.gif)


