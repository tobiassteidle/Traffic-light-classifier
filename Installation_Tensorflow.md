# Installation Tensorflow Object Detection API

Informationen zur Tensorflow Object Detection API [hier](https://github.com/tensorflow/models/tree/master/research/object_detection)

### Installation (Tensorflow Requirements) - Teil 1
```
git clone https://github.com/tensorflow/models.git
cd models/research
sudo apt-get install protobuf-compiler python-pil python-lxml
```

##### Anleitung im Tensorflow Repository
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md

##### Achtung:
Die Installation der Tensorflow Requirements installiert die Protobuf Version 2.
Für die Tensorflow Object Detection wird Protobuf 3+ benötigt.

##### Aktualisierung von Protobuf 2 auf Protobuf 3
https://gist.github.com/sofyanhadia/37787e5ed098c97919b8c593f0ec44d8

### Installation (Tensorflow Requirements) - Teil 2
```
protoc object_detection/protos/*.proto --python_out=.
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim
```

#### Installation (Tensorflow Requirements) - Teil 3
Für den GPU Support wird CUDA 8.0 benötigt.
[https://developer.nvidia.com/cuda-80-ga2-download-archive ](https://developer.nvidia.com/cuda-80-ga2-download-archive)

##### Installation CUDA 8.0
```
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

### Installation (Tensorflow Requirements) - Teil 4
Erstellen des Conda environments mit der environment.yml aus diesem Repository
```
cd Traffic-light-classifier
conda env create -f environment.yml
```
Aktivieren des Conda environments
```
source activate traffic-light-classifier
``` 


### Abschluss: Testen des Model Builders
Zum testen wieder zurück in das Repository der Tensorflow Object Detection API.
```
cd model/research
python object_detection/builders/model_builder_test.py
```


