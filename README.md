# 基于 YOLOv5 的火焰目标检测

本项目为《高级语言编程》课程小组作业，基于 YOLOv5 实现火焰目标检测。模型类别为 `fire`，可对图片中的火焰区域进行定位，并输出检测框、类别名称和置信度。

## 项目内容

- 使用 YOLOv5s 作为基础模型
- 使用火焰检测数据集进行迁移学习
- 类别数量：1
- 类别名称：`fire`
- 训练权重：`weights/best.pt`
- 支持单张图片检测、文件夹批量检测和验证集评估

## 仓库结构

```text
yolov5-fire-detection-github/
  README.md
  .gitignore
  yolov5/
    detect.py
    train.py
    val.py
    requirements.txt
    models/
    utils/
    data/
      fire.yaml
  weights/
    best.pt
  samples/
    images/
    labels/
  results/
    test_detected.jpg
    PR_curve.png
    confusion_matrix.png
  report/
    基于YOLOv5的火焰目标检测实验报告_修订版.docx
```

## 环境配置

进入 `yolov5` 目录：

```powershell
cd yolov5
```

安装依赖：

```powershell
python -m pip install -r requirements.txt
```

如果 pip 访问较慢，可以使用国内镜像：

```powershell
python -m pip install -r requirements.txt -i http://mirrors.aliyun.com/pypi/simple --trusted-host mirrors.aliyun.com
```

## 使用方法

检测样例图片：

```powershell
python detect.py --weights ../weights/best.pt --source ../samples/images/018c2fdb-c9e1-4653-b98f-07e226b62ae5.jpg
```

检测自己的图片：

```powershell
python detect.py --weights ../weights/best.pt --source "D:\desktop\test.jpg"
```

检测整个文件夹：

```powershell
python detect.py --weights ../weights/best.pt --source ../samples/images
```

验证模型：

```powershell
python val.py --weights ../weights/best.pt --data data/fire.yaml --img 640
```

## 实验结果

模型在验证集上的主要指标：

| 指标 | 数值 |
|---|---:|
| Precision | 0.684 |
| Recall | 0.643 |
| mAP@0.5 | 0.684 |
| mAP@0.5:0.95 | 0.334 |

检测结果示例见 `results/test_detected.jpg`。

## 文件说明

- `weights/best.pt`：训练得到的最佳模型权重。
- `yolov5/detect.py`：图片、视频、摄像头检测入口。
- `yolov5/train.py`：模型训练入口。
- `yolov5/val.py`：模型验证入口。
- `yolov5/data/fire.yaml`：火焰数据集配置文件。
- `report/`：课程实验报告。

## 说明

完整训练数据集未全部放入本仓库，仅保留少量样例图片和标签用于演示。若需要重新训练，请将完整数据集按以下结构放入 `yolov5/dataset`：

```text
dataset/
  images/train
  images/val
  labels/train
  labels/val
```

