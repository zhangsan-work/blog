---

title: 如何解决Blender预览正常渲染无灯光照明
categories:
  - blender
  - 渲染
tags: Blender渲染
cover: 'https://pic.imgdb.cn/item/62ccecddf54cd3f937e8d612.jpg'
thumbnail: 'https://pic.imgdb.cn/item/62cceceaf54cd3f937e8e411.jpg'
abbrlink: 202207110940
---

{% raw %}<article class="message is-danger"><div class="message-body">{% endraw %}

### 1.你有没有遇到这样的问题？

{% raw %}</div></article>{% endraw %}

历经坎坷做了一个作品，Blender预览渲染的图那个漂亮，都想给自己点个赞👍🏻，奖励鸡腿都在网上订了一大袋，满怀期待的点了正式渲染按钮，准备静静欣赏一个小时。

结果却发现正式渲染图灯光非常的暗、金属材质也缺少真实的反射，明明我的预览渲染图那么的好看，怎么办？

<!-- more -->

![点击图片可以放大](https://pic.imgdb.cn/item/62ccecf6f54cd3f937e8f525.png)

在线等~~~挺急的

{% raw %}<article class="message is-success"><div class="message-body">{% endraw %}

### 2.解决办法

{% raw %}</div></article>{% endraw %}

#### 2.1 产生这个问题的原因

说问题之前需要先了解一个单词：HDRI

DHRI的全名叫做高动态范围图像，是一个特殊的图像格式，除了保存图像颜色信息还能保存亮度信息，在HDRI中白色在三维软件中经常用于创建真实的照明和反射或者作为背景使用。

Blender可能出于方便用户调试材质和预览渲染的原因，提供了8个HDRI的环境。但是这8个HDRI环境并没有参与最终渲染，所以导致预览渲染和正式渲染的结果相差非常大。

解决的思路是我们去Blender安装目录把这8个HDRI环境复制出来，由我们自己添加到环境中去，这样正式渲染就拥有和预览图一样的HDRI环境。

#### 2.2 导出Blender默认提供的HDRI文件

Windows系统的HDRI路径默认在C:\Program Files\Blender Foundation\Blender 3.1\3.1\datafiles\studiolights\world文件夹中

![点击图片可以放大](https://pic.imgdb.cn/item/62cced06f54cd3f937e906d5.png)

Mac系的HDRI路径默认在/Applications/Blender3.2.app/Contents/Resources/3.2/datafiles/studiolights/world 文件夹中

![点击图片可以放大](https://pic.imgdb.cn/item/62cced13f54cd3f937e9176c.png)

把这几个文件复制到你喜欢保存的文件夹中

### 2.3 如何调用导出的HDRI文件

在菜单栏顶部切换到Shading工作区→切换着色器数据类型为世界环境→添加→纹理→环境纹理→在节点编辑器中打开之前导入的Blender默认HDRI文件,把节点连接上去，现在正式渲染和预览渲染的照明反射就相同，就大功告成。

![点击图片可以放大](https://pic.imgdb.cn/item/62cced22f54cd3f937e92e96.png)

恭喜你，又学会了一个小技巧，赶紧给你的小伙伴分享一下吧。

### 3. 补充知识点

Blender视图着色方式中场景灯光和场景世界是什么意思？

![点击图片可以放大](https://pic.imgdb.cn/item/62cced2ef54cd3f937e93e6c.png)

**场景灯光**

在我们没有创建任何灯光的情况，Blender提供了一个默认的灯光。勾选场景灯光后，Blender默认灯光就会自动关闭，使用我们自己创建灯光进行照明。

**场景世界**

点击预览球可以在8个HDRI中相互切换，勾选场景世界后，Blender就会关闭默认提供的HDRI环境，启用我们自己创建的HDRI环境照明，这就是为什么预览渲染和正式渲染的照明结果不一致的原因。

**旋转**

调整HDRI的角度，比如让DHRI图中的窗户对着场景会让场景更亮。

什么？20分钟了你还没学会？

{% raw %}<article class="message is-info"><div class="message-header">{% endraw %}
我是张三，我的QQ是：152746199
{% raw %}</div><div class="message-body">{% endraw %}
我不包吃，不包住，但是这个技巧我可以包你会，有问题请愉快的Q我！
{% raw %}</div></article>{% endraw %}

