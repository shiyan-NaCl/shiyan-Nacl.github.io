---
layout: post
title:  "节拍脉冲发生器时序电路实验"
date:   2018-05-27 15:44:05 +0800
categories: blog
---
节拍脉冲发生器时序电路实验
========================================  


实验目的：
---------
掌握节拍脉冲发生器的设计方法，理解节拍脉冲发生器的工作原理。

实验原理：
--------
连续节拍发生电路可由4个D触发器组成（见下图），可产生4个等间隔的时序信号T1~T4，其中CLK1为时钟信号，由实验台方波信号源提供，实验者可根据实验自行选择信号频率。当RST1为低电平时，T1输出为“1”，而T2、T3、T4输出为“0”；当RST1由低电平变为高电平后，T1~T4将在CLK1的输入脉冲作用下，周期性地轮流输出正脉冲，机器进入连续运行状态。

![1](/styles/images/third/01.png)
实验任务
----------------

* 连续节拍发生电路设计
 ----------
设计工程文件，硬件电路如上图所示。使实验平台工作于模式5，主系统时钟源接4Hz，键8控制RST1，高电平时可以看到，发光管D1、D2、D3、D4分别显示T1、T2、T3、T4的输出电平，锁定引脚并硬件下载测试。引脚锁定后进行编译、下载和硬件测试实验。


+ 单步节拍发生电路设计
 ----------
用单步节拍发生电路可以对微程序进行单步运行调试，电路如下图所示。该电路每当RST1出现一个负脉冲后，仅输出一组T1、T2、T3、T4节拍信号，直到RST1出现下一个负脉冲

![图2](/styles/images/third/03.png)

实验步骤
------------------------------
**连续节拍发生电路设计**

1.原理图输入，如下图所示
![图3](/styles/images/third/05.png)

2.引脚锁定，主系统时钟源接4Hz，键8控制RST1，并将T1、T2、T3、T4绑定与发光管D1、D2、D3、D4，本次引脚定义情况如下： 
![图4](/styles/images/third/06.png)

3.结果测试，实验中选择实验电路模式为NO.5，测试时会发现当RST1为低电平时，T1输出为“1”，而T2、T3、T4输出为“0”；当RST1由低电平变为高电平后，T1~T4将在CLK1的输入脉冲作用下，周期性地轮流输出正脉冲，机器进入连续运行状态结合课堂知识易知实验结果正确。

5.生成元件符号。
![图5](/styles/images/third/07.png)

**单步节拍发生电路设计**

1.原理图输入，如下图所示
![图6](/styles/images/third/08.png)

2.引脚锁定，主系统时钟源接4Hz，键8控制RST1，并将T1、T2、T3、T4绑定与发光管D1、D2、D3、D4，本次引脚定义情况如下：
![图7](/styles/images/third/09.png)

3.结果测试，实验中选择实验电路模式为NO.5，测试时会发现电路每当RST1出现一个负脉冲后，仅输出一组T1、T2、T3、T4节拍信号，直到RST1出现下一个负脉冲。结合课堂知识易知实验结果正确。

5.生成元件符号。
![图5](/styles/images/third/10.png)

