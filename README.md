# AIcompetiton
Description of an AI Competition 



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

## 数据处理

详见data_process.ipynb

将原始数据集转换为ctrgcn需要的数据格式

三维数据（N，M，T，V，C）

二维数据（N，T，M，V，2）

由于我们主要使用的是三维数据，我们将x_vai,y_vai,x_train,y_train封装为模型所需的npz文件，保存在processed_data/joint/train/V1.npz，同时将x_test,y_test保存为processed_data/joint/test/V1.npz




## 模型选择
我们主要使用 https://github.com/liujf69/ICMEW2024-Track10.git 和https://github.com/ben0i0d/TE-GCN 的模型

我们使用joint数据集训练了tegcn模型，
使用joint、bone数据集，及其数据增强版本上训练了ctrgcn模型。

训练前要将**processed_data/joint/train/V1.npz**复制到**dataset/save_3d_pose**目录下

测试前要将**processed_data/joint/test/V1.npz**复制到**dataset/save_3d_pose**目录下



训练指令如下：



```sh
cd ./Model_inference/Mix_GCN
# train_joint
python main.py --config ./config/ctrgcn_V1_J_3d.yaml --device 0
# test_joint
python main.py --config ./config/ctrgcn_V1_J_3d.yaml --phase test --save-score True --weights ./output/ctrgcn_V1_J_3D/runs-39-9984.pt --device 0

# train_bone
python main.py --config ./config/ctrgcn_V1_B_3d.yaml --device 0
# train_bone
python main.py --config ./config/ctrgcn_V1_B_3d.yaml --phase test --save-score True --weights ./output/ctrgcn_V1_B_3D/runs-39-9984.pt --device 0
```



ctrgcn的训练结果见我们目录下的PT_model



## 集成学习
