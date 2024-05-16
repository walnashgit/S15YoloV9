# YOLOV9 model trained on custom dataset.
Trained to detect tabla (Indian classical musical instrument)

[Original Repo](https://github.com/SkalskiP/yolov9)

## Usage

### Clone the repo in a jupityer note book or where ever you are going to train:
`git@github.com:walnashgit/S15YoloV9.git`

The custom data set is in the folder `tabla`. If using a different dataset, follow the folder structue same as the one here and update the `data.yaml` file accordingly.

### Move to the root folder and install the requirements:

```
%cd S15YoloV9
!pip install -r requirements.txt -q
```


### Download one of the weights from the below. This repo is trained on yolov9-e.pt
```
#!wget https://github.com/WongKinYiu/yolov9/releases/download/v0.1/yolov9-c.pt
!wget https://github.com/WongKinYiu/yolov9/releases/download/v0.1/yolov9-e.pt
# !wget https://github.com/WongKinYiu/yolov9/releases/download/v0.1/gelan-c.pt
#!wget https://github.com/WongKinYiu/yolov9/releases/download/v0.1/gelan-e.pt

```

### Base on the weight downloaded use below code to start training:
```
# train yolov9 models
!python train_dual.py \
--batch 8 --epochs 25 --img 640 --device 0 --min-items 0 --close-mosaic 15 \
--data /content/S15YoloV9/tabla/data.yaml \
--weights /content/S15YoloV9/yolov9-e.pt \
--cfg /content/S15YoloV9/models/detect/yolov9-e.yaml \
--hyp hyp.scratch-high.yaml
```

```
# train gelan models
!python train.py \
--batch 8 --epochs 25 --img 640 --device 0 --min-items 0 --close-mosaic 15 \
--data /content/S15YoloV9/tabla/data.yaml \
--weights /content/S15YoloV9/yolov9-e.pt \
--cfg /content/S15YoloV9/models/detect/gelan-c.yaml \
--hyp hyp.scratch-high.yaml
```
Note the cfg file should be based on the model weight being used. Adjust batch size to suit the available memory.

#### The results of trainig are stored in `runs/train/exp`. The trained model weight is in `runs/train/exp/weights/best.pt`.

### To viualise the validation images:
```
from IPython.display import Image
Image(filename=f"/content/S15YoloV9/runs/train/exp/val_batch0_pred.jpg", width=1000)
```

### To run trained model on validation or anyother test dataset:
```
!python detect.py \
--img 1280 --conf 0.1 --device 0 \
--weights /content/S15YoloV9/runs/train/exp/weights/best.pt \
--source /content/S15YoloV9/tabla/valid/images
```
The training results are stored in `runs/detect/exp`

Ref [video](https://www.youtube.com/watch?v=Opr53ctUVlA&ab_channel=TechWatt) for training.


### Read the [Readme](https://github.com/SkalskiP/yolov9/blob/main/README.md) from the original repo for details about the model

Check out this [video](https://www.youtube.com/watch?v=oZ6I1VHpil0&ab_channel=Dr.PriyantoHidayatullah) to understand the architecture.

