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
Herunterladen des Pre-Trained models z.B.  [ssd_mobilenet_v2_coco](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz) aus dem [Tensorflow detection model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md).  
und extrahieren in das Verzeichnis ```/pre_trained```.

Die Verzeichnisstruktur sollte so aussehen (je nachdem welches Model man geladen hat):
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
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=config/faster_rcnn_resnet101_coco.config
```
oder
```
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=config/faster_rcnn_resnet50_coco.config
```
oder
```
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=config/ssd_mobilenet_v1_coco.config
```

##### Training mit Tensorboard überwachen
```
tensorboard --logdir=training
```

##### Exportieren des Graph
```
python export_inference_graph.py --input_type image_tensor --pipeline_config_path config/faster_rcnn_resnet50_coco.config --trained_checkpoint_prefix training/model.ckpt-12000 --output_directory inference_graph
```

Nach Abschluss des Trainings ist das gesamte Model im Ordner ```training/``` zu finden.

#### Graph Transformieren
Achtung: Hierfür ist wird [Tensorflow](https://github.com/tensorflow/tensorflow) benötigt.  
Die Installationsanleitung findet man hier: [Tensorflow install from Source](https://www.tensorflow.org/install/install_sources)   
```
bazel-bin/tensorflow/tools/graph_transforms/transform_graph \
--in_graph=frozen_inference_graph.pb \
--out_graph=optimized_inference_graph.pb \
--inputs='image_tensor:0' \
--outputs='detection_classes:0,num_detections:0,detection_scores:0,detection_boxes:0' \
--transforms='
  strip_unused_nodes(type=float, shape="1,1280,720,3")
  fold_constants(ignore_errors=true)
  fold_batch_norms
  fold_old_batch_norms
  quantize_weights'
```
 
