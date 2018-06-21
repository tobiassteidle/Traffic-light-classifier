# Traffic-light-classifier
Detection and Classifier for (Udacity CarND Capstone (System Integration) Project)[https://github.com/tobiassteidle/CarND-Capstone].

Um das Model für den Traffic light classifier (oder ein anderes Projekt) zu trainieren
wird die [Tensorflow Object Detection API](https://github.com/tensorflow/models/tree/master/research/object_detection)
benötigt.

Eine Installationsanleitung gibt es [hier](Installation_Tensorflow.md).

### Informationen
Das erkennen von Ampeln funktioniert mit einem Vortrainiertem Model (z.B. ssd_mobilenet_v1_coco_2017_11_17)
wie im Beispiel [object_detection_tutorial](https://github.com/tensorflow/models/blob/master/research/object_detection/object_detection_tutorial.ipynb)
schon relativ gut und kann in einem Testbild die Ampeln erkennen.


##### Beispiel
![SSD_Mobilenet_v1](sample_images/ssd_mobilenet_v1_coco_traffic.png)

Allerdings ist das erkennen der Ampel an sich nicht ausreichend.  
Es muss zusätzlich erkannt werden welche Farbe die Ampel anzeigt.

Dazu ist es notwenig ein Model zu trainieren.

Ein vollständig trainiertes Model ist im Ordner ```training/``` abgelegt.

##### Trainieren (optional)
Eine Beschreibung zum trainieren der Models findet man [hier](Training.md)




 



