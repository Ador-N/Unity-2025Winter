# 软设第六讲-Unity

**by gx, whr**

## 〇、目录

额这东西应该存在吗

过会儿再说

可能考虑做成 ppt 或者迁移到 typst，markdown 限制太大了

## 一、Unity介绍

### 1、什么是游戏引擎？
-   游戏引擎（Game Engine）是一个用于开发电子游戏或其他交互式实时图像应用程序的综合软件框架，为开发者提供实现游戏功能所需的基本工具系统，包括图形渲染、物理模拟、声音、动画、网络通信等。功能上，它通常包含可视化编辑器、脚本支持以及与硬件交互的接口，使得游戏开发更加高效和灵活。
-   游戏引擎的主要作用是简化游戏开发流程，不需要开发者从零开始编写每个基础功能，而是允许开发者专注于游戏内容和创意，直接使用引擎的部分功能快速编写出游戏。
-   目前常用的游戏引擎有：Unity、Unreal Engine（虚幻）、Cocos2dx、Godot 等

### 2、什么是Unity？
- Unity 是一款跨平台的游戏开发引擎，可以用于开发 2D 和 3D 游戏。它提供了一个可视化的开发环境，使开发者可以轻松地创建游戏场景、添加游戏对象、设置动画和物理效果等。
- Unity 使用 C# 作为主要的脚本编程语言，开发者可以通过编写脚本来控制游戏对象的行为逻辑；Unity 还提供了许多内置的功能和工具，如碰撞检测、音频管理、粒子效果等，使开发者能够更加方便地实现各种功能。
- Unity 支持跨平台发布，开发者可以通过一次开发，将同一个游戏高效地发布到 Windows、macOS、iOS、Android、WebGL 等多个平台，触达更多的玩家。
### 3、为什么选择 Unity？
- 成熟，应用广泛
- 简单易学，上手快
- 学习路径完善，学习资源丰富，教程、文档、社区论坛等全面充足
## 二、环境配置与安装
### 1、版本

截至讲义编写时的最新 LTS（长期支持）版本：

- Unity Hub：3.11.0 / 3.3.3-c2 (*)
- Unity Editor：2022.3.56f1 / 2022.3.52f1c1 (*) (**)
- 代码编辑器：Visual Studio / Visual Studio Code / JetBrains Rider

> (&#42;) 注1：如果不使用*额外的网络工具*，大陆地区下载到的 Unity Hub / Unity Editor 通常为版本号带 c 后缀的国内特供版，而不带 c 后缀的则为国际版。通常情况下两者在使用上没有明显差别，但需要注意，最新的国内版 Unity Hub 在较为明显的位置放置了“团结引擎”的下载按钮（如下图），无视即可。
>
> <img src="pics/image-20250119211304746.png" alt="image-20250119211304746" style="zoom:25%;" />
>
> (&#42;&#42;) 注2：考虑新版本可能存在的稳定性问题，本次培训暂时不以 Unity 6 为基准版本。

### 2、安装步骤
1. Unity Hub 安装：官网下载 Unity Hub，用于管理 Unity 版本和项目 (https://unity.com/cn/download)

2. Unity Editor 安装：安装完成后，在 Unity Hub 界面的左侧栏选择“安装”，点击右上角“安装编辑器”按钮，在“正式发行”（LTS）一栏找到需要下载的 Unity Editor（此处选择版本 2022.3.52f1c1）进行安装：

   <img src="pics/image-20250119215904554.png" alt="image-20250119215904554" style="zoom:33%;" />

   安装时，Visual Studio 、开发平台和文档等项可视需求勾选。新版本 Unity 安装时可以直接选择简体中文配置，不需要额外汉化包。

   <img src="pics/image-20250119215948789.png" alt="image-20250119215948789" style="zoom:33%;" />

   需要注意的是，Unity 各版本之间兼容性较差，一旦选定了一个版本进行团队开发，就要统一 Unity 版本并一直使用到项目结束。

3. 获取 Unity 授权的免费个人版激活许可证

4. 代码编辑器可使用 Visual Studio（需要在安装时勾选“使用 Unity 的游戏开发”）或者 Visual Studio Code（具体在 Unity Editor 内配置，后续说明）

## 三、创建第一个项目
### 0、Unity 基本知识
#### Scene（场景）
Scene（场景）是一个包含游戏世界的容器，包含了若干 GameObject（游戏对象）。一个游戏可能由多个场景组成，通过脚本在它们之间进行切换。例如，一个游戏可能包含 MenuScene（菜单场景）和 GameScene（游戏场景）。对于关卡类的游戏，可以为每个关卡独立创建一个游戏场景。
#### GameObject（游戏对象）
GameObject（游戏对象）是 Unity 中最基本的实体单位。它可以代表场景中的任何物件，如角色、道具、环境物体等。GameObject 之间可以存在父子关系，这里的父子关系是一种层级上的组合关系或从属关系，并非父类与子类的继承关系。

#### Component（组件）

每个 GameObject 可以拥有若干个 Component（组件），两者之间也是一种从属关系。每个组件都代表着 GameObject 所具有的一种功能、行为或性质，当 GameObject 被实例化并且处于活动（Active）状态，且 Component 也处于活动状态时，它便可以控制 GameObject 的行为。通过在某些游戏对象上挂载对应的组件，可以实现特定的功能。

以下列举一些常见的 Components 及其对应功能：

| 分类      | 名称                                | 功能                                                         |
| --------- | ----------------------------------- | ------------------------------------------------------------ |
| 通用      | Transform                           | 所有游戏对象的固有属性：位置、朝向、缩放、层级关系           |
| 外观 (3D) | MeshFilter                          | 为游戏对象指定一个 3D 模型                                   |
|           | MeshRenderer                        | 用指定的材质（Material）渲染 MeshFilter 中的 3D 模型         |
| 外观 (2D) | SpriteRenderer                      | 用指定的材质渲染 2D 精灵图                                   |
| 渲染      | Camera                              | 使游戏对象具备摄像机功能                                     |
|           | Light                               | 使游戏对象具备灯光功能                                       |
|           | Volume / <br />PostProcessingVolume | URP / HDRP 自带，指定后处理功能的生效范围<br />若使用内置渲染管线，则需自行导入 Post Processing 包 |
| 物理      | xxxCollider                         | 各种形状的碰撞器                                             |
|           | Rigidbody                           | 刚体物理模拟                                                 |
| 动画      | Animation                           | 在游戏对象上播放某个固定的动画片段（Animation Clip）         |
|           | Animator                            | 动画状态机，详见后文介绍                                     |

#### Script / MonoBehaviour（脚本）

脚本实际上就是一种自定义的 Component，可以通过编写 C# 脚本来自定义对 GameObject 行为的控制方式，从而实现游戏所需的各种复杂逻辑。

#### Prefab（预设/预制件/预制体）

游戏中经常会有一些在不同时间、不同位置或不同场景重复出现的物件（如子弹、NPC、环境装饰等），在这种情况下我们可以使用 Prefab，以减少不必要的重复工作。Prefab 相当于一个 GameObject 的模板，在游戏开发和运行过程中，可以由它实例化（Instantiate）出对应的 GameObject。开发过程中，当 Prefab 被修改时，它的所有 GameObject 实例也会被修改。

#### Material（材质）和 Shader（着色器）

TODO

#### Sprite（精灵）

TODO

#### Assets（资源/资产）
项目中的所有 Prefab、脚本、材质、2D 精灵图、3D 模型/纹理、音乐、场景结构数据、配置文件等资源都被称作 Asset，置于项目的 Assets 文件夹中。对于规模较大的工程，应该建立规范的目录结构。

### 1、界面介绍
#### Unity Hub
在Unity Hub界面，点击“新项目”，进入创建项目界面。本次培训中，我们主要以 3D 项目为例，介绍 Unity 的基本操作；同时，为了避免后半渲染部分的配置过于复杂，我们可以直接以 URP（通用渲染管线）模板创建项目：（关于渲染管线，在昨天的图形学一讲中已经初步提及，更进一步的解释详见后文介绍）

<img src="pics/image-20250120001819635.png" alt="image-20250120001819635" style="zoom:33%;" />

<img src="pics/image-20250120003714504.png" alt="image-20250120003714504" style="zoom:33%;" />

左侧可以选择创建模板类型，选择“核心模板”，“Universal 3D”，在右侧点击“下载模板”。待下载结束后，可以修改合适的项目名称和位置，然后点击“创建项目”。（不要勾选“启用游戏云服务”和“使用团结云开发”）
（注1：“游戏云服务”是 Unity 中国提供的一系列*付费*服务；“团结云开发”是指 Unity 自己开发的版本管理系统 Plastic SCM，由于安装过程较为繁琐且只适用于 Unity，感兴趣的同学们可以自行了解。培训第一天我们讲解了 git，如果在此之前还没有使用 git 的经验，推荐借助软设开发的机会熟悉一下 git 的操作）
（注2：下文演示中使用的 Unity 是 2022.3.56f1 版本）

<img src="pics/image-20250120003354507.png" alt="image-20250120003354507" style="zoom:33%;" />

等待一小段时间过后，我们进入了 Unity Editor 界面

<img src="pics/image-20250120005214146.png" alt="image-20250120005214146" style="zoom:33%;" />

此时，界面右侧显示的是 URP 模板的欢迎页面，点击中部的 "Remove Readme Assets" 按钮以移除相关内容。

#### Unity Editor
##### 常用窗口
- Hierarchy（层级）：用于查看当前所选场景中的各个 GameObject 以及它们之间的层级关系（父子关系）。通过将对应资源拖拽进入该区域，可以为场景添加新的 GameObject。
- Project（项目）：用于查看当前项目所用到的各种资源（脚本代码、预制体、美术资源、材质资源、音乐资源等）。项目中的各种资源主要存放在 Assets 和 Library 两个文件夹中，前者是项目构建中主要用于操作的文件夹，后者用于引入外部包资源。
- Console（控制台）：用于查看控制台输出，可用于查看报错信息和项目 Debug 输出信息。
- Inspector（检查器）：检查当前所选 GameObject 或 Asset 的属性，为游戏对象添加、更改或删除组件等。
- Scene（场景）、Game（游戏）：这两个是**核心操作面板**。场景面板用于调整游戏对象位置、大小等在游戏场景中的形态。游戏面板等于是对游戏功能的测试，能够准确体验游戏的运行状态。当我们在场景中完成全部的部署之后，点击运行按钮，就可以开始游戏（开始测试）。中断按钮可以暂停当前游戏并切换回场景面板以查看对象的实时属性。
### 2、游戏对象
#### 1.Main Camera
- 项目初始化后，初始场景 Sample Scene 会自带游戏对象 Main Camera，用于将其范围内的游戏场景在游戏界面中显示出来。
- Main Camera 挂载的 Camera 组件可以设置摄像机的诸多属性（如画面大小），Transform组件可以使摄像机在游戏进程中随时改变位置，获得灵活的运镜效果（这在3D游戏中尤为重要）
#### 2.静态对象的创建
- Unity 提供了一系列简单的几何对象

  <img src="D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205420328.png" alt="image-20240130205420328" style="zoom:80%;" />

  利用“场景”左上角提供的变换工具对图形进行变换，在检查器面板上观察图形的 Transform 组件变化

  ![image-20240130205440854](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205440854.png)

- 如何添加素材作为游戏对象？

1.将素材导入到项目文件夹 Assets 下（注意尽可能按照资源类别细分素材并建立文件夹，如Scenes、Scripts、Materials等）
2.在检查器中设置需要导入的素材的相关属性（对于一般素材，推荐更改过滤模式为“点”，压缩修改为“无”，更改后点击应用）

![image-20240130205638172](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205638172.png)

3.拖拽素材进入场景，可以看到“层级”视图中新增了游戏对象

- 如何切分帧图片和导入动画？
  1.选择需要切分的帧图片，在检查器中选择Sprite模式为“多个”，点击“应用”后单击“Sprite Editor”进入Sprite编辑器，在左上角的切片中按照cell大小完成切分。

  ![image-20240130205653050](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205653050.png)

- 2.按照顺序选择合成动画的帧，拖拽至对应游戏对象上，Unity即可自动生成动画文件。
3.选择对应游戏对象后，在“动画”选项卡（注意不是“动画器”)即可播放对应动画。

-   关于动画，更全面、系统、深层次的应用：动画状态机。（Animator）
    -   状态，即动画的效果，比如人物静止的时候会有上下轻微浮动的动画，人物走的时候有个行走的动画，人物攻击的时候有个攻击的动画，跳跃的时候有个跳跃的动画，这些不同的动画状态，都是通过**状态机**连接起来的。
    -   既然有不同的状态，那么就应该有状态转换的条件
        -   比如人物什么时候从站立状态转而变成走路的状态——按下 WSAD 键盘
        -   再比如人物放完技能之后应该自动返回站立（挂机）状态，肯定不能一直放技能。（有 CD 存在）
        -   这些控制条件是通过挂载在人物下的脚本结合 Unity 的动画状态机来控制的。
## 四、交互逻辑：组件与脚本
-   组件就是积木，需要用到的时候就添加。
-   一个个组件共同构建起了**功能完整**的游戏对象。
#### 1.一般组件
常涉及的组件：Transform（控制游戏对象的几何变换以及层级关系）、Camera（控制游戏相机）、SpriteRenderer（将2D精灵渲染到屏幕上）、Animator（控制对象动画）等。
值得注意的是，Unity内置了强大的物理系统，可以给对象挂载组件使其符合一定物理规律。

- 给游戏对象挂载Rigidbody 2D组件，观察游戏对象行为

  ![image-20240130210029878](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130210029878.png)

- 使游戏对象之间发生碰撞：两个对象均挂载了碰撞体（Collider / Collider 2D）组件，运动的一方的Rigidbody 2D组件碰撞检测设置为“持续”

  ![image-20240130205955717](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130205955717.png)

- 更改游戏对象物理材质（增加反弹、摩擦等）：新建2D物理材质，设置相关摩擦和弹力系数，替换掉Rigidbody 2D组件原物理材质。
#### 2.脚本
1.配置脚本编辑环境：在 Unity 中选择编辑->首选项->外部工具->外部脚本编辑器，选中Visual Studio或Visual Studio Code即可
2.创建一个简单的脚本（Project窗口右键->创建->C#脚本）

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
   - MonoBehavior：脚本创建时默认会挂载到游戏对象上，class自动继承MonoBehavior。如果该脚本不需要直接挂载到游戏对象上发挥效果，则不需要继承自MonoBehavior
   - void Start()：场景加载时执行一次的函数，用于初始化。
   - void Update()：游戏运行时每一帧都会执行一次，用于实时同步游戏数据，主要代码通常都需要每一帧都执行。

3.在Start函数中写入以下代码并将脚本挂载到player上
```csharp
Debug.Log("Hello world!");
```
运行游戏，控制台输出了一次Hello world信息

![image-20240130210158347](D:\Users\hanzhifeng\AppData\Roaming\Typora\typora-user-images\image-20240130210158347.png)
4.碰撞事件和触发事件：
游戏对象的碰撞体与其他碰撞体发生碰撞时会调用碰撞事件：
包括 OnCollisionEnter2D （碰撞开始时执行）、 OnCollisionExit2D （碰撞结 束时执行）、 OnCollisionStay （碰撞过程每帧执行)

```csharp
private void OnCollisionEnter2D(Collision2D collision)//Collision2D类型包含 碰撞信息
{
	Debug.Log(name + " collided with " + collision.collider.name);
}
```
在碰撞器组件上勾选了“是触发器”后，物体便不会与其他碰撞体发生碰撞，取而代之的是在相互穿过时调用触发事件：
包括 OnTriggerEnter2D （接触开始时执行）、 OnTriggerExit2D （接触结束时执行）、 OnTriggerStay （接触过程每帧执行）

```csharp
private void OnTriggerStay2D(Collider2D collision)
{
	Debug.Log(name + " contacting with " + collision.collider.name);
}
```
## 四、视觉效果：材质与渲染

### 0、光栅渲染管线基础

#### 此处 Copy 2024 寒培：实时渲染部分

### 1、ShaderGraph

#### 此处参考往年 Unity，但是要大改

### 2、后处理

#### 这个简单

### 3、HLSL

#### 可能来不及准备/讲，先放个标题在这

## 五、写在最后

作为一个最简单的入门教程，本篇基本只是让大家认识unity，下载安装unity并且了解unity的基本界面和用法。作为一个工具型软件，最好的学习方法永远是实战，推荐大家直接按照教程开发一个小项目，体会到游戏开发的乐趣。

下面是一些实用的文档和教程，希望对大家有所帮助

- [Unity官方文档及API说明](https://docs.unity3d.com/cn/current/Manual/UnityManual.html)
- [完整游戏制作合集教程](https://space.bilibili.com/390481111/channel/collectiondetail?sid=1064344)
- [Unity特效渲染合集教程](https://space.bilibili.com/390481111/channel/collectiondetail?sid=1181615)
- [【Unity】有趣的游戏技巧（轮子）教程合集](https://space.bilibili.com/390481111/channel/collectiondetail?sid=1097746)

素材网站：

- [itch.io](https://itch.io/) （2D 为主）
- [Quixel Megascans](https://quixel.com/megascans/home) （大量 3D 高模素材，免费）
- [Unity Asset Store](https://assetstore.unity.com/zh) （可直接导入 Unity 的素材和脚本库等）
- [HotpotDesign/Game-Assets-And-Resources](https://github.com/HotpotDesign/Game-Assets-And-Resources) （素材网站集合）

参考&致谢：

* 寒培2023Unity by ysq&ltx- THUEE-Unity暑培教程
* 寒培2024Unity by hzf
* 寒培2024《实时渲染基础魔法》 by Tianyu Huang
