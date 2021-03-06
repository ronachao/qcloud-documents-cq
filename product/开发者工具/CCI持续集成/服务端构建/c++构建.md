## c++ 构建 
### 新建工程
1. 进入 CCI 持续集成界面后，单击左侧菜单栏中的 【服务端构建】。单击 【新建】 按钮，新建服务端构建工程。
![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/da6a3b45337946e40f0fe17512d11570/image.png)
2. 进入新建工程后时，依次填写工程名称和工程描述（选填）。
3. 选择代码仓库（必填）和分支（必填），代码仓库和分支的创建请参考 [Tgit 代码托管文档](/document/product/612)。
4. **编程语言** 中单击 【 c++ 】选项，在 **构建类型** 中，根据用户实际需求选择 `make`  或 `cmake` 构建类型,构建环境会根据构建类型自动定位。
   - 当您选择 `make` 时，编译参数 `makefile` 用来指定 Makefile 文件的名称，默认值为 makefile 。编译参数 `target and options` 用来指定 make 编译的 target 和选项。编译参数 `path` 用来指定 makefile 文件的相对路径。
  - 当您选择 `camke` 时，编译参数 `path` 用来指定 `CMakeLists.txt` 文件的相对路径，由用户根据具体情况输入。编译参数 `cmake options` 是 cmake 命令的选项，如输入 `-G "Unix Makefiles"` 表示用 GCC 编译生成 makefile 工程文件 。编译参数 `make target and options` 用来指定 make 编译的 target 和选项，由用户根据具体情况输入。
6. 填写 **归档路径**（选填），默认为工程根目录。
7. 选择 **触发方式**（选填），根据需求勾选 【定时触发】 或 【代码变更触发】（可同时勾选两种方式，或勾选其一，或都不勾选）。
   若您勾选了 【定时触发】，可以滑动选择定时触发时间（选填）。
8. 若您想对工程的超时时间，构建结构通知和环境变量进行设置时，单击 【显示高级设置】，在显示的页面中进行填写和勾选。
 ![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/97e4dc84142cd8557f56b8fd460e4c52/image.png)
9. 填写完成后，单击页面右下方 【确认】，完成新建工程创建，或单击 【返回】，取消新建工程创建。
 
 
### 触发构建

-  新建工程后，单击 【确认】，进入工程的触发构建页面。![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/e75b9ea5b10efa9d9685b2b061424fda/image.png)
 触发构建的方式有三种：
   -  手动触发
   在 **工作区** 中单击【手动创建】，选择代码段，单击【构建】，开始构建。![](http://imgcache.tcecqpoc.fsphere.cn/image/mc.qcloudimg.com/static/img/b9dc7c8f40576e4e883c15905b1798d0/image.png)
   -  代码变更触发
   代码变更码发生变更时，CCI 平台即开始以最新版本代码执行构建的方式。
   -  定时触发
   定时触发是在指定时间自动开始执行构建。
- 您可以在页面右上方单击 【配置修改】，改变触发构建方式。单击 【禁用工程】，停止自动触发构建方式，只能发起“手动构建”。单击 【删除工程】，删除当前的工程。
- 您可以在 **工作区** 中查看构建日志。您可以在构建过程中，单击 **工作区** 中的 【停止构建】，停止当前工程的构建。
- 您可以在 **构建记录** 中查看构建结果，构建成功后，可以在新建工程页面下载该构建包。
- 您可以在 **代码提交历史** 中查看提交的代码段。

 
 
