# par-22-23-detection-raquette
Dans cette 1 ère tache, nous avons commencé à extraire des datasets de vidéos de matchs de ping pong.
Ensuite, on les a subdivisé en images(en utilisant la fonction "split"), annoté ces images par le logiciel "LabelImg", et converti les images annotées en un fichier CSV(contenant chacun la position inférieure et supérieure du rectangle créé autour de la raquette).
Le but de cette étape est de fournir une base de données variée pour un algorithme de Machine Learning, qui va par la suite apprendre tout seul à détecter la raquette en temps réel(dans une vidéo).
