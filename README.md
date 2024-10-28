# AIcompetiton
Description of an AI Competition 
## 数据处理
详见data_process.ipynb



## 数据增强
详见init_data_process.ipynb
在数据集中随机选取15%的数据进行x轴翻转
在数据集中随机选取15%的数据进行y轴翻转
在数据集中随机选取15%的数据进行水平移动翻转
在数据集中随机选取30%的数据进行旋转操作。
这里的各项参数选择如下：
水平移动（0，10）
x旋转（-30,30）
y旋转（-30,30）
z旋转（0,360）

## 模型选择
我们主要使用 https://github.com/liujf69/ICMEW2024-Track10.git和tegcn的模型

我们使用joint数据集训练了tegcn模型，
使用joint、bone数据集，及其数据增强版本上训练了ctrgcn模型。

训练指令如下：

cd ./Model_inference/Mix_GCN
python main.py --config ./config/ctrgcn_V1_J_3d.yaml --device 0
python main.py --config ./config/ctrgcn_V1_J_3d.yaml --phase test --save-score True --weights ./output/ctrgcn_V1_J_3D/runs-39-9984.pt --device 0

python main.py --config ./config/ctrgcn_V1_B_3d.yaml --device 0
python main.py --config ./config/ctrgcn_V1_B_3d.yaml --phase test --save-score True --weights ./output/ctrgcn_V1_B_3D/runs-39-9984.pt --device 0

训练结果见我们目录下的PT_for_Mix

## 集成学习
