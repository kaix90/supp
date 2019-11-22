# Learning in the Frequency Domain
Our work is based on [mmdetection](https://github.com/open-mmlab/mmdetection).
mmdetection is an open source object detection toolbox based on PyTorch. It is
a part of the open-mmlab project developed by [Multimedia Laboratory, CUHK](http://mmlab.ie.cuhk.edu.hk/).


## Prerequisites
* PyTorch compatible GPU
* Python 3.7
* PyTorch >= 1.2.0
* libjpeg-turbo 2.0.3
* [MMDetection](https://github.com/open-mmlab/mmdetection)

## Install
* Please refer to [INSTALL.md](docs/INSTALL.md) for installation and dataset preparation.
* Download pretrained [models][1] and extract to [`work_dirs`](work_dirs). The folder structure should look like this:
```
work_dirs
├── mask_rcnn_r50_fpn_1x_dct_24_wofreeze
│   ├── 20191029_145538.log
│   └── latest.pth
└── mask_rcnn_r50_fpn_1x_dct_64_wofreeze
    ├── 20191029_151515.log
    └── latest.pth
```

## Evaluation
Run [`test.py`](tools/test.py) to start testing

### Testing the proposed model with 24 channels 
```
python tools/test.py configs/mask_rcnn_r50_rpn_1x_DCT_static_24_wofreeze.py work_dirs/mask_rcnn_r50_fpn_1x_dct_24_wofreeze/latest.pth --out results.pkl --eval bbox segm
```

### Testing the proposed model with 64 channels 
```
python tools/test.py configs/mask_rcnn_r50_rpn_1x_DCT_static_64_wofreeze.py work_dirs/mask_rcnn_r50_fpn_1x_dct_64_wofreeze/latest.pth --out results.pkl --eval bbox segm
```
## Results

### Performance of the proposed model - ResNet-50-FPN
|       Backbone      | #Channels | Size Per Channel | bbox |        |         |      |      |      |
|:-------------------:|:---------:|:----------------:|:----:|:------:|:-------:|:----:|:----:|:----:|
|                     |           |                  |  AP  | AP@0.5 | AP@0.75 |  AP<sub>S</sub> |  AP<sub>M</sub> |  AP<sub>L</sub> |
| ResNet-50-FPN (RGB) |     3     |     800x1333     | 37.3 |  59.0  |   40.2  | 21.9 | 40.9 | 48.1 |
| [DCT-24 (ours)][2]  |     24    |      200x334     | 37.7 |  59.2  |   40.9  | 21.7 | 41.4 | 49.1 |
| [DCT-64 (ours)][3]  |     64    |      200x334     | 38.1 |  59.6  |   41.1  | 22.5 | 41.6 | 49.7 |

|       Backbone      | #Channels | Size Per Channel | mask |        |         |      |      |      |
|:-------------------:|:---------:|:----------------:|:----:|:------:|:-------:|:----:|:----:|:----:|
|                     |           |                  |  AP  | AP@0.5 | AP@0.75 |  AP<sub>S</sub> |  AP<sub>M</sub> |  AP<sub>L</sub> |
| ResNet-50-FPN (RGB) |     3     |     800x1333     | 34.2 |  55.9  |   36.2  | 15.8 | 36.9 | 50.1 |
| [DCT-24 (ours)][2]  |     24    |      200x334     | 34.6 |  56.1  |   36.9  | 16.1 | 37.4 | 50.7 |
| [DCT-64 (ours)][3]  |     64    |      200x334     | 35.0 |  56.5  |   37.4  | 16.9 | 37.6 | 51.6 |

[1]: https://drive.google.com/open?id=1UKmNORizsulH9E4awxjBR4fAlW1KlC5s
[2]: https://drive.google.com/open?id=14eTsI_LMjjQHyx_uOsb_DSy2pAIZFny-
[3]: https://drive.google.com/open?id=18WbbwpQuoAt--GMlZuWhNLjxN83A0g_i