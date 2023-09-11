## Prism

Prism 是 南京市金陵中学学生研究性学习项目，本项目的目标是构建基于深度学习和linux平台实现的文字扫描翻译硬件，类似于翻译笔。

我们的项目涉及计算机视觉，深度学习，应用开发，linux，电子电路等多个方面的知识，预期在1年内完成。

项目的作者包括 **彭勃(micraow),赵陈晨，盛宇博，孙延，沈锦良**

本项目基于GPL-2.0协议开源，商业使用请先联系我们！

[开发文档](https://gitee.com/micraow/prism/tree/master/docs)

## 技术方案
功能：使用摄像模块在待识别文字上划过，通过API调用第三方翻译服务，将对应中文显示在屏幕上。要求能在一定程度上克服因纸张或字体风格（斜体、花体等）而造成的识别困难。

分层：
    ①硬件：考虑树莓派Zero2W，要能上网，有相机模块，显示模块，可能需要LED用以照明纸张。
        *所需知识：Linux，电子电路，光学相关知识
    ②采集与预处理：从相机模块获取画面（视频或连拍的照片）。首先将单词与单词分隔，再将每个字母分出来，并进行画面校正，提高对比度，去除噪声。
        *所需知识：PIL，Opencv，Python（必须）
        *可能出现的问题：如何从连续的照片或视频中确定镜头的相对位置，避免重复或漏扫？
                e.g.  a.I have a cat.
                     b.I have a cat.         I have have a cat.
         解决方案：参照全景照片用Opencv实现
    ③模型：从输入的图片预测该字母（或数字，或标点）
        *所需知识：pytorch，卷积神经网络，深度学习，Python
        *可能出现的问题：如何适应多种字体？
         解决方案：印刷和手写字体分别处理？准备多种模型？
    ④翻译层：与第三方在线翻译服务交互，返回翻译结果。
        *所需知识：requests，json，http，python
    ⑤显示（大前端）：一个开销小，流畅，美观的与用户交互的UI
        *所需知识：GTK/Qt，Python/C++，Linux界面设计，Linux显示，Linux网络连接，json
        *可能出现的问题：中文显示有误（同时需要更适合小屏幕，弱性能设备的框架）

所有人都应会的知识：
    Markdown（用于写文档）2.git（版本控制）

阶段：
    Stage1：本学期期末前完成所有基本功能，能较好实现印刷字体识别，同时有基本界面。
    Stage2：完善手写识别与抗干扰能力，美化界面，如有可能3D打印一个外壳。
