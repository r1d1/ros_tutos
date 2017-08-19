# ros_tutos

Ce repository contient un ensemble de tutoriels pour l’initiation à ROS (en français). Les tutoriels sont organisés en épisodes couvrant les sujets suivants :

[x] episode 1 : 
[ ] episode 2 : 
[ ] ...

Il s'agit plus ou moins d'une adaptation en français des [http://wiki.ros.org/](tutos officiels) que je recommande si vous lisez l'anglais. La documentation a bien évolué et couvre la plupart des sujets essentiels. À noter qu'une version incomplète existe en français, mais pour le coup, il n'y a pas grand chose : [http://wiki.ros.org/fr](http://wiki.ros.org/fr).

## Pré-requis

Commencer avec ROS demande certains pré-requis :
* connaissance de Linux : commandes de base (cd, ls, mv, rm ...), usage de sudo ...
* conaissances en programmation : C++ ou Python principalement. Il existe des [https://fr.wikipedia.org/wiki/Interface_de_programmation](API) en Java, nodejs, mais dans ce tutoriel, nous nous concentrerons sur C++ (et probablement un peu de python). Par conséquent, une bonne compréhension de la compilation C++ / de l'écriture de scripts Python, la connaissance de Make/CMake sont très utiles.
* Notions de réseau informatique.

Il est possible d'utiliser ROS sans ces pré-requis, mais ça rend le debug et l'identification des problèmes assez compliqués. Il est donc judicieux de revoir ou se former sur ces sujets pour bien comprendre ROS.

## Robots
Les tutoriels s’appuient d’une part sur la simulation dans Gazebo du robot Fetch de Fetch Robotics et d’autre part sur mon robot personnel [http://www.robot-maker.com/forum/topic/6949-froggy-la-grenouille-robotique-mutante/](Froggy) pour les épisodes sur ros_control. Ils ont été préparés et testés sur Ubuntu 14.04 et 16.04 avec ROS indigo et kinetic. Si vous les testez sous d'autres versions de ROS, d'autres systèmes d'exploitations et avec d'autres robots, votre retour m'intéresse, n'hésitez pas à me contacter par les moyens listés ci-dessous.

Une erreur ? Une coquille ? Ouvrez une “issue” sur github, envoyez moi un MP sur [Robot-maker](http://www.robot-maker.com/) ou postez sur le [topic dédié](http://www.robot-maker.com/forum/topic/545874-thislinkneedstobeupdated).

OS | Distribution ROS | Robot | Statut
--------------------------------------
Ubuntu 14.04 | indigo | Fetch | :heavy_check_mark:
 |  | Froggy | :x:
 | jade | Fetch | :x:
 |  | Froggy | :x:
Ubuntu 16.04 | kinetic | Fetch | :x:
 | | Froggy | :x:
