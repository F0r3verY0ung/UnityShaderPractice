# GetStartedWithShaders

个人基于 Unity 的 Shader 学习项目，从基础到进阶掌握卡通渲染、透明/AlphaTest 处理、轮廓描边以及后处理效果的实现方式。

- 学习 Unity ShaderLab / HLSL 基础
- 理解 Toon Shading 的常见实现方式
- 探索渐变明暗、边缘光、透明材质与后处理调色
- 作为教程式练习项目进行逐步扩展

## 概览

当前仓库包含:
- 卡通渲染基础着色器
- 艺术风格的渐变明暗与高光处理
- AlphaTest / Transparent 分离实现
- 共享 `cginc` 公共函数
- Outline 轮廓效果
- Stylized Tonemap 后处理
- Unity 场景与材质示例

## 当前版本说明

使用的 Unity 版本为:
- Unity 2022.3.62f3c1

依赖项包括:
- `com.unity.postprocessing`
- `com.unity.ai.navigation`
- `com.unity.textmeshpro`
- `com.unity.timeline`
- `com.unity.ugui`

## 目录结构

```text
GetStartedWithShaders/
├── Assets/
│   ├── Materials/              # Unity 材质示例
│   ├── Scenes/                 # 场景与后处理配置
│   ├── Scripts/                # 后处理脚本
│   ├── Shaders/                # 着色器与共享 cginc
│   └── StepByStep/             # 教程步骤资产
├── Packages/
│   ├── manifest.json
│   └── packages-lock.json
├── ProjectSettings/
├── .gitignore
├── README.md
├── build_shader_pdf.py
├── build_toonopaque_step2_docx.py
├── Assembly-CSharp.csproj
├── GetStartedWithShaders.sln
└── LICENSE
```

## 关键着色器

### 1. `Toonopaque.shader`
用于基础卡通渲染，核心特征包括:
- 渐变贴图三阶明暗
- 高光
- 边缘光
- 教程第 2 步对齐的材质参数设计

### 2. `ToonAlphaTest.shader`
用于 AlphaTest 透明裁剪材质，适合处理:
- 需要透明裁剪但不是真正半透明的材质
- 例如毛发、叶片、装饰面片等

### 3. `Toonopaque Transparent.shader`
用于真正透明效果，适合:
- 玻璃
- 薄膜
- 半透明表面

### 4. `ShadingCommon.cginc`
公共光照相关函数，统一共享:
- 漫反射计算
- 高光计算
- 渐变明暗逻辑
- 统一材质参数接口

### 5. `OutlineCommon.cginc`
轮廓描边公共逻辑，负责处理:
- 边缘轮廓参数
- 统一的描边属性声明
- 避免跨平台编译问题

### 6. `StylizedTonemap.shader`
风格化色调映射后处理，适合对最终画面做:
- 低饱和
- 电影级色彩压缩
- 统一整体风格

## 后处理说明

项目中已经接入了 Unity Post Processing，并提供了:
- `StylizedTonemap.cs`：脚本挂载与参数驱动
- `MainScene_Profiles`：后处理配置文件

这样可以在场景中直接观察:
- 低对比度风格化色调
- 更统一的卡通着色输出
- 视觉风格一致性

## 学习步骤进度

当前项目较为接近:
- 第 1 步：基础 Toon Shading
- 第 2 步：渐变明暗 + AlphaTest/Transparent 拆分 + Stylized Tonemap

后续可以继续扩展:
- 更细致的阴影处理
- 脚本控制材质参数
- 多种光源类型
- 物理材质/法线贴图集成
- 更复杂的边缘光和描边系统

