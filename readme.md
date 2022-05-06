### 一、下载初始代码

创建工作目录

```
git clone https://github.com/hoitab/TFLClassify.git
```



### 二、运行初始代码

运行start模块

![image](https://github.com/IlIlIlIlIlIlIlIlIlIlIl/exp3/blob/main/TFLClassify/image/1.png?raw=true)



### 三、向应用中添加TensorFlow Lite

 右键“start”模块，或者选择File，然后New>Other>TensorFlow Lite Model 

 选择finish模块中ml文件下的FlowerModel.tflite自定义模型

导入成功， 生成摘要信息 

![image](https://github.com/IlIlIlIlIlIlIlIlIlIlIl/exp3/blob/main/TFLClassify/image/2.png?raw=true)



### 四、检查代码中的TODO项

 查看TODO列表视图，View>Tool Windows>TODO 

 默认情况下了列出项目所有的TODO项，进一步按照模块分组（Group By） 



### 五、添加代码重新运行APP

1、定位“start”模块**MainActivity.kt**文件的TODO 1，添加初始化训练模型的代码

```
// TODO 1: Add class variable TensorFlow Lite Model
  private val flowerModel = FlowerModel.newInstance(ctx)
```

2、定位“start”模块**MainActivity.kt**文件的TODO 2， 将摄像头的输入`ImageProxy`转化为`Bitmap`对象，并进一步转化为`TensorImage` 对象 

```
// TODO 2: Convert Image to Bitmap then to TensorImage
  val tfImage = TensorImage.fromBitmap(toBitmap(imageProxy))
```

3、定位“start”模块**MainActivity.kt**文件的TODO 3， 对图像进行处理 

按照属性`score`对识别结果按照概率从高到低排序

列出最高k种可能的结果，k的结果由常量`MAX_RESULT_DISPLAY`定义

```
// TODO 3: Process the image using the trained model, sort and pick out the top results
  val outputs = flowerModel.process(tfImage)
      .probabilityAsCategoryList.apply {
          sortByDescending { it.score } // Sort with highest confidence first
      }.take(MAX_RESULT_DISPLAY) // take the top results
```

4、定位“start”模块**MainActivity.kt**文件的TODO 4，将识别的结果加入数据对象`Recognition` 中，包含`label`和`score`两个元素，后续将用于`RecyclerView`的数据显示

```
// TODO 4: Converting the top probability items into a list of recognitions
  for (output in outputs) {
      items.add(Recognition(output.label, output.score))
  }
```

5、注释掉原先用于虚拟显示识别结果的代码 

```
// START - Placeholder code at the start of the codelab. Comment this block of code out.
for (i in 0..MAX_RESULT_DISPLAY-1){
    items.add(Recognition("Fake label $i", Random.nextFloat()))
}
// END - Placeholder code at the start of the codelab. Comment this block of code out.
```

6、以物理设备运行start模块

手机通过USB接口连接开发平台，并设置手机开发者选项允许调试

 允许应用获取手机摄像头的权限 

运行结果如下

![image](https://github.com/IlIlIlIlIlIlIlIlIlIlIl/exp3/blob/main/TFLClassify/image/3.png?raw=true)