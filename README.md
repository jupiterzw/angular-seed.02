# angular-seed.02
angular-seed.01续篇


单元测试工具karma安装：

打开cmd,输入：D:\>cd D:\Program Files\nodejs，切换到nodejs安装目录下，安装命令：npm  install karma

创建karma.cmd文件，内容如下：

@IF EXIST "%~dp0\node.exe" (
  "%~dp0\node.exe"  "%~dp0\node_modules\karma\bin\karma" %*
) ELSE (
  node  "%~dp0\node_modules\karma\bin\karma" %*
)

# 测试是否安装成功

~ D:\workspace\javascript\karma>karma start

INFO [karma]: Karma v0.10.2 server started at http://localhost:9876/

INFO [Chrome 28.0.1500 (Windows 7)]: Connected on socket nIlM1yUy6ELMp5ZTN9Ek

从浏览器打开http://localhost:9876/，看到karam界面，karma安装成功。
