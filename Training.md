# Trainieren des Models
Zum trainieren werden Bilder aus dem [Bosch Small Traffic Lights Dataset](https://hci.iwr.uni-heidelberg.de/node/6132) verwendet.  
Da die Tensorflow Object Detection API [TFRecord - Dateien](https://www.tensorflow.org/programmers_guide/datasets#consuming_tfrecord_data)
verwendet muss das Bosch Dataset in eine *.record Datei konvertiert werden.  

Da die *.record Datei eine beachtliche Größe hat, wurde sie nicht in dieses Repository
eingecheckt und muss von jedem selbst erstellt werden.

Das Bosch Dataset muss ebenfalls selbst heruntergeladen werden und anschließend in das
Verzeichnis ```data/bosch/dataset_train_rgb``` und ```data/bosch/dataset_test_rgb``` entzippt werden.

Zum konvertieren dann das Script [data_conversion_bosch.py](./data_conversion_bosch.py) aufrufen.
```
python data_conversion_bosch.py
```
Die fertige TFRecord Dateien findet man dann hier:  
```tf_record/training.record``` und ```tf_record/test.record```
  
An dieser Stelle noch einmal Danke an [**Anthony Sarkis**](https://medium.com/@anthony_sarkis).  
Von ihm ist das [original Script](https://github.com/swirlingsand/deeper-traffic-lights/blob/master/data_conversion_bosch.py).

##### Download des Pre-Trained models
Herunterladen des Pre-Trained models [ssd_mobilenet_v2_coco](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz) aus dem [Tensorflow detection model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md).  
und extrahieren in das Verzeichnis ```/pre_trained```.

Die Verzeichnisstruktur sollte so aussehen:
```
pre_trained/
    ssd_mobilenet_v2_coco_2018_03_29/
        saved_model/
        frozen_inference_graph.pb
        model.ckpt.index
        ...
```  
 
##### Starten des Trainings
```
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=config/ssd_mobilenet_v2_coco.config
```

Nach Abschluss des Trainings ist das gesamte Model im Ordner ```training/``` zu finden. 