
## 环境

1. label
- anylabelimg,labelme,labelimg
- [anylabeling](https://github.com/vietanhdev/anylabeling)
- 
2. onncx
- python3.8, cudatoolkit11.3.1, cudnn8.2.1, onnxruntime-gpu1.14.1
[onnxruntime配置](https://blog.csdn.net/weixin_45303602/article/details/132642257)
3. torch
```bash
# linux
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```
4. yolo

[pytorch模型转onnx，tensorRT部署](https://zhuanlan.zhihu.com/p/642337184)

## 数据集

常见格式
1. yolo
2. coco
3. voc
4. json

### 转换脚本
```python
import json
import os
# 读取json文件
def read_json(json_file):
    with open(json_file,'r') as f:
        load_dict = json.load(f)
    f.close()
    return load_dict

# 读取txt文件中的类
def read_classes(txt_file):
    classes_dict={}
    with open(txt_file,'r') as f:
        classes = f.read().splitlines()
        for i, item in enumerate(classes): 
            # print(i, item)
            classes_dict[i] = item
    return classes_dict

# 定义一个函数，用于将json数据转换为yolo格式
# 参数：json_data：json格式的数据；classes_dict：类别字典
# 返回：转换后的yolo格式的数据
def json_yolo(json_data,classes_dict):
    L=[]
    imageHeight,imageWidth = json_data["imageHeight"],json_data["imageWidth"]
    for i, item in enumerate(json_data['shapes']):  
        # print(i,item)
        # 矩形框
        if  item['shape_type']=="rectangle": 
            label = item['label']
            x1 = item['points'][0][0]
            x2 = item['points'][1][0]
            y1 = item['points'][0][1]
            y2 = item['points'][1][1]
            # print(x1,x2,y1,y2)
            #将标注框按照图像大小压缩
            x_center = (x1+x2)/2/imageWidth
            y_center = (y1+y2)/2/imageHeight
            bbox_w = (x2-x1)/imageWidth
            bbox_h = (y2-y1)/imageHeight
            bbox = (x_center,y_center,bbox_w,bbox_h)
            # 遍历classes_dict，查找value等于label的key，并将其赋值给index
            for key, value in classes_dict.items():
                if value == label:
                    index = key
            # print(index,x_center,y_center,bbox_w,bbox_h)
            L.append([index,x_center,y_center,bbox_w,bbox_h])
    return L
    

classes_dict = read_classes("classes.txt")
json_data = read_json("bus.json")
L = json_yolo(json_data,classes_dict)

with open("labels/bus0.txt","w") as f:
    for i,item in enumerate(L):
        for k in item:
            f.write(str(k))
            f.write(" ")
        f.write("\n")
```

[开源数据集大汇总](https://zhuanlan.zhihu.com/p/508022823)


https://t.zsxq.com/0bHMNbi6T

http://ip111.cn/