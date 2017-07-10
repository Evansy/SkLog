# webstorm小技巧
昨天在webstorm创建vue templete的时候,突然看到其他文件模板里有一些特殊字符（类似内置变量），创建之后会被替换
其实就是内置变量，

### 自定义变量
> 在templete里写`$Title`，根据该模板文件创建文件时，弹窗里会多出一个Title的输入框，所有基本可以断定，`$名称`是新建输入框的意思。

### 内置变量(写在templete里会被替换)
* ${USER}(当前系统用户名),
* ${NAME}(当前创建的文件名)
* ${DATE}(当前年月日)