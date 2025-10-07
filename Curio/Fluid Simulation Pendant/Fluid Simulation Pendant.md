---
tags:
  - 手工
  - ESP32
  - Index
title: Fluid Simulation Pendant
created: 2025-10-04 23:46:05
modified: 2025-10-07 09:47:18
status: On Going
类别: "[[../Curio|Curio]]"
cssclasses:
  - curio
---

# Fluid Simulation Pendant

## 项目概览

> 原项目：[Fluid Simulation Pendant by mitxela](https://mitxela.com/projects/fluid-pendant)

偶然在网上看到了mitxela做的这个流体挂坠，很喜欢，遂想要复刻。不过奈何水平实在有限，做不到原作那种从零开发，只能退而求其次选择一些半成品组装。

## 硬件

硬件部分主要由屏幕、开发板、电源、外壳组成。

详见[[details/硬件]]部分介绍。
## 软件与开发环境

- 开发工具选择（Arduino IDE / PlatformIO / ESP-IDF）
    
- 驱动与库安装记录
    
    - TFT/AMOLED 显示库（LovyanGFX、TFT_eSPI）
        
    - 触摸屏驱动
        
    - UI/动画库（LVGL，可选）
        
- 配置说明
    
    - PSRAM 启用
        
    - SPI 时钟设置
        

## 显示与渲染实现

- **基础显示测试**（颜色渐变、文字、图像）
    
- **帧缓冲管理**（单缓冲/双缓冲）
    
- **流体仿真 / 动画算法**
    
    - 简化目标（美观优先，不追求真实流体力学）
        
    - 实现方法（噪声场、粒子场、涟漪扩散等）
        
- **触摸交互**
    
    - 手势检测
        
    - 液体搅动效果
        

## 性能与优化

- 内存使用情况（帧缓冲大小、PSRAM 分配）
    
- 帧率测试（目标 FPS 与实际 FPS）
    
- 优化手段
    
    - 降低运算分辨率 → 插值放大
        
    - 使用 DMA 传输提升刷新效率
        
    - 色彩与功耗平衡
        

## 成品与展示

- 外壳与电路组装
    
- 吊坠佩戴效果
    
- 成品演示视频 / 照片
    
- 与原版作品对比总结
    

## 经验与反思

- 复刻过程中的主要困难与解决方案
    
- 下一步改进方向（例如：更高分辨率屏幕、AI 生成流体效果、无线交互等）
    
- 对未来类似项目的建议
