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


下面我们要开始配置karam：

一、Karma + Jasmine配置

1、初始化karma配置文件karma.conf.js

D:\Program Files\nodejs>karma init


Which testing framework do you want to use ?
Press tab to list possible options. Enter to move to the next question.
> jasmine

Do you want to use Require.js ?
This will add Require.js plugin.
Press tab to list possible options. Enter to move to the next question.
> no

Do you want to capture a browser automatically ?
Press tab to list possible options. Enter empty string to move to the next question.
> Chrome
>

What is the location of your source and test files ?
You can use glob patterns, eg. "js/*.js" or "test/**/*Spec.js".
Enter empty string to move to the next question.
>

Should any of the files included by the previous patterns be excluded ?
You can use glob patterns, eg. "**/*.swp".
Enter empty string to move to the next question.
>

Do you want Karma to watch all the files and run the tests on change ?
Press tab to list possible options.
> yes

Config file generated at "D:\Program Files\nodejs\karma.conf.js".

2、安装集成包karma-jasmine

D:\Program Files\nodejs>npm install karma-jasmine

二、自动化单元测试

3步准备工作：

1. 创建源文件：用于实现某种业务逻辑的文件，就是我们平时写的js脚本

2. 创建测试文件：符合jasmineAPI的测试js脚本

3. 修改karma.conf.js配置文件

1). 创建源文件：用于实现某种业务逻辑的文件，就是我们平时写的js脚本。文件地址：D:\Program Files\nodejs\src.js

有一个需求，要实现单词倒写的功能。如：”ABCD” ==> “DCBA”

function reverse(name){
    return name.split("").reverse().join("");
}

2). 创建测试文件：符合jasmineAPI的测试js脚本

describe("A suite of basic functions", function() {
    it("reverse word",function(){
        expect("DCBA").toEqual(reverse("ABCD"));
        expect("onan").toEqual(reverse("nano"));
    });
});

3). 修改karma.conf.js配置文件

我们这里需要修改：files和exclude变量

module.exports = function (config) {
    config.set({
        basePath: '',
        frameworks: ['jasmine'],
        files: ['*.js'],
        exclude: ['karma.conf.js'],
        reporters: ['progress'],
        port: 9876,
        colors: true,
        logLevel: config.LOG_INFO,
        autoWatch: true,
        browsers: ['Chrome'],
        captureTimeout: 60000,
        singleRun: false
    });
};

启动karma

单元测试全自动执行,浏览器会自动打开

三、Karma和istanbul代码覆盖率

增加代码覆盖率检查和报告，增加istanbul依赖

D:\Program Files\nodejs>npm install karma-coverage

修改karma.conf.js配置文件

reporters: ['progress','coverage'],
preprocessors : {'src.js': 'coverage'},
coverageReporter: {
    type : 'html',
    dir : 'coverage/'
}

启动karma start，在工程目录下面找到index.html文件，D:/Program Files/nodejs/coverage/chrome/index.html

打开后，我们看到代码测试覆盖率报告，点击查看src.js的覆盖率报告

覆盖率是100%，说明我们完整了测试了src.js的功能。

接下来，我们修改src.js，增加一个if分支

function reverse(name){
    if(name=='AAA') return "BBB";
    return name.split("").reverse().join("");
}

再看src.js的覆盖率报告

Statements：75%覆盖，Branches：50%覆盖。

为了产品的质量我们要尽量达到更多的覆盖率，一般对于JAVA项目来说，能达到80%就是相当高的标准了。对于Javascript的代码测试及覆盖率研究，我还要做更多的验证。
