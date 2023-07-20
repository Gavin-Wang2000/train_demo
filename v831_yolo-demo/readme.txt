v831训练demo
0.配置环境
安装pytoch 			pip3 install torch torchvision torchaudio
安装torchsummary、pycocotools	pip3 install torchsummary pycocotools
安装 Opencv			pip3 install opencv-python opencv-contrib-python

1.训练集放置
#voc格式的yolo训练数据集
├── custom    #数据集文件夹名
│   ├── Annotations		#标注文件
│   ├── ImageSets		#训练参数划分
│   │    └── Main
│   │         ├── train.txt
│   │         └── val.txt/
│   ├── JPEGImages		#训练图片

train.txt 写着用于训练的图片名称
val.txt  写着用于验证的图片名称

2.修改 data/custom.py 中的 CUSTOM_CLASSES 变量为正确的 labels
~可修改 data/config.py中训练次数'max_epoch': 


3.开始训练
python3 train.py -d custom --cuda -v slim_yolo_v2 -hr -ms


4.导出模型
python3 test.py -d custom -v slim_yolo_v2 --trained_model weights/custom/slim_yolo_v2/slim_yolo_v2_~.pth --visual_threshold 0.3 -size 224 --export
slim_yolo_v2_~.pth选择自己最佳的pt

5.导出out目录下的test测试效果和模型文件