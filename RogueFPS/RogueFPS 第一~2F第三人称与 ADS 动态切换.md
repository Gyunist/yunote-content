# RogueFPS 第一/第三人称与 ADS 动态切换

## 1. 总体叙述

### 1.1 当前实现达到的效果

当前系统使用一个 Gameplay Tag 保存玩家的人称状态：

```text
Status.Perspective.ThirdPerson 不存在
→ 第一人称

Status.Perspective.ThirdPerson 存在
→ 第三人称
```

第一人称作为默认状态，因此没有创建：

```text
Status.Perspective.FirstPerson
```

当前实现覆盖以下内容：

```text
V 键输入
→ 切换人称状态标签
→ 选择普通第一/第三人称相机

右键 ADS
→ 根据当前人称状态选择第一/第三人称 ADS 相机

ADS 期间按 V
→ 切换人称状态标签
→ 同步切换对应的 ADS 相机

松开右键
→ 清除 ADS 临时相机
→ 根据当前人称状态返回普通第一/第三人称相机
```

第一人称当前由 `CM_FirstPerson` 相机模式表示。角色模型、Character Parts 和动画继续使用 Lyra 当前的角色表现系统。

***

### 1.2 按一次 V 时发生的完整过程

输入链条为：

```text
V
→ IMC_ShooterGame
→ IA_TogglePerspective
→ InputData_ShooterGame_AddOns
→ InputTag.Ability.TogglePerspective
→ AbilitySet_ShooterHero 中对应的 Ability Spec
→ 激活 GA_TogglePerspective
```

`GA_TogglePerspective` 激活后，从角色所属的 Ability System Component 查询：

```text
Status.Perspective.ThirdPerson
```

然后执行：

```text
标签不存在
→ AddLooseGameplayTags
→ 添加 Status.Perspective.ThirdPerson
→ 进入第三人称

标签存在
→ RemoveLooseGameplayTags
→ 移除 Status.Perspective.ThirdPerson
→ 进入第一人称
```

完成添加或移除标签后：

```text
GA_TogglePerspective
→ EndAbility
```

`GA_TogglePerspective` 是一次性 Ability。人称状态保存在 ASC 的 Loose Gameplay Tag 中，因此 Ability 结束不会自动清除人称状态。

***

### 1.3 普通状态下如何选择相机

`ULyraCameraComponent` 通过委托调用：

```cpp
ULyraHeroComponent::DetermineCameraMode()
```

当前优先级为：

```text
1. AbilityCameraMode
2. TaggedCameraModes 中第一个匹配项
3. PawnData->DefaultCameraMode
```

普通状态下没有 Ability 临时相机，因此继续检查：

```text
B_Hero_ShooterMannequin
→ LyraHero
→ TaggedCameraModes
```

当前配置为：

```text
TaggedCameraModes[0]
├─ RequiredTag = Status.Perspective.ThirdPerson
└─ CameraMode  = CM_ThirdPerson
```

因此：

```text
拥有 Status.Perspective.ThirdPerson
→ TaggedCameraModes[0] 匹配
→ 返回 CM_ThirdPerson
```

如果没有任何规则匹配，则读取：

```text
HeroData_ShooterGame
→ DefaultCameraMode
→ CM_FirstPerson
```

因此：

```text
没有 Status.Perspective.ThirdPerson
→ 返回 CM_FirstPerson
```

***

### 1.4 右键 ADS 时发生的过程

按下右键并激活 `GA_ADS` 后，`GA_ADS` 查询同一个人称状态标签：

```text
Status.Perspective.ThirdPerson
```

分支逻辑为：

```text
标签不存在
→ SetCameraMode(CM_FirstPersonADS)

标签存在
→ SetCameraMode(CM_ThirdPersonADS)
```

`SetCameraMode()` 最终把相机类记录到：

```text
ULyraHeroComponent.AbilityCameraMode
```

`DetermineCameraMode()` 首先检查：

```cpp
if (AbilityCameraMode)
{
    return AbilityCameraMode;
}
```

因此 ADS 相机在瞄准期间拥有最高优先级：

```text
普通第一人称 CM_FirstPerson
→ 按右键
→ CM_FirstPersonADS

普通第三人称 CM_ThirdPerson
→ 按右键
→ CM_ThirdPersonADS
```

***

### 1.5 ADS 期间按 V 时发生的过程

`GA_ADS` 激活期间同时运行两项 Gameplay Tag 等待任务：

```text
WaitGameplayTagAdd
Tag = Status.Perspective.ThirdPerson
OnlyTriggerOnce = false

标签被添加
→ SetCameraMode(CM_ThirdPersonADS)
```

以及：

```text
WaitGameplayTagRemove
Tag = Status.Perspective.ThirdPerson
OnlyTriggerOnce = false

标签被移除
→ SetCameraMode(CM_FirstPersonADS)
```

因此第一人称 ADS 期间按 V：

```text
当前 AbilityCameraMode = CM_FirstPersonADS
→ 按 V
→ GA_TogglePerspective 添加第三人称状态标签
→ GA_ADS 的 WaitGameplayTagAdd 被触发
→ AbilityCameraMode 更新为 CM_ThirdPersonADS
```

第三人称 ADS 期间按 V：

```text
当前 AbilityCameraMode = CM_ThirdPersonADS
→ 按 V
→ GA_TogglePerspective 移除第三人称状态标签
→ GA_ADS 的 WaitGameplayTagRemove 被触发
→ AbilityCameraMode 更新为 CM_FirstPersonADS
```

`OnlyTriggerOnce = false` 允许同一次 ADS 持续期间多次切换：

```text
CM_FirstPersonADS
↔ CM_ThirdPersonADS
```

***

### 1.6 松开右键时发生的过程

松开右键后：

```text
WaitInputRelease
→ EndAbility
→ GA_ADS.OnEndAbility
→ ClearCameraMode
```

`ClearCameraMode()` 清除 `GA_ADS` 设置的：

```text
AbilityCameraMode
```

然后 `DetermineCameraMode()` 重新按普通相机规则选择：

```text
当前存在 Status.Perspective.ThirdPerson
→ CM_ThirdPerson

当前不存在 Status.Perspective.ThirdPerson
→ HeroData_ShooterGame.DefaultCameraMode
→ CM_FirstPerson
```

例如：

```text
第一人称 ADS
→ ADS 期间按 V
→ 第三人称 ADS
→ 松开右键
→ 清除 CM_ThirdPersonADS
→ 根据仍然存在的第三人称状态标签返回 CM_ThirdPerson
```

***

### 1.7 死亡和重生时的人称状态

`GA_TogglePerspective` 的激活阻止标签包括：

```text
Status.Death.Dying
Status.Death.Dead
```

角色处于死亡或濒死状态时，V 键不会激活该 Ability。

人称状态使用 Loose Gameplay Tag 保存在 Lyra 的 PlayerState ASC 上：

```text
ALyraPlayerState
└─ ULyraAbilitySystemComponent
   └─ Status.Perspective.ThirdPerson
```

Pawn 死亡和重新生成时，PlayerState ASC 继续作为人称状态的数据来源。重生后的相机继续根据该标签选择第一或第三人称。

***

### 1.8 当前系统的职责分布

```text
IA_TogglePerspective
→ 表示“切换人称”这一输入动作

IMC_ShooterGame
→ 把键盘 V 映射到 IA_TogglePerspective

InputData_ShooterGame_AddOns
→ 把 IA_TogglePerspective 转换成 InputTag.Ability.TogglePerspective

AbilitySet_ShooterHero
→ 授予 GA_TogglePerspective
→ 给对应 Ability Spec 关联 InputTag.Ability.TogglePerspective

GA_TogglePerspective
→ 添加或移除 Status.Perspective.ThirdPerson
→ 只负责改变人称状态

ASC
→ 保存 Status.Perspective.ThirdPerson

ULyraHeroComponent
→ 根据通用 TaggedCameraModes 规则选择普通相机

B_Hero_ShooterMannequin
→ 配置具体的 Tag → CameraMode 对应关系

HeroData_ShooterGame
→ 保存默认第一人称相机

GA_ADS
→ 根据当前人称状态选择临时 ADS 相机
→ ADS 期间监听人称状态变化

Lyra Camera System
→ 使用 DetermineCameraMode 返回的 CameraMode 生成和混合最终视图
```

***

## 2. 详细描述修改部分

### 2.1 C++ 修改清单

修改文件：

```text
Source/LyraGame/Character/LyraHeroComponent.h
Source/LyraGame/Character/LyraHeroComponent.cpp
```

修改内容：

```text
LyraHeroComponent.h
├─ 引入 GameplayTagContainer.h
├─ 创建 FLyraTaggedCameraMode
├─ 创建 TaggedCameraModes 数组
└─ 移除专用 ThirdPersonCameraMode 属性

LyraHeroComponent.cpp
├─ DetermineCameraMode 遍历 TaggedCameraModes
├─ 保留 AbilityCameraMode 最高优先级
├─ 保留 PawnData->DefaultCameraMode 最终回退
├─ 移除 Status.Perspective.ThirdPerson 字符串硬编码
├─ 移除 ThirdPersonCameraMode 构造函数初始化
└─ 移除 GameplayTagsManager.h
```

***

### 2.2 Gameplay Tag 修改清单

配置文件：

```text
Plugins/GameFeatures/ShooterCore/Config/Tags/ShooterCoreTags.ini
```

包含：

```text
InputTag.Ability.TogglePerspective
Status.Perspective.ThirdPerson
```

两个标签承担不同职责：

```text
InputTag.Ability.TogglePerspective
→ 表示一次“切换人称”的输入命令

Status.Perspective.ThirdPerson
→ 表示当前处于第三人称状态
```

***

### 2.3 输入资产修改清单

创建：

```text
/ShooterCore/Input/Actions/IA_TogglePerspective
```

修改：

```text
/ShooterCore/Input/Mappings/IMC_ShooterGame
/ShooterCore/Input/Actions/InputData_ShooterGame_AddOns
/ShooterCore/Game/AbilitySet_ShooterHero
```

参与加载的现有资产：

```text
LAS_ShooterGame_SharedInput
```

具体配置：

```text
IA_TogglePerspective
├─ Value Type = Boolean
└─ Trigger = Pressed
```

```text
IMC_ShooterGame
└─ V
   └─ IA_TogglePerspective
```

```text
InputData_ShooterGame_AddOns
└─ Ability Input Actions
   └─ IA_TogglePerspective
      └─ InputTag.Ability.TogglePerspective
```

```text
AbilitySet_ShooterHero
└─ GA_TogglePerspective
   ├─ InputTag = InputTag.Ability.TogglePerspective
   └─ Ability Level = 1
```

`LAS_ShooterGame_SharedInput` 负责将两类输入配置加入玩家：

```text
AddInputContextMapping
→ IMC_ShooterGame

AddInputBinding
→ InputData_ShooterGame_AddOns
```

***

### 2.4 `GA_TogglePerspective` 创建与配置

创建资产：

```text
/ShooterCore/Input/Abilities/GA_TogglePerspective
```

Ability 设置：

```text
Activation Policy
= OnInputTriggered

Activation Group
= Independent

Instancing Policy
= InstancedPerActor

Net Execution Policy
= LocalOnly

Replication Policy
= ReplicateNo
```

激活阻止标签：

```text
Status.Death.Dying
Status.Death.Dead
```

`Activation Owned Tags` 保持为空。

当前 EventGraph 核心逻辑：

```text
ActivateAbility
→ GetAbilitySystemComponentFromActorInfo
→ ToGameplayTagAssetInterface
→ HasMatchingGameplayTag
   Tag = Status.Perspective.ThirdPerson
→ Branch
```

True 分支：

```text
ASC 已有 Status.Perspective.ThirdPerson
→ MakeGameplayTagContainerFromTag
→ RemoveLooseGameplayTags
→ EndAbility
```

False 分支：

```text
ASC 没有 Status.Perspective.ThirdPerson
→ MakeGameplayTagContainerFromTag
→ AddLooseGameplayTags
→ EndAbility
```

添加和移除节点使用：

```text
Target
= GetOwningActorFromActorInfo

bShouldReplicate
= false
```

***

### 2.5 普通相机资产修改清单

创建：

```text
/Game/Characters/Cameras/CM_FirstPerson
/Game/Characters/Cameras/FirstPersonOffsetCurve
```

修改或参与选择：

```text
/Game/Characters/Cameras/CM_ThirdPerson
/Game/Characters/Cameras/ThirdPersonOffsetCurve
/ShooterCore/Game/HeroData_ShooterGame
/ShooterCore/Game/B_Hero_ShooterMannequin
```

当前基础相机配置：

```text
CM_FirstPerson
├─ Parent Class = ULyraCameraMode_ThirdPerson
├─ TargetOffsetCurve = FirstPersonOffsetCurve
├─ Field Of View = 80
└─ Blend Time = 0.5
```

```text
CM_ThirdPerson
├─ Parent Class = ULyraCameraMode_ThirdPerson
├─ TargetOffsetCurve = ThirdPersonOffsetCurve
├─ Field Of View = 80
└─ Blend Time = 0.5
```

`HeroData_ShooterGame`：

```text
PawnClass
= B_Hero_ShooterMannequin

DefaultCameraMode
= CM_FirstPerson
```

`B_Hero_ShooterMannequin` 的 `LyraHero` 组件：

```text
TaggedCameraModes.Num
= 1

TaggedCameraModes[0]
├─ RequiredTag = Status.Perspective.ThirdPerson
└─ CameraMode  = CM_ThirdPerson
```

***

### 2.6 `LyraHeroComponent.h` 的通用相机规则

新增头文件依赖：

```cpp
#include "GameplayTagContainer.h"
```

新增结构体：

```cpp
USTRUCT(BlueprintType)
struct FLyraTaggedCameraMode
{
    GENERATED_BODY()

    /** Tag that must be present on the owning ASC. */
    UPROPERTY(EditDefaultsOnly, BlueprintReadOnly)
    FGameplayTag RequiredTag;

    /** Camera mode selected when RequiredTag is present. */
    UPROPERTY(EditDefaultsOnly, BlueprintReadOnly)
    TSubclassOf<ULyraCameraMode> CameraMode;
};
```

新增数组：

```cpp
/** Camera mode rules evaluated in array order after an ability camera override. */
UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Lyra|Camera")
TArray<FLyraTaggedCameraMode> TaggedCameraModes;
```

已移除的专用属性：

```cpp
TSubclassOf<ULyraCameraMode> ThirdPersonCameraMode;
```

***

### 2.7 `DetermineCameraMode()` 的最终逻辑

当前实现：

```cpp
TSubclassOf<ULyraCameraMode> ULyraHeroComponent::DetermineCameraMode() const
{
    if (AbilityCameraMode)
    {
        return AbilityCameraMode;
    }

    const APawn* Pawn = GetPawn<APawn>();
    if (!Pawn)
    {
        return nullptr;
    }

    if (ULyraPawnExtensionComponent* PawnExtComp =
        ULyraPawnExtensionComponent::FindPawnExtensionComponent(Pawn))
    {
        if (const ULyraAbilitySystemComponent* LyraASC =
            PawnExtComp->GetLyraAbilitySystemComponent())
        {
            for (const FLyraTaggedCameraMode& Rule : TaggedCameraModes)
            {
                if (Rule.RequiredTag.IsValid()
                    && Rule.CameraMode
                    && LyraASC->HasMatchingGameplayTag(Rule.RequiredTag))
                {
                    return Rule.CameraMode;
                }
            }
        }

        if (const ULyraPawnData* PawnData =
            PawnExtComp->GetPawnData<ULyraPawnData>())
        {
            return PawnData->DefaultCameraMode;
        }
    }

    return nullptr;
}
```

当前 C++ 中已经移除：

```cpp
ThirdPersonCameraMode = nullptr;
```

```cpp
#include "GameplayTagsManager.h"
```

```cpp
UGameplayTagsManager::Get().RequestGameplayTag(
    FName(TEXT("Status.Perspective.ThirdPerson")));
```

`LyraHeroComponent` 当前只实现通用逻辑：

```text
读取 ASC 标签
→ 遍历配置数组
→ 返回第一个匹配的 CameraMode
```

具体标签和相机资产由 `B_Hero_ShooterMannequin` 配置。

***

### 2.8 ADS 资产和蓝图修改清单

创建：

```text
/ShooterCore/Camera/CM_FirstPersonADS
```

修改：

```text
/ShooterCore/Input/Abilities/GA_ADS
```

参与逻辑的现有资产：

```text
/ShooterCore/Camera/CM_ThirdPersonADS
/ShooterCore/Camera/ThirdPersonADSOffsetCurve
```

当前两套 ADS 相机参数：

```text
CM_FirstPersonADS
├─ TargetOffsetCurve = ThirdPersonADSOffsetCurve
├─ Field Of View = 70
├─ Blend Time = 0.22
└─ Camera Type Tag = Lyra.Weapon.SteadyAimingCamera
```

```text
CM_ThirdPersonADS
├─ TargetOffsetCurve = ThirdPersonADSOffsetCurve
├─ Field Of View = 70
├─ Blend Time = 0.22
└─ Camera Type Tag = Lyra.Weapon.SteadyAimingCamera
```

两套资产当前参数相同，逻辑上已经分别引用两个独立相机类。

`GA_ADS` 激活时：

```text
GetAbilitySystemComponentFromActorInfo
→ ToGameplayTagAssetInterface
→ HasMatchingGameplayTag
   Tag = Status.Perspective.ThirdPerson
→ Branch
```

分支：

```text
True
→ SetCameraMode(CM_ThirdPersonADS)

False
→ SetCameraMode(CM_FirstPersonADS)
```

`GA_ADS` 激活期间：

```text
WaitGameplayTagAdd
→ Status.Perspective.ThirdPerson
→ CM_ThirdPersonADS
```

```text
WaitGameplayTagRemove
→ Status.Perspective.ThirdPerson
→ CM_FirstPersonADS
```

`GA_ADS` 结束时：

```text
ClearCameraMode
→ 清除 AbilityCameraMode
→ 恢复当前人称对应的普通相机
```

原有 ADS 行为继续保留：

```text
ADS 移速倍率
IMC_ADS_Speed
UI ADS 状态通知
ZoomIn / ZoomOut 声音
WaitInputRelease
恢复移动速度
移除 ADS 输入映射
```

***

### 2.9 Gameplay Tag 查询修复

`GA_TogglePerspective` 和 `GA_ADS` 当前都从确定有效的 ASC 开始查询：

```text
GetAbilitySystemComponentFromActorInfo
→ ToGameplayTagAssetInterface
→ HasMatchingGameplayTag
```

这里转换为 `GameplayTagAssetInterface` 的对象是：

```text
UAbilitySystemComponent
```

`UAbilitySystemComponent` 实现了：

```cpp
IGameplayTagAssetInterface
```

因此当前查询链能够直接读取 ASC 中的 Gameplay Tag。

这项修复使人称判断统一读取真正保存标签的对象：

```text
PlayerState ASC
└─ Status.Perspective.ThirdPerson
```

***

## 3. 具体解释每项修改的意义

### 3.1 创建两个不同语义的 Gameplay Tag

```text
InputTag.Ability.TogglePerspective
```

表示一次输入请求：

```text
玩家请求切换人称
```

```text
Status.Perspective.ThirdPerson
```

表示当前状态：

```text
玩家当前处于第三人称
```

二者分开后：

```text
输入请求
→ 触发 Ability
→ Ability 改变状态
→ 相机系统读取状态
```

输入标签不会承担长期状态保存职责，人称状态标签也不直接绑定某个键位。

***

### 3.2 创建 IA、IMC、InputData 和 AbilitySet 的意义

`IA_TogglePerspective` 定义抽象动作：

```text
切换人称
```

`IMC_ShooterGame` 决定当前设备如何产生这个动作：

```text
键盘 V
→ IA_TogglePerspective
```

`InputData_ShooterGame_AddOns` 把 Enhanced Input 动作转换成 Lyra 输入标签：

```text
IA_TogglePerspective
→ InputTag.Ability.TogglePerspective
```

`AbilitySet_ShooterHero` 在角色初始化时：

```text
授予 GA_TogglePerspective
→ 给 Ability Spec 添加 InputTag.Ability.TogglePerspective
```

玩家按 V 时，Lyra ASC 根据 Ability Spec 上的输入标签找到目标 Ability。

最终形成：

```text
物理按键
→ 抽象输入动作
→ Gameplay 输入标签
→ Ability Spec
→ Gameplay Ability
```

键位、输入动作、Gameplay Tag 和 Ability 类分别由不同资产配置。

***

### 3.3 使用一次性 `GA_TogglePerspective` 的意义

`GA_TogglePerspective` 只执行：

```text
读取当前人称状态
→ 添加或移除第三人称标签
→ 立即结束
```

Ability 不需要持续运行，因为持续状态由 Loose Gameplay Tag 保存。

这种结构把两个概念分开：

```text
GA_TogglePerspective
→ 执行一次“改变状态”的命令

Status.Perspective.ThirdPerson
→ 保存改变后的结果
```

因此 Ability 结束后，人称状态仍然存在。

***

### 3.4 把人称状态保存在 ASC 上的意义

相机、ADS 和后续其他系统都可以读取同一个 ASC 状态：

```text
Status.Perspective.ThirdPerson
├─ 普通相机选择
├─ ADS 相机选择
└─ ADS 期间动态切换
```

各系统不需要互相保存独立的：

```text
bIsThirdPerson
```

Lyra 将 ASC 放在 PlayerState 上，因此人称状态可以作为跨 Pawn 生命周期的数据来源。

***

### 3.5 修正 Gameplay Tag 查询对象的意义

Gameplay Tag 实际保存在 ASC 上，因此查询从：

```text
GetAbilitySystemComponentFromActorInfo
```

开始。

ASC 实现 `IGameplayTagAssetInterface`，所以：

```text
ASC
→ GameplayTagAssetInterface
→ HasMatchingGameplayTag
```

是一条有效的标签查询路径。

这使 `GA_TogglePerspective` 与 `GA_ADS` 查询的是同一个状态容器。

***

### 3.6 使用 `TaggedCameraModes` 的意义

此前专用实现让基础 `LyraHeroComponent.cpp` 直接包含：

```text
Status.Perspective.ThirdPerson
ThirdPersonCameraMode
```

这会让基础 `LyraGame` 模块知道 ShooterCore 的具体第三人称语义。

现在改为：

```text
FLyraTaggedCameraMode
├─ RequiredTag
└─ CameraMode
```

`ULyraHeroComponent` 只知道一条通用规则：

```text
ASC 拥有某个标签
→ 使用为该标签配置的 CameraMode
```

具体规则放在 ShooterCore 蓝图资产中：

```text
B_Hero_ShooterMannequin
└─ Status.Perspective.ThirdPerson
   → CM_ThirdPerson
```

职责关系变为：

```text
LyraGame C++
→ 提供通用的 Tag → CameraMode 选择机制

ShooterCore 蓝图
→ 配置具体的第三人称标签和相机资产
```

这使基础 C++ 可以继续支持其他相机规则，例如：

```text
Status.Vehicle.Driving
→ CM_Vehicle

Status.Spectating
→ CM_Spectator
```

而不需要继续在 `DetermineCameraMode()` 中增加 ShooterCore 专用判断。

***

### 3.7 使用有序数组的意义

`TaggedCameraModes` 是：

```cpp
TArray<FLyraTaggedCameraMode>
```

数组顺序就是匹配优先级：

```text
Index 0
→ 最先检查

Index 1
→ Index 0 未匹配时检查

Index 2
→ 前面规则均未匹配时检查
```

第一个同时满足以下条件的规则被返回：

```text
RequiredTag 有效
CameraMode 已配置
ASC 拥有 RequiredTag
```

当前只有一条规则：

```text
Index 0
→ Status.Perspective.ThirdPerson
→ CM_ThirdPerson
```

***

### 3.8 保留 `PawnData->DefaultCameraMode` 的意义

`HeroData_ShooterGame` 已经拥有 Lyra 原生的：

```text
DefaultCameraMode
```

当前将其设置为：

```text
CM_FirstPerson
```

因此第一人称不需要额外状态标签：

```text
没有临时 Ability 相机
＋
没有 TaggedCameraModes 匹配项
→ 返回 PawnData->DefaultCameraMode
→ CM_FirstPerson
```

`DefaultCameraMode` 继续承担基础回退相机的职责。

***

### 3.9 保留 `AbilityCameraMode` 最高优先级的意义

ADS 是一个持续时间有限的 Ability 相机覆盖。

当 `GA_ADS` 调用：

```text
SetCameraMode(CM_FirstPersonADS)
```

或者：

```text
SetCameraMode(CM_ThirdPersonADS)
```

对应相机被写入：

```text
AbilityCameraMode
```

`DetermineCameraMode()` 首先返回它：

```text
AbilityCameraMode
> TaggedCameraModes
> DefaultCameraMode
```

因此普通相机规则不会在 ADS 期间覆盖 ADS 相机。

***

### 3.10 `GA_ADS` 根据人称状态选择相机的意义

普通相机和 ADS 相机是两组不同职责的资产：

```text
普通第一人称
→ CM_FirstPerson

普通第三人称
→ CM_ThirdPerson

第一人称 ADS
→ CM_FirstPersonADS

第三人称 ADS
→ CM_ThirdPersonADS
```

`GA_ADS` 本身知道当前正在执行瞄准，因此由它负责选择 ADS 相机。

`ULyraHeroComponent` 只负责保存 Ability 的临时相机覆盖并提供统一优先级，不需要知道该 Ability 是 ADS、冲刺相机还是其他临时相机。

***

### 3.11 ADS 期间监听人称标签变化的意义

ADS 激活后：

```text
AbilityCameraMode 已经有值
```

因此 `DetermineCameraMode()` 会优先返回当前 ADS 相机，不会继续遍历 `TaggedCameraModes`。

ADS 期间按 V 后，必须更新：

```text
AbilityCameraMode
```

所以 `GA_ADS` 使用：

```text
WaitGameplayTagAdd
WaitGameplayTagRemove
```

监听人称状态变化，并把当前 ADS 相机替换成另一套 ADS 相机。

由此支持：

```text
按住右键
→ 持续 ADS
→ 多次按 V
→ CM_FirstPersonADS 与 CM_ThirdPersonADS 动态切换
```

***

### 3.12 `ClearCameraMode()` 的意义

松开右键时，`GA_ADS` 只清除自己创建的临时相机覆盖：

```text
AbilityCameraMode = 空
```

随后普通相机选择机制重新生效：

```text
第三人称状态存在
→ TaggedCameraModes
→ CM_ThirdPerson

第三人称状态不存在
→ DefaultCameraMode
→ CM_FirstPerson
```

基础人称状态始终由：

```text
Status.Perspective.ThirdPerson
```

决定，而不是由 ADS Ability 保存。

***

### 3.13 最终整体结构

```text
输入层
V
→ IA_TogglePerspective
→ InputTag.Ability.TogglePerspective

Ability 激活层
InputTag.Ability.TogglePerspective
→ GA_TogglePerspective

状态层
GA_TogglePerspective
→ 添加或移除 Status.Perspective.ThirdPerson
→ ASC 保存状态

普通相机层
ULyraHeroComponent.DetermineCameraMode
├─ AbilityCameraMode
├─ TaggedCameraModes
└─ PawnData.DefaultCameraMode

普通第一人称
→ CM_FirstPerson

普通第三人称
→ CM_ThirdPerson

ADS 层
GA_ADS
├─ 第一人称 → CM_FirstPersonADS
├─ 第三人称 → CM_ThirdPersonADS
├─ 监听人称标签添加/移除
└─ 结束时 ClearCameraMode

数据配置层
HeroData_ShooterGame
→ DefaultCameraMode = CM_FirstPerson

B_Hero_ShooterMannequin
→ Status.Perspective.ThirdPerson
→ CM_ThirdPerson
```

当前结构的核心关系为：

```text
GA_TogglePerspective 只改变状态
ULyraHeroComponent 只按通用规则选择基础相机
B_Hero_ShooterMannequin 提供具体规则数据
GA_ADS 只管理 ADS 期间的临时相机
ASC 作为所有系统共享的人称状态来源
```

