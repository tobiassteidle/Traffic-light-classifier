# Installation Tensorflow Object Detection API

Informationen zur Tensorflow Object Detection API [hier](https://github.com/tensorflow/models/tree/master/research/object_detection).

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

##### Aktualisierung von Protobuf 2 auf Protobuf 3 (Thx to [Sofyan Hadi Ahmad](https://gist.github.com/sofyanhadia/37787e5ed098c97919b8c593f0ec44d8))
```
curl -OL https://github.com/google/protobuf/releases/download/v3.3.0/protoc-3.3.0-linux-x86_64.zip
unzip protoc-3.3.0-linux-x86_64.zip -d protoc3

sudo mv protoc3/bin/* /usr/local/bin/
sudo mv protoc3/include/* /usr/local/include/

sudo chown $USER /usr/local/bin/protoc
sudo chown -R $USER /usr/local/include/google
```

### Installation (Tensorflow Requirements) - Teil 2
```
protoc object_detection/protos/*.proto --python_out=.
export PYTHONPATH=$PYTHONPATH:pwd:pwd/slim
```
##### Achtung:
```pwd``` ist der Absolute Pfad zum model/research Verzeichnis.  

#### Installation (Tensorflow Requirements) - Teil 3
Für den GPU Support wird CUDA 9.0 benötigt.
[https://developer.nvidia.com/cuda-90-download-archive](https://developer.nvidia.com/cuda-90-download-archive).

##### Installation CUDA 9.0
```
sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
sudo apt-key add /var/cuda-repo-9-0-local/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda
```

##### Installation cuDNN
[cuDNN Download](https://developer.nvidia.com/rdp/form/cudnn-download-survey) (Account benötigt).  
[cuDNN v7.0.5 Runtime Library for Ubuntu16.04 (Deb)](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/9.0_20171129/Ubuntu16_04-x64/libcudnn7_7.0.5.15-1+cuda9.0_amd64)
```
sudo dpkg -i libcudnn7_7.1.4.18-1+cuda9.0_amd64.deb
```

#### Installation (Tensorflow Requirements) - Teil 4
Erstellen des Conda environments mit der environment.yml aus diesem Repository.

```
cd Traffic-light-classifier
conda env create -f environment.yml
```
Aktivieren des Conda environments
```
source activate traffic-light-classifier
``` 

#### Abschluss - Testen des Model Builders
Zum testen wieder zurück in das Repository der Tensorflow Object Detection API.
```
cd model/research
python object_detection/builders/model_builder_test.py
```
          
Der Output sollte sein (oder Ähnlich):
```
Ran 15 tests in 0.064s

OK
```