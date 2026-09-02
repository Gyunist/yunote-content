# RogueFPS 第一/第三人称与 ADS 动态切换总体结构

本文档描述 `D:\RogueFPS` 当前已经落地并保存的第一/第三人称相机切换结构，并包含后续对 Gameplay Tag 查询和 ADS 中途切换的修复。

当前工程基准：

```text
项目：D:\RogueFPS\Lyra.uproject
Git HEAD：d4f93da999504901e0bafe8d20624883b7351a50
提交说明：V键切换第一/第三人称, 尚未调整具体视角
```

当前保存状态：

```text
蓝图和相机资产：
已保存到磁盘
已包含在 d4f93da9 提交中

Gameplay Tag 定义：
存在于当前工作区
尚未提交 Git

LyraHeroComponent C++ 修改：
存在于当前工作区
尚未提交 Git

Character Parts 模型显隐：
尚未实现
```

***

## 1. 总体叙述

### 1.1 最终结构达成的效果

当前结构把“玩家正在使用哪一种人称”保存为一个 Gameplay Tag 状态：

```text
Status.Perspective.ThirdPerson
```

判断规则为：

```text
ASC 不包含 Status.Perspective.ThirdPerson
→ 第一人称

ASC 包含 Status.Perspective.ThirdPerson
→ 第三人称
```

因此只需要一个第三人称状态标签。

第一人称是默认状态，不需要额外创建：

```text
Status.Perspective.FirstPerson
```

当前实现达到的相机行为是：

```text
进入游戏
→ 默认使用 CM_FirstPerson

普通状态下按 V
→ 第一人称切换为第三人称
→ 或第三人称切换为第一人称

第一人称状态下按住右键
→ 使用 CM_FirstPersonADS

第三人称状态下按住右键
→ 使用 CM_ThirdPersonADS

按住右键期间继续按 V
→ 在 CM_FirstPersonADS 和 CM_ThirdPersonADS 之间切换
→ GA_ADS 不结束
→ ADS 的其他逻辑继续运行

松开右键
→ GA_ADS 结束
→ 清除 ADS 临时相机
→ 根据 Status.Perspective.ThirdPerson 返回对应的基础相机
```

当前 `GA_TogglePerspective` 是一次性 Ability：

```text
按 V
→ Ability 激活
→ 修改 Gameplay Tag
→ Ability 立即结束
```

Gameplay Tag 是通过 `AddLooseGameplayTags` 添加的，不属于 Ability 的 `Activation Owned Tags`，因此：

```text
GA_TogglePerspective 结束
→ Status.Perspective.ThirdPerson 仍然保留
```

不需要让 `GA_TogglePerspective` 持续激活。

***

### 1.2 按下 V 后发生的完整链条

完整输入链如下：

```text
物理按键 V
↓
IMC_ShooterGame
将 V 映射到 IA_TogglePerspective
↓
IA_TogglePerspective
产生一次 Boolean Pressed 输入
↓
InputData_ShooterGame_AddOns
将 IA_TogglePerspective 映射为
InputTag.Ability.TogglePerspective
↓
Lyra 输入系统
把该 InputTag 交给 Ability System Component
↓
AbilitySet_ShooterHero
找到使用相同 InputTag 的
GA_TogglePerspective
↓
激活 GA_TogglePerspective
```

`GA_TogglePerspective` 激活后执行：

```text
GetAbilitySystemComponentFromActorInfo
↓
把有效 ASC 作为 GameplayTagAssetInterface 使用
↓
HasMatchingGameplayTag
检查 Status.Perspective.ThirdPerson
↓
Branch
```

分支规则为：

```text
Status.Perspective.ThirdPerson 不存在
→ AddLooseGameplayTags
→ 添加 Status.Perspective.ThirdPerson
→ EndAbility

Status.Perspective.ThirdPerson 已存在
→ RemoveLooseGameplayTags
→ 移除 Status.Perspective.ThirdPerson
→ EndAbility
```

这一步只修改“当前人称状态”，`GA_TogglePerspective` 本身不直接调用：

```text
SetCameraMode(CM_FirstPerson)
SetCameraMode(CM_ThirdPerson)
```

基础相机由 `ULyraHeroComponent::DetermineCameraMode()` 统一决定。

***

### 1.3 Gameplay Tag 改变后，相机如何改变

`ULyraHeroComponent` 已经把自己的 `DetermineCameraMode()` 绑定到：

```text
ULyraCameraComponent::DetermineCameraModeDelegate
```

Lyra Camera Component 更新相机时，会调用该函数询问：

```text
“这一帧应该使用哪个 CameraMode？”
```

`DetermineCameraMode()` 当前按照以下优先级判断：

```text
优先级 1：
AbilityCameraMode 是否存在

存在
→ 返回 AbilityCameraMode
→ 例如 GA_ADS 设置的 ADS 相机

不存在
→ 继续判断


优先级 2：
ASC 是否包含 Status.Perspective.ThirdPerson

包含标签，并且 ThirdPersonCameraMode 已配置
→ 返回 ThirdPersonCameraMode
→ 当前为 CM_ThirdPerson

不包含标签
→ 继续判断


优先级 3：
返回 PawnData->DefaultCameraMode

HeroData_ShooterGame 当前默认相机为 CM_FirstPerson
→ 返回 CM_FirstPerson
```

因此普通状态下：

```text
没有第三人称标签
→ CM_FirstPerson

有第三人称标签
→ CM_ThirdPerson
```

该实现不需要在 `ULyraHeroComponent` 中额外注册 Gameplay Tag 变化事件。

原因是 Lyra Camera Component 会持续调用 `DetermineCameraMode()`，状态标签改变后，下一次相机更新会读取到新状态。

***

### 1.4 右键 ADS 的完整相机链条

右键输入链为：

```text
RightMouseButton
↓
IMC_ShooterGame
↓
IA_ADS
↓
InputData_ShooterGame_AddOns
↓
InputTag.Weapon.ADS
↓
AbilitySet_ShooterHero
↓
GA_ADS
```

`GA_ADS` 激活时先检查当前人称：

```text
GetAbilitySystemComponentFromActorInfo
↓
ToGameplayTagAssetInterface
↓
HasMatchingGameplayTag
检查 Status.Perspective.ThirdPerson
↓
Branch
```

分支规则：

```text
存在 Status.Perspective.ThirdPerson
→ SetCameraMode(CM_ThirdPersonADS)

不存在 Status.Perspective.ThirdPerson
→ SetCameraMode(CM_FirstPersonADS)
```

`SetCameraMode` 设置的是 `ULyraHeroComponent` 中的：

```text
AbilityCameraMode
```

由于 `AbilityCameraMode` 在 `DetermineCameraMode()` 中拥有最高优先级，所以 ADS 激活期间：

```text
基础 CM_FirstPerson 或 CM_ThirdPerson
不会覆盖 ADS CameraMode
```

***

### 1.5 瞄准期间按 V 的完整链条

`GA_ADS` 激活时，同时创建两个等待任务。

等待进入第三人称：

```text
WaitGameplayTagAdd
Tag = Status.Perspective.ThirdPerson
OnlyTriggerOnce = false
External Target = GetOwningActorFromActorInfo
↓
标签被添加
↓
SetCameraMode(CM_ThirdPersonADS)
```

等待返回第一人称：

```text
WaitGameplayTagRemove
Tag = Status.Perspective.ThirdPerson
OnlyTriggerOnce = false
External Target = GetOwningActorFromActorInfo
↓
标签被移除
↓
SetCameraMode(CM_FirstPersonADS)
```

因此瞄准期间按 V 的实际过程为：

```text
玩家按住右键
→ GA_ADS 保持激活
→ 当前使用 CM_FirstPersonADS

玩家按 V
→ GA_TogglePerspective 激活
→ 添加 Status.Perspective.ThirdPerson
→ GA_TogglePerspective 结束
→ GA_ADS 的 WaitGameplayTagAdd 收到通知
→ GA_ADS 改为 CM_ThirdPersonADS
→ GA_ADS 继续运行

玩家再次按 V
→ GA_TogglePerspective 激活
→ 移除 Status.Perspective.ThirdPerson
→ GA_TogglePerspective 结束
→ GA_ADS 的 WaitGameplayTagRemove 收到通知
→ GA_ADS 改为 CM_FirstPersonADS
→ GA_ADS 继续运行
```

由于两个等待任务都是：

```text
OnlyTriggerOnce = false
```

所以同一次 ADS 过程中可以多次切换：

```text
第一人称 ADS
↔
第三人称 ADS
```

***

### 1.6 松开右键后发生什么

松开右键后：

```text
WaitInputRelease
↓
EndAbility
↓
触发 GA_ADS 的 OnEndAbility
↓
ClearCameraMode
```

`ClearCameraMode` 清除：

```text
AbilityCameraMode
```

清除之后，`DetermineCameraMode()` 重新执行普通基础相机判断：

```text
仍然存在 Status.Perspective.ThirdPerson
→ 返回 CM_ThirdPerson

不存在 Status.Perspective.ThirdPerson
→ 返回 HeroData 默认的 CM_FirstPerson
```

因此 ADS 结束后不会固定返回第一人称，也不会固定返回第三人称，而是返回玩家松开右键时对应的人称。

***

### 1.7 死亡和重生期间的人称状态

Lyra 的玩家 Ability System Component 位于 `ALyraPlayerState`。

初始化时的关系为：

```text
ASC Owner Actor
= LyraPlayerState

ASC Avatar Actor
= 当前 LyraCharacter
```

`GA_TogglePerspective` 使用：

```text
GetOwningActorFromActorInfo
```

添加和移除 Loose Gameplay Tag。

在 Lyra 玩家角色中，该 Owning Actor 对应拥有 ASC 的 `LyraPlayerState`。

因此状态保存位置为：

```text
PlayerState 拥有的 ASC
└─ Status.Perspective.ThirdPerson
```

角色死亡主要更换或重新初始化 Avatar Pawn，PlayerState 继续存在。按照当前数据归属：

```text
角色死亡
→ 第三人称状态标签继续保存在 PlayerState ASC

角色重生
→ 新 Pawn 重新连接同一个 PlayerState ASC
→ LyraHeroComponent 再次读取该标签
→ 恢复死亡前对应的人称
```

`GA_TogglePerspective` 还配置了以下阻止标签：

```text
Status.Death.Dying
Status.Death.Dead
```

因此：

```text
角色活着
→ 可以按 V 切换

角色正在死亡或已经死亡
→ GA_TogglePerspective 不激活

死亡和重生过程本身
→ 不主动添加或移除人称状态
```

当前 `GA_TogglePerspective` 的网络配置为：

```text
Net Execution Policy = LocalOnly
Replication Policy = ReplicateNo
Add/Remove Loose Gameplay Tags 的 bShouldReplicate = false
```

所以该标签当前表示本地玩家的本地相机状态。

***

### 1.8 当前实现的范围

当前已经完成的是：

```text
V 输入
→ 人称状态标签切换
→ 第一/第三人称基础 CameraMode 切换
→ ADS 激活时选择对应 ADS CameraMode
→ ADS 过程中按 V 动态替换 ADS CameraMode
→ ADS 结束后返回正确的基础 CameraMode
→ 人称状态保存在 PlayerState ASC
```

当前还没有实现：

```text
第一人称时隐藏 Lyra Character Parts
第三人称时重新显示 Lyra Character Parts

独立第一人称 Arms
独立第一人称 Weapon Mesh
第一人称 AnimBP
第一人称 IK/Retarget
第一人称和第三人称武器 VFX 分流
```

因此当前结构是“相机与状态切换系统”，还不是完整的“两套角色模型第一人称系统”。

***

## 2. 详细描述修改部分

### 2.1 修改和创建清单

#### 2.1.1 C++ 文件

当前工作区中修改、尚未提交：

```text
D:\RogueFPS\Source\LyraGame\Character\LyraHeroComponent.h
D:\RogueFPS\Source\LyraGame\Character\LyraHeroComponent.cpp
```

没有修改：

```text
ULyraPawnData 类定义
LyraPawnComponent_CharacterParts.h
LyraPawnComponent_CharacterParts.cpp
```

***

#### 2.1.2 Gameplay Tag 配置

当前工作区中修改、尚未提交：

```text
D:\RogueFPS\Plugins\GameFeatures\ShooterCore\Config\Tags\ShooterCoreTags.ini
```

新增标签：

```text
InputTag.Ability.TogglePerspective
Status.Perspective.ThirdPerson
```

***

#### 2.1.3 输入资产

创建：

```text
/ShooterCore/Input/Actions/IA_TogglePerspective
```

修改：

```text
/ShooterCore/Input/Mappings/IMC_ShooterGame
/ShooterCore/Input/Actions/InputData_ShooterGame_AddOns
```

现有、继续作为输入桥接使用：

```text
/ShooterCore/Experiences/LAS_ShooterGame_SharedInput
```

***

#### 2.1.4 Ability 资产

创建：

```text
/ShooterCore/Input/Abilities/GA_TogglePerspective
```

修改：

```text
/ShooterCore/Input/Abilities/GA_ADS
/ShooterCore/Game/AbilitySet_ShooterHero
```

***

#### 2.1.5 角色和 Pawn Data 资产

修改：

```text
/ShooterCore/Game/HeroData_ShooterGame
/ShooterCore/Game/B_Hero_ShooterMannequin
```

这里修改的是 `HeroData_ShooterGame` 资产中的已有字段，没有修改 `ULyraPawnData` C++ 类。

***

#### 2.1.6 基础相机资产

创建：

```text
/Game/Characters/Cameras/CM_FirstPerson
/Game/Characters/Cameras/FirstPersonOffsetCurve
```

修改：

```text
/Game/Characters/Cameras/CM_ThirdPerson
/Game/Characters/Cameras/ThirdPersonOffsetCurve
```

***

#### 2.1.7 ADS 相机资产

创建：

```text
/ShooterCore/Camera/CM_FirstPersonADS
```

现有并继续使用：

```text
/ShooterCore/Camera/CM_ThirdPersonADS
/ShooterCore/Camera/ThirdPersonADSOffsetCurve
```

***

### 2.2 ShooterCoreTags.ini 的修改

新增输入路由标签：

```ini
GameplayTagList=(Tag="InputTag.Ability.TogglePerspective",DevComment="")
```

新增人称状态标签：

```ini
GameplayTagList=(Tag="Status.Perspective.ThirdPerson",DevComment="Local player currently uses the third-person perspective.")
```

两个标签用途不同：

```text
InputTag.Ability.TogglePerspective
→ 表示“玩家触发了切换人称输入”
→ 用于输入系统找到 GA_TogglePerspective

Status.Perspective.ThirdPerson
→ 表示“玩家当前处于第三人称”
→ 用于相机和 ADS 判断当前状态
```

***

### 2.3 输入资产的修改

#### 2.3.1 IA\_TogglePerspective

当前属性：

```text
Value Type = Boolean
Trigger = InputTriggerPressed
Consume Input = true
Trigger When Paused = false
Modifiers = 空
```

这使 V 键每次按下只产生一次触发。

***

#### 2.3.2 IMC\_ShooterGame

在 UE 5.8 当前资产结构中，映射存放于：

```text
DefaultKeyMappings.Mappings
```

新增映射：

```text
Action = IA_TogglePerspective
Key = V
```

完整含义：

```text
V
→ IA_TogglePerspective
```

***

#### 2.3.3 InputData\_ShooterGame\_AddOns

`IA_TogglePerspective` 放入：

```text
Ability Input Actions
```

而不是：

```text
Native Input Actions
```

配置为：

```text
IA_TogglePerspective
→ InputTag.Ability.TogglePerspective
```

当前 `Native Input Actions` 仍为空。

***

#### 2.3.4 LAS\_ShooterGame\_SharedInput

该资产没有因为人称功能而新建，但它是实际输入链的一部分。

当前包含：

```text
GameFeatureAction_AddInputBinding
→ InputData_ShooterGame_AddOns

GameFeatureAction_AddInputContextMapping
→ IMC_ShooterGame
→ Priority = 0
→ bRegisterWithSettings = true
```

因此 ShooterGame Experience 激活后，会实际加载：

```text
IMC_ShooterGame
InputData_ShooterGame_AddOns
```

***

### 2.4 AbilitySet\_ShooterHero 的修改

在 `Granted Gameplay Abilities` 中新增：

```text
Ability = GA_TogglePerspective
Ability Level = 1
Input Tag = InputTag.Ability.TogglePerspective
```

形成输入标签和 Ability 之间的最终连接：

```text
InputData_ShooterGame_AddOns
产生 InputTag.Ability.TogglePerspective
↓
AbilitySet_ShooterHero
找到相同 Input Tag 的 GA_TogglePerspective
↓
激活 GA_TogglePerspective
```

`HeroData_ShooterGame` 已经引用：

```text
AbilitySet_ShooterHero
```

所以玩家 Pawn 初始化 ASC 时会获得该 Ability。

***

### 2.5 GA\_TogglePerspective 的创建和后续修复

#### 2.5.1 Ability 默认设置

当前属性：

```text
Parent Class = ULyraGameplayAbility

Activation Policy = OnInputTriggered
Activation Group = Independent
Instancing Policy = InstancedPerActor

Net Execution Policy = LocalOnly
Replication Policy = ReplicateNo

Ability Tags = 空
Activation Owned Tags = 空

Activation Blocked Tags：
- Status.Death.Dying
- Status.Death.Dead
```

当前没有添加：

```text
Ability.Type.StatusChange
Ability.Type.StatusChange.Perspective
```

***

#### 2.5.2 EventGraph

当前逻辑：

```text
ActivateAbility
↓
GetAbilitySystemComponentFromActorInfo
↓
ToGameplayTagAssetInterface
↓
HasMatchingGameplayTag
Tag = Status.Perspective.ThirdPerson
↓
Branch
```

True 分支：

```text
RemoveLooseGameplayTags
Actor = GetOwningActorFromActorInfo
GameplayTags = Status.Perspective.ThirdPerson
bShouldReplicate = false
↓
EndAbility
```

False 分支：

```text
AddLooseGameplayTags
Actor = GetOwningActorFromActorInfo
GameplayTags = Status.Perspective.ThirdPerson
bShouldReplicate = false
↓
EndAbility
```

***

#### 2.5.3 Gameplay Tag 查询修复

发生运行时错误后，查询来源被修正为：

```text
GetAbilitySystemComponentFromActorInfo
→ ToGameplayTagAssetInterface
→ HasMatchingGameplayTag
```

这里保留 `ToGameplayTagAssetInterface` 是有效的。

UE 5.8 中：

```cpp
class UAbilitySystemComponent
    : public UGameplayTasksComponent,
      public IGameplayTagAssetInterface,
      public IAbilitySystemReplicationProxyInterface
```

所以：

```text
有效的 UAbilitySystemComponent
→ 可以合法转换为 GameplayTagAssetInterface
→ 可以执行 HasMatchingGameplayTag
```

修复重点是：

```text
先取得有效 ASC
→ 再把 ASC 作为 GameplayTagAssetInterface 查询
```

`GA_TogglePerspective` 和 `GA_ADS` 当前都使用这一查询来源。

***

### 2.6 LyraHeroComponent.h 的修改

在现有 `ULyraHeroComponent` 类中新增：

```cpp
/** Base camera mode used while the owning ASC has the third-person perspective status. */
UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Lyra|Camera")
TSubclassOf<ULyraCameraMode> ThirdPersonCameraMode;
```

该属性保存的是：

```text
ULyraCameraMode 子类
```

不是相机对象实例，也不是 Gameplay Tag。

它用于保存：

```text
处于第三人称状态时应该返回哪一个 CameraMode 类
```

***

### 2.7 LyraHeroComponent.cpp 的修改

新增头文件：

```cpp
#include "GameplayTagsManager.h"
```

构造函数新增初始化：

```cpp
ThirdPersonCameraMode = nullptr;
```

`DetermineCameraMode()` 中加入第三人称状态判断。

当前逻辑等价于：

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
        static const FGameplayTag ThirdPersonPerspectiveTag =
            UGameplayTagsManager::Get().RequestGameplayTag(
                FName(TEXT("Status.Perspective.ThirdPerson")));

        if (ThirdPersonCameraMode)
        {
            if (const ULyraAbilitySystemComponent* LyraASC =
                PawnExtComp->GetLyraAbilitySystemComponent())
            {
                if (LyraASC->HasMatchingGameplayTag(
                    ThirdPersonPerspectiveTag))
                {
                    return ThirdPersonCameraMode;
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

最终优先级为：

```text
AbilityCameraMode
>
Status.Perspective.ThirdPerson 对应的 ThirdPersonCameraMode
>
PawnData->DefaultCameraMode
```

***

### 2.8 B\_Hero\_ShooterMannequin 的修改

`B_Hero_ShooterMannequin` 继承自：

```text
B_Hero_Default
```

`B_Hero_Default` 中已经包含一个：

```text
LyraHeroComponent
```

该组件在蓝图组件列表中的名称为：

```text
LyraHero
```

没有创建新的 Hero Component。

在 `B_Hero_ShooterMannequin` 的继承组件默认值中，将 C++ 新增属性设置为：

```text
LyraHeroComponent.ThirdPersonCameraMode
= /Game/Characters/Cameras/CM_ThirdPerson
```

因此：

```text
C++ 定义 ThirdPersonCameraMode 属性
↓
B_Hero_ShooterMannequin 给该属性赋值 CM_ThirdPerson
↓
运行时 DetermineCameraMode() 读取该值
```

蓝图没有重新定义 `ThirdPersonCameraMode`，而是在给 C++ 属性赋默认值。

***

### 2.9 HeroData\_ShooterGame 的修改

当前关键属性：

```text
Pawn Class
= B_Hero_ShooterMannequin

Ability Sets
= AbilitySet_ShooterHero

Default Camera Mode
= CM_FirstPerson
```

因此：

```text
没有 Status.Perspective.ThirdPerson
→ DetermineCameraMode()
→ PawnData->DefaultCameraMode
→ CM_FirstPerson
```

没有修改 `ULyraPawnData` C++ 类。

只修改了 `HeroData_ShooterGame` 这个 `ULyraPawnData` 资产实例中已经存在的：

```text
DefaultCameraMode
```

***

### 2.10 基础相机资产的修改

#### 2.10.1 CM\_FirstPerson

资产路径：

```text
/Game/Characters/Cameras/CM_FirstPerson
```

父类：

```text
ULyraCameraMode_ThirdPerson
```

当前主要属性：

```text
Target Offset Curve
= FirstPersonOffsetCurve

Field Of View
= 80

Blend Time
= 0.5

Blend Function
= EaseOut
```

虽然资产名是 `CM_FirstPerson`，它当前仍复用：

```text
ULyraCameraMode_ThirdPerson
```

通过不同的 Target Offset Curve 产生第一人称位置。

这不是 UE 5.8 的 First Person Rendering API。

***

#### 2.10.2 CM\_ThirdPerson

资产路径：

```text
/Game/Characters/Cameras/CM_ThirdPerson
```

父类：

```text
ULyraCameraMode_ThirdPerson
```

当前主要属性：

```text
Target Offset Curve
= ThirdPersonOffsetCurve

Field Of View
= 80

Blend Time
= 0.5

Blend Function
= EaseOut
```

当前 `CM_FirstPerson` 和 `CM_ThirdPerson` 的相机属性中，主要结构差异是：

```text
CM_FirstPerson
→ FirstPersonOffsetCurve

CM_ThirdPerson
→ ThirdPersonOffsetCurve
```

因此两种基础视角的位置差异由两条 Curve 决定。

***

### 2.11 GA\_ADS 的修改

#### 2.11.1 保留的原有设置

当前主要属性：

```text
Parent Class
= GA_AbilityWithWidget

Ability Tags
= Ability.Type.Action.ADS

Activation Owned Tags
= Event.Movement.ADS

Activation Policy
= OnInputTriggered

Net Execution Policy
= LocalPredicted

ADS Multiplier
= 0.5
```

原有 ADS 行为继续保留：

```text
保存当前 MaxWalkSpeed
按照 ADSMultiplier 降低移动速度
添加 IMC_ADS_Speed
BroadcastToUI(true)
播放 ZoomIn 声音
等待输入松开
结束时恢复移动速度
移除 IMC_ADS_Speed
BroadcastToUI(false)
播放 ZoomOut 声音
```

***

#### 2.11.2 激活时选择人称 ADS 相机

`ActivateAbility` 的第一个 Sequence 分支新增：

```text
GetAbilitySystemComponentFromActorInfo
↓
ToGameplayTagAssetInterface
↓
HasMatchingGameplayTag
Tag = Status.Perspective.ThirdPerson
↓
Branch
```

分支：

```text
True
→ SetCameraMode(CM_ThirdPersonADS)

False
→ SetCameraMode(CM_FirstPersonADS)
```

该查询也使用修复后的 ASC 来源。

***

#### 2.11.3 ADS 过程中监听人称变化

新增：

```text
WaitGameplayTagAdd
Tag = Status.Perspective.ThirdPerson
OnlyTriggerOnce = false
External Target = GetOwningActorFromActorInfo
↓
SetCameraMode(CM_ThirdPersonADS)
```

新增：

```text
WaitGameplayTagRemove
Tag = Status.Perspective.ThirdPerson
OnlyTriggerOnce = false
External Target = GetOwningActorFromActorInfo
↓
SetCameraMode(CM_FirstPersonADS)
```

***

#### 2.11.4 ADS 结束时清除临时相机

`OnEndAbility` 开始时执行：

```text
ClearCameraMode
```

随后执行原有 ADS 清理流程。

***

### 2.12 ADS 相机资产的当前配置

#### 2.12.1 CM\_FirstPersonADS

资产路径：

```text
/ShooterCore/Camera/CM_FirstPersonADS
```

当前属性：

```text
Parent Class
= ULyraCameraMode_ThirdPerson

Target Offset Curve
= ThirdPersonADSOffsetCurve

Field Of View
= 70

Blend Time
= 0.22

Camera Type Tag
= Lyra.Weapon.SteadyAimingCamera
```

***

#### 2.12.2 CM\_ThirdPersonADS

资产路径：

```text
/ShooterCore/Camera/CM_ThirdPersonADS
```

当前属性：

```text
Parent Class
= ULyraCameraMode_ThirdPerson

Target Offset Curve
= ThirdPersonADSOffsetCurve

Field Of View
= 70

Blend Time
= 0.22

Camera Type Tag
= Lyra.Weapon.SteadyAimingCamera
```

当前两个 ADS CameraMode 的全部公开相机属性相同：

```text
CM_FirstPersonADS
=
CM_ThirdPersonADS
```

所以目前已经分离的是：

```text
相机资产身份
切换逻辑
未来独立调整入口
```

目前还没有产生不同的是：

```text
第一人称 ADS 和第三人称 ADS 的实际相机参数
```

这与当前提交说明中的：

```text
尚未调整具体视角
```

一致。

***

### 2.13 当前没有落地的 Character Parts 显隐修改

以下文件当前仍未修改：

```text
D:\RogueFPS\Source\LyraGame\Cosmetics\LyraPawnComponent_CharacterParts.h
D:\RogueFPS\Source\LyraGame\Cosmetics\LyraPawnComponent_CharacterParts.cpp
```

当前不存在以下人称相关实现：

```text
RegisterGameplayTagEvent
HandlePerspectiveTagChanged
ApplyPerspectiveVisibility
SetOwnerNoSee
SetOnlyOwnerSee
```

当前 `BroadcastChanged()` 也没有根据人称重新应用模型可见性。

因此当前状态标签只驱动：

```text
基础 CameraMode
ADS CameraMode
```

尚未驱动：

```text
B_Manny / B_Quinn Character Parts 的隐藏和显示
```

***

## 3. 具体解释修改意义

### 3.1 为什么需要两个 Gameplay Tag

对应第 2.2 节。

两个 Tag 分别解决两个不同问题。

`InputTag.Ability.TogglePerspective` 表示输入事件：

```text
玩家刚刚按了切换键
```

它只负责找到并激活 `GA_TogglePerspective`。

`Status.Perspective.ThirdPerson` 表示持久状态：

```text
玩家当前正在使用第三人称
```

它供以下系统查询：

```text
LyraHeroComponent
GA_TogglePerspective
GA_ADS
未来的 Character Parts 显隐系统
```

输入 Tag 是一次事件，状态 Tag 是持续数据，因此不能只使用一个 Tag 代替两者。

***

### 3.2 为什么需要 IA、IMC 和 InputData 三层

对应第 2.3 节。

三层分别回答三个问题。

`IMC_ShooterGame` 回答：

```text
哪个物理按键触发哪个 Input Action？
```

当前答案：

```text
V
→ IA_TogglePerspective
```

`IA_TogglePerspective` 回答：

```text
这个输入是什么类型，什么时候算触发？
```

当前答案：

```text
Boolean
Pressed 时触发一次
```

`InputData_ShooterGame_AddOns` 回答：

```text
这个 Input Action 在 Lyra Gameplay 系统中代表什么输入标签？
```

当前答案：

```text
IA_TogglePerspective
→ InputTag.Ability.TogglePerspective
```

这种分层允许以后分别修改：

```text
键位
输入触发方式
Gameplay 语义
```

而不需要重新修改 Ability 蓝图。

***

### 3.3 为什么还需要 AbilitySet\_ShooterHero

对应第 2.4 节。

`InputData_ShooterGame_AddOns` 只产生：

```text
InputTag.Ability.TogglePerspective
```

它本身不知道应该运行哪一个 Gameplay Ability。

`AbilitySet_ShooterHero` 建立：

```text
InputTag.Ability.TogglePerspective
→ GA_TogglePerspective
```

因此完整关系是：

```text
IA_TogglePerspective
→ InputTag.Ability.TogglePerspective
→ GA_TogglePerspective
```

缺少 `AbilitySet_ShooterHero` 这一层时：

```text
V 可以产生 Input Action
InputData 也可以产生 Input Tag
ASC 中没有匹配该 Input Tag 的 Ability
→ GA_TogglePerspective 不会激活
```

***

### 3.4 为什么 GA\_TogglePerspective 是一次性 Ability

对应第 2.5 节。

人称状态不需要依赖 Ability 的持续生命周期。

当前过程是：

```text
Ability 负责修改状态
Gameplay Tag 负责保存状态
```

因此：

```text
按 V
→ GA 激活
→ 添加或移除 Loose Gameplay Tag
→ GA 结束
→ Loose Gameplay Tag 继续存在或继续保持不存在
```

这样可以避免让一个只负责切换状态的 Ability 长期处于激活状态。

状态持续性来自：

```text
ASC 中的 Loose Gameplay Tag
```

而不是：

```text
GA_TogglePerspective 持续激活
```

***

### 3.5 为什么使用 AddLooseGameplayTags，而不是 Activation Owned Tags

对应第 2.5 节。

`Activation Owned Tags` 的生命周期与 Ability 激活状态绑定：

```text
Ability 激活
→ 自动添加标签

Ability 结束
→ 自动移除标签
```

如果把第三人称状态放入 `Activation Owned Tags`，而 `GA_TogglePerspective` 又立即结束，就会发生：
