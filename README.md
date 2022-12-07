# par-22-23-detection-raquette
Description des codes utilisés : 
Train.py ( disponible via ce lien : https://github.com/centralelyon/par-22-23-detection-raquette/blob/main/models/YOLOv5_trained/train.py) : ce code est la base de l’entraînement. Il est constitué d’une fonction “ train” qui permet d’initialiser le réseau de neurones, les poids, le learning rate pour le gradient Descent et d’affecter les données d’entrée ( nos datas) au réseau de neurones.
!python train.py --batch 32 --epochs 150 --data 'data/raquette_data.yaml' --weights 'yolov5s6.pt' --project 'runs_raquette' --name 'feature_extraction' --cache --freeze 12
 
On appelle cette fonction via la ligne ( ci dessus) en précisant respectivement : 
Le batch : hyperparamètre qui précise la fréquence d’ajustement des poids ( après feedforward et rétropropagation)
Epochs : le nombre de fois que le code passe sur les données par étape d’entraînement.
Weights : fichier dans lequel on stocke les valeurs des poids lorsque l’algorithme de descente du gradient converge.
Project/ name : le dossier où stocker le résultat de la détection.


Val.py ( disponible via le lien Github suivant : https://github.com/centralelyon/par-22-23-detection-raquette/blob/main/models/YOLOv5_trained/val.py)
: permet de choisir le modèle avec les paramètres les plus optimisés. Il est constitué principalement de la fonction main() qui permet d’optimiser les poids du réseau de neurones.
!python val.py --weights 'runs_raquette/fine_tuning/weights/best.pt' --batch 64 --data 'data/raquette_data.yaml' --task test --project 'runs_raquette' --name 'validation_on_test_data' --augment
La ligne ci-dessous permet d'exécuter le code val.py en lui passant comme paramètres:
Les poids résultant du fine-tuning ( éviter le sur apprentissage) ( fichier best.pt) , le batch, la data ( le fichier yaml contenant le nombre de classes d’objets à détecter et leurs noms).


Et les autres paramètres spécifient le dossier de sauvegarde.


detect.py ( disponible via ce lien Github : https://github.com/centralelyon/par-22-23-detection-raquette/blob/main/models/YOLOv5_trained/detect.py) : ce code permet de tester notre modèle sur le test set et sur des vidéos pour avoir une détection en temps réel.
!python detect.py --weights 'runs_raquette/fine_tuning/weights/best.pt'  --conf 0.6 --source 'match_Trim.mp4' --project 'runs_raquette' --name 'detect_test' --augment --line=3
 
La ligne du code ci-dessus permet de spécifier les paramètres en entrée du code detect.py ( les poids du modèle, la source qu’est les images ou les vidéos à tester, et le path d’enregistrement.
Les résultats du tracking sur la data du test est disponible via ce lien Github : https://github.com/centralelyon/par-22-23-detection-raquette/tree/main/runs_raquettes/detect_test
). Les résultats du tracking sur des vidéos sont disponibles via ce lien gitHub : 

Metrics.py ( disponible via ce lien : https://github.com/centralelyon/par-22-23-detection-raquette/blob/main/models/YOLOv5_trained/utils/metrics.py )
: code qui permet de tracer les métriques en fonction des epochs pour l’entraînement. On trace la précision donnée par la relation : 
Précision=TP(true positives)/TP+FP( false positives) 

Le modèle nous donne aussi la matrice de confusion dans notre cas, ce qui constitue une bonne base de quantification des erreurs de l’apprentissage.
Toutes les métriques sont tracées et disponibles via le lien Github suivant  : https://github.com/centralelyon/par-22-23-detection-raquette/tree/main/runs_raquettes/validation_on_test_data)

general.py(disponible via ce lien : https://github.com/centralelyon/par-22-23-detection-raquette/blob/main/models/YOLOv5_trained/utils/general.py)
: code qui permet de tracer les bounding boxes sur les images et vidéos à tester.



