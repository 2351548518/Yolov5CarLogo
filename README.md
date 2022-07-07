## **一、题目内容和要求：**

车标检测与识别主要对视频和图像中车辆标识进行分辨，在智能交通系统、车辆追踪、车辆管理等方面具有重要的应用价值。传统车标识别方法主要包括两大级联模块，首先是定位车标，可通过车牌位置、车前脸排气扇水平、垂直边缘特征实现定位；其次是对车标进行识别，识别过程可通过模板匹配及边缘检测等技术完成。此外，车标识别也可基于深度学习方法实现。

**实现要求**：

1) 具体方法、算法、模型的选择不受限制；

2) 识别的车标类别在5类以上；

3) 车标数据可以采用公开数据集，也可自建，但要求数据集多样化、例如多尺度、多分辨率、背景多样、包含噪声等；

4) 要达到一定的识别正确率； 

## **二、问题背景和相关工作介绍**

基于视频的车辆信息的检测和识别是智能交通系统的一个重要分支，而车标作为车辆的一个重要信息，具有显著和不易更换的特点，因此其检测和识别具有重要意义。实际生活中单靠车牌的识别不能完全准确确认车辆身份，正确识别车标有助于车辆身份的确认，因此对于车标的准确快速识别在套牌车识别、车辆布控查询、车辆章逃逸等方面有广泛的应用。

目前对车标识别技术的研究一般分为定位和识别两部分。

对于车标定位算法，其中较为普遍的定位算法是两步定位法，即车标的粗定位和精定位。李哲等［2］ 利用车牌与车标相对位置关系对车标进行粗定位，再利用投影方法进行车标精定位；杨正云等［3］ 利用Sobel算子和Shen算子对车牌进行定位，然后利用车牌与车标的相对位置确定车标大概位置，再利用纹理特征对车标精定位；李熙莹等［4］ 根据散热器栅格背景的纹理信息对车标进行精确定位；张闯等［5］在 HSV（Hue，Saturation，Value）下使用滤镜定位车牌位置来粗定位车标，然后运用垂直投影法分割并分离出车标图像。这些方法定位过程繁琐，受车型、环境影响较大，定位速度慢且精度低。对于车标识别的算法主要有模板匹配算法、传统的机器学 习 方 法 和 基 于 卷 积 神 经 网 络（Convolutional NeuralNetwork，CNN）的深度学习方法。李哲等［6］ 采用改进的方向梯度直方图（Histogram of Oriented Gradient，HOG）特征和局部 二 值 化 特 征 作 为 联 合 特 征 ，训 练 反 向 传 播（BackPropagation，BP）神经网络分类器来识别车标；耿庆田等［7］利用 尺 度 不 变 特 征 变 换（Scale-Invariant Feature Transform，SIFT）算子对图像的视角、平移、放射、亮度、旋转等不变特性进行提取，并采用 BP 神经网络算法自主选取车标图像特征进行分类、匹配和识别；张硕［8］ 利用 Adaboost 算法训练出各种车标分类器，并将各种车标分类器组合在一起，实现车标的识别。上述方法使用 HOG、SIFT 等机器学习提取图像特征，使用支持向量机（Support Vector Machine，SVM）、BP 神经网络等分类器进行识别，该方法可识别较多类车标，但是对误识别的车标无法判断，且识别率与训练样本数量、种类密切相关。Huang等［9］ 采用基于卷积神经网络模型的方法对车标进行分类，利用主成分分析提高了车标的识别精度和速度，但是出现前期训练时间过长且对于未知品牌的车标不可识别的问题，而且受车标种类密度影响较大；叶玉双等［10］使用基于 OpenCV 模板匹配和边缘检测技术来解决识别的任务，该方法有较高的识别精度，但需要车标较为清晰，不适

用于交通道路中的车标识别。

Yue Huang 等使用 CNN 来进行车标的检测和识别，提升 了识别的准确性和鲁棒性，与此同时，通过使用一种高效的预训练策略，降低了在使用 CNN 时所需的高计算花费。 Redmon提出的 YOLO 算法，在保证

检测精度优良的情况下， 依然能够将检测速度提升到 45 FPS。 基于此，可以利 用 YOLO 来进行车辆信息检测，比如 车 标 检 测和识别、车身颜色识别和车辆检测，也可以将车辆检测的结果作为跟踪器的观测值，进而进行多车辆跟踪。

本文的工作是，基于 YOLOv5+StrongSORT，完成车标识别工作。

>[1] [基于最小二乘法拟合的Otsu快速图像分割方法](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=JSSY202101011&dbcode=CJFD&dbname=CJFDTEMP&v=LmjLkIT_JUEfygi17kxWZLxXr61G5Xkb-Z0Nj9ULZ-pUbtsHw5MaJINbC8htRS7H)[J]. 徐建东. 常州大学学报(自然科学版). 2021(01)
>
>[2] [基于MFC+opencv的车标识别系统](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=JSJS202012002&dbcode=CJFD&dbname=CJFDTEMP&v=UOvkzvZkG40SRFNkaO75J3jsSqqKp7yRcwQq1QgSkc2zdzZdnWup1Zn_P-QGJNr_)[J]. 叶玉双,杨洁. 计算机时代. 2020(12)
>
>[3] [OPENCV在汽车车标识别中的研究与实践](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=FJDN202011002&dbcode=CJFD&dbname=CJFDTEMP&v=DragDv1JruoFwyK3umBaS-M5-UGusMWqbdVewxskjISGIAA2d-XUA7pPbQZ4jc8U)[J]. 张闯,王景龙. 福建电脑. 2020(11)
>
>[4] [基于Kittler最小误差分割算法的小视场星图分割](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=XNJT202101022&dbcode=CJFD&dbname=CJFDTEMP&v=huNtCaRtGDVVINLhlpikueaV5O2W5tp4IGMvTJ3u_A1j1XoMXj2gsYerwwW_Wt6Q)[J]. 时春霖,杨培章,张超,杜兰,叶凯,范承啸,李建,祖安然. 西南交通大学学报. 2021(01)
>
>[5] [基于MATLAB的边缘检测算法研究](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=DBCH202002055&dbcode=CJFD&dbname=CJFDTEMP&v=X4lp2MpjTa0rrpUIGz4yOwBQAj4e6HkSJKeij1ruvABte17uAJYC3hK6fEEATZZh)[J]. 田梦娜,徐泮林,丁鹏文. 测绘与空间地理信息. 2020(02)
>
>[6] [基于改进的HOG与LBP特征值的车标识别方法](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=JSSG201912041&dbcode=CJFD&dbname=CJFDTEMP&v=eupiAATKazyQSIOrJiifyQ0PP-iELLWlJRfHJ1zKbLf50beZOAzVvhsZT_0FAHrZ)[J]. 李哲,于梦茹. 计算机与数字工程. 2019(12)
>
>[7] [基于多种LBP特征集成学习的车标识别](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=JSGG201920020&dbcode=CJFD&dbname=CJFDTEMP&v=M9qWRE8bApiXMD1roxrHYObTdmISCG7D2a7so40n3d00bMv4s5p6fFfQtK8QlURW)[J]. 李哲,于梦茹. 计算机工程与应用. 2019(20)
>
>[8] [反馈式ICM神经网络和FPF相结合的剪影识别](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=GXKZ201803026&dbcode=CJFD&dbname=CJFDTEMP&v=SplwkblymQuPLrUUETAPwzgUiPM2KNU55-9CrzTvWOmDEi8R_Jw1X-yehZ1LhjtW)[J]. 李迪,徐光柱,王亚文,雷帮军,邹耀斌,夏平. 广西大学学报(自然科学版). 2018(03)
>
>[9] [基于SIFT的车标识别算法](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=JLDX201803029&dbcode=CJFD&dbname=CJFD2018&v=98zYOz-MI94XylBV4PYSYTB82lxwRbWCiCyKx_lms9M3C0_FidYF_cH6emumfQW_)[J]. 耿庆田,于繁华,王宇婷,赵宏伟,赵东. 吉林大学学报(理学版). 2018(03)
>
>[10] [基于散热器栅格背景精确分类的车标定位方法](https://webvpn.hfut.edu.cn/https/77726476706e69737468656265737421fbf952d2243e635930068cb8/kcms/detail/detail.aspx?filename=JSGG201702038&dbcode=CJFD&dbname=CJFD2017&v=ViHbkhBu832NcwyAlBjo4gE2MzIEmrX-1BFZY87szvUkc1IsCvJRiPz-4ZUpJOcF)[J]. 李熙莹,吕硕,袁敏贤,江倩殷,余志. 计算机工程与应用. 2017(02)



## **三、解题思路**

简述：

1. 制作数据集
2. 利用YOLOv5进行训练
3. 改进

详述：

1. ### 制作数据集

   车标数据的获取是整个识别过程的根基。

   下图简要描述了车标识别研究中的现存数据库。显然，它们各自存在着一些问题，包括数据规模偏小、车标种类少、成像环境较单一、仅含车标区域样本、公开性较差。大部分工作所使用的样本数为几百到几千不等; 虽然文献［8］包含一万余个样本，其中却只有 1 000 个是真实拍摄所得，其余则由数据增广等手段获取。文献［13］公布了目前最大的数据库 HFUT － VL，但32 000 幅图像均为车标或其附近限定区域，由此建立的车标识别模型对真实场景的适用性不强; 文献［7 －9，16，19］同样存在这一局限性( 如图 6 所示) 。LPＲ 库［11］提供了自然场景下的车辆数据，但部分样本不具有车标区域。[10]

   ![image-20220707174604813](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207071746889.png)

   

   > 自然场景车标数据集的构建及其应用 邹北骥,雷太航，刘 姝，廖望旻，姜灵子 中南大学  (2019JJ50808)

   因此，本文构建了一个有标注的、自然场景和其他场景混合的数据集，所有图片均来自于必应搜图，并标注了车标位置和类别。

   数据标注采用VOC2007格式进行分类，标签格式采用YOLO格式，标注工具采用labelimg。

   整体数据集共有500张图片，分辨率各不相同，并且考虑了多种场景，数据集共有10个类别，选取了HFUT-VL中的前十个类别作为收集对象['Benz', 'Buick', 'Citroen', 'FAW', 'Fukude', 'Honda', 'Hyundai', 'KIA', 'Lexus', 'Mazda']，每一类共有50张图片，数据集挺小的，可以想到训练结果不会很好。

   ![image-20220707175255769](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207071752246.png)

   ![image-20220707175358305](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207071753369.png)

   ![image-20220707175412748](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207071754167.png)

2. ### 基于 YOLOV5 车标识别算法流程

   目前使用深度学习进行的目标检测算法已经非常的成熟，其中目标检测算法有单阶段和双阶段两种主流方法。目前使用最多的为单阶段方法，能以较高的准确率同时实现实时检测的效果。其中YOLO系列算法是单阶段目标检测的开山之作也是代表作。本项目选择YOLO系列中在2021年发行的YOLO v5版本来实现实时的车标检测。

   YOLO系列是典型的目标检测算法，被广泛运用于目标跟踪任务。包含了多层卷积操作提取目标特征，分别输入至分类网络和检测网络得到目标的类别信息和坐标信息，通过与训练集标签中的类别和坐标进行对比，不断更新网络参数，以提升特征提取能力和网络的预测准确性。其中YOLO v5是一个较为新颖的检测网络模型，整个计算过程可分为四个模块：图像输入、骨干网络、颈部网络和预测输出。

   YOLOV4出现之后不久，YOLOv5横空出世。YOLOv5在YOLOv4算法的基础上做了进一步的改进，检测性能得到进一步的提升。虽然YOLOv5算法并没有与YOLOv4算法进行性能比较与分析，但是YOLOv5在COCO数据集上面的测试效果还是挺不错的。大家对YOLOv5算法的创新性半信半疑，有的人对其持肯定态度，有的人对其持否定态度。在我看来，YOLOv5检测算法中还是存在很多可以学习的地方，虽然这些改进思路看来比较简单或者创新点不足，但是它们确定可以提升检测算法的性能。其实工业界往往更喜欢使用这些方法，而不是利用一个超级复杂的算法来获得较高的检测精度。本文将对YOLOv5检测算法中提出的改进思路进行详细的解说，大家可以尝试者将这些改进思路应用到其它的目标检测算法中。

   2.1[YOLOv5](https://so.csdn.net/so/search?q=YOLOv5&spm=1001.2101.3001.7020)算法简介

   YOLOv5是一种单阶段目标检测算法，该算法在YOLOv4的基础上添加了一些新的改进思路，使其速度与精度都得到了极大的性能提升。主要的改进思路如下所示：

   输入端：在模型训练阶段，提出了一些改进思路，主要包括Mosaic数据增强、自适应锚框计算、自适应图片缩放；
   基准网络：融合其它检测算法中的一些新思路，主要包括：Focus结构与CSP结构；
   Neck网络：目标检测网络在BackBone与最后的Head输出层之间往往会插入一些层，Yolov5中添加了FPN+PAN结构；
   Head输出层：输出层的锚框机制与YOLOv4相同，主要改进的是训练时的损失函数GIOU_Loss，以及预测框筛选的DIOU_nms。

   #### 2.1.1 YOLOv5网络架构

   Yolov5s网络是Yolov5系列中**深度最小**，特征图的**宽度最小**的网络。后面的3种都是在此基础上不断加深，不断加宽。

   ![image-20220707200218754](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072002838.png)

   ### 2.2 Yolov5核心基础内容

   Yolov5的结构和Yolov4**很相似**，但也有一些不同，分为**输入端、Backbone、Neck、Prediction**四个部分。

   ![preview](https://pic1.zhimg.com/v2-770a51ddf78b084affff948bb522b6c0_r.jpg)

   它和Yolov3的一些主要的不同点，并和Yolov4进行比较。

   **（1）输入端：**Mosaic数据增强、自适应锚框计算、自适应图片缩放
   **（2）Backbone：**Focus结构，CSP结构
   **（3）Neck：**FPN+PAN结构
   **（4）Prediction：**GIOU_Loss

   Yolov5作者的算法性能测试图：

   ![img](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072006079.png)

   YOLOv5-P5 640 Figure (click to expand)

   ![img](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072006025.png)

   Yolov5s网络最小，速度最快，追求速度，对于实时的车标识别是个不错的选择。其他的三种网络，在此基础上，不断加深加宽网络，AP精度也不断提升，但速度的消耗也在不断增加。

   ### 2.3 输入端

   #### 2.3.1 **Mosaic数据增强**

   Yolov5的输入端采用了和Yolov4一样的Mosaic数据增强的方式。**随机缩放**、**随机裁剪**、**随机排布**的方式进行拼接，对于小目标的检测效果还是很不错的。

   ![preview](https://pic2.zhimg.com/v2-641bd9a5f9fc0517a7f315d1e4734d19_r.jpg)

   

   #### 2.3.2**自适应锚框计算**

   在Yolo算法中，针对不同的数据集，都会有**初始设定长宽的锚框**。

   在网络训练中，网络在初始锚框的基础上输出预测框，进而和**真实框groundtruth**进行比对，计算两者差距，再反向更新，**迭代网络参数**。

   因此初始锚框也是比较重要的一部分，比如Yolov5在Coco数据集上初始设定的锚框：

   ![img](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072012193.jpeg)

   

   在Yolov3、Yolov4中，训练不同的数据集时，计算初始锚框的值是通过单独的程序运行的。

   但Yolov5中将此功能嵌入到代码中，每次训练时，自适应的计算不同训练集中的最佳锚框值。

   #### 2.3.3 **自适应图片缩放**

   在常用的目标检测算法中，不同的图片长宽都不相同，因此常用的方式是将原始图片统一缩放到一个标准尺寸，再送入检测网络中。

   比如Yolo算法中常用**416\*416，608\*608**等尺寸，比如对下面**800\*600**的图像进行缩放。

   ![preview](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072013036.jpeg)

   但**Yolov5代码**中对此进行了改进，也是**Yolov5推理速度**能够很快的一个不错的原因。

   作者认为，在项目实际使用时，很多图片的长宽比不同，因此缩放填充后，两端的黑边大小都不同，而如果填充的比较多，则存在信息冗余，影响推理速度。

   因此在Yolov5的代码中datasets.py的letterbox函数中进行了修改，对原始图像**自适应的添加最少的黑边**。

   ![image-20220707201507034](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072015173.png)

   图像高度上两端的黑边变少了，在推理时，计算量也会减少，即目标检测速度会得到提升。

   **第一步：计算缩放比例**

   ![img](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072016868.jpeg)

   

   原始缩放尺寸是416*416，都除以原始图像的尺寸后，可以得到0.52，和0.69两个缩放系数，选择小的缩放系数。

   **第二步：计算缩放后的尺寸**

   ![preview](https://pic3.zhimg.com/v2-2c9a77f1b484d49ce3beba9c70a2effe_r.jpg)

   

   原始图片的长宽都乘以最小的缩放系数0.52，宽变成了416，而高变成了312。

   **第三步：计算黑边填充数值**

   ![img](https://pic3.zhimg.com/80/v2-799a7cb6bb7e5994472f0162abc4cf02_720w.jpg)

   

   将416-312=104，得到原本需要填充的高度。再采用numpy中np.mod取余数的方式，得到8个像素，再除以2，即得到图片高度两端需要填充的数值。

   此外，需要注意的是：

   a.这里大白填充的是黑色，即**（0，0，0）**，而Yolov5中填充的是灰色，即**（114,114,114）**，都是一样的效果。

   b.训练时没有采用缩减黑边的方式，还是采用传统填充的方式，即缩放到416*416大小。只是在测试，使用模型推理时，才采用缩减黑边的方式，提高目标检测，推理的速度。

   c.为什么np.mod函数的后面用**32**？因为Yolov5的网络经过5次下采样，而2的5次方，等于**32**。所以至少要去掉32的倍数，再进行取余。

   ### 2.4Backbone

   #### 2.4.1 **Focus结构**

   ![preview](https://pic3.zhimg.com/v2-5c6d24c95f743a31d90845a4de2e5a36_r.jpg)

   

   

   Focus结构，在Yolov3&Yolov4中并没有这个结构，其中比较关键是切片操作。

   比如右图的切片示意图，4*4*3的图像切片后变成2*2*12的特征图。

   以Yolov5s的结构为例，原始608*608*3的图像输入Focus结构，采用切片操作，先变成304*304*12的特征图，再经过一次32个卷积核的卷积操作，最终变成304*304*32的特征图。

   **需要注意的是**：Yolov5s的Focus结构最后使用了32个卷积核，而其他三种结构，使用的数量有所增加，先注意下，后面会讲解到四种结构的不同点。

   #### 2.4.2**CSP结构**

   Yolov4网络结构中，借鉴了CSPNet的设计思路，在主干网络中设计了CSP结构。

   ![preview](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072023310.jpeg)

   Yolov5与Yolov4不同点在于，Yolov4中只有主干网络使用了CSP结构。

   而Yolov5中设计了两种CSP结构，以**Yolov5s网络**为例，**CSP1_X结构**应用于**Backbone主干网络**，另一种**CSP2_X**结构则应用于**Neck**中。

   ![preview](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072024742.jpeg)

   

   

   #### 2.4.3Neck

   Yolov5现在的Neck和Yolov4中一样，都采用FPN+PAN的结构，但在Yolov5刚出来时，只使用了FPN结构，后面才增加了PAN结构，此外网络中其他部分也进行了调整。

   Yolov5和Yolov4的不同点在于，Yolov4的Neck结构中，采用的都是普通的卷积操作。而Yolov5的Neck结构中，采用借鉴CSPnet设计的CSP2结构，加强网络特征融合的能力。

   ![preview](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072025980.jpeg)

   

   ### 2.5 输出端

   #### 2.5.1**Bounding box损失函数**

   Yolov5中采用其中的CIOU_Loss做Bounding box的损失函数。

   ![preview](https://pic3.zhimg.com/v2-9a11f74c96cb3470e536b05bcb662db2_r.jpg)

   Yolov4中也采用CIOU_Loss作为目标Bounding box的损失。

   ![preview](https://pic4.zhimg.com/v2-cbf40db4e99e04d739fbded43cab925f_r.jpg)

   #### 2.5.2 mAP 目标检测算法的评估指标

   评价一个检测算法，主要看两个标准：第一，是否正确预测了框内的物体；第

   二，预测框和人工标注的框的重合程度。这两个标准的量化指标分别是 mAP（mean Average Precision）和 IOU（Intersection Over Union）。IOU 交并比，用来衡量预测的物体框和真实框的重合程度，即模型计算产生的目标窗口与原来标记窗口的交叠率，如图 3-9 所示。

   ![image-20220707205632028](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072056077.png)

   

   利用 IOU，可以分辨检测结果是否正确，最常用的阈值是 0.5，当 IOU 大于0.5，认为这是一个正确检测，否则认为是错误检测。利用算法模型生成的每一个检测框计算其 IOU 值，及设定的 IOU 阈值（如 0.5）进行比较，可以为每一个类计算其正确检测的数量。对于每一张图片，通过标准参考数据，可以得到图片中某个特定类别的真实目标数量(B)，通过算法计算的预测数量(A)(True Postives)，计算模型对该类别的精确率(A/B)。即给定图片中类别 C 的精确率=图片中类别 C 的真正类数量/图片中类别C 所有目标的数量

   ![image-20220707205745940](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072057976.png)

   对于一个给定的类别，对验证集中每张图片都计算它的精确率，例如验证集中共 100 张图片，每张图片都包含所有类别。这样对于每个类别都会有 100 个精度率的值。对这 100 个值进行平均，叫做该类的平均精度(Average Precision)

   ![image-20220707205949567](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072059603.png)

   

   假设预测数据集中有 20 个类别，对于每一个类别，执行相同的操作，计算 IOU、精确率(Precision)和平均精度(Average Precision)，会得到 20 个不同的平均精度值。利用这些平均精度值，可以判断模型对任何给定的类别的性能。只用一个度量指标来说明结果，可以很直观的看到算法的效果，并容易对效果进行对比，对所有类别的平均预测精度值计算平均值(average/mean)，只用一个数字表示一个计算模型的性能，可以采用平均精度均值 mAP(Mean Average Precision)

   ![image-20220707210024081](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072100117.png)

   mAP 的内部含义为，平均精度均值=所有类别的平均经度值之和/所有类别的数量。平均精度均值是数据集中所有类别的平均精度的均值，mAP 总是在固定的数据集上进行计算，它不是量化模型输出的绝对度量，它是一个相对不错的相对度量。当在公开数据集上计算这个度量的时，它可以很容易地被用来比较目标检测新老方法的性能好坏。由于训练集中的类别较多，各类的分布情况并不完全相同，导致各类别的训练数据不一致，平均精度值可能对于某些类别非常高，个别类别非常低。当 mAP 值可能看上去不错，但是模型只是对个别类别较好，其他类别较差，所以通过分析模型的 AP 统计结果，对平均精度值较低的类别，需要添加更多的训练样本。

   

   

   

   

   

   

   #### 2.5.3 **nms非极大值抑制**

   在目标检测的后处理过程中，针对很多目标框的筛选，通常需要nms操作。

   因为CIOU_Loss中包含影响因子v，涉及groudtruth的信息，而测试推理时，是没有groundtruth的。

   所以Yolov4在DIOU_Loss的基础上采用DIOU_nms的方式，而Yolov5中采用加权nms的方式。

   非极大抑制算法(Non-Maximum Suppression，NMS)，在经过目标检测算法对

   图片根据默认中心点和默认框进行扫描后，得到很多指向同一个物体的多个预测

   框，基本所有目标检测都会用到这个方法，实验最终只需要一个与目标检测物体最

   匹配的框，NMS 的本质是搜索局部最大值，抑制非极大值元素。利用非极大抑制

   算对车标进行定位的效果图如图 3-10 所示。

   ![image-20220707210142961](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072101019.png)

   NMS 的计算流程如下：

   扫描图像得到所有目标检测结果定义为集合 A，及各个区域对应检测物体种类的置信度；

   查找集合 A 某一目标种类置信度最高的区域框 a，从集合 A 中移除；

   计算集合 A 中剩余此类预测目标的区域框，与 a 之间的重叠率，若大于一定

   的阈值则认为此区域框与 a 是检测的同一物体，并将起移除；

   依次遍历完成后，将 a 加入最终检测结果集合 PreA；

   每个预测种类重复步骤 2 到步骤 4，直到集合 A 为空值；

   输出最终的预测结果 PreA。

   NMS 算法函数有 Liner NMS 和 Gaussian NMS：

   ![image-20220707210225958](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072102991.png)

   

   公式参数说明如下：

   Si 预测目标区域框分值；

   M 具有最大得分数据的预测框；

   bi 原始预测框中第 i 个预测框，i=1，2，3...； 

   N 为设定的 IoU 阈值；

   б尺度参数，本实验为 0.5； 

   D 最终预测框集合。

   车标识别计算过程中，阈值设置为 0.7。Liner NMS 对与 IoU 大于等于 0.7 的

   包围框进行得分数衰减，对于 IoU 小于 0.7 的保持原有分值；Gaussian NMS 则采

   用惩罚机制，对于所有包围框 IoU 越大，惩罚因子越大，得分相对越低。如果目标

   识别过程中图像有近距离重叠现场，可使用柔性非极大抑制算法（Soft-NMS），本

   实验中的车标都在车身上，车标之间由于车身间隔原因，不会发生近距离重叠现象，

   所以没有采用柔性非极大抑制算法。

   

   

   ### 整体流程

   首先，在输入过程中，将图像进行随机缩放、随机裁剪、随机排布的方式进行拼接，以达到扩充训练数据集的目的。

   ![train_batch0](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072032100.jpg)

   接着，在骨干网络中，将车辆图像进行切片操作，输入至Focus结构，得到多个图像子图，对多个子图分别进行卷积操作，得到中间特征图。中间特征图会通过多个CSP结构，将中间特征进行多层次的残差连接，结合BN层归一化操作以及LeakyRelu激活函数引入非线性，目的是为了提取出包含更多语义信息的特征图输入至颈部网络。

   进一步地，颈部网络使用CSP2结构，结合特征金字塔结构多尺度融合车标特征信息，以提升网络特征的融合能力。

   最后，网络的预测输出分为边界框和标签分类，边界框对应车标的位置信息，通过原始训练集中的标定的边界框坐标，与网络输出的边界框坐标进行损失计算，通过损失函数得到的结果，使用深度学习的反向传播机制更新网络权重参数。同样的，标签分类是将边界框中的车辆图像输入至分类网络，多次使用卷积操作提取车辆图像特征，最后使用Softmax函数得到网络预测概率最大的车辆类别，与训练集标签对比，进行损失函数计算，更新分类网络权重信息。需要说明的是，网络参数需要经过多次训练更新，以达到最佳的表现性能，预测出正确的车标位置信息以及分类结果。 

   

3. ### 分析问题性，进行下一步改进

   由于选用的数据集太少，对车标的分类不准确，所以采用双段式结构，使用yolov5进行车标位置的识别，再使用训练好的CNN进行车标类别的识别。

   



## **四、算法伪代码**



## **五、实验设置**

本实验测试及验证硬件环境主要参数：

AMD 4800H CPU、NVIDIA GeForce RTX 2060laptop 型 GPU 显卡，显存 6G。

软件环境主要参数：

Windows 10 操作系统，PyCharm2022.1.3 集成开发环境，基于 Anaconda2021.3 的 Python 3.9 编程环境，本文所有算法是在 PyTorch1.10.0 深度学习框架完成的，Torch 是一个用于机器学习和科学计算的模块化开源库，PyTorch 在 Python 中重新设计和实现了 Torch，同时在后端代码中共享了相同的核心 C 库。 它不是一种Python 语言绑定，而被作为 Python 的一个完整部分。PyTorch 将它的所有功能都构建为 Python 类，PyTorch 代码能够与 Python 函数和其他 Python 包无缝集成。PyTorch 适合开发人员调节其后端代码，来高效运行 Python。使用 YOLOV4目标检测模型并完成对模型的训练和验证，同时使用 CUDA11.7 进行并行计算，CUDNN 深度神经网络加速库.采用 TensorboardX  进行查看识别的训练趋势图。

![image-20220707211453540](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072114581.png)

## **六、实验结果**

### 6.1对图片进行识别

![image-20220707211701438](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072117543.png)

可见能够正常识别出来的车标并准确预测。

### 6.2对视频进行识别

https://1drv.ms/v/s!AlnEs35oV25UlIZYb2LfoSMx7RVNkQ?e=oalQOn 视频已经上传到云盘，可以查看。

![image-20220707211900067](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072119208.png)

### 6.3**混淆矩阵分析**

![confusion_matrix](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072123418.png)

### 6.4 F1_curve

![F1_curve](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072123240.png)

### 6.5 PR曲线

![PR_curve](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072124599.png)

### 6.6  训练结果

![results](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072125063.png)

![image-20220707212644191](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072126282.png)

![image-20220707212656744](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072126942.png)

## **七、实验结果分析**

### 7.1 结果分析

#### 7.1.1 PR曲线分析

**PR曲线实则是以precision（精准率）和recall（召回率）这两个为变量而做出的曲线，其中recall为横坐标，precision为纵坐标。**

![img](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072130764.webp)

注：**把正例正确地分类为正例，表示为TP（true positive），把正例错误地分类为负例，表示为FN（false negative）。
 把负例正确地分类为负例，表示为TN（true negative）， 把负例错误地分类为正例，表示为FP（false positive）。**

一个阈值对应PR曲线上的一个点。通过选择合适的阈值，比如50%，对样本进行划分，概率大于50%的就认为是正例，小于50%的就是负例,从而计算相应的精准率和召回率。（选取不同的阈值，就得到很多点，连起来就是PR曲线）

如果一个学习器的P-R曲线被另一个学习器的P-R曲线完全包住，则可断言后者的性能优于前者，例如上面的A和B优于学习器C。但是A和B的性能无法直接判断，我们可以根据曲线下方的面积大小来进行比较，但更常用的是平衡点或者是F1值。平衡点（BEP）是P=R时的取值，如果这个值较大，则说明学习器的性能较好。而F1  =  2 \* P \* R ／( P + R )，同样，F1值越大，我们可以认为该学习器的性能较好。

![img](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072133671.webp)

根据得到的曲线，可以看出训练的还是相当不错的，起码对现在的数据集来说。

![image-20220707213619644](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072136704.png)

#### 7.1.2 map0.5 、map5.95 分析

**mAP@0.5：mean Average Precision（IoU=0.5）**

即将IoU设为0.5时，计算每一类的所有图片的AP，然后所有类别求平均，即mAP

IOU即置信度，目标检测评价函数，如下图所示，当真实框与我们的预测框完全没有相交的时候，IOU=0；当IOU=0.25时证明真实框与我们的预测框有相交部分，当IOU=1时则证明我们的预测框和真实框完全重合。

![img](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072144220.png)

**mAP@.5:.95（mAP@[.5:.95]）**
表示在不同IoU阈值（从0.5到0.95，步长0.05）（0.5、0.55、0.6、0.65、0.7、0.75、0.8、0.85、0.9、0.95）上的平均mAP。

![image-20220707214508959](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072145999.png)

由上图可知，map.5普遍再0.9左右，map5.95普遍在0.6左右，训练还可以。

### 7.2 过程分析

![image-20220707215657002](https://raw.githubusercontent.com/2351548518/images/main/20220608/202207072156051.png)

根据训练过程中的**精准率**可知，在前80epochs已经达到了最好。可能是因为数据集太少，导致训练很快，容易发生过拟合。

## **八、总结**

## **九、附录：算法源代码**

## l **感想、体会、建议∶**

