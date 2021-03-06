---
title: Blender应用变换的原理
categories:
  - blender
  - BL基础
tags: BL基础
cover: 'https://pic.imgdb.cn/item/62ce3394f54cd3f93770d414.jpg'
thumbnail: 'https://pic.imgdb.cn/item/62ccebc8f54cd3f937e787e5.jpg'
abbrlink: 202207121236
date: 2022-07-12 12:12:36 
---
{% raw %}<article class="message is-danger"><div class="message-body">{% endraw %}
## 你有没有遇到这样的问题？
{% raw %}</div></article>{% endraw %}

在学习blender的时候经常要使用应用位置、缩放、旋转命令，为什么隔壁火热的“西四帝”没有这个繁琐的操作，Blender却如此优秀，频繁锻炼你发财的小手？

先来看看不应用位置、缩放、旋转命令会产生最常见什么问题？

<!-- more -->

- 倒角命令及倒角生成器产生错误倒角
- 编辑模式下内插面、法线挤出面的问题
- UV拉伸问题
- 无法列出所有的问题进行说明，比如编辑模式下新建圆环等比缩放拉伸问题，动画问题等等，解决办法文章下方有说明。

### **倒角命令及倒角生成器产生的错误倒角问题**

场景中有2个一样大小的立方体

![点击图片可以放大](https://pic.imgdb.cn/item/62ccebb2f54cd3f937e76e24.png)

前面这个长方体是缩放未使用应用缩放命令，后边的长方体是应用过缩放命令。两个立方体分别选择一个边倒角后，没有应用过变换命令的长方体倒角被拉伸；使用倒角生成器进行统一倒角后未使用应用缩放也产生了严重的倒角拉伸。

![点击图片可以放大](https://pic.imgdb.cn/item/62cceba5f54cd3f937e76080.png)

![点击图片可以放大](https://pic.imgdb.cn/item/62cceb99f54cd3f937e7510f.png)

### **编辑模式下内插面、法线挤出面、新建对象缩放的问题**

内插面因为在物体模式下缩放导致边距不均匀

![点击图片可以放大](https://pic.imgdb.cn/item/62cceb8df54cd3f937e74322.png)

法线挤出面勾选均等偏移依然不均等问题

![点击图片可以放大](https://pic.imgdb.cn/item/62cceb7ef54cd3f937e73160.png)

### **UV拉伸问题**

给立方体创建默认材质→赋予默认的棋盘格纹理，正常如下图

![点击图片可以放大](https://pic.imgdb.cn/item/62cceb73f54cd3f937e724e4.png)

刚才创建正常的立方体进行Y轴放大2倍，观察棋盘格纹理发现已经被拉伸得严重

![点击图片可以放大](https://pic.imgdb.cn/item/62cceb4df54cd3f937e6f908.png)

{% raw %}<article class="message is-success"><div class="message-body">{% endraw %}

## **解决办法**

{% raw %}</div></article>{% endraw %}

### **倒角命令、倒角生成器、内插面、法线挤出错误解决办法**

在物体菜单→应用→应用位置、旋转、缩放或者应用全部变换就能解决

### UV**因为缩放导致拉伸解决办法**

UV拉伸得解决办法还要多一步操作，在纹理坐标中切换到物体模式

![点击图片可以放大](https://pic.imgdb.cn/item/62cceb3ff54cd3f937e6e8f2.png)

## **我认为的原理**

说明：这个原理不一定正确，只是我个人查阅资料理解而成

原理比较复杂一些，如果不想了解也没关系知道怎么解决就行了，毕竟很多小伙伴只需要知道踩下油门车能走就行，至于为什么踩油门车可以走起来适合那些有点小闲，有较大好奇心的小伙伴。

### **我个人认为原理涉及到以下几个知识点**

- 对象的概念
- 网格的概念
- 对象和网格的关系
- 优先级概念
- 应用变换的背后做了什么？

### **对象的概念**

Blender中创建一个猴头，在大纲视图中可以看到有个猴头名字的额黄色对象，这就是对象。

对象我理解为是个合集，可以比如成一“盒子”，盒子里面装着灯光就是灯光对象，盒子里面装的是网格就是网格对象。

![点击图片可以放大](https://pic.imgdb.cn/item/62cceb32f54cd3f937e6da6b.png)

### **网格的概念**

Blender创建一个猴头可以在大纲视图中展开网格对象，看到一个绿色三角形标志写着猴头，这个就是网格。
![点击图片可以放大](https://pic.imgdb.cn/item/62cceb25f54cd3f937e6cc9c.png)

网格是什么？

点、边、面的合集就是网格。

在编辑模式下可以看到有点、线、面，改变点、边、面的位置从而形成模型，这就是我们建模的过程。

### **对象和网格的关系**

在三维软件中每个东西都有自己的坐标轴，对象和网格都有自己的坐标系统。

对象是个“大盒子”改变自己的坐标进行移动、旋转、缩放也会带动里面的网格这个“小盒子”进行移动、旋转、缩放。需要注意是比如对象在Y轴缩放了3倍，在对象自己的坐标轴中可以看到坐标是X1、Y3、Z1，但是网格自己的坐标可是没有变化的依然是X1、Y1、Z1。

这里还需要了解个小知识点，Blender物体模式操作的就是对象，Blender编辑模式操作的对象就是网格

我的数学是体育老师教的，我先来做个计算

创建1个默认大小2米的立方体（称为1号立方体），在物体模式缩放坐标Y轴中输入数值3，这样立方体对象的大小是X轴2米，Y轴2*3米，Z轴是2米，那么请问立方体的网格是多大？

这个推测非常重要我另起一行加粗表示

**我推测立方体的网格依然是X轴2米，Y轴2米，Z轴是2米，也就是所物体本身的数据并没有被改变，要改变物体本身的数据需要进入编辑模式改变**。

![点击图片可以放大](https://pic.imgdb.cn/item/62ccead0f54cd3f937e659c9.png)

复制这个立方体到旁边（称为2号立方体），按Ctrl+A 应用缩放，在物体模式可以看到缩放的坐标是X1、Y1、Z1,此时2号立方体的大小是X轴2米，Y轴6米，Z轴2米

![点击图片可以放大](https://pic.imgdb.cn/item/62cceaecf54cd3f937e68259.png)

接下来分别给两个立方体添加一个倒角生成器，倒角数值是0.1，可以看到1号立方体倒角出现了拉伸的问题，2号立方体倒角正常。

![点击图片可以放大](https://pic.imgdb.cn/item/62cceafcf54cd3f937e69509.png)

发生了什么？为什么都是一样大小的立方体进行一样的倒角，出现了截然不同的结果？

为了解释这个问题，这里引入一个优先级别的概念

### **优先级别的概念**

优先级别看名字很好理解，就是谁先谁后嘛，了解优先级别后我们就可以来看看倒角出现问题的根本原因。

同样都是2个一样大小的立方体，分别添加倒角生成器后，1号立方体为什么出错了呢？而且出错的地方非常巧合的出现在了我们缩放了3倍大小的Y轴。

我推测导致错误的原因是因为优先级别导致的，还记得创建1号立方体时候我有个加粗的推测，在对象模式下缩放对象，放大模型并没有真正改变模型网格的数据。

倒角生成器的优先级别比对象级别高，是先计算倒角后计算对象的缩放数值

展开这个过程就是，倒角生成器先基于立方体网格(X轴2米、Y轴2米、Z轴2米)的尺寸做了倒角，然后再计算对象缩放坐标轴上的Y轴放大3倍，这样就导致了倒角在Y轴上被拉长了。

产生错误的原因总算推测完了接下来看看为什么应用变换后的2号立方体倒角正常，这背后又发生了什么？

### **应用变换命令做了什么事情**？

应用变换做的事情其实很简单，还是来拿1号立方体来距离

1号立方体本身的网格大小是X轴2米、Y轴2米、Z轴2米，通过对象的Y轴缩放3倍达到了6米的长度，我应用缩放就是把对象的缩放数值传递给了网格本身，这样对象的缩放数值就是X1、Y1、Z1，网格本身的大小就是X轴2米、Y轴6米、Z轴2米.

这样倒角命令在2号立方体的计算是什么过程？

倒角生成器对2号立方体网格本身的大小（X轴2米、Y轴6米、Z轴2米）进行倒角，然后乘以对象的缩放值（X1、Y1、Z1）

这样2号立方体的倒角并没有被拉伸，倒角完美。

恭喜你又学会了一个Blender的小技巧，赶紧给你的朋友分享一下你学到的知识吧。



## **总结**

- 不要在物体模式下缩放对象，进入编辑模式缩放模型就不会出现这个问题，出现了问题也不要慌应用变换就能解决
- 应用变换就是对象的变换数值传递给网格本身，并把对象的变换数值重置为位置0、旋转0、缩放1（应用全部变换就3个都重置，如果只是应用缩放并不会改变位置和旋转的数值）
- 基于网格的计算优先级大于对象的变换计算，网格在前，对象在后。

## **说明**

这篇文章的内容只是我的推测结果，并不意味着完全正确，非常欢迎有大佬给我指出错误的地方。

{% raw %}<article class="message is-info"><div class="message-header">{% endraw %}
我是张三，我的QQ是：152746199
{% raw %}</div><div class="message-body">{% endraw %}
我不包吃，不包住，但是这个技巧我可以包你会，有问题请愉快的Q我！
{% raw %}</div></article>{% endraw %}

