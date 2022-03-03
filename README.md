# HNU-Auto-Clockin

HNU疫情防控和健康监测系统每日自动打卡

**2022.2.24 感谢 [@Mufanc](https://github.com/Mufanc) 同学关于本地验证码识别的commit，这触及到我的知识盲区了。另外我也很好奇他怎么在有自己的打卡脚本的情况下发现我的打卡脚本失效了😂**

**2021.6.4 更新：使用百度云公开验证码识别OCRapi，不再需要百度账号，此处感谢[GGP](https://github.com/2X-ercha)老哥的提醒。**

之前使用本脚本的同学请在fetch and merge之后进入Secrets删除用于配置验证码识别的3个id即可（不删也行）。

参考开源仓库：[中南大学nCov健康打卡定时自动脚本](https://github.com/lxy764139720/Auto_Attendance)

## 觉得有用的话先给👴点个Star呗~

## 食用方法

本品通过GitHub Actions实现自动化，~~具有美容养颜、改善睡眠、舒肝理气、应该不会再被辅导员电话轰炸或被喝茶等功效。~~ 需要你做的前期工作有：

1. **创建一个GitHub账号，将本项目fork到你自己的账号下**
   ![QQ20210316-0.png](https://i.loli.net/2021/03/16/1krc8KwVATBUWCl.png)

2. **配置学号与个人中心密码**

    进入刚刚你fork过去到自己名下的项目，再进入Settings -> Secrets页面，点击New repository Secret，在Name栏输入**USERNAME**，Value栏输入你的学号。然后再添加一个Secret，Name栏为**PASSWORD**，Value栏填写你登录个人中心的密码。
    ![QQ20210316-2.png](https://i.loli.net/2021/03/16/4vqF6bsBPfSUDZc.png)

3. **填写打卡地址**

    你还需要分别以**PROVINCE**, **CITY**, **COUNTY**为NAME添加相应的Secret，Value中请注意须在地名后面添加“省“、”市“、”县/区“，如”湖南省“、”长沙市“、”岳麓区“。另外，详细地址默认为一个句号，你可以在源代码（clock_in.py）中修改。

4. **开始自动化运行**

    进入到**Actions**界面，点击该工作流，然后Run workflow，即可开启自动化运行，你可以在设置里绑定邮箱以接收运行失败的通知，防止未来哪天打卡系统升级了你还蒙在鼓里。
    ![Snipaste_2021-03-15_21-56-15.png](https://i.loli.net/2021/03/16/oxSp8VYlfskWq53.png)
    ![Snipaste_2021-03-15_21-56-34.png](https://i.loli.net/2021/03/16/xETNukAF8hVS1nw.png)
    ![Snipaste_2021-03-15_21-57-11.png](https://i.loli.net/2021/03/16/XtR6lphCxLQg3an.png)

    你可以在如下界面中检查自动化运行情况：
    ![Snipaste_2021-03-15_21-57-49.png](https://i.loli.net/2021/03/16/8RwnFvq1ZBTuMxe.png)
    ![Snipaste_2021-03-15_21-58-06.png](https://i.loli.net/2021/03/16/MSok2D9VYJOBRK7.png)
    ![image.png](https://i.loli.net/2021/03/16/vnaiPEmyx5ugNlW.png)

    我设定为每天早晨6：10自动运行，你可以在/.github/workflows/python-app.yml文件里修改，请注意cron语法下的时间为零时区时间，需要将北京时间减8个小时，且分钟在前小时在后。详情参见[POSIX cron 语法](https://crontab.guru/)和[官方文档](https://docs.github.com/cn/actions/reference/events-that-trigger-workflows#)。

6. **如果一切顺利的话，应该没有第六步。若不是那样，可以在Discussion里面说。**

**寒暑假离校返校状态切换：进入clockin.py中的main函数改这个IsInCampus的数值就行了**
![Snipaste_2022-01-15_21-32-04.png](https://s2.loli.net/2022/01/15/GHs2EvakgqNlBOn.png)
