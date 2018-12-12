## 目录

1. 概述
2. 获取代码
3. 注入 Blockly
4. 配置
5. 代码生成器
6. 引入和导出 Blocks
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

`Blockly.inject` 方法的第二个参数是一个对象, 具体的内容给出在下面了, 