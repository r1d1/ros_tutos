# Episode 01 - Introduction

_A long time ago in a galaxy far, far away ..._


## Qu'est-ce que ROS ?
ROS est un framework logiciel destiné à la robotique. Il est issu des travaux des chercheurs du Computer Science Department à Stanford, et présenté initialement dans la publication [Quigley et al., 2009](http://www.willowgarage.com/sites/default/files/icraoss09-ROS.pdf). L'idée est que la robotique est déjà un domaine très complexe, donc il est important de réutiliser les contributions d'autres sources plutôt que de réimplémenter tous les algos nécessaires dans chaque labo. Depuis, la communauté des chercheurs en robotique (et domaines proches) a développé le framework, ajouté des packages, ROS est désormais utilisé dans le monde entier, et équipe certains robots industriels également.
ROS signifie Robot Operating system, ce qui peut être confusionnant : il s'agit d'un framework logiciel, donc une "library" de programmes qui ont eux-même besoin d'un système d'exploitation (OS) pour tourner. L'OS principal pour utiliser ROS est Ubuntu mais il existe des versions expériementales pour Windows/Mac et les sources sont disponibles si vous voulez le compiler sur votre plateforme.

### Les distributions.
Comme votre OS préféré, ROS évolue et différentes versions sont publiées pour intégrer les derniers outils. Dans ROS, chaque version est une distribution (une distribution de packages ; j'utiliserai le terme de "distro" dans la suite). Comme ROS est principalement destiné à fonctionner sur Ubuntu Linux, le rythme des mises à jour suit l'évolution des versions d'Ubuntu. À la date d'écriture de ce tuto (août 2017), la dernière Long-Term-Support est Kinetic Kame. Normalement, les packages développés dans des distros précédentes sont compatibles dans les distros plus récentes, mais mieux vaut jeter un oeil au changelog pour éviter les mauvaises surprises. La suite suppose que vous utilisez Ubuntu 14.04 ou 16.04 avec ROS Indigo ou Kinetic.

### Premiers pas.
On va ici traiter rapidement de l'installation, mais il n'y a normalement rien de bien compliqué. Le but est ici surtout de fournir une ressource en français.
Les instructions de base sont disponibles [ici](http://wiki.ros.org/kinetic/Installation/Ubuntu). Remplacez si besoin kinetic dans le lien par la distribution que vous souhaitez installer (indigo ou kinetic dans le cadre de ce tutoriel).

Si ça n'est pas déjà fait, modifiez les sources logicielles d'Ubuntu (les repositories à partir desquels vous installer des logiciels) pour autoriser les sources "restricted", "universe", "multiverse".
On va ensuite ajouter le repository où sont disponibles les packages spécifiques à ROS. Dans un terminal, entrez la commande suivante :

sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

Cette commande ajoute dans /etc/apt/sources.list.d la ligne contenant d'url du repository pour votre distribution d'Ubuntu (avec le résultat de lsb_release).


Simulons un robot
[Simulated turtlebot]

Première chose, choisissons-nous un robot avec lequel jouer en simulation. Une liste est disponible sur [url=http://robots.ros.org/]http://robots.ros.org/[/url]. Pour ces tutoriels, nous allons utiliser Fetch de l'entreprise Fetch Robotics. La documentation est disponible [url=http://docs.fetchrobotics.com/gazebo.html]ici[/url]. Leur robot est une évolution du PR2 de Willowgarage, c'est un produit actuel donc le code et la documentation sont à jour, il est composé d'une plateforme mobile et d'un bras ce qui va nous permettre de jouer à la fois avec de la navigation mais aussi de la manipulation. Si vous voulez juste tester avec des robots plus simples, je conseille le turtlebot (le 2 est plutôt pas mal, le 3 est sorti récemment mais je ne l'ai pas testé) ou les robots de Clearpath Robotics (le husky par exemple, cependant, le package de simulation buggue à l'heure où j'écris ces lignes).

Une fois les packages du robot installés, lançons une simulation de base.
[video fetch]
Gazebo est le simulateur, RViz permet de visualiser les capteurs du robot. Ici, on voit une démo de fetch & carry : prendre un objet pour l'apporter ailleurs. On notera d'ailleurs le fail du robot à la fin qui fait tomber le cube, mais qui s'en fiche. À peine créés, déjà feignantes ces machines !
Plus sérieusement, la démo est probablement scriptée simplement. J'ai testé plusieurs autres fois et il arrive que le robot se trompe sur sa position dans l'environnement mais n'adapte pas sa navigation à la position des tables. Bref ... on fera mieux plus tard. :)

Ici, l'environnement est simulé par Gazebo, mais notre robot est contrôlé à l'aide de ROS. Utilisons la commande rqt_graph dans un terminal.

[output rqt_graph]

On voit ici un ensemble de *nodes* (les ovales) connectés entre eux par des *topics* (les flèches qui passent à travers les rectangles). Sur l'image, mon curseur attire l'attention sur le node qui fait tourner le simulateur. Une des forces de ROS, c'est son système de communication : au travers des topics /head_camera/* je peux récupérer toutes les infos sur ma camera (l'image, mais également d'autres infos utiles) quelque soit le hardware ou le simulateur derrière. Ici, j'utilise Gazebo, mais je pourrais avoir un node qui fait l'interface avec V-Rep ou Marilou, tant que ce node fournit les mêmes topics, je n'ai pas besoin de changer mon architecture de contrôle. Et bien évidemment, quand je passe sur le robot réel, si les drivers me fournissent aussi ces topics, je n'ai rien à faire de plus. Magique, non ?

Un peu de pratique
Une fois ROS installé

erwan@sheepy:~$ roslaunch fetch_gazebo playground.launch 
erwan@sheepy:~$ rosrun rviz rviz -d .rviz/ErwanFetch.rviz 
erwan@sheepy:~$ rostopic pub -r 100 /cmd_vel geometry_msgs/Twist '{linear: {x: -0.2}, angular: {z: 0.}}'
