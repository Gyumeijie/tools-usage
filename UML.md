#### plantuml
> 在菜单栏Intellij IDEA打开插件安装窗口安装PlantUML插件

在Intellij IDEA中使用`PlantUML`除了在Intellij IDEA中安装PlantUML插件之外，需要安装Graphviz工具安装完成后，设置环境变量：
1. 在Path中将Graphviz\bin路径添加进去
2. 添加一个新的系统变量： 
     - 变量名：GRAPHVIZ_DOT
     - 变量值：[Graphviz安装路径]\bin\dot.exe   
