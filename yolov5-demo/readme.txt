*用yolo格式下标签生成的.txt
1.训练集放置
#voc格式的yolo训练数据集
├── datasets    #数据集文件夹名
│   ├── labels		#数据集标签划分
│   │    └── train
│   │         ├── ~0.txt
│   │          :
│   │         └── ~5.txt
│   │     └── val
│   │         ├── ~0.txt
│   │          :
│   │         └── ~5.txt
│   ├── images		#数据集图片划分
│   │    └── train
│   │         ├── ~0.jpg
│   │          :
│   │         └── ~5.jpg
│   │     └── val
│   │         ├── ~0.jpg
│   │          :
│   │         └── ~5.jpg

labels文件夹下写着用于训练和验证图片标签
images文件夹下放着训练和验证图片

2.添加配置文件
cp data/coco128.yaml data/~.yaml
添加
# Train/val/test sets as 1) dir: path/to/imgs, 2) file: path/to/imgs.txt, or 3) list: [path/to/imgs1, path/to/imgs2, ..]
path: /root/yolov5_demo/datasets  # dataset root dir
train: images/train  # train images (relative to 'path')
val: images/val  # val images (relative to 'path')
test:  # test images (optional)

# Classes
nc: ~  # number of classes
names: ['labels']  # class names //your labels

3.下载yolov5权重文件.pt

4.开始训练
python3 train.py --weights yolov5s.pt --data data/~.yaml --workers 1 --batch-size 8 
*可在train.py中调整训练参数

5.训练完成后将runs/exp/weights下的模型（best.pt）复制在yolov5文件夹下

5.开始检测
python detect.py --weights best.pt --source ../datasets/images/val 
--weights为训练好的权重 --source 为测试集路径

6.利用工具将.pt模型转为其他模型

---https://netron.app/
----查看模型