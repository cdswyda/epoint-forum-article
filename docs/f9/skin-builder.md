# F9 在线换肤工具

![](./_image/skinBuilder.gif)

## 体验入口

**OA首页 :arrow_right: 门户 :arrow_right: 产品设计中台 :arrow_right: 在线工具 :arrow_right: 框架在线换肤**

体验地址： [https://fe.epoint.com.cn/fedemo/pages/f9skinbuilder/](https://fe.epoint.com.cn/fedemo/pages/f9skinbuilder/)

## 使用介绍

![skin-builder](./_image/skinbuilder.png)

直接调整各个色板的颜色，即可在右侧实时看到对应的效果。

生成皮肤文件基于9个色值， 不过大多数情况下，仅用配置一个主色和对应的两个辅色即可。

颜色的具体规则可参考[控件换肤配色规则](https://docs.qq.com/sheet/DSnVyZmhkTHluYUJN?opendocxfrom=admin&tab=BB08J2)

:::tip
文本框聚焦边框默认使用主色调，直接和主色调进行联动，但当主色调为红色时，请将其配置为其他颜色，以避免聚焦的红色和验证失败的红色存在冲突和歧义。
:::

## 背后工作

能做到目前这样的效果，前期可是下了大工夫的：

### 图标字体化

为了实现如此的效果，目前框架布局以及miniui控件中使用的所有的小图标均是字体图标，没有任何一张是图片。因为在使用字体图标时，可以直接通过css为其设置颜色。而如果是图片的话，要想直接通过css来改变其颜色，实现比较复杂，而且更关键的是，IE浏览器还完全不支持这一项技术。

在此过程中，针对很多操作图标进行了优化，同时还新增了一些操作图标和模块图标，具体请在 [产品设计中台 (控件 :arrow_right: 图标 icon)](https://designplatform.epoint.com.cn/epoint-web/designstage/designplatform/dist/#/design/multiple/60009229-813d-4bdb-aa1c-2486c2dbcc56) 中查看。

图标的设计和调整是一项很耗费时间的工作，此过程中特别感谢UI团队的鼎立支持。

### 颜色规则形成

调整几个颜色就要能生成一套皮肤，各个地方如何根据所选定的一种或几种颜色进行特定的变化，既要能满足视觉效果，又要能够利于运算和实现，最终形成这一套规则也经历了很久的研究和实践。此过程中也需要感谢UI团队的支持。

### 皮肤编译过程实践

之前的换肤相关的预编译是通过 [SASS](https://sass-lang.com/) 来完成的，此工具基于 Ruby 开发，需本地安装，不利于做成在线工具。虽有 node-sass 的版本，但其安装容易出错，且需要在服务端运行，也不利于直接做成在线工具。 经过实践研究，发现 [Less](http://lesscss.org/) 本身就是以 JavaScript 开发的，虽然大多数情况是作为小工具在node中运行的， 但其本身可以在浏览器中运行，且支持简单的编译工作，因此选定改为 Less 来作为皮肤的预编译语言。

### 在线换肤工具的开发

有了字体图标的支持，就可以用css来控制图标颜色，再也不用逐个切图替换了。同时颜色规则的形成和皮肤编译的支持，使得可以直接配置几个颜色来生成一份皮肤样式文件。但是如何修改几个颜色，如何进行文件的编译，此过程对不具备相关知识的人来说，还是一个很高的门槛。因此我们开发了本文所介绍的在线工具：

- 直接点击更改颜色，工具将立即进行编译，并在右侧提供实时预览。
- 可随时查看和下载编译好的皮肤文件。
- 同时还提供框架已有的预设皮肤颜色配置
- 你还可以将你的调整在本地进行存储，下次可直接载入。

## 说明

:::warning
- 目前此工具仅支持 **F9.4**
- 此工具基于对框架和miniui相关图标全部有图片改为字体图标的，无法不升级直接使用
- 此功能和工具对其他版本的支持尚未确定
:::

<Vssue title="F9 在线换肤工具" />