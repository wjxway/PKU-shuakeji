# 北大刷课机

**最后更新于 2020年6月2日**

**本次更新修复了有太极拳等就会选课失败的bug，修复了双学位选课无法进入的bug。**

## 基本情况

**强烈建议如果你没有Mathematica，则使用[这个](https://github.com/zhongxinghong/PKUAutoElective)刷课机**

**经常有同学在配置ChromeDriver的过程中出现问题，所以没有Mathematica的慎用这个选课机（下载安装一套下来，如果还不成那真的太难过了）**

**运行需求：** Mathematica 11.0+ ，Chrome最新版（目前是83.0版本，亲测可用）。（注：Raspberry Pi自带Mathematica，所以可以很方便的在Raspberry Pi上托管！）Mathematica安装请见<u>[这里](https://tiebamma.github.io/InstallTutorial/)</u>，请注意一定要下载Mathematica而非Wolfram Engine，目前推荐下载11.3版本，下载12.0版本的请注意一定**不要**把现在这个文件放在中文目录下（其实好习惯是不要把任何东西放在带有中文的目录下）.

**基本功能：** **支持普通选课，本科生双学位选课，研究生选课.** 会自动输入验证码（总体正确率约为93%），自动选课，自动退课（例如如果什么课出现空位，则退掉其它几门课，如果选课失败会立刻尝试补回来。）。程序有友善的Mathematica界面。

**实现方法：** 以Mathematica为控制/计算平台，通过Chrome Driver托管Google Chrome浏览器实现，所以理论上是和人刷是没有任何区别的（除了能一直刷，搞不好刷的频次还比人低一点……）。

**一些细节：**

0. 如果你有Mathematica它将十分方便，下载直接运行即可， **无需任何额外配置** ，即下即用。
1. 如果你没有Mathematica，唯一的麻烦是Mathematica的下载&破解（文件比较大），安装也是无脑安装，还是无需额外繁琐的配置！
2. 去年曾尝试过一晚上刷新，没问题的，长时间运行是可靠的。
3. 目前还没听说过谁的课被这个选课机退光了2333（毕竟也没几个人用X



**如果出现问题，请看下面的“可能遇到的问题”部分**

**具体初始化的帮助在.nb文件里，请务必读完再跑！！！**



## 基本操作 

0. 先激活安装Mathematica/Chrome
1. 打开 **选课机.nb** 文件，依次确认各个事项。
2. 在每次使用前，点击 菜单栏->Evaluation(计算)->Evaluate Initialization Cells(计算初始化单元)
3. 滑到最后，运行代码ShuaKeJi\[\]。 **在这之后你都不应该碰触浏览器！**
4. 你应该马上看见如下界面：

![登录界面](https://raw.githubusercontent.com/wjxway/image-storage/master/shuakeji1.png)

5. **一定在右侧Mathematica窗口中输入学号和密码！否则无法在意外退出后恢复！**

5.1 如果是双学位的同学则需要再进行一步，选择到底需要刷主修还是辅双的课程。

6. 点击Login并登录成功后你应该见到Mathematica弹出如下界面。如果没有弹出那是浏览器和驱动的问题，请参见后面**可能遇到的问题**部分：

![选课界面](https://raw.githubusercontent.com/wjxway/image-storage/master/shuakeji2.png)

7. 选择多门需要的课（注意左上角点击不同页数翻页哦），点击Confirm，并再次点击Correct确认即可。若需要返回请点击右下角的Edit。

   ![确认界面](https://raw.githubusercontent.com/wjxway/image-storage/master/shuakeji3.png)

8. 确认后即开始刷课，假如你看见Chrome在刷来刷去的话，那就对了！就放手吧！

9. (*高级操作*)自动退课：进入上图界面后，例如我们希望能选上流体力学的话就退掉广相，那么就点击流体力学一栏右侧的Edit键，你应该看见如下界面：

![自动退课](https://raw.githubusercontent.com/wjxway/image-storage/master/shuakeji4.png)

10. 选择广相，并保存。这时候流体力学左侧会出现下拉菜单的按钮，点开你应该可以看到如下的界面。

![确认界面2](https://raw.githubusercontent.com/wjxway/image-storage/master/shuakeji5.png)

11. 如果没问题了，确认好后点击Correct即可。

12. 如果碰到了问题，例如不小心关掉了什么窗口，那么你可以在Mathematica里面同时点按“Alt”和“.”键来停止运算，然后重新从第二步开始即可。实在搞不懂这个的话就完全关掉Mathematica重来一次也行。


## 可能遇到的问题

1. 在运行代码后没有弹出Chrome！

    a) 检查你是否仔细阅读了.nb文件里面的注意事项，极有可能是你没有运行初始化单元或者安装WebTools包失败了。
   
    b) 如果Mathematica弹出了一个输入用户名密码的窗口，且报了StringFreeQ打头的错误，那这多半是Mathematica的锅！
    
      i. 请先在Mathematica里面运行
      
      ```mathematica
      SystemOpen[$UserBaseDirectory<>"\\Paclets\\Repository\\WebTools-0.1.1\\WebDriver\\ChromeDriver"]
      ```
      
      应该会打开一个窗口.
      
      ii. 请完全关闭Mathematica。
      
      iii. 而后打开刚刚打开的文件夹下对应操作系统的可执行文件，例如Windows的话就打开Windows-x86-64文件夹下的chromedriver.exe。
      
      iv. 重新打开Mathematica，从头开始运行，应该就可以了。
      
   c) 如果上述方法仍然不行请更新一下Chrome版本（目前83.0版本亲测可用）。如果你实在不方便更新的话可以如下操作：
   
      i. 先确认你的Chrome版本号，如68.0.xxxxx。
     
      ii. [点击这里](http://npm.taobao.org/mirrors/chromedriver)并下载对应版本和操作系统的Chrome驱动
      
      iii. 在Mathematica中运行
      
      ```mathematica
      SystemOpen[$UserBaseDirectory<>"\\Paclets\\Repository\\WebTools-0.1.1\\WebDriver\\ChromeDriver"]
      ```
      
      并把下载下来的驱动文件拷贝到对应的文件夹下覆盖（什么系统的你就进什么子文件夹）。
      
   d) 如果还是不行请汇报bug，十分感谢！！！
   
2. 我选好了我需要的课，点击了确认，但是似乎浏览器页面没动静啊？

    假如你的整个选课计划只有一页，那么你的Chrome应该不动，只要Mathematica还在运行这就是没问题的！Mathematica会点击刷新，只不过我禁用了所有的Alert所以你看不见弹出的“课程人数没有变化！”罢了。~假如你觉得虚就请狂添加课程直到列表有两页，那你就能看到Mathematica翻页啦~

3. 我遇到了其他问题！

    请汇报bug，十分感谢！！！

## 免责声明

本程序仅用于学习交流，不建议同学过量使用本刷课机刷课，干扰选课秩序。本人不对该选课机造成的**一切**后果（例如由于使用不当退光了你的课！）担责！！！！
如果出现问题，欢迎提出issue或者通过wjxway@163.com或者vx: wjxway进行反馈。

