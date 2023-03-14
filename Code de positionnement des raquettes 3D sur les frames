import bpy
import sys
sys.path.append("search-ms:displayname=Résultats%20de%20la%20recherche%20dans%20pkgs&crumb=System.Generic.String%3Apillow&crumb=location:C%3A%5CUsers%5Cpc%5Canaconda3%5Cpkgs")
import csv

from PIL import Image

# Chemin vers le fichier CSV
csv_file = "C:\\Users\pc\Desktop\CSV+data-squelettes\CSV.csv"

# Chemin vers le dossier contenant les images
image_folder = "C:\\Users\pc\Desktop\CSV+data-squelettes\img_squelette"

#Chargement du fichier CSV
with open(csv_file, newline='') as csvfile:
    csv_reader = csv.reader(csvfile, delimiter=',')
    line_count = 0
    for row in csv_reader:
        if line_count == 0:
            # Ignorer la première ligne (en-têtes)
            line_count += 1
        else:
            # Récupérer les données de position des objets pour la frame actuelle
            if int(row[6])==1 and (int(row[2])==4 or int(row[2])==7):
                frame_number = int(row[0])
                object1_position = [float(row[3]), float(row[4])]
                object2_position = [float(row[3]), float(row[4])]
                # Charger l'image pour cette frame
                image_path = image_folder + "frame_" + str(frame_number) + ".png"
                img = Image.open(image_path)
                bpy.data.images.load(image_path, check_existing=True)
                img_idx = len(bpy.data.images)-1
            
                # Accéder aux objets dans Blender et positionner
                if int(row[1])==1 and int(row[2])==4:
                    obj1 = bpy.data.objects['Point.001']
                    obj1.location = object1_position
                if int(row[1])==0 and int(row[2])==7:
                    obj2 = bpy.data.objects['Point.002']
                    obj2.location = object2_position
            
                # Ajouter une nouvelle keyframe pour chaque objet
                obj1.keyframe_insert(data_path="location", index=-1)
                obj2.keyframe_insert(data_path="location", index=-1)
            
                # Définir l'image actuelle comme frame courante et ajouter une keyframe
                bpy.context.scene.frame_set(frame_number)
                bpy.data.scenes['Scene'].frame_current = frame_number
                bpy.data.scenes['Scene'].render.image_settings.file_format = 'JPEG'
                bpy.data.scenes['Scene'].render.filepath = image_folder + "output/frame_" + str(frame_number) + ".jpg"
                bpy.ops.render.render(write_still=True)
            
                line_count += 1
