#### IDEA错误：Cannot start compilation: the output path is not specified for module "Test". Specify the out  
#### class not found

https://blog.csdn.net/zZ_life/article/details/51318306



错误是发生在从github上checkout自己的项目时。因为没有将配置文件一起上传，所以在运行java程序时有了这个报错：

Cannot start compilation: the output path is not specified for module “Test”. Specify the output path in Configure Project.

其实这个错误是因为没有设置output的路径，只要修改两个地方的设置就可以了：
1. 在Modules设置里勾选”Inherit project compile path”

2. 设置Project中的”Project compiler output”

选择”Project的路径”+”\out”，比如说我的就是


将这两处改好后就能正常运行了。





