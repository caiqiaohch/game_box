[![CI](https://github.com/QQxiaoming/game_box/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/QQxiaoming/game_box/actions/workflows/ci.yml)
[![CodeFactor](https://www.codefactor.io/repository/github/qqxiaoming/game_box/badge)](https://www.codefactor.io/repository/github/qqxiaoming/game_box)
[![GitHub tag (latest SemVer)](https://img.shields.io/github/tag/QQxiaoming/game_box.svg)](https://github.com/QQxiaoming/game_box/releases)
[![GitHub All Releases](https://img.shields.io/github/downloads/QQxiaoming/game_box/total.svg)](https://github.com/QQxiaoming/game_box/releases)

# game box

## 概述

GameBox是一款游戏家用机模拟器，本项目基于Qt,可在windous\mac\linux等多平台使用。由于本项目基于多种开源代码开发而成，强烈提醒注意license说明。

### 平台支持

- 基于InfoNES实现NES游戏模拟器(基本完成，InfoNES的好处是性能开销较少，但目前看起来兼容性较差，且音频处理较差，有计划考虑重构改用fceux实现)
- 基于dgen-sdl实现MD游戏模拟器(已完成)
- 基于VBA-M实现GBA游戏模拟器(计划中)

### 功能机制

- 静音(已完成)
- 按键配置(进行中)
- 存档读档的全局机制(计划中)
- 截图(计划中)

## nes

基本移植完成，针对常见的InfoNES移植进行了一些问题修复：

- 图像颜色输出正确（部分其他项目存在图像输出颜色发红）
- 画面纹理输出正常不错位（部分其他项目在不同编译器下存在该问题，可以使用本项目中SuperMario.nes文件测试）

目前还存在的一些待解决的问题：

- 音频输出音质不高，且存在一些错误

> 2021.02.07:完成InfoNES显示，输入移植并优化代码修复bug。<br>
> 2021.02.08:回家过年，高铁度过。<br>
> 2021.02.09:音频移植，声音看起来有些不对啊，但没找到可靠的资料，待分析。<br>
> 2021.02.10:优化一下整体框架结构代码，nes准备放一下开始移植md了。<br>
> 2021.02.13:音频问题看来解决不了，目前考虑改用移植fceux/fceu，已测试fceux-2.3.0和fceu-0.98.12版本，兼容性良好，音频正确，但存在一些国产修改版rom打开不正确反而InfoNES是正确的，有待结合分析并给出最终移植。<br>
> 2021.02.14:一个人的情人节，没啥心情，早上简单优化了些代码写法，出去转转，晚上回来没写代码，查查资料，测试一下fceu。经过测试发现部分国产修改版rom无法正确工作的原因与模拟器RAM初值有关，由于ROM修改者错误修改导致未进行初值赋值操作因而依赖原本的RAM值，该问题已在fceu上测试确认该问题，经过分析目前基本决定基于fceu-0.98.12版本移植，并增加模拟器配置选项选择RAM初始化模式以兼容更多（低质量）ROM。<br>
> 2021.02.15:不死心，又分析了一天InfoNES的APU移植代码，基本确认问题出在没有根据FrameAPU时钟计算音频sweep、hold等信息导致触发（事件）类的音频生成错误，可以参考这个地址说明：[Nesdev wiki](http://wiki.nesdev.com/w/index.php/APU#Noise_.28.24400C-400F.29)。尝试fceu移植，比较麻烦耦合的内容过多不是很好移植，目前考虑暂时搁置，看是否有可能修复InfoNES的问题。<br>
> 2021.02.15:今天在这个网站：[nes emulators](https://patpend.net/ftp/emulators/nes/)找到了早年间NES的各种移植版本，合并了InfoNES097J版本，并且修改了部分APU相关代码，目前的效果有所改善，但还达不到fceu的程度。<br>
> 2021.02.16:基本上确定了pulse通道的envelope generator和sweep unit未正确实现，triangle/noise/DPCM通道实现错误，修复了部分triangle/noise通道的频率计算错误问题，其他的暂时不好修复，需要修改实现框架，假期结束了，暂时就进行到这了，后面有空慢慢完善。<br>

## md

基于dgen-sdl-1.33移植完成，效果良好，目前未发现任何问题。存档功能还未移植实现，目前考虑实现一个整体上的存档机制而不去移植实现具体平台的存档机制。

> 2021.02.10:开始合入dgen-sdl-1.33代码。<br>
> 2021.02.11:移植完成，显示正常，还算比较顺利，准备过年了。<br>
> 2021.02.12:大年初一，早上小改了一下，出去玩，鸽一天。<br>
> 2021.02.13:输入和音频移植完成，效果非常好，优化了帧率计算，这个太顺利了。<br>

## gba

计划中
