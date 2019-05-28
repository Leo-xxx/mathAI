## 高数解题神器：拍照上传就出答案，这个中国学霸做的AI厉害了 | Demo

原创： 关注前沿科技 [量子位](javascript:void(0);) *前天*

##### 铜灵 晓查 发自 凹非寺 量子位 出品 | 公众号 QbitAI

一位叫Roger的中国学霸小哥的拍照做题程序**mathAI**一下子火了，这个AI，堪称数学解题神器。

输入一张包含手写数学题的图片，AI就能识别出输入的数学公式，然后给出计算结果。

不仅加减乘除基本运算，就连**高等数学**中的微积分都不在话下。

就像下面这样：

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KZ73nNoazyXlkmcGTUpU6eQPofCsJBEOiafRLptK5Kg3mXlP16eiaENVQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

还在苦苦纠结高数作业如何求解？还在东奔西走的找学霸借作业？手握mathAI，不就是手握了新时代的解题利器么！

短短几天时间，这个项目在微博就收获了上百次转发。看到画风如此新奇，似乎还能开启无限可能应用，网友们纷纷召唤自己的印象笔记小助手收藏，大呼：牛逼，以后教宝宝数学就是它了。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KQAdXfnJ63LhbUA3wafmskNtpcNCpibH5d2wnDNZzRKCoonN6SBRuHMQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

作者表示，这个项目已经是**半开源状态**了，目前开源的部分可以识别计算加减乘除简单运算。

如果想要识别更加复杂的表达式，可以参考数学公式识别的论文自己进行扩展。

具体来看看这个解题神器。

## 实现过程

全能型选手mathAI是怎么实现这个功能的？

作者在Github中介绍说，整个程序使用python实现，具体**处理流程**包括：图像预处理→字符识别→数学公式识别→数学公式语义理解→结果输出。

整个系统的处理流程如下：

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KQg5kdjia6Qbd42A3icQia55ib2bNu3Bfaib5pa1AEe23Xpn3aOv5NP9o20g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图片预处理主要以OpenCV作为主要工具，将图片中的字符单独切割出来，避免无关变量对字符识别的影响。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KJk9cYTNe7jLnBAjvqPuGFNH5QKzJTTUo9rmw7Pars8gN2yE46ibhJmQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

随后，国际数学公式识别比赛数据集（CROHME）对通过卷积神经网络进行训练。

此外，还进行结构分析，对字符的空间关系进行判定。比如一个字符的上标和下标，含义自然不一样。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KuiaWNuMJnjCJBTYPic9p4bYv4lQPfwhB2EzwZ6qZDvNMU50AiaQQv9tnQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在语义分析阶段，就需要汇集上面得到的信息，判断运算该如何进行了。节点属性传递过程如下图所示：

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KAmnr54xKwVFQ3s1ncCR1F5JKoDQqT8gQoWmXoMBawBDTMdbRtkVrPw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

作者在用160道手写测试题进行了测试：

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KIYG3FzMEibfF1ZSUYQ8YoicQVEfbjBgPIjo0iaficibiahChp6fWJxbRemVQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

结果表明，平均字符识别率达到了96.23%，且系统做题的平均正确率达到了79.38%。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KJZG4EOaCATnkicxr5V29iacACqRPibsesmdBdSDuicxnWmalll13CJxMgQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 上手实操 

来，实际上手操作下。

作者给出两种使用模式：网页模式和接口模式。接口模式比较直观，只需打开网页上传图片即可自动给出解题结果。

下面以接口模式为例介绍一下mathAI的安装使用方法。

首先需要安装**flask**、**虚拟环境**、科学计算库numpy、sympy等，它们都可以用pip安装。

```
pip install flask
pip install virtualenv
```

将项目的lib.zip文件解压到系统目录的venv文件夹下。（lib.zip可以回复**lib**获取）

配置置好运行环境后，用**PyCharm**打开下载好的项目，在载入过程中，PyCharm会自动安装好项目依赖的软件库。

使用命令行进入项目所在目录，并启动虚拟环境：

```
. venv/bin/activate
```

将FLASK_ENV环境变量设置为启用开发模式：

```
export FLASK_ENV=development
```

然后使用指令运行flask网站框架:

```
export FLASK_APP=welcome.py
flask run
```

打开浏览器，在地址中输入127.0.0.1:5000，即可打开项目网页。在网页中输入一张包含数学公式的图片，就好返回运算结果。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KUriaMHB76MCWrwturyrWia1Zv9FicYVFncIS1VMibrATxDDWYgqASd2yAg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

目前GitHub项目页上的代码只支持加减乘除这样的简单运算。

## 中国少年

做出这个自动求解系统的，还是一位中国少年。

这位GitHub ID为Roger，本名罗文杰，是中山大学数据科学与计算机学院的研一在读硕士生，主要攻读计算机视觉方向。

不仅这个解题神器，在小哥哥的GitHub主页上还能看到其此前参与的很多有趣研究。

比如这个基于帖子的校园互助交友平台**LiBond**。用户可以在里面发布任务，然后使用虚拟币荔枝进行交易。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KcdKbYTDkiarIhJy2icKtLZ3GNRd4hZb7q5ux40L5gc0Zy10eiayNyF4GA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

罗同学的设想是，有空闲时间的同学可以在此平台上帮助他人，然后结交好朋友，荔枝币还能用来兑换喜欢的物品。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KEordSu72NibhpUXy8MfibhCJkpwD72e9ia6s5dX4ugZm0rvwuoWEzAjvw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

再比如，一个基于C++的无禁手五子棋AI，可以通过openGL实现图形界面。

![img](https://mmbiz.qpic.cn/mmbiz_png/YicUhk5aAGtBjDzu4H678y2uXFpW2Nib2KQgqjL4hjmTHEibRkzNHEpv8KuXkic2Rqft7VVibtiaGO5HkvLvDJhFYsow/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在这个项目中，罗同学使用了最经典的极大极小博弈树、alpha-beta剪枝、置换表等算法，还附上了核心代码。

确认过眼神，是学霸无疑了。

# 传送门

最后，附上神器的Github地址：
https://github.com/Roujack/mathAI

里面还附有Demo使用的word、ppt和视频教程~

作者系网易新闻·网易号“各有态度”签约作者



— **完** —

**订阅AI内参，获取AI行业资讯**

![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtAkpibldb6tu0lfWoPMdPlFKOhiaKOf4PibMlFibooQe4JdMLqxAN1PpoaQfD0RfpkkSzZsEeBzR1FLwA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**加入社群**

量子位AI社群开始招募啦，社群矩阵：**AI讨论群**、**AI+行业群**、**AI技术群**；



目前已有**4万**AI行业从业者、爱好者加入，AI技术群更有来自**海内外各大高校实验室大牛**、**各明星AI公司工程师**等。自由互相交流AI发展现状及趋势



欢迎对AI感兴趣的同学，在量子位公众号（QbitAI）对话界面回复关键字“微信群”，获取入群方式。（技术群与AI+行业群需经过审核，审核较严，敬请谅解）

**诚挚招聘**

量子位正在招募编辑/记者，工作地点在北京中关村。期待有才气、有热情的同学加入我们！相关细节，请在量子位公众号(QbitAI)对话界面，回复“招聘”两个字。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/YicUhk5aAGtAWR7KMTicXl4micou1JFQYicKuicoLdfTGicbTQVODlcKpQOobfgv8PhpRbsDdXvXUia2CJZxC2tQzQzwg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)



**量子位** QbitAI · 头条号签约作者





վ'ᴗ' ի 追踪AI技术和产品新动态



喜欢就点「好看」吧 !











微信扫一扫
关注该公众号