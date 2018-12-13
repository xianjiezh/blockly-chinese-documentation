## 目录

1. 概述
2. 获取代码
3. 注入 Blockly
4. 配置
5. 代码生成器
6. 引入和导出块
7. 云存储

### 概述

Blockly 可以很容易的添加到你的 web 应用, 用户拖拽砖块, Blockly 就会生成代码, 你的应用去执行这些代码. 在你的应用的角度上看, Blockly 就是一个使用 JavaScript, python, PHP, Lua, Dart或者其他语言的程序猿在一个 `<textarea>`写代码的地方

Blocky 全部都在客户端, 不需要从服务器的支持(除非你想用它的云存储特性). 并且没有第三方的依赖(除非你想去重新编译它的核心), 所有的都是开源的.

### 获取代码

第一步, 从 github 上面下载源代码. 如果你知道如何去使用 git 或者 Subversion , 我们墙裂推荐你去同步我们的仓库, 这样你的代码库就会保持最新的

[下载 ZIP](https://github.com/google/blockly/zipball/master)

[下载 TAR](https://github.com/google/blockly/tarball/master)

[去往github](https://github.com/google/blockly)

在你拿到代码后, 用你的浏览器打开这个目录的文件 `demos/fixed/index.html` , 然后看一下是不是可以拖动砖块

### 注入 Blockly

在你下载上面的文件并且确定 Blockly 可以用之后, 用一个固定尺寸的 div 把 Blockly 放到你的html页面吧
-> 更多信息可以看这里 https://developers.google.com/blockly/guides/configure/web/fixed-size

很多比较高级的页面会希望Block跟页面是自适应的
-> 更多信息查看这里 https://developers.google.com/blockly/guides/configure/web/resizable

### 配置

上面的使用的`Blockly.inject` 方法的第二个参数是一个对象,  这些都被用于配置, 支持下面的选项. 

|项目            |    类型         |      描述
| --------       | -----:         | :----: |
|collapse        |   boolean      | 允许块折叠或展开, 如果 toolbox 的下面有 categories, 则默认为 true, 否则为false
|comments        |   boolean      | 允许块有备注, 如果 toolbox 的下面有 categories, 则默认为 true, 否则为false
|css             |   boolean      | 如果是false, 不会注入css, 会只依靠用户写的css
|disable         |   boolean      | 允许块是否被disable, 如果 toolbox 的下面有 categories, 则默认为 true, 否则为false
|grid            |   object       | 配置块的栅格布局, [看这里](https://developers.google.com/blockly/guides/configure/web/grid)
|horizontalLayout|   boolean      | toolbox 是否是横向的, true是横向的, false 是垂直的, 默认是false
|maxBlocks       |   number       | 能创建的最大的block数量, 默认是无限的
|media           |   stirng       | Blockly媒体(如音频)的路径, 默认是https://blockly-demo.appspot.com/static/media/"
|oneBasedIndex   |   boolean      |  字符串和数组操作开始的下标, true为1, false 为 0, 默认是true
|readOnly        |   boolean      |  如果是 true, 用户不能修改, 不会显示toolbox和trashcan.默认是false
|rtl             |   boolean       |  如果为true, 则会镜像编辑器(对于阿拉伯语或希伯来语语言环境). 请参阅RTL演示. 默认为false.
|scrollbars      |   boolean       |  设置 workspace 是否可被滚动, 默认是true
|sounds          |   boolean       |  如果是false, 不会有声音(比如点击和删除的声音) 默认是true
|toolbox         |  xml结构的string|  用户可用的categories和块的树状结构. 请看下面的详细信息.
|toolboxPosition |  boolean       |  如果"start"toolbox位于顶部(如果是水平)或左侧(如果是垂直和LTR)或右侧(如果是垂直和RTL). 如果"end"toolbox位于对面. 默认为"start"。
|trashcan        |  boolean       |  展示或者不展示垃圾桶, 如果 toolbox 的下面有 categories, 则默认为 true, 否则为false
|zoom            |  object        |  配置块的空间特征, 具体的[看这里](https://developers.google.com/blockly/guides/configure/web/zoom)

最重要的选项是 `toolbox`, 这是一个树状的 xml, 它指定了在 toolbox(侧边菜单)内的有什么块, 是怎样组织起来的, 以及他们里面是含有 categories

更多的信息在这里 [定义toolbox](https://developers.google.com/blockly/guides/configure/web/toolbox)

除了Blockly默认提供的, 有时你的web应用也需要一些定制的块去调用这个应用的接口, 
下面是一个[迷宫游戏](https://blockly-games.appspot.com/maze), 它就使用了定制的块

更多的信息在这里[创建定制的块](https://developers.google.com/blockly/guides/create-custom-blocks/overview)

### 代码的生成

Blockly并不是一个编程语言, 你不能去"run"一个Blockly程序. 不过, 你可以把用户创建的Blockly程序转换成JavaScript/python/PHP/Dart 或者其他的语言

更多的信息在这里 [代码生成](https://developers.google.com/blockly/guides/configure/web/code-generators)

### 引入和导出块

如果你的应用需要去保存并且存储用户生成的的块, 以便他们之后还可以去访问, 可以去用这个块去把页面上的块导出生成 xml
```JavaScript
var xml = Blockly.Xml.workspaceToDom(workspace);
var xml_text = Blockly.Xml.domToText(xml);
```
这会生成一个最小的(但是可读性不好)字符串, 它包括与用户创建的砖块所对应的xml. 如果你想生成一个可读性比较好的字符串(不过这样会更大一些)可以用这个方法
```JavaScript
Blockly.Xml.domToPrettyText
```
把一个字符串的xml生成页面上的块也是同理
```JavaScript
var xml = Blockly.Xml.textToDom(xml_text);
Blockly.Xml.domToWorkspace(xml, workspace);
```

### 云存储

Blockly附带可选的云存储功能. 它使用户能够保存, 加载, 共享和发布他们的程序. 如果您的项目托管在App Engine上, 则可以利用此服务. 


未完待续...