# RogueFPS V 键第一/第三人称切换最终流程

# 1. 核心状态

使用 Gameplay Tag：

```text
Status.Perspective.ThirdPerson
```

表达当前人称状态：

```text
标签不存在
→ 第一人称

标签存在
→ 第三人称
```

第一人称由“第三人称标签不存在”表达，因此只需要一个状态标签。

状态保存在玩家当前使用的 `ULyraAbilitySystemComponent` 中。Lyra 玩家使用 PlayerState 承载 ASC，因此该状态可以跨 Pawn 的死亡和重生继续存在。

## 2. 总体结构

```text
V 键
↓
IA_TogglePerspective
↓
IMC_ShooterGame
↓
InputData_ShooterGame_AddOns
↓
InputTag.Ability.TogglePerspective
↓
AbilitySet_ShooterHero
↓
GA_TogglePerspective
↓
读取 LyraASC 中的 Status.Perspective.ThirdPerson
↓
添加或移除 Status.Perspective.ThirdPerson
↓
GA_TogglePerspective 立即结束
↓
┌─────────────────────────┬──────────────────────────┐
│                         │                          │
↓                         ↓                          ↓
LyraHeroComponent         GA_ADS                     CharacterParts
选择基础相机               选择 ADS 相机               隐藏或显示第三人称身体
```

V 键的职责是修改状态。

相机、ADS 和模型显示是这个状态的三个独立使用者。

## 3. 输入链条

### 3.1 Input Action

资产：

```text
IA_TogglePerspective
```

含义：

```text
抽象的“切换人称”输入动作
```

### 3.2 Input Mapping Context

资产：

```text
IMC_ShooterGame
```

映射：

```text
V
→ IA_TogglePerspective
```

`IMC_ShooterGame` 负责把物理按键 V 转换成 Input Action。

### 3.3 Lyra Input Config

资产：

```text
InputData_ShooterGame_AddOns
```

在 Ability Input Actions 中建立：

```text
IA_TogglePerspective
→ InputTag.Ability.TogglePerspective
```

这一步把 Enhanced Input 的 Input Action 转换成 Lyra Ability 输入标签。

### 3.4 Ability Set

资产：

```text
AbilitySet_ShooterHero
```

授予：

```text
Ability：GA_TogglePerspective
Input Tag：InputTag.Ability.TogglePerspective
```

最终连接关系：

```text
IA_TogglePerspective
→ InputTag.Ability.TogglePerspective
→ GA_TogglePerspective
```

## 4. GA\_TogglePerspective 最终正确逻辑

`GA_TogglePerspective` 是一次性 Ability。

每次按 V：

```text
激活 Ability
→ 修改一次 Perspective Status
→ End Ability
```

Gameplay Tag 保留在 ASC 中，Ability 本身立即结束。

### 4.1 正确的 Tag 查询对象

Tag 查询、添加和移除全部使用同一个：

```text
ULyraAbilitySystemComponent
```

蓝图逻辑：

```text
Activate Ability
↓
Get Lyra Ability System Component From Actor Info
↓
保存为 LyraASC
↓
Is Valid
↓
LyraASC.Has Matching Gameplay Tag
Tag = Status.Perspective.ThirdPerson
↓
Branch
```

分支逻辑：

```text
True
→ LyraASC.Remove Loose Gameplay Tag
→ Status.Perspective.ThirdPerson

False
→ LyraASC.Add Loose Gameplay Tag
→ Status.Perspective.ThirdPerson
```

两个分支最后都执行：

```text
End Ability
```

### 4.2 等价 C++ 逻辑

```cpp
ULyraAbilitySystemComponent* LyraASC =
	GetLyraAbilitySystemComponentFromActorInfo();

if (!LyraASC)
{
	EndAbility(CurrentSpecHandle, CurrentActorInfo,
		CurrentActivationInfo, true, true);
	return;
}

const FGameplayTag ThirdPersonTag =
	UGameplayTagsManager::Get().RequestGameplayTag(
		FName(TEXT("Status.Perspective.ThirdPerson")));

if (LyraASC->HasMatchingGameplayTag(ThirdPersonTag))
{
	LyraASC->RemoveLooseGameplayTag(ThirdPersonTag);
}
else
{
	LyraASC->AddLooseGameplayTag(ThirdPersonTag);
}

EndAbility(CurrentSpecHandle, CurrentActorInfo,
	CurrentActivationInfo, true, false);
```

### 4.3 修复后的关键点

Tag 查询目标为：

```text
LyraASC
```

查询方法为：

```text
Has Matching Gameplay Tag
```

标签修改目标同样为：

```text
LyraASC
```

因此两次按 V 的状态变化为：

```text
初始：标签不存在

第一次 V
→ 查询结果 False
→ 添加 Status.Perspective.ThirdPerson
→ 第三人称

第二次 V
→ 查询结果 True
→ 移除 Status.Perspective.ThirdPerson
→ 第一人称
```

此前的运行时错误来自无效的：

```text
Object
→ Conv Object To GameplayTagAssetInterface
→ 返回空
→ 查询 Tag
```

修复后直接查询真实 ASC，完整解决：

```text
尝试读取非 UClass 中的属性，结果为无
```

以及：

```text
第一次 V 可以切换
第二次 V 无法切回
```

## 5. 基础相机选择

基础相机由：

```text
ULyraHeroComponent::DetermineCameraMode()
```

决定。

修改文件：

```text
D:\RogueFPS\Source\LyraGame\Character\LyraHeroComponent.h
D:\RogueFPS\Source\LyraGame\Character\LyraHeroComponent.cpp
```

### 5.1 ThirdPersonCameraMode 属性

在 `ULyraHeroComponent` 中增加：

```cpp
/** Base camera mode used while the owning ASC has the third-person perspective status. */
UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Lyra|Camera")
TSubclassOf<ULyraCameraMode> ThirdPersonCameraMode;
```

构造函数初始化：

```cpp
ThirdPersonCameraMode = nullptr;
```

在角色蓝图的 HeroComponent 中赋值：

```text
ThirdPersonCameraMode
= CM_ThirdPerson
```

### 5.2 默认第一人称

`HeroData_ShooterGame` 的默认相机设置为：

```text
DefaultCameraMode
= CM_FirstPerson
```

因此：

```text
没有第三人称标签
→ 返回 PawnData 默认相机
→ CM_FirstPerson
```

### 5.3 DetermineCameraMode 最终优先级

```cpp
TSubclassOf<ULyraCameraMode>
ULyraHeroComponent::DetermineCameraMode() const
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
		ULyraPawnExtensionComponent::
			FindPawnExtensionComponent(Pawn))
	{
		static const FGameplayTag ThirdPersonPerspectiveTag =
			UGameplayTagsManager::Get().RequestGameplayTag(
				FName(TEXT(
					"Status.Perspective.ThirdPerson")));

		if (ThirdPersonCameraMode)
		{
			if (const ULyraAbilitySystemComponent* LyraASC =
				PawnExtComp->
					GetLyraAbilitySystemComponent())
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

最终优先级：

```text
1. AbilityCameraMode
2. Status.Perspective.ThirdPerson 对应的 ThirdPersonCameraMode
3. PawnData.DefaultCameraMode
```

普通状态下：

```text
第三人称标签存在
→ CM_ThirdPerson

第三人称标签不存在
→ CM_FirstPerson
```

## 6. ADS 相机逻辑

ADS 使用 Ability Camera Mode，因此优先级高于普通人称相机。

相机资产：

```text
CM_FirstPersonADS
CM_ThirdPersonADS
```

右键按下激活 `GA_ADS` 时：

```text
执行 GA_ADS 公共瞄准逻辑
↓
查询 LyraASC
↓
检查 Status.Perspective.ThirdPerson
```

选择规则：

```text
标签不存在
→ Set Ability Camera Mode
→ CM_FirstPersonADS

标签存在
→ Set Ability Camera Mode
→ CM_ThirdPersonADS
```

右键松开时：

```text
Clear Ability Camera Mode
→ End GA_ADS
→ LyraHeroComponent 重新决定基础相机
```

返回规则：

```text
标签不存在
→ CM_FirstPerson

标签存在
→ CM_ThirdPerson
```

## 7. 瞄准过程中按 V

瞄准期间：

```text
AbilityCameraMode
```

具有最高优先级。

因此，V 改变 Perspective Tag 后，当前激活的 `GA_ADS` 同步刷新 ADS Camera Mode：

```text
第一人称 ADS 状态按 V
→ 添加 Status.Perspective.ThirdPerson
→ 模型状态切换为第三人称
→ ADS 相机刷新为 CM_ThirdPersonADS

第三人称 ADS 状态按 V
→ 移除 Status.Perspective.ThirdPerson
→ 模型状态切换为第一人称
→ ADS 相机刷新为 CM_FirstPersonADS
```

对应的统一逻辑为：

```text
Apply ADS Camera Mode From Perspective
↓
Has Matching Gameplay Tag
↓
True  → CM_ThirdPersonADS
False → CM_FirstPersonADS
```

该逻辑在以下时机执行：

```text
1. GA_ADS 激活时
2. 瞄准期间 Perspective Tag 发生变化时
```

## 8. 第三人称身体显示

第三人称身体显示同样读取：

```text
Status.Perspective.ThirdPerson
```

Lyra 的可见身体来自动态生成的 Character Part：

```text
B_Manny
B_Quinn
```

`CharacterMesh0 / GetMesh()` 是隐形动画驱动 Mesh，实际显示控制作用于 Character Part Actor 内的 `UPrimitiveComponent`。

状态规则：

```text
标签不存在
→ 第一人称
→ SetOwnerNoSee(true)

标签存在
→ 第三人称
→ SetOwnerNoSee(false)
```

等价逻辑：

```cpp
const bool bIsThirdPerson =
	LyraASC->HasMatchingGameplayTag(
		ThirdPersonPerspectiveTag);

const bool bOwnerNoSee =
	!bIsThirdPerson;

PrimitiveComponent->
	SetOwnerNoSee(bOwnerNoSee);
```

`OwnerNoSee` 的显示结果：

```text
第一人称本地玩家
→ 隐藏自己的第三人称身体

其他客户端
→ 继续看到该玩家的第三人称身体

第三人称本地玩家
→ 显示自己的第三人称身体
```

Character Parts 在两个时机应用状态：

```text
1. Perspective Tag 变化
2. Character Part 动态生成或重建
```

## 9. 完整状态表

| Perspective Tag | ADS | 基础/临时相机             | 本地第三人称身体 |
| :-------------- | --: | :------------------ | :------- |
| 不存在             |   否 | `CM_FirstPerson`    | 隐藏       |
| 存在              |   否 | `CM_ThirdPerson`    | 显示       |
| 不存在             |   是 | `CM_FirstPersonADS` | 隐藏       |
| 存在              |   是 | `CM_ThirdPersonADS` | 显示       |

## 10. 完整运行流程

### 10.1 默认进入游戏

```text
HeroData 默认相机 = CM_FirstPerson
Status.Perspective.ThirdPerson 不存在
↓
LyraHeroComponent 返回 CM_FirstPerson
↓
CharacterParts 设置 OwnerNoSee = true
```

### 10.2 第一次按 V

```text
V
→ IA_TogglePerspective
→ InputTag.Ability.TogglePerspective
→ GA_TogglePerspective
→ LyraASC 查询第三人称标签
→ 标签不存在
→ 添加 Status.Perspective.ThirdPerson
→ GA 结束
↓
LyraHeroComponent 返回 CM_ThirdPerson
↓
CharacterParts 设置 OwnerNoSee = false
```

### 10.3 第二次按 V

```text
V
→ GA_TogglePerspective
→ LyraASC 查询第三人称标签
→ 标签存在
→ 移除 Status.Perspective.ThirdPerson
→ GA 结束
↓
LyraHeroComponent 返回 CM_FirstPerson
↓
CharacterParts 设置 OwnerNoSee = true
```

### 10.4 第一人称按住右键

```text
GA_ADS 激活
→ 标签不存在
→ AbilityCameraMode = CM_FirstPersonADS
```

### 10.5 第一人称 ADS 中按 V

```text
添加 Status.Perspective.ThirdPerson
→ CharacterParts 显示第三人称身体
→ GA_ADS 刷新 AbilityCameraMode
→ CM_ThirdPersonADS
```

### 10.6 松开右键

```text
Clear Ability Camera Mode
→ End GA_ADS
→ LyraHeroComponent 检查 Perspective Tag
→ 返回 CM_ThirdPerson
```

## 11. 最终职责划分

```text
IA_TogglePerspective
→ 表示切换人称输入动作

IMC_ShooterGame
→ 把 V 映射到 IA_TogglePerspective

InputData_ShooterGame_AddOns
→ 把 IA 转换为 InputTag

AbilitySet_ShooterHero
→ 把 InputTag 连接到 GA_TogglePerspective

GA_TogglePerspective
→ 添加或移除 Perspective Status

LyraASC
→ 保存 Perspective Status

LyraHeroComponent
→ 根据 Perspective Status 决定普通相机

GA_ADS
→ 根据 Perspective Status 决定 ADS 相机

LyraPawnComponent_CharacterParts
→ 根据 Perspective Status 控制第三人称身体可见性
```

最终状态源只有：

```text
Status.Perspective.ThirdPerson
```

所有相机和模型表现均从该状态派生。
