**Note:** This is a re-implementation of [GGCNN](https://github.com/dougsm/ggcnn) for training the Cornell Dataset with image-wise and object-wise split and
Abridged Jacquard Dataset. More information about the work of GGCNN can be referred to their official Github Repository. 


## Installation

This code was developed with Python 3.6 on Ubuntu 16.04.  Python requirements can installed by:

```bash
pip install -r requirements.txt
```

## Datasets

Currently, both the Cornell Grasping Dataset and Jacquard Dataset are supported.

### Cornell Grasping Dataset

1. Download the and extract [Cornell Grasping Dataset](https://www.kaggle.com/oneoneliu/cornell-grasp). The official websit is down and it is provided in kaggle.
2. Convert the PCD files to depth images by running `python -m utils.dataset_processing.generate_cornell_depth <Path To Dataset>`

### Jacquard Dataset

You will need to download both AJD and original Jacquard Dataset.
[AJD](https://www.dropbox.com/sh/nikrxio9mbkxpub/AADpt-6MKbZFEO8wCmbT1Y3xa?dl=0) can be downloaded here.
[Jacquard Dataset](https://jacquard.liris.cnrs.fr/) can be downloaded from their official website.

## Training
Path provided in the command line is used for reference. You will need to modify it based on your dataset structure.
```bash
# Train GG-CNN on Cornell Dataset with image-wise split
python train_ggcnn_imagewise.py --description cornell_imagewise --network ggcnn --dataset cornell --dataset-path ../../Dataset/Cornell/

# Train GG-CNN on Cornell Dataset with object-wise split
python train_ggcnn_objectwise.py --description cornell_objectwise --network ggcnn --dataset cornell --dataset-path ../../Dataset/Cornell/

# Train GG-CNN on AJD Datset
python train_ggcnn_ajd.py --dataset jacquard --description ajd --network ggcnn --dataset_pth_ajd_train ../../Dataset/Jacquard/coco/512_cnt_angle/train/grasps_train2018 --dataset-path-ajd-test ../../Dataset/Jacquard/coco/512_cnt_angle/test/grasps_test2018/ --dataset-path ../../Dataset/Jacquard/original
```

Trained models are saved in `output/models` by default, with the validation score appended.

## Evaluation/Visualisation
Path provided in the command line is used for reference. You will need to modify it based on your dataset structure.
```bash
# Test GG-CNN on Cornell Dataset with image-wise split
python eval_ggcnn_imagewise.py --network <Path to Trained Network> --dataset cornell --dataset-path ../../Dataset/Cornell/ --iou-eval

# Test GG-CNN on Cornell Dataset with object-wise split
python eval_ggcnn_objectwise.py --network <Path to Trained Network> --dataset cornell --dataset-path ../../Dataset/Cornell/ --iou-eval

# Test GG-CNN on AJD
python eval_ggcnn_ajd.py --network <Path to Trained Network> --dataset jacquard --dataset-path ../../Dataset/Jacquard/original --iou-eval --dataset-
path-ajd-test ../../Dataset/Jacquard/coco/512_cnt_angle/test/grasps_test2018/
```


