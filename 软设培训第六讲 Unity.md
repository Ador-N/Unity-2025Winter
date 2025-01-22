# 软设第六讲-Unity

**by gx, whr**

## 〇、目录

[TOC]

可能考虑做成 ppt 或者迁移到 typst，markdown 限制太大了

但是先在这里写着吧

## 一、Unity 介绍

### 1. 什么是游戏引擎？
-   游戏引擎（Game Engine）是一个用于开发电子游戏或其他交互式实时图像应用程序的综合软件框架，为开发者提供实现游戏功能所需的基本工具系统，包括图形渲染、物理模拟、声音、动画、网络通信等。功能上，它通常包含可视化编辑器、脚本支持以及与硬件交互的接口，使得游戏开发更加高效和灵活。
-   游戏引擎的主要作用是简化游戏开发流程，不需要开发者从零开始编写每个基础功能，而是允许开发者专注于游戏内容和创意，直接使用引擎的部分功能快速编写出游戏。
-   目前常用的游戏引擎有：Unity、Unreal Engine、Cocos2dx、Godot 等

### 2. 什么是 Unity？
- Unity 是一款跨平台的游戏开发引擎，可以用于开发 2D 和 3D 游戏。它提供了一个可视化的开发环境，使开发者可以轻松地创建游戏场景、添加游戏对象、设置动画和物理效果等。
- Unity 使用 C# 作为主要的脚本编程语言，开发者可以通过编写脚本来控制游戏对象的行为逻辑；Unity 还提供了许多内置的功能和工具，如碰撞检测、音频管理、粒子效果等，使开发者能够更加方便地实现各种功能。
- Unity 支持跨平台发布，开发者可以通过一次开发，将同一个游戏高效地发布到 Windows、macOS、iOS、Android、WebGL 等多个平台，触达更多的玩家。
### 3. 为什么选择 Unity？
- 成熟，应用广泛
- 简单易学，上手快
- 学习路径完善，学习资源丰富，教程、文档、社区论坛等资源全面充足
## 二、环境配置与安装
### 1. 版本

截至讲义编写时的最新 LTS（长期支持）版本：

- Unity Hub：3.11.0 / 3.3.3-c2 (*)
- Unity Editor：2022.3.56f1 / 2022.3.52f1c1 (*) (**)
- 代码编辑器：Visual Studio / Visual Studio Code / JetBrains Rider

> (&#42;) 注1：如果不使用*额外的网络工具*，大陆地区下载到的 Unity Hub / Unity Editor 通常为版本号带 c 后缀的国内特供版，而不带 c 后缀的则为国际版。通常情况下两者在使用上没有明显差别，但需要注意，最新的国内版 Unity Hub 在较为明显的位置放置了“团结引擎”的下载按钮（如下图），无视即可。
>
> <img src="pics/image-20250119211304746.png" alt="image-20250119211304746" style="zoom:25%;" />
>
> (&#42;&#42;) 注2：考虑新版本可能存在的稳定性问题，本次教程暂时不以 Unity 6 为基准版本。

### 2. 安装步骤
1. Unity Hub 安装：官网下载 Unity Hub，用于管理 Unity 版本和项目 (https://unity.com/cn/download)

2. Unity Editor 安装：安装完成后，在 Unity Hub 界面的左侧栏选择“安装”，点击右上角“安装编辑器”按钮，在“正式发行”（LTS）一栏找到需要下载的 Unity Editor（此处选择版本 2022.3.52f1c1）进行安装：

   <img src="pics/image-20250119215904554.png" alt="image-20250119215904554" style="zoom:33%;" />

   Visual Studio 、开发平台和文档等项可视需求勾选。新版本 Unity 安装时可以直接选择简体中文配置，不需要额外汉化包。

   <img src="pics/image-20250119215948789.png" alt="image-20250119215948789" style="zoom:33%;" />

   需要注意的是，Unity 各大版本之间兼容性较差。一般而言同一大版本的 LTS 版本之间差距不大，但切换大版本时通常会出现一些兼容性问题，因此一旦选定了一个大版本进行团队开发，就要统一 Unity 版本并一直使用到项目结束。

3. 获取 Unity 授权的免费个人版激活许可证

4. 代码编辑器可使用 Visual Studio（需要在安装时勾选“使用 Unity 的游戏开发”）或者 Visual Studio Code（具体在 Unity Editor 内配置，后续说明）

## 三、创建第一个项目
### 0. Unity 基本知识

<big>**Scene（场景）**</big>

**Scene（场景）** 是一个包含游戏世界的容器，包含了若干 **GameObject（游戏对象）**。一个游戏可能由多个场景组成，通过脚本在它们之间进行切换。例如，一个游戏可能包含 MenuScene（菜单场景）和 GameScene（游戏场景）。对于关卡类的游戏，可以为每个关卡独立创建一个游戏场景。

<big>**GameObject（游戏对象）**</big>
**GameObject（游戏对象）** 是 Unity 中最基本的实体单位。它可以代表场景中的任何物件，如角色、道具、环境物体等。GameObject 之间可以存在父子关系，这里的父子关系是一种层级上的组合关系或从属关系，并非父类与子类的继承关系。

<big>**Component（组件）**</big>

每个 GameObject 可以拥有若干个 **Component（组件）**，每个组件都代表着 GameObject 所具有的一种功能、行为或性质，当 GameObject 被实例化并且处于活动（Active）状态，且 Component 也处于活动状态时，它便可以控制 GameObject 的行为。通过在某些游戏对象上挂载对应的组件，可以实现特定的功能。

<big>**Script / MonoBehaviour（脚本）**</big>

**MonoBehaviour 脚本**实际上就是一种自定义的 Component，可以通过编写 C# 脚本来自定义对 GameObject 行为的控制方式，从而实现游戏所需的各种复杂逻辑。

<big>**Prefab（预设/预制件/预制体）**</big>

游戏中经常会有一些在不同时间、不同位置或不同场景重复出现的物件（如子弹、NPC、环境装饰等），在这种情况下我们可以使用 **Prefab** 以减少不必要的重复工作。Prefab 相当于一个 GameObject 的**模板**，在游戏开发和运行过程中，可以由它实例化（Instantiate）出对应的 GameObject。开发过程中，当 Prefab 被修改时，它的所有 GameObject 实例也会被修改。

<big>**Material（材质）和 Shader（着色器）**</big>

**Shader（着色器）** 是定义如何渲染物体的程序，主要包括顶点着色器和片段着色器。它负责计算物体的颜色、光照等效果；
**Material（材质）** 是控制游戏对象外观的资源，包含颜色、纹理、透明度等基本属性，也可以包括高光度、粗糙度、法线等物理 / 几何信息。每个材质都与一个 Shader 关联，决定物体如何与光源互动和呈现视觉效果。

<big>**Mesh（网格）/ Model（模型）**</big>

**Mesh** 是 3D 模型的几何数据，包含顶点、边和面，定义物体的形状。在 Unity 中，Mesh 通过 `MeshFilter` 和 `MeshRenderer` 组件显示和渲染。习惯上 **Model** 指 Mesh 加上材质、动画等其他数据构成的可渲染对象，不过区分这两者并不重要。

<big>**Sprite（精灵）**</big>

**Sprite（精灵）** 是 2D 游戏中的图像对象，使用 `SpriteRenderer` 组件进行渲染。UI 元素（如按钮、图标等）也使用 Sprite 显示图像。

<big>**Assets（资源/资产）**</big>
项目中的所有 Prefab、脚本、材质、2D 精灵图、3D 模型/纹理、音乐、场景结构数据、配置文件等资源都被称作 **Asset**，置于项目的 Assets 文件夹中。对于规模较大的工程，应该建立规范的目录结构。

### 1. 界面介绍
#### Unity Hub
在Unity Hub界面，点击“新项目”，进入创建项目界面。本次培训中，我们主要以 3D 项目为例，介绍 Unity 的基本操作；同时，为了节约环境配置时间，我们直接以 URP（通用渲染管线）模板创建项目：（关于渲染管线，在昨天的图形学一讲中已经初步提及，更进一步的解释详见后文介绍）

<img src="pics/image-20250120001819635.png" alt="image-20250120001819635" style="zoom:33%;" />

左侧可以选择创建模板类型，选择“核心模板”，“Universal 3D”，在右侧点击“下载模板”。

<img src="pics/image-20250120003714504.png" alt="image-20250120003714504" style="zoom:33%;" />

待下载结束后，可以修改合适的项目名称和位置，然后点击“创建项目”。（不要勾选“启用游戏云服务”和“使用团结云开发”）
（注1：“游戏云服务”是 Unity 中国提供的一系列*付费*服务；“团结云开发”是指 Unity 自己开发的版本管理系统 Plastic SCM，由于安装过程较为繁琐且只适用于 Unity，感兴趣的同学们可以自行了解。培训第一天我们讲解了 git，如果在此之前还没有使用 git 的经验，推荐借助软设开发的机会熟悉一下 git 的操作）
（注2：下文演示中使用的 Unity 是 2022.3.56f1 版本）
（注3：项目名和项目路径中最好不要有中文，可能会导致导出项目时因编码问题报错）

<img src="pics/image-20250120003354507.png" alt="image-20250120003354507" style="zoom:33%;" />

等待一小段时间过后，我们进入了 Unity Editor 界面

<img src="pics/image-20250120005214146.png" alt="image-20250120005214146" style="zoom:33%;" />

此时，界面右侧显示的是 URP 模板的欢迎页面，点击中部的 "Remove Readme Assets" 按钮以移除相关内容。

#### Unity Editor
##### 常用窗口
- Hierarchy（层级）：用于查看当前所选场景中的各个 GameObject 以及它们之间的层级关系（父子关系）。通过将对应资源拖拽进入该区域，可以为场景添加新的 GameObject。
- Project（项目）：用于查看当前项目所用到的各种资源（脚本代码、预制体、美术资源、材质资源、音乐资源等）。项目中的各种资源主要存放在 Assets 和 Library 两个文件夹中，前者是项目构建中主要用于操作的文件夹，后者主要存放项目引用的外部包资源和项目运行过程中生成的各种缓存文件。
- Console（控制台）：用于查看控制台输出，可用于查看报错信息和项目 Debug 输出信息。
- Inspector（检查器）：检查当前所选 GameObject 或 Asset 的属性，为游戏对象添加、更改或删除组件等。
- Scene（场景）、Game（游戏）：**核心操作面板**。场景面板用于调整游戏对象位置、大小等在游戏场景中的形态。游戏面板等于是对游戏功能的测试，能够准确体验游戏的运行状态。当我们在场景中完成全部的部署之后，点击运行按钮，就可以开始游戏（开始测试）。中断按钮可以暂停当前游戏并切换回场景面板以查看对象的实时属性。
### 2. 游戏对象
#### 1. Main Camera
- 项目初始化后，初始场景 Sample Scene 会自带游戏对象 Main Camera，用于将其范围内的游戏场景在游戏界面中显示出来。
- Main Camera 挂载的 Camera 组件可以设置摄像机的诸多属性（如画面大小），Transform组件可以使摄像机在游戏进程中随时改变位置，获得灵活的运镜效果（这在3D游戏中尤为重要）
#### 2. 静态对象的创建
- Unity 提供了一系列简单的几何对象

  <img src="pics/image-20250121005749877.png" alt="image-20250121005749877" style="zoom: 50%;" />

  利用“场景”左上角提供的变换工具对模型进行变换，在检查器面板上观察图形的 Transform 组件变化

  <img src="pics/image-20250121120405403.png" alt="image-20250121120405403" style="zoom:33%;" />

- 如何添加素材作为游戏对象？

1. 将素材导入到项目文件夹 Assets 下（注意尽可能按照资源类别细分素材并建立文件夹，如 Scenes、Scripts、Materials、Sprites、Models 等）
2. 在检查器中设置需要导入的素材的相关属性（对于一般的 2D Sprite 图片素材，推荐更改过滤模式为“点”，压缩修改为“无”，更改后点击应用）

![image-20240130205638172](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205638172.png)

3. 拖拽素材进入场景，可以看到“层级”视图中新增了游戏对象

- 如何切分帧图片和导入动画？
  
  1. 选择需要切分的帧图片，在检查器中选择Sprite模式为“多个”，点击“应用”后单击“Sprite Editor”进入Sprite编辑器，在左上角的切片中按照cell大小完成切分。
  
  ![image-20240130205653050](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205653050.png)
  
  2. 按照顺序选择合成动画的帧，拖拽至对应游戏对象上，Unity即可自动生成动画文件。
  3. 选择对应游戏对象后，在“动画”选项卡（注意不是“动画器”)即可播放对应动画。
  
-   关于动画，更全面、系统、深层次的应用：动画状态机（Animator）
    -   状态，即动画的效果，比如人物静止的时候会有上下轻微浮动的动画，人物走的时候有个行走的动画，人物攻击的时候有个攻击的动画，跳跃的时候有个跳跃的动画，这些不同的动画状态，都是通过**状态机**连接起来的。
    -   既然有不同的状态，那么就应该有状态转换的条件，比如：
        -   人物什么时候从站立状态转而变成走路的状态 —— 按下 WSAD 键盘
        -   人物放完技能之后应该自动回到站立（挂机）状态，肯定不能一直放技能（有 CD 存在）
        -   这些控制条件由挂载在人物上的脚本，结合 Unity 的动画状态机控制
## 四、交互逻辑：组件与脚本
-   组件就是积木，需要用到的时候就添加。
-   一个个组件共同构建起了**功能完整**的游戏对象。
#### 1. 一般组件
一些常见的 Components 及其对应功能：

| 分类      | 名称                                 | 功能                                                         |
| --------- | ------------------------------------ | ------------------------------------------------------------ |
| 通用      | `Transform`（变换）                  | 所有 GameObject 的固有属性：位置、朝向、缩放、层级关系       |
| 外观 (3D) | `MeshFilter`                         | 为 GameObject 指定一个 3D 模型                               |
|           | `MeshRenderer`                       | 用指定的材质（Material）渲染 MeshFilter 中的 3D 模型         |
| 外观 (2D) | `SpriteRenderer`                     | 用指定的材质渲染 2D 精灵图                                   |
| 渲染      | `Camera`                             | 使游戏对象具备摄像机功能                                     |
|           | `Light`                              | 使游戏对象具备灯光功能                                       |
|           | `Volume` / <br />Post-process Volume | URP / HDRP 自带，指定后处理功能的生效范围<br />若使用内置渲染管线，则需自行导入 Post Processing 包 |
| 物理      | `xxxCollider`                        | 各种形状的碰撞器                                             |
|           | `Rigidbody`                          | 刚体物理模拟                                                 |
| 动画      | `Animation`                          | 在游戏对象上播放某个固定的动画片段（Animation Clip）         |
|           | `Animator`                           | 动画状态机，详见后文介绍                                     |

值得注意的是，Unity内置了强大的物理系统，可以给对象挂载组件使其符合一定物理规律。

- 给游戏对象挂载 Rigidbody 组件，观察游戏对象行为

  ![image-20240130210029878](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130210029878.png)

- 使游戏对象之间发生碰撞：两个对象均挂载了碰撞体（Collider / Collider 2D）组件，运动一方的 Rigidbody 组件碰撞检测设置为“持续”

  ![image-20240130205955717](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205955717.png)

- 更改游戏对象物理材质（增加反弹、摩擦等）：新建物理材质，设置相关摩擦和弹力系数，替换掉Rigidbody 组件原物理材质。

#### 2. 脚本
1. 配置脚本编辑环境：在 Unity 中选择编辑 → 首选项 → 外部工具 → 外部脚本编辑器，选中 Visual Studio 或 Visual Studio Code 即可
2. 创建一个简单的脚本（Project窗口右键 → 创建 → C#脚本）

      ```csharp
      using System.Collections;
      using System.Collections.Generic;
      using UnityEngine;
      public class PlayerControl : MonoBehaviour
      {
      	// Start is called before the first frame update
      	void Start()
      	{
      
      	}
      	// Update is called once per frame
      	void Update()
      	{
      
      	}
      }
      ```
  - `MonoBehavior`：脚本创建时默认会挂载到游戏对象上，class 自动继承 MonoBehavior。如果该脚本不需要直接挂载到游戏对象上发挥效果，则不需要继承自MonoBehavior。
  - `void Start()`：场景加载时执行一次的函数，用于初始化。
  - `void Update()`：游戏运行时每一帧都会执行一次，用于实时同步游戏数据，主要代码通常都需要每一帧都执行。

3. 在 `Start` 函数中写入以下代码，并将脚本挂载到 player 上

	```csharp
	Debug.Log("Hello world!");
	```
运行游戏，控制台输出了一次Hello world信息

![image-20240130210158347](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130210158347.png)

4. 碰撞事件和触发事件：
   游戏对象的碰撞体与其他碰撞体发生碰撞时会调用碰撞事件：
   包括 OnCollisionEnter(2D) （碰撞开始时执行）、 OnCollisionExit(2D) （碰撞结 束时执行）、 OnCollisionStay(2D) （碰撞过程中每个时间步长执行一次)

   ```csharp
   private void OnCollisionEnter(Collision collision) // Collision 类，存储碰撞对象、位置等信息
   {
		Debug.Log(name + " collided with " + collision.collider.name);
   }
   ```
   在碰撞器组件上勾选了“是触发器”后，物体便不会与其他碰撞体发生碰撞，取而代之的是在相互穿过时调用触发事件：
   包括 OnTriggerEnter(2D) （接触开始时执行）、 OnTriggerExit(2D) （接触结束时执行）、 OnTriggerStay(2D) （接触过程中每个时间步长执行一次）

   ```csharp
   private void OnTriggerStay2D(Collider2D collider) // Collider 类，仅包含碰撞体本身的信息
   {
		Debug.Log(name + " contacting with " + collider.name);
   }
   ```

#### 3. MonoBehaviour 生命周期

<img src="pics/Unity MonoBehaviour Main Lifecycle.svg" alt="image-20250121120405403"/>

TODO

## 五、视觉效果：材质与渲染

### 0. 光栅渲染管线

#### 概念

<img src="pics\SRP Minimal.svg" alt="SRP Minimal" style="zoom:60%;" />

<img src="pics\SRP Detailed.svg" alt="SRP Detailed" />

（以上两张图片分别出自 2024 暑培 / 寒培《实时渲染基础魔法》）

* 本教程不再强调“可编程”，因为事实上所谓的“固定渲染管线”早在 2000 年代就基本消失了。
  * 2008 年 OpenGL 3.0 将固定渲染管线标记为过时（deprecated），2009 年 OpenGL 3.2 完全移除固定渲染管线。

<img src="pics\Unity 渲染管线.png" alt="Unity 渲染管线" style="zoom:40%;" />

* Unity 的 Scriptable Rendering Pipeline（SRP）中的 "Scriptable" 实际上也并不是指顶点着色器和片元着色器的"可编程"，因为此前的内置（Built-In）渲染管线显然也可以对着色器进行编程，它并不是所谓的“固定渲染管线”。此处的”可编程“指的是在着色器之外，对整个渲染流程进行控制，当然这些就并不在本次教程的范围内了。

#### 顶点着色器

将 **模型空间（Model / Object / Local Space）** 的顶点坐标通过一系列矩阵变换，转换到 **屏幕空间（View / Screen Space）**。

此处的一系列矩阵变换，被称为 **MVP**（Model View Projection）变换。当然，这些变换矩阵都会由管线的其他部分提供，因此我们无需关注具体的数学细节，此处仅列出变换的大致流程：

|                   模型空间（Object Space）                   |                   世界空间（World Space）                    |                   相机空间（Camera Space）                   |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img src="pics\image-20250122181433789.png" alt="image-20250122181433789" style="zoom: 25%;" /> | <img src="pics\image-20250122181441125.png" alt="image-20250122181441125" style="zoom: 25%;" /> | <img src="pics\image-20250122181447153.png" alt="image-20250122181447153" style="zoom: 25%;" /> |

以上三个空间坐标间的转换较简单，仅涉及刚体变换（旋转、平移）

| 相机空间（Camera Space） →   裁切空间（Clip Space） →   归一化设备坐标（NDC） |
| :----------------------------------------------------------: |
| ![img](pics\Screenshot_2022-04-27_094119_efatap.png) |

以上转换涉及一些较复杂的透视变换，最后还会由归一化的设备坐标变换到实际的屏幕空间坐标。

> 注 1：除了 NDC 和屏幕空间坐标外，这里所有的变换矩阵和向量实际上都是四维的。为什么？[Wikipedia:齐次坐标](https://zh.wikipedia.org/wiki/齐次坐标)
> 注 2：从裁切空间到NDC、屏幕空间的变换由渲染管线和驱动程序自动完成，因此实际 Shader 中只需变换到裁切空间即可。

理论上来说，所有与模型的几何信息相关，并且 **不改变顶点数量** 的功能，都可以由顶点着色器实现，例如，可以根据时间等输入来动态地改变顶点位置，以实现波动、变形等效果。除此之外，在实际的工程应用中，顶点着色器也可以用于将更多的几何数据传递给片元着色器，以备处理。后文将用 ShaderGraph 可视化编程的形式编写顶点着色器，实现模型描边功能。

#### 中间步骤

这一步包括三角形建形、光栅化等步骤，这些计算由引擎或驱动程序等完成。

但在此之前，还可以插入两个步骤：*曲面细分着色器* 和 *几何着色器*。这两个着色器的引入，主要是为了解决顶点着色器<u>无法改变顶点数量</u>的限制，从而对视觉效果实现更灵活的调控，具体细节可以自行了解。

#### 片元着色器

给 **片元（Fragment）**（即未上色的**像素**）上色，通常利用 BRDF 对光照信息的计算通常就发生在此步骤：
$$
L(\boldsymbol{x},\boldsymbol{\omega}_o)
=\mathcal{K}_\text{S} L + L_\text{r}^\text{e}(\boldsymbol{x})
=L_\text{r}^\text{e}(\boldsymbol{x},\boldsymbol{\omega}_o)
+\int_\Omega f_\text{r}(\boldsymbol{x}, -\boldsymbol{\omega}_i \rightarrow \boldsymbol{\omega}_o)
\cdot L(\boldsymbol{x},\boldsymbol{\omega}_i)
\cdot \cos\theta_i \, \mathrm{d} \boldsymbol{\omega}_i
$$
理论上来说，所有与颜色（RGB**A**）有关的功能，都可以由片元着色器实现。后文将用 HLSL 编写片元着色器，实现非真实感渲染中的 Toon Shading（卡通着色）功能。

### 1. ShaderGraph

#### 此处参考往年 Unity，但是要大改

目前计划：顶点着色器描边

Toon Shading 没法直接做，放后处理或者HLSL那边吧

### 2. PBR（Physics-Based Rendering）工作流

在 2D 作品中，我们基本只需要一系列精灵图和一些简 单的特效处理，就可以实现大部分的视觉效果。但是在 3D 游戏，尤其是追求物理真实感的 3D 作品中，是否仍然这么简单？

回顾 BRDF 表示的渲染方程：

$$
L(\boldsymbol{x},\boldsymbol{\omega}_o)
=L_\text{r}^\text{e}(\boldsymbol{x},\boldsymbol{\omega}_o)
+\int_\Omega f_\text{r}(\boldsymbol{x}, -\boldsymbol{\omega}_i \rightarrow \boldsymbol{\omega}_o)
\cdot L(\boldsymbol{x},\boldsymbol{\omega}_i)
\cdot (\boldsymbol{n} \cdot \boldsymbol\omega_i)\, \mathrm{d} \boldsymbol{\omega}_i
$$

如果已知发射部分（即 $L_\text{r}^\text{e}$）和 BRDF（即 $f_\text{r}$），我们便能写出片元着色器，让渲染管线帮我们计算以上表达式。现在的问题是，如何表示这两者，即：如何对物理表面建模？

图形学一讲中介绍了 Lambert 漫射模型和 GGX 高光模型。现实生活中，一个表面显然并不会非黑即白地表现为“漫射”和“高光”中的一种，而往往是两种属性的混合，因此我们用这两个模型的加权求和来表示 BRDF，这便是实时渲染中常用的 Cook-Torrance BRDF：

$$
f_\text{r}(\boldsymbol{x}, -\boldsymbol{\omega}_i \rightarrow \boldsymbol{\omega}_o)
= \frac{\boldsymbol\rho_\text{d}(\boldsymbol{x})}{\pi}
+ \frac{\boldsymbol\rho_\text{s}(\boldsymbol{x}) \cdot F\cdot D_{\alpha} \cdot G_{\alpha} }{4(\boldsymbol{n}\cdot\boldsymbol\omega_i)(\boldsymbol{n}\cdot\boldsymbol\omega_o)}
$$

其中， $\boldsymbol\rho_\text{d}$ 表示漫射颜色， $\boldsymbol\rho_\text{s}$ 表示高光强度， $\alpha$ 表示表面的粗糙程度，它们都与空间位置 $\boldsymbol{x}$ 有关。实际上，漫射颜色就是我们平时一般所说的模型上的“贴图”。以此类比，高光度、粗糙度、自发光颜色等与位置有关的参数，也都可以用 uv 坐标下的纹理贴图（灰度图）的形式来表达、存储。通过生成并使用各种物理参数纹理，并结合基于物理的光照模型，以渲染出具有真实感和物理一致性的材质表现，这一完整流程便被称为 **PBR 工作流**。

目前流行的 PBR 工作流主要有两种：**金属—粗糙度**（Metallic-Roughness）工作流和**镜面—光泽度**（Specular-Glossiness）工作流。你能找到的 PBR 材质资源都属于这两种工作流之一，两者的区别仅在于对漫射/高光强度和粗糙程度参数作了不同的映射，感兴趣的话可以查阅这两篇文章以了解它们的具体[联系](https://docs.unity3d.com/Manual/StandardShaderMaterialCharts.html)和[区别](https://blog.csdn.net/s178435865/article/details/134975030)。

除此之外，为了节省各种开销，通常会把 Blender、ZBrush 等建模软件中制作的高模转化为面数较少的低模，再导入 Unity 等实时渲染引擎中。为了弥补这一过程带来的模型精度损失，我们可以将这些损失掉的高度、法线、曲率等几何信息也制作成纹理，使其参与到渲染方程的计算中，获得更逼真的效果。（注意，这些纹理并不会用于对网格的几何信息作任何修改，只会通过渲染的光照明暗表现出来，也可以认为是一种“幻术”）

为了便于理解和配置，这里列出 PBR 工作流中常见的贴图名称及其含义，更详细的介绍可见这篇[文章存档](https://web.archive.org/web/20230812220537/https://help.quixel.com/hc/en-us/articles/115000612165-What-maps-are-included-and-how-do-I-use-them-)：

<table><tbody>
    <tr><td colspan="2"> <strong>金属度流程</strong> </td><td colspan="2"> <strong>镜面反射流程</strong> </td></tr>
    <tr><td> <strong>Base Color (COL)</strong> </td><td> 漫射颜色 + 镜面反射F0 </td><td> <strong>Diffuse / Albedo</strong> </td><td> 漫射颜色 </td></tr>
    <tr><td> <strong>Metallic</strong> </td><td> 金属度 </td><td> <strong>Specular (REFL)</strong> </td><td> 镜面度 </td></tr>
    <tr><td> <strong>Roughness</strong> </td><td> 粗糙度 </td><td> <strong>Gloss / Smoothness</strong> </td><td> 光泽度（1 - 粗糙度） </td></tr>
</tbody></table>

| Emission | Bump / Height | Normal (NRM) | AO / Occlusion |
| -------- | ------------- | ------------ | -------------- |
| 自发光   | 高度          | 法线方向     | 环境光遮蔽信息 |

以下贴图对应 URP 默认着色器未直接实现的功能：

| Cavity | Curvature | Fuzz         | SSS        | Displacement (DISP)        |
| ------ | --------- | ------------ | ---------- | -------------------------- |
| 缝隙   | 曲率      | （织物）模糊 | 次表面散射 | 置换（**真正的**几何变换） |

（→ 实操环节）

### 3. 后处理

图形学一讲中已经介绍过后处理技术，它实际上是为了弥补光栅管线的不真实性而诞生的一种“补正措施”，由于它的实质是对二维图像的处理与合成，可以将其理解为某种“滤镜”；当然，在实际游戏开发中，除了追求真实性，一些特殊的视觉特效也可以利用后处理的手段实现。

Unity 中的后处理系统主要由以下模块配置：

- Post-process Volume（后处理体积，SRP 中简称为 Volume / 体积）及其对应配置文件
  - 主要包括辉光（Bloom）、景深（Depth of View）、运动模糊（Motion Blur）及各种颜色调整等接近于纯粹图像处理的后处理效果
  - “体积”的含义：在不同空间范围内施加不同的后处理效果，默认使用 Global Volume（全局体积）

- Settings 文件夹内 Renderer 配置文件中的 Renderer Feature 配置项
  - 主要包括屏幕空间环境光遮蔽（SSAO）等较复杂的后处理效果，以及用于附加自定义的后处理效果、


<div style="text-align: center"><img src="pics/image-20250121130327223.png" alt="image-20250121130327223" style="zoom:33%;" /><img src="pics/image-20250121130823344.png" alt="image-20250121130823344" style="zoom: 33%;" /></div>

如图所示，在 URP 模板自带的 Global Volume 和 高保真度 Renderer 中，分别已经预先配置了 Tone Mapping（色调映射）、Bloom（辉光）、Vignette（光晕）三个后处理 Override 和 Screen Space Ambient Occlusion（屏幕空间环境光遮蔽）一个渲染特性。可以勾选属性左侧的复选框，然后修改对应的属性配置；点击下方的 Add Override / Add Renderer Feature，即可添加并配置新的后处理效果。

例如，在 Global Volume 下点击 Add Override，选择 Post-processing → Chromatic Aberration，勾选 Intensity（强度）左侧的复选框，拖动滑动条，即可观察到画面边缘出现了明显的色散效果。

<img src="pics/image-20250121132118218.png" alt="image-20250121132118218" style="zoom:33%;" />

TODO：ShaderGraph Toon Shading？

### 4. HLSL

#### 可能来不及准备/讲，先放个标题在这

不过 ShaderGraph 这个内嵌 HLSL 用起来感觉还凑合，可以简单提两句。

不是 ShaderGraph 怎么不支持多 pass，那还是提一下吧，但是 URP 疑似本来就不支持多 pass

## 六、写在最后

作为一个最简单的入门教程，本篇基本只是让大家认识unity，下载安装unity、了解unity的基本界面和用法。作为一个工具型软件，最好的学习方法永远是实战，推荐大家直接按照教程开发一个小项目，体会到游戏开发的乐趣。

下面是一些实用的文档和教程，希望对大家有所帮助

- [Unity官方文档及API说明](https://docs.unity3d.com/cn/current/Manual/UnityManual.html)
- [完整游戏制作合集教程](https://space.bilibili.com/390481111/channel/collectiondetail?sid=1064344)
- [Unity特效渲染合集教程](https://space.bilibili.com/390481111/channel/collectiondetail?sid=1181615)
- [【Unity】有趣的游戏技巧（轮子）教程合集](https://space.bilibili.com/390481111/channel/collectiondetail?sid=1097746)

素材网站：

- [itch.io](https://itch.io/) （2D 为主）
- [Quixel Megascans](https://quixel.com/megascans/home) （大量 3D PBR 素材）
- [Unity Asset Store](https://assetstore.unity.com/zh) （可直接导入 Unity 的素材和脚本库等）
- [HotpotDesign/Game-Assets-And-Resources](https://github.com/HotpotDesign/Game-Assets-And-Resources) （素材网站集合）

参考 & 致谢：

* 寒培2023 Unity by ysq&ltx- THUEE-Unity暑培教程
* 寒培2024 Unity by hzf
* 寒培2024 & 暑培2024《实时渲染基础魔法》 by Tianyu Huang
