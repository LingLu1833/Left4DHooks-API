# Left 4 Dead Hooks

本文档由AI自动生成工具生成。如有任何问题或建议，请参考源码中的详细注释并告知作者进行更新。<br>
Left 4 Dead Hooks 是一个用于 Left 4 Dead 和 Left 4 Dead 2 的 SourceMod 扩展，提供了丰富的接口用于修改和扩展游戏功能。本文档提供了所有可用接口的详细说明。

## 主要钩子接口

以下接口在 `left4dhooks.inc` 中定义，提供了对游戏关键事件的钩子功能：

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_OnGameFrame()` | 无 | 无 | 游戏每一帧调用的钩子 |
| `L4D_OnFirstSurvivorLeftSafeArea_PostHandled()` | client - 第一个离开安全区域的幸存者索引 | 无 | 当L4D_OnFirstSurvivorLeftSafeArea被阻止时调用 |
| `L4D_OnForceSurvivorPositions_Pre()` | 无 | 无 | 幸存者被强制进入起始位置前调用（通常在第一张地图和最终逃脱开始时） |
| `L4D_OnForceSurvivorPositions()` | 无 | 无 | 幸存者被强制进入起始位置时调用（通常在第一张地图和最终逃脱开始时） |
| `L4D_OnReleaseSurvivorPositions()` | 无 | 无 | 幸存者从起始位置被释放时调用（通常在第一张地图和最终逃脱开始时） |
| `L4D_OnSpeakResponseConcept_Pre()` | entity - 说话的实体索引（可能是func_orator） | 无 | 角色使用对话概念前调用 |
| `L4D_OnSpeakResponseConcept_Post()` | entity - 说话的实体索引（可能是func_orator） | 无 | 角色使用对话概念后调用 |
| `L4D_OnGetCrouchTopSpeed()` | target - 目标客户端索引<br>&retVal - 要覆盖的返回值 | Action | 获取玩家最大蹲伏速度时调用 |
| `L4D_OnGetRunTopSpeed()` | target - 目标客户端索引<br>&retVal - 要覆盖的返回值 | Action | 获取玩家最大奔跑速度时调用 |
| `L4D_OnGetWalkTopSpeed()` | target - 目标客户端索引<br>&retVal - 要覆盖的返回值 | Action | 获取玩家最大行走速度时调用 |
| `L4D_OnFirstSurvivorLeftSafeArea()` | client - 第一个离开安全区域的幸存者索引 | Action | 第一个幸存者离开安全区域时调用，可阻止回合开始 |
| `L4D_OnFirstSurvivorLeftSafeArea_Post()` | client - 第一个离开安全区域的幸存者索引 | 无 | 第一个幸存者离开安全区域后的回调 |
| `L4D_OnIncapacitatedSurvivorKilled()` | victim - 受害者索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | 无 | 被击倒的幸存者死亡时调用 |
| `L4D_OnChargerCollide()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger碰撞到幸存者时调用 |
| `L4D_OnChargerGrab()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger抓住幸存者时调用 |
| `L4D_OnChargerReleased()` | charger - Charger索引<br>victim - 受害者索引 | 无 | Charger释放幸存者时调用 |
| `L4D_OnChargerPummel()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger殴打幸存者时调用 |
| `L4D_OnJockeyMount()` | jockey - Jockey索引<br>victim - 受害者索引 | Action | Jockey骑到幸存者身上时调用 |
| `L4D_OnJockeyDismount()` | jockey - Jockey索引<br>victim - 受害者索引 | 无 | Jockey从幸存者身上下来时调用 |
| `L4D_OnSpitterSpit()` | spitter - Spitter索引 | Action | Spitter吐口水时调用 |
| `L4D_OnSurvivorDeathStart()` | victim - 受害者索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | Action | 幸存者开始死亡过程时调用 |
| `L4D_OnSurvivorDeathFinish()` | victim - 受害者索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | 无 | 幸存者死亡过程结束时调用 |
| `L4D_OnSurvivorHurt()` | victim - 受害者索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引<br>&Float:damage - 伤害值<br>&int:damagetype - 伤害类型 | Action | 幸存者受伤时调用 |
| `L4D_OnTankRockThrown()` | tank - Tank索引<br>&entity - 石头实体索引 | Action | Tank扔石头时调用 |
| `L4D_OnTankRockHit()` | tank - Tank索引<br>rock - 石头实体索引<br>hitEnt - 被击中的实体索引<br>&bool:allowDamage - 是否允许伤害 | Action | Tank的石头击中目标时调用 |
| `L4D_OnTryOfferingTankBot()` | survivorCount - 当前幸存者数量<br>botCount - 当前电脑AI数量 | Action | 尝试提供AI Tank时调用，可控制Tank是否使用AI控制 |
| `L4D_OnTryOfferingTankBot_Post()` | survivorCount - 当前幸存者数量<br>botCount - 当前电脑AI数量<br>result - 结果 | 无 | 尝试提供AI Tank后的回调 |
| `L4D_OnCThrowActivate()` | client - 客户端索引<br>&weapon - 近战武器索引 | Action | 近战武器激活时调用 |
| `L4D_OnGetMissionVSBossSpawning_PostHandled()` | mission - 任务索引<br>&numBosses - 要设置的Boss数量 | 无 | 当L4D_OnGetMissionVSBossSpawning被阻止时调用 |
| `L4D_OnReplaceTank()` | tank - Tank实体索引<br>&replacement - 替换Tank类型的实体索引 | Action | 替换Tank时调用 |
| `L4D2_OnSelectTankAttackPre()` | tank - Tank实体索引<br>&attackType - 攻击类型 | Action | Tank选择攻击类型前调用（仅L4D2） |
| `L4D_TankClaw_DoSwing_Pre()` | tank - Tank实体索引<br>&result - 返回值引用（1-成功，0-失败） | Action | Tank挥爪前调用 |
| `L4D_TankClaw_DoSwing_Post()` | tank - Tank实体索引<br>result - 结果（1-成功，0-失败） | 无 | Tank挥爪后调用 |
| `L4D_TankClaw_OnPlayerHit_Pre()` | tank - Tank实体索引<br>victim - 被击中的受害者索引<br>&retVal - 要覆盖的返回值 | Action | Tank爪子击中玩家前调用 |
| `L4D_TankClaw_OnPlayerHit_Post()` | tank - Tank实体索引<br>victim - 被击中的受害者索引<br>retVal - 返回值 | 无 | Tank爪子击中玩家后调用 |
| `L4D_TankClaw_OnPlayerHit_PostHandled()` | tank - Tank实体索引<br>victim - 被击中的受害者索引<br>&retVal - 要覆盖的返回值 | 无 | 当L4D_TankClaw_OnPlayerHit_Pre被阻止时调用 |
| `L4D_TankRock_OnDetonate()` | rock - 岩石实体索引<br>&result - 结果引用（1-成功，0-失败） | Action | Tank岩石爆炸前调用 |
| `L4D_TankRock_OnRelease()` | tank - Tank实体索引<br>rock - 岩石实体索引 | 无 | Tank释放岩石时调用 |
| `L4D_TankRock_BounceTouch()` | rock - 岩石实体索引<br>entity - 接触实体索引<br>&result - 结果引用（1-成功，0-失败） | Action | Tank岩石碰撞时调用 |
| `L4D_OnGetScriptValueInt()` | key - 脚本键名<br>&retVal - 要覆盖的返回值 | Action | 获取脚本整数值时调用（L4D2专用） |
| `L4D_OnGetScriptValueString()` | key - 脚本键名<br>defaultVal - 默认返回值<br>retVal[128] - 返回的字符串 | Action | 获取脚本字符串值时调用（L4D2专用） |
| `L4D2_OnGetScriptValueVector()` | key - 脚本键名<br>retVal[3] - 要覆盖的返回值<br>hScope - 脚本范围句柄 | Action | 获取脚本向量值时调用（L4D2专用） |
| `L4D_OnHasConfigurableDifficulty()` | &retVal - 要覆盖的返回值（1-允许难度配置，0-拒绝） | Action | 检查是否允许难度配置时调用（L4D2专用） |
| `L4D_OnHasConfigurableDifficulty_Post()` | retVal - 返回值 | 无 | 检查是否允许难度配置后的回调（L4D2专用） |
| `L4D_OnGetSurvivorSet()` | &retVal - 要覆盖的返回值 | Action | 获取幸存者角色集时调用（L4D2专用） |
| `L4D_OnTryOfferingTankBot()` | tank_index - Tank客户端索引<br>&enterStasis - Tank是否处于停滞状态 | Action | 尝试提供Tank机器人时调用，用于显示"X获得Tank"窗口和转移Tank控制 |
| `L4D_OnWitchKilled()` | witch - Witch索引<br>killer - 杀手索引<br>inflictor - 伤害来源索引 | 无 | Witch被杀死时调用 |
| `L4D_OnWitchAttack()` | witch - Witch索引<br>victim - 受害者索引 | Action | Witch攻击时调用 |
| `L4D_OnWitchFlinch()` | witch - Witch索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | Action | Witch被击中退缩时调用 |
| `L4D_OnWitchIgnite()` | witch - Witch索引 | 无 | Witch被点燃时调用 |
| `L4D_OnWitchRespawn()` | witch - Witch索引 | 无 | Witch重生时调用 |
| `L4D_OnWitchStunned()` | witch - Witch索引 | 无 | Witch被击晕时调用 |
| `L4D2_OnChangeFinaleStage()` | stage - 终局阶段<br>&newStage - 新的终局阶段 | Action | 终局阶段变更时调用（仅L4D2） |
| `L4D2_OnEndVersusModeRound()` | &bWin - 是否胜利<br>&bIsSurvivorTeam - 是否为幸存者队伍 | Action | 对抗模式回合结束时调用（仅L4D2） |
| `L4D_OnLedgeGrabbed()` | client - 客户端索引<br>&ledgetype - 边缘类型 | Action | 玩家抓住边缘时调用 |
| `L4D2_OnRevived()` | client - 被复活的客户端索引<br>reviver - 复活者客户端索引 | 无 | 玩家被复活时调用（仅L4D2） |
| `L4D_OnSwingStart()` | client - 客户端索引<br>weapon - 武器索引<br>&swingtype - 挥砍类型 | Action | 玩家开始挥砍时调用 |
| `L4D_OnShovedBySurvivor()` | victim - 受害者客户端索引<br>attacker - 攻击者客户端索引<br>&result - 结果 | Action | 玩家被其他幸存者推搡时调用 |
| `L4D2_OnEntityShoved()` | victim - 受害者实体索引<br>attacker - 攻击者实体索引<br>&result - 结果 | Action | 实体被推搡时调用（仅L4D2） |
| `L4D2_OnEntityShoved_Post()` | victim - 受害者实体索引<br>attacker - 攻击者实体索引<br>result - 结果 | 无 | 实体被推搡后的回调（仅L4D2） |
| `L4D2_OnEntityShoved_PostHandled()` | victim - 受害者实体索引<br>attacker - 攻击者实体索引<br>&result - 结果 | 无 | 实体被推搡被阻止时的回调（仅L4D2） |
| `L4D2_OnStagger()` | client - 客户端索引<br>attacker - 攻击者索引<br>&result - 结果 | Action | 玩家进入stagger状态时调用（仅L4D2） |
| `L4D2_OnStagger_Post()` | client - 客户端索引<br>attacker - 攻击者索引<br>result - 结果 | 无 | 玩家进入stagger状态后的回调（仅L4D2） |
| `L4D2_OnStagger_PostHandled()` | client - 客户端索引<br>attacker - 攻击者索引<br>&result - 结果 | 无 | 玩家进入stagger状态被阻止时的回调（仅L4D2） |
| `L4D_OnCancelStagger()` | client - 客户端索引<br>&result - 结果 | Action | 取消stagger状态时调用 |
| `L4D_OnCancelStagger_Post()` | client - 客户端索引<br>result - 结果 | 无 | 取消stagger状态后的回调 |
| `L4D_OnCancelStagger_PostHandled()` | client - 客户端索引<br>&result - 结果 | 无 | 取消stagger状态被阻止时的回调 |
| `L4D2_OnPlayerFling()` | client - 客户端索引<br>attacker - 攻击者索引<br>vecDir[3] - 方向向量 | Action | 玩家被击飞时调用（仅L4D2） |
| `L4D2_OnPlayerFling_Post()` | client - 客户端索引<br>attacker - 攻击者索引<br>vecDir[3] - 方向向量 | 无 | 玩家被击飞后的回调（仅L4D2） |
| `L4D_OnMotionControlledXY()` | client - 客户端索引<br>&vecMotion[2] - 运动向量<br>flFrameTime - 帧时间 | Action | 当运动控制器改变玩家移动时调用 |
| `L4D2_OnPounceOrLeapStumble()` | client - 客户端索引<br>attacker - 攻击者索引<br>&result - 结果 | Action | 玩家在被扑或跳跃时摇晃时调用（仅L4D2） |
| `L4D_OnPlayerCough_PostHandled()` | client - 客户端索引 | 无 | 玩家咳嗽后被阻止时的回调 |
| `L4D_OnIncapacitated()` | client - 客户端索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | Action | 玩家被击倒时调用 |
| `L4D_OnIncapacitated_Post()` | client - 客户端索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | 无 | 玩家被击倒后的回调 |
| `L4D_OnIncapacitated_PostHandled()` | client - 客户端索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | 无 | 玩家被击倒被阻止时的回调 |
| `L4D_OnDeathDroppedWeapons()` | victim - 受害者索引<br>bool:primary - 是否为主武器<br>bool:secondary - 是否为副武器 | 无 | 玩家死亡掉落武器时调用 |
| `L4D2_OnSpitSpread()` | spitter - Spitter索引<br>spitEntity - 口水实体索引 | 无 | Spitter口水扩散时调用（仅L4D2） |
| `L4D_PlayerExtinguish()` | client - 客户端索引<br>attacker - 攻击者索引 | 无 | 玩家被扑灭时调用 |
| `L4D2_OnUseHealingItems()` | client - 客户端索引<br>target - 目标索引<br>&weapon - 武器索引 | Action | 玩家使用医疗物品时调用（仅L4D2） |
| `L4D2_OnFindScavengeItem()` | client - 客户端索引<br>item - 物品实体索引 | 无 | 玩家找到补给物品时调用（仅L4D2） |
| `L4D2_OnChooseVictim()` | specialInfected - 特感索引<br>&victim - 目标幸存者索引 | Action | 特感选择受害者时调用（仅L4D2） |
| `L4D2_OnChooseVictim_Post()` | specialInfected - 特感索引<br>victim - 目标幸存者索引 | 无 | 特感选择受害者后的回调（仅L4D2） |
| `L4D2_OnChooseVictim_PostHandled()` | specialInfected - 特感索引<br>&victim - 目标幸存者索引 | 无 | 特感选择受害者被阻止时的回调（仅L4D2） |
| `L4D_OnPouncedOnSurvivor()` | pouncer - 扑击者索引<br>victim - 受害者索引 | Action | 特感扑到幸存者时调用 |
| `L4D_OnPouncedOnSurvivor_Post()` | pouncer - 扑击者索引<br>victim - 受害者索引 | 无 | 特感扑到幸存者后的回调 |
| `L4D_OnPouncedOnSurvivor_PostHandled()` | pouncer - 扑击者索引<br>victim - 受害者索引 | 无 | 特感扑到幸存者被阻止时的回调 |
| `L4D_OnGrabWithTongue()` | smoker - Smoker索引<br>victim - 受害者索引<br>vecDir[3] - 方向向量 | Action | Smoker用舌头抓住幸存者时调用 |
| `L4D_OnGrabWithTongue_Post()` | smoker - Smoker索引<br>victim - 受害者索引<br>vecDir[3] - 方向向量 | 无 | Smoker用舌头抓住幸存者后的回调 |
| `L4D_OnGrabWithTongue_PostHandled()` | smoker - Smoker索引<br>victim - 受害者索引<br>vecDir[3] - 方向向量 | 无 | Smoker用舌头抓住幸存者被阻止时的回调 |
| `L4D2_OnStartCarryingVictim()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger开始携带受害者时调用（仅L4D2） |
| `L4D2_OnStartCarryingVictim_Post()` | charger - Charger索引<br>victim - 受害者索引 | 无 | Charger开始携带受害者后的回调（仅L4D2） |
| `L4D2_OnStartCarryingVictim_PostHandled()` | charger - Charger索引<br>victim - 受害者索引 | 无 | Charger开始携带受害者被阻止时的回调（仅L4D2） |
| `L4D2_OnChargerImpact()` | client - Charg索引 | 无 | Charger撞击墙壁或物体后调用（仅L4D2） |
| `L4D2_OnPummelVictim()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger开始殴打受害者时调用（仅L4D2） |
| `L4D2_OnPummelVictim_Post()` | charger - Charger索引<br>victim - 受害者索引 | 无 | Charger开始殴打受害者后的回调（仅L4D2） |
| `L4D2_OnPummelVictim_PostHandled()` | charger - Charger索引<br>victim - 受害者索引 | 无 | Charger开始殴打受害者被阻止时的回调（仅L4D2） |
| `L4D_OnIsDominatedBySpecialInfected()` | victim - 受害者索引<br>dominator - 控制者索引 | 无 | 玩家被特感控制时调用（Hunter、Smoker、Jockey、Charger） |
| `L4D_OnVomitedUpon()` | victim - 受害者索引<br>attacker - Boomer索引 | Action | 幸存者被Boomer胆汁喷到时调用 |
| `L4D_OnVomitedUpon_Post()` | victim - 受害者索引<br>attacker - Boomer索引 | 无 | 幸存者被Boomer胆汁喷到后的回调 |
| `L4D_OnVomitedUpon_PostHandled()` | victim - 受害者索引<br>attacker - Boomer索引 | 无 | 幸存者被Boomer胆汁喷到被阻止时的回调 |
| `L4D2_OnJockeyRide()` | jockey - Jockey索引<br>victim - 受害者索引<br>&vecDir[3] - 方向向量 | Action | Jockey控制幸存者移动时调用（仅L4D2） |
| `L4D2_OnJockeyRide_Post()` | jockey - Jockey索引<br>victim - 受害者索引<br>vecDir[3] - 方向向量 | 无 | Jockey控制幸存者移动后的回调（仅L4D2） |
| `L4D2_OnJockeyRide_PostHandled()` | jockey - Jockey索引<br>victim - 受害者索引<br>&vecDir[3] - 方向向量 | 无 | Jockey控制幸存者移动被阻止时的回调（仅L4D2） |
| `L4D2_OnSlammedSurvivor()` | charger - Charger索引<br>victim - 受害者索引<br>vecDir[3] - 方向向量<br>&bool:wall - 是否撞到墙<br>&bool:ground - 是否撞到地面 | Action | Charger将幸存者撞到墙上或地面时调用（仅L4D2） |
| `L4D2_OnSlammedSurvivor_Post()` | charger - Charger索引<br>victim - 受害者索引<br>vecDir[3] - 方向向量<br>bool:wall - 是否撞到墙<br>bool:ground - 是否撞到地面 | 无 | Charger将幸存者撞到墙上或地面后的回调（仅L4D2） |
| `L4D2_OnSlammedSurvivor_PostHandled()` | charger - Charger索引<br>victim - 受害者索引<br>vecDir[3] - 方向向量<br>&bool:wall - 是否撞到墙<br>&bool:ground - 是否撞到地面 | 无 | Charger将幸存者撞到墙上或地面被阻止时的回调（仅L4D2） |
| `L4D_OnSpawnSpecial()` | &zombieClass - 特感类型<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | Action | 特感（Bot）生成前调用 |
| `L4D_OnSpawnSpecial_Post()` | client - 生成的客户端索引<br>zombieClass - 特感<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | 特感生成后的回调 |
| `L4D_OnSpawnSpecial_PostHandled()` | client - 生成的客户端索引<br>zombieClass - 特感<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | 特感生成被阻止时的回调 |
| `L4D_OnSpawnTank()` | vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | Action | Tank生成前调用 |
| `L4D_OnSpawnTank_Post()` | client - 生成的客户端索引<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | Tank生成后的回调 |
| `L4D_OnSpawnTank_PostHandled()` | client - 生成的客户端索引<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | Tank生成被阻止时的回调 |
| `L4D_OnSpawnWitch()` | vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | Action | Witch生成前调用 |
| `L4D_OnSpawnWitch_Post()` | entity - 生成的实体索引<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | Witch生成后的回调 |
| `L4D_OnSpawnWitch_PostHandled()` | entity - 生成的实体索引<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | Witch生成被阻止时的回调 |
| `L4D2_OnSpawnWitchBride()` | vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | Action | Witch Bride生成前调用（仅L4D2） |
| `L4D2_OnSpawnWitchBride_Post()` | entity - 生成的实体索引<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | Witch Bride生成后的回调（仅L4D2） |
| `L4D2_OnSpawnWitchBride_PostHandled()` | entity - 生成的实体索引<br>vecPos[3] - 生成位置<br>vecAng[3] - 朝向 | 无 | Witch Bride生成被阻止时的回调（仅L4D2） |
| `L4D_OnMobRushStart()` | 无 | Action | 尸潮开始前调用 |
| `L4D_OnMobRushStart_Post()` | 无 | 无 | 尸潮开始后的回调 |
| `L4D_OnMobRushStart_PostHandled()` | 无 | 无 | 尸潮开始被阻止时的回调 |
| `L4D_OnSpawnITMob()` | &amount - 僵尸数量 | Action | Boomer尸潮生成前调用 |
| `L4D_OnSpawnITMob_Post()` | amount - 僵尸数量 | 无 | Boomer尸潮生成后的回调 |
| `L4D_OnSpawnITMob_PostHandled()` | amount - 僵尸数量 | 无 | Boomer尸潮生成被阻止时的回调 |
| `L4D_OnSpawnMob()` | &amount - 僵尸数量 | Action | 普通尸潮生成前调用 |
| `L4D_OnSpawnMob_Post()` | amount - 僵尸数量 | 无 | 普通尸潮生成后的回调 |
| `L4D_OnSpawnMob_PostHandled()` | amount - 僵尸数量 | 无 | 普通尸潮生成被阻止时的回调 |
| `L4D_OnWitchSetHarasser()` | witch - Witch实体索引<br>victim - 骚扰者客户端索引 | 无 | Witch被骚扰时调用 |
| `L4D2_VomitJar_Detonate_Post()` | entity - 胆汁瓶实体索引 | 无 | 胆汁瓶引爆后的回调（仅L4D2） |
| `L4D2_GrenadeLauncher_Detonate()` | entity - 榴弹发射器实体索引 | Action | 榴弹发射器引爆前调用（仅L4D2） |
| `L4D_CBreakableProp_Break()` | prop - 可破坏物体实体索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | Action | 可破坏物体被破坏时调用 |
| `L4D1_FirstAidKit_StartHealing()` | healer - 治疗者客户端索引<br>patient - 被治疗者客户端索引 | Action | 使用急救包开始治疗时调用（仅L4D1） |
| `L4D1_FirstAidKit_FinishedHealing()` | healer - 治疗者客户端索引<br>patient - 被治疗者客户端索引 | 无 | 使用急救包完成治疗时调用（仅L4D1） |
| `L4D1_FirstAidKit_CancelHealing()` | healer - 治疗者客户端索引<br>patient - 被治疗者客户端索引 | 无 | 取消使用急救包治疗时调用（仅L4D1） |
| `L4D2_OnStartUseAction_PostHandled()` | client - 客户端索引<br>entity - 使用的实体索引<br>useType - 使用类型 | 无 | 当L4D2_OnStartUseAction被阻止时调用（仅L4D2） |
| `L4D2_BackpackItem_StartAction()` | client - 客户端索引<br>item - 背包物品索引<br>ActionType - 动作类型 | Action | 开始使用背包物品动作时调用（仅L4D2） |
| `L4D2_BackpackItem_FinishedAction()` | client - 客户端索引<br>item - 背包物品索引<br>ActionType - 动作类型 | 无 | 完成使用背包物品动作时调用（仅L4D2） |
| `L4D2_BackpackItem_CancelAction()` | client - 客户端索引<br>item - 背包物品索引<br>ActionType - 动作类型 | 无 | 取消使用背包物品动作时调用（仅L4D2） |
| `L4D2_CGasCan_EventKilled()` | entity - 油桶实体索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引<br>bool:aleardyDead - 是否已死亡 | Action | 油桶被摧毁时调用（仅L4D2） |
| `L4D2_CGasCan_EventKilled_Post()` | entity - 油桶实体索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引<br>bool:aleardyDead - 是否已死亡 | 无 | 油桶被摧毁后的回调（仅L4D2） |
| `L4D2_CGasCan_EventKilled_PostHandled()` | entity - 油桶实体索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引<br>bool:aleardyDead - 是否已死亡 | 无 | 当L4D2_CGasCan_EventKilled被阻止时调用（仅L4D2） |
| `L4D_OnGameModeChange()` | newMode - 新模式索引 | 无 | 游戏模式改变时调用 |
| `L4D_OnServerHibernationUpdate()` | bool:inHibernation - 是否处于休眠状态 | 无 | 服务器休眠状态更新时调用 |
| `L4D_OnSavingEntities()` | info_changelevel - 变更级别信息 | Action | 服务器保存实体时调用 |
| `L4D_OnSavingEntities_Post()` | info_changelevel - 变更级别信息 | 无 | 服务器保存实体后的回调 |
| `L4D_OnSavingEntities_PostHandled()` | info_changelevel - 变更级别信息 | 无 | 当L4D_OnSavingEntities被阻止时调用 |
| `L4D2_OnSavingEntities()` | info_changelevel - 变更级别信息 | Action | 服务器保存实体时调用（仅L4D2） |
| `L4D2_OnSavingEntities_Post()` | info_changelevel - 变更级别信息 | 无 | 服务器保存实体后的回调（仅L4D2） |
| `L4D2_OnSavingEntities_PostHandled()` | info_changelevel - 变更级别信息 | 无 | 当L4D2_OnSavingEntities被阻止时调用（仅L4D2） |
| `L4D_OnEnterStasis()` | tank - Tank客户端索引 | 无 | Tank进入停滞状态时调用 |
| `L4D_OnLeaveStasis()` | tank - Tank客户端索引 | 无 | Tank离开停滞状态时调用 |
| `L4D_OnEnterGhostStatePre()` | client - 客户端索引 | Action | 玩家进入幽灵状态前调用 |
| `L4D_OnEnterGhostState()` | client - 客户端索引 | 无 | 玩家进入幽灵状态后的回调 |
| `L4D_OnEnterGhostState_PostHandled()` | client - 客户端索引 | 无 | 玩家进入幽灵状态被阻止时的回调 |
| `L4D_OnTakeOverBot()` | client - 客户端索引 | Action | 玩家接管Bot前调用 |
| `L4D_OnTakeOverBot_Post()` | client - 客户端索引<br>success - 是否成功 | 无 | 玩家接管Bot后的回调 |
| `L4D_OnTakeOverBot_PostHandled()` | client - 客户端索引<br>success - 是否成功 | 无 | 玩家接管Bot被阻止时的回调 |
| `L4D_OnMaterializeFromGhostPre()` | client - 客户端索引 | Action | 玩家从幽灵状态实体化前调用 |
| `L4D_OnMaterializeFromGhost()` | client - 客户端索引 | 无 | 玩家从幽灵状态实体化后的回调 |
| `L4D_OnMaterializeFromGhost_PostHandled()` | client - 客户端索引 | 无 | 玩家从幽灵状态实体化被阻止时的回调 |
| `L4D_OnFinishIntro()` | 无 | 无 | 开场动画结束时调用 |
| `L4D_OnIsTeamFull()` | team - 队伍ID<br>&full - 是否已满 | Action | 检查队伍是否满员时调用 |
| `L4D_OnClearTeamScores()` | newCampaign - 是否新战役 | Action | 清除队伍分数前调用 |
| `L4D_OnSetCampaignScores()` | &scoreA - 队伍A分数<br>&scoreB - 队伍B分数 | Action | 设置战役分数前调用 |
| `L4D_OnSetCampaignScores_Post()` | scoreA - 队伍A分数<br>scoreB - 队伍B分数 | 无 | 设置战役分数后的回调 |
| `L4D_OnRecalculateVersusScore()` | client - 客户端索引 | Action | 重新计算对抗分数前调用（仅L4D1） |
| `L4D_OnRecalculateVersusScore_Post()` | client - 客户端索引 | 无 | 重新计算对抗分数后的回调（仅L4D1） |
| `L4D_OnGameFrame()` | 无 | 无 | 游戏每一帧调用的钩子 |
| `L4D_OnFirstSurvivorLeftSafeArea_PostHandled()` | client - 第一个离开安全区域的幸存者索引 | 无 | 当L4D_OnFirstSurvivorLeftSafeArea被阻止时调用 |
| `L4D_OnForceSurvivorPositions_Pre()` | 无 | 无 | 幸存者被强制进入起始位置前调用（通常在第一张地图和最终逃脱开始时） |
| `L4D_OnForceSurvivorPositions()` | 无 | 无 | 幸存者被强制进入起始位置时调用（通常在第一张地图和最终逃脱开始时） |
| `L4D_OnReleaseSurvivorPositions()` | 无 | 无 | 幸存者从起始位置被释放时调用（通常在第一张地图和最终逃脱开始时） |
| `L4D_OnSpeakResponseConcept_Pre()` | entity - 说话的实体索引（可能是func_orator） | 无 | 角色使用对话概念前调用 |
| `L4D_OnSpeakResponseConcept_Post()` | entity - 说话的实体索引（可能是func_orator） | 无 | 角色使用对话概念后调用 |
| `L4D_OnGetCrouchTopSpeed()` | target - 目标客户端索引<br>&retVal - 要覆盖的返回值 | Action | 获取玩家最大蹲伏速度时调用 |
| `L4D_OnGetRunTopSpeed()` | target - 目标客户端索引<br>&retVal - 要覆盖的返回值 | Action | 获取玩家最大奔跑速度时调用 |
| `L4D_OnGetWalkTopSpeed()` | target - 目标客户端索引<br>&retVal - 要覆盖的返回值 | Action | 获取玩家最大行走速度时调用 |
| `L4D_OnFirstSurvivorLeftSafeArea()` | client - 第一个离开安全区域的幸存者索引 | Action | 第一个幸存者离开安全区域时调用，可阻止回合开始 |
| `L4D_OnFirstSurvivorLeftSafeArea_Post()` | client - 第一个离开安全区域的幸存者索引 | 无 | 第一个幸存者离开安全区域后的回调 |
| `L4D_OnIncapacitatedSurvivorKilled()` | victim - 受害者索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引 | 无 | 被击倒的幸存者死亡时调用 |
| `L4D_OnChargerCollide()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger碰撞到幸存者时调用 |
| `L4D_OnChargerGrab()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger抓住幸存者时调用 |
| `L4D_OnChargerReleased()` | charger - Charger索引<br>victim - 受害者索引 | 无 | Charger释放幸存者时调用 |
| `L4D_OnChargerPummel()` | charger - Charger索引<br>victim - 受害者索引 | Action | Charger殴打幸存者时调用 |
| `L4D_OnJockeyMount()` | jockey - Jockey索引<br>victim - 受害者索引 | Action | Jockey骑到幸存者身上时调用 |
| `L4D_OnJockeyDismount()` | jockey - Jockey索引<br>victim - 受害者索引 | 无 | Jockey从幸存者身上下来时调用 |
| `L4D_OnSpitterSpit()` | spitter - Spitter索引 | Action | Spitter吐口水时调用 |
| `L4D2_OnTransitionRestore()` | client - 客户端索引 | Action | 玩家数据恢复前调用（仅L4D2） |
| `L4D2_OnTransitionRestore_Post()` | client - 客户端索引<br>pkv - keyvalues指针地址 | 无 | 玩家数据恢复后的回调（仅L4D2） |
| `L4D2_OnTransitionRestore_PostHandled()` | client - 客户端索引<br>pkv - keyvalues指针地址 | 无 | 玩家数据恢复被阻止时的回调（仅L4D2） |
| `L4D2_OnRestoreTransitionedSurvivorBots()` | 无 | Action | 幸存者机器人数据恢复前调用（仅L4D2） |
| `L4D2_OnRestoreTransitionedSurvivorBots_Post()` | 无 | 无 | 幸存者机器人数据恢复后的回调（仅L4D2） |
| `L4D2_OnRestoreTransitionedSurvivorBots_PostHandled()` | 无 | 无 | 幸存者机器人数据恢复被阻止时的回调（仅L4D2） |
| `L4D2_OnClientDisableAddons()` | SteamID - 客户端SteamID | Action | 客户端材质系统期望服务器指令时调用（仅L4D2） |
| `PlayerAnimState_MarkNativeAsOptional()` | 无 | void | 将PlayerAnimState相关的原生函数标记为可选 |
| `Ammo_t_MarkNativeAsOptional()` | 无 | void | 将Ammo_t相关的原生函数标记为可选 |
| `AmmoDef_MarkNativeAsOptional()` | 无 | void | 将AmmoDef相关的原生函数标记为可选 |
| `IsValidSurvivorBot()` | client - 客户端索引 | bool | 检查客户端是否是有效的幸存者机器人 |
| `IsValidSpecialInfectedBot()` | client - 客户端索引 | bool | 检查客户端是否是有效的特感机器人 |
| `IsValidSurvivor()` | client - 客户端索引 | bool | 检查客户端是否是有效的幸存者玩家 |
| `IsValidInfected()` | client - 客户端索引 | bool | 检查客户端是否是有效的感染者玩家 |
| `IsPlayerInFirstPerson()` | client - 客户端索引 | bool | 检查玩家是否在第一人称视角 |
| `GetWeaponTypeFromWeaponIndex()` | weaponIndex - 武器索引 | WeaponType | 根据武器索引获取武器类型 |
| `GetWeaponTypeFromWeaponName()` | weaponName - 武器名称 | WeaponType | 根据武器名称获取武器类型 |
| `L4D_GetTankBossZombieCount()` | 无 | int | 获取当前游戏中的Tank和Boss数量 |
| `L4D_GetMissionVersusBossLimit()` | mission - 任务索引 | int | 获取特定任务的Boss限制数量 |
| `L4D2_GetWeaponClassname()` | type - WeaponType | char[] | 从WeaponType值返回武器类名（仅L4D2） |
| `IsValidSurvivorBot()` | client - 客户端索引 | bool | 检查客户端是否为有效的幸存者机器人 |
| `IsValidSurvivor()` | client - 客户端索引 | bool | 检查客户端是否为有效的幸存者（玩家或机器人） |
| `IsValidInfected()` | client - 客户端索引 | bool | 检查客户端是否为有效的感染者 |
| `IsValidSpecialInfected()` | client - 客户端索引 | bool | 检查客户端是否为有效的特感 |
| `IsValidTank()` | client - 客户端索引 | bool | 检查客户端是否为有效的Tank |
| `L4D_GetTankBossZombieCount()` | 无 | int | 返回当前Tank的数量 |
| `L4D_GetSpecialsBossZombieCount()` | 无 | int | 返回当前特感的数量 |
| `L4D_GetTotalBossZombieCount()` | 无 | int | 返回总特感和Tank的数量 |
| `L4D_GetSurvivorCount()` | 无 | int | 返回存活的幸存者数量 |
| `L4D_GetInfectedCount()` | 无 | int | 返回存活的感染者数量 |
| `L4D2_GetTeamScore()` | team - 队伍编号 | int | 获取指定队伍的分数（仅L4D2） |
| `L4D2_SetTeamScore()` | team - 队伍编号<br>score - 新的分数 | void | 设置指定队伍的分数（仅L4D2） |
| `L4D2_IncreaseTeamScore()` | team - 队伍编号<br>score - 增加的分数 | void | 增加指定队伍的分数（仅L4D2） |
| `L4D2_RefreshScoreboard()` | 无 | void | 刷新记分板（仅L4D2） |
| `L4D_MolotovProjectile_Pre()` | &entity - 燃烧瓶实体索引 | Action | 燃烧瓶投射物创建前调用 |
| `L4D_MolotovProjectile_Post()` | entity - 燃烧瓶实体索引 | 无 | 燃烧瓶投射物创建后的回调 |
| `L4D_PipeBombProjectile_Pre()` | &entity - 破片手雷实体索引 | Action | 破片手雷投射物创建前调用 |
| `L4D_PipeBombProjectile_Post()` | entity - 破片手雷实体索引 | 无 | 破片手雷投射物创建后的回调 |
| `L4D2_VomitJarProjectile_Pre()` | &entity - 胆汁瓶实体索引 | Action | 胆汁瓶投射物创建前调用（仅L4D2） |
| `L4D2_VomitJarProjectile_Post()` | entity - 胆汁瓶实体索引 | 无 | 胆汁瓶投射物创建后的回调（仅L4D2） |
| `L4D2_GrenadeLauncherProjectile_Pre()` | &entity - 榴弹发射器实体索引 | Action | 榴弹发射器投射物创建前调用（仅L4D2） |
| `L4D2_GrenadeLauncherProjectile_Post()` | entity - 榴弹发射器实体索引 | 无 | 榴弹发射器投射物创建后的回调（仅L4D2） |
| `L4D_Molotov_Detonate()` | entity - 燃烧瓶实体索引 | Action | 燃烧瓶引爆前调用 |
| `L4D_Molotov_Detonate_Post()` | entity - 燃烧瓶实体索引 | 无 | 燃烧瓶引爆后的回调 |
| `L4D_PipeBomb_Detonate()` | entity - 破片手雷实体索引 | Action | 破片手雷引爆前调用 |
| `L4D_PipeBomb_Detonate_Post()` | entity - 破片手雷实体索引 | 无 | 破片手雷引爆后的回调 |
| `L4D2_VomitJar_Detonate()` | entity - 胆汁瓶实体索引 | Action | 胆汁瓶引爆前调用（仅L4D2） |
| `L4D2_VomitJar_Detonate_Post()` | entity - 胆汁瓶实体索引 | 无 | 胆汁瓶引爆后的回调（仅L4D2） |
`L4D2_CGasCan_EventKilled()` | entity - 油桶实体索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引<br>bool:aleardyDead - 是否已死亡 | Action | 油桶被摧毁前调用（仅L4D2） |
| `L4D2_CGasCan_EventKilled_Post()` | entity - 油桶实体索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引<br>bool:aleardyDead - 是否已死亡 | 无 | 油桶被摧毁后的回调（仅L4D2） |
| `L4D2_CGasCan_EventKilled_PostHandled()` | entity - 油桶实体索引<br>attacker - 攻击者索引<br>inflictor - 伤害来源索引<br>bool:aleardyDead - 是否已死亡 | 无 | 当L4D2_CGasCan_EventKilled被阻止时调用（仅L4D2） |
| `L4D_OnGameModeChange()` | newMode - 新模式索引 | 无 | 游戏模式改变时调用 |
| `L4D_OnServerHibernationUpdate()` | bool:inHibernation - 是否处于休眠状态 | 无 | 服务器休眠状态更新时调用 |
| `L4D_OnSavingEntities()` | info_changelevel - 变更级别信息 | Action | 服务器保存实体时调用 |
| `L4D_OnSavingEntities_Post()` | info_changelevel - 变更级别信息 | 无 | 服务器保存实体后的回调 |
| `L4D_OnSavingEntities_PostHandled()` | info_changelevel - 变更级别信息 | 无 | 当L4D_OnSavingEntities被阻止时调用 |
| `L4D2_OnSavingEntities()` | info_changelevel - 变更级别信息 | Action | 服务器保存实体时调用（仅L4D2） |
| `L4D2_OnSavingEntities_Post()` | info_changelevel - 变更级别信息 | 无 | 服务器保存实体后的回调（仅L4D2） |
| `L4D2_OnSavingEntities_PostHandled()` | info_changelevel - 变更级别信息 | 无 | 当L4D2_OnSavingEntities被阻止时调用（仅L4D2） |
| `L4D_OnEnterStasis()` | tank - Tank客户端索引 | 无 | Tank进入停滞状态时调用 |
| `L4D_OnLeaveStasis()` | tank - Tank客户端索引 | 无 | Tank离开停滞状态时调用 |
| `L4D_OnEnterGhostStatePre()` | client - 客户端索引 | Action | 玩家进入幽灵状态前调用 |
| `L4D_OnEnterGhostState()` | client - 客户端索引 | 无 | 玩家进入幽灵状态后的回调 |
| `L4D_OnEnterGhostState_PostHandled()` | client - 客户端索引 | 无 | 玩家进入幽灵状态被阻止时的回调 |
| `L4D_OnTakeOverBot()` | client - 客户端索引 | Action | 玩家接管Bot前调用 |
| `L4D_OnTakeOverBot_Post()` | client - 客户端索引<br>success - 是否成功 | 无 | 玩家接管Bot后的回调 |
| `L4D_OnTakeOverBot_PostHandled()` | client - 客户端索引<br>success - 是否成功 | 无 | 玩家接管Bot被阻止时的回调 |
| `L4D_OnMaterializeFromGhostPre()` | client - 客户端索引 | Action | 玩家从幽灵状态实体化前调用 |
| `L4D_OnMaterializeFromGhost()` | client - 客户端索引 | 无 | 玩家从幽灵状态实体化后的回调 |
| `L4D_OnMaterializeFromGhost_PostHandled()` | client - 客户端索引 | 无 | 玩家从幽灵状态实体化被阻止时的回调 |
| `L4D_OnFinishIntro()` | 无 | 无 | 开场动画结束时调用 |
| `AnimHookEnable` | client - 要钩子的客户端<br>callback - 前钩子回调函数（使用"ACT_*"活动编号）或INVALID_FUNCTION<br>callbackPost - 后钩子回调函数（使用"m_nSequence"序列编号）或INVALID_FUNCTION | bool | 添加客户端动画钩子，所有钩子在地图更改时移除 |
| `AnimHookDisable` | client - 要移除钩子的客户端<br>callback - 前钩子回调函数或INVALID_FUNCTION<br>callbackPost - 后钩子回调函数或INVALID_FUNCTION | bool | 移除客户端动画钩子 |
| `AnimGetActivity` | sequence - 要检索的活动编号<br>activity - 存储活动的目标字符串<br>maxlength - 目标字符串的大小 | bool | 从相对活动编号中检索活动字符串 |
| `AnimGetFromActivity` | activity - 要检索的活动字符串 | int | 从活动字符串中检索动画活动编号，失败返回-1 |
| `L4D_GetPointer()` | ptr_type - 指针类型枚举 | Address | 返回各种内部游戏对象的地址指针 |
| `L4D_GetClientFromAddress()` | addy - 内存地址 | int | 从内存地址返回客户端索引 |
| `L4D_GetEntityFromAddress()` | addy - 内存地址 | int | 从内存地址返回实体索引 |
| `L4D_ReadMemoryString()` | addy - 内存地址<br>buffer - 缓冲区<br>maxlength - 最大长度 | int | 从内存地址读取字符串 |
| `L4D_WriteMemoryString()` | addy - 内存地址<br>buffer - 要写入的字符串 | void | 向内存地址写入字符串 |
| `L4D_PrecacheParticle()` | sEffectName - 粒子效果名称 | void | 预加载粒子效果 |
| `L4D_RemoveEntityDelay()` | entity - 要删除的实体<br>time - 延迟时间<br>user - 用户输入/输出编号(1-4) | void | 在指定时间后删除实体 |
| `L4D_Dissolve()` | entity - 要溶解的实体 | int | 在实体上创建溶解效果 |
| `L4D_GetEntityWorldSpaceCenter()` | entity - 实体索引<br>vecPos - 返回世界坐标中心的向量 | void | 返回实体的世界坐标中心 |
| `L4D_AngularVelocity()` | entity - 实体索引<br>vecAng - 角速度向量 | void | 设置物理实体的角速度向量 |
| `L4D_GetServerOS()` | 无 | int | 返回服务器操作系统(0=Windows, 1=Linux) |
| `Left4DHooks_Version()` | 无 | int | 返回Left4DHooks版本号 |
| `L4D_HasMapStarted()` | 无 | bool | 检查地图和地址是否已加载 |
| `L4D_GetGameModeType()` | 无 | int | 返回当前游戏模式类型 |
| `L4D_Deafen()` | client - 客户端索引 | void | 使玩家短暂失聪（高音调耳鸣声） |
| `L4D_GetTempHealth()` | client - 客户端索引 | float | 返回幸存者当前的临时生命值 |
| `L4D_SetTempHealth()` | client - 客户端索引<br>health - 要设置的生命值 | void | 设置幸存者的临时生命值 |
| `L4D_GetReserveAmmo()` | client - 客户端索引<br>weapon - 武器实体索引 | int | 返回玩家武器的备用弹药 |
| `L4D_SetReserveAmmo()` | client - 客户端索引<br>weapon - 武器实体索引<br>ammo - 要设置的备用弹药 | void | 设置玩家武器的备用弹药 |
| `L4D_PlayMusic()` | client - 客户端索引<br>music_str - 音乐字符串名称<br>source_ent - 音源实体<br>one_float - 未知参数<br>one_bool - 未知参数<br>two_bool - 未知参数 | void | 播放指定的音乐 |
| `L4D_StopMusic()` | client - 客户端索引<br>music_str - 音乐字符串名称<br>one_float - 未知参数<br>one_bool - 未知参数 | void | 停止播放指定的音乐 |
| `L4D_OnITExpired()` | client - 客户端索引 | void | 移除玩家身上的Boomer呕吐效果 |
| `L4D_EstimateFallingDamage()` | client - 客户端索引 | float | 返回玩家的估计坠落伤害 |
| `L4D_GetRandomPZSpawnPosition()` | client - 客户端索引<br>zombieClass - 特感类型<br>attempts - 尝试次数<br>vecPos - 返回位置的向量 | bool | 尝试找到一个随机有效的特感生成位置 |
| `L4D_GetNearestNavArea()` | vecPos - 向量位置<br>maxDist - 最大距离<br>anyZ - 是否任意Z坐标<br>checkLOS - 是否检查视线<br>checkGround - 是否检查地面<br>teamID - 队伍ID | any | 返回指定位置的相对导航区域 |
| `L4D_GetLastKnownArea()` | client - 客户端索引 | any | 返回最后已知区域的导航地址 |
| `L4D_IsTouchingTrigger()` | trigger - 触发器实体<br>entity - 要测试的实体 | bool | 返回实体是否触摸触发器 |
| `L4D2_GetScriptScope()` | entity - 实体索引 | int | 返回实体的脚本作用域（仅L4D2） |
| `L4D2_GetVScriptEntity()` | 无 | int | 创建或使用现有的"logic_script"实体（仅L4D2） |
| `L4D2_ExecVScriptCode()` | code - 要执行的VScript代码 | bool | 运行指定的VScript代码（仅L4D2） |
| `L4D2_GetVScriptOutput()` | code - 要执行的VScript代码<br>buffer - 返回数据的缓冲区<br>maxlength - 缓冲区最大大小 | bool | 运行VScript代码并返回值（仅L4D2） |
| `L4D2_GetFirstSpawnClass()` | 无 | int | 获取Director将生成的第一个特感类型（仅L4D2） |
| `L4D2_SetFirstSpawnClass()` | zombieClass - 特感类型 | void | 设置Director将生成的第一个特感类型（仅L4D2） |
| `L4D2_GetFurthestSurvivorFlow()` | 无 | float | 获取任何幸存者已达到的最大流程距离（仅L4D2） |
| `L4D_FindRandomSpot()` | NavArea - 要搜索有效位置的导航区域<br>vecPos - 存储有效位置的向量数组 | void | 在导航区域中返回随机选择的生成位置 |
| `L4D2_IsVisibleToPlayer()` | client - 检查可见性的客户端<br>vecPos - 目标位置的向量<br>team - 客户端队伍，可传递0-3<br>team_target - 目标点队伍，为0时考虑客户端角度<br>NavArea - 目标的导航区域，或0自动获取 | bool | 检查玩家是否对指定位置可见 |
| `L4D2_GetSpecialInfectedDominatingMe()` | victim - 要检查的受害者客户端索引 | int | 返回正在控制受害者的特感客户端索引（仅L4D2） |
| `L4D_WarpToValidPositionIfStuck()` | client - 执行操作的客户端 | void | 如果玩家卡住，则将其传送到有效位置 |
| `L4D_HasAnySurvivorLeftSafeArea()` | 无 | bool | 当任何幸存者离开起始区域或在对抗模式中安全门自动打开时返回true |
| `L4D_IsAnySurvivorInStartArea()` | 无 | bool | 当任何幸存者在起始检查点区域时返回true |
| `L4D_IsAnySurvivorInCheckpoint()` | 无 | bool | 当任何幸存者在起始或结束检查点区域时返回true |
| `L4D_AreAllSurvivorsInFinaleArea()` | 无 | bool | 当所有幸存者在最终区域时返回true |
| `L4D_IsInFirstCheckpoint()` | client - 检查其检查点的客户端ID | bool | 当指定的幸存者或特感在起始检查点区域时返回true |
| `L4D_IsInLastCheckpoint()` | client - 检查其检查点的客户端ID | bool | 当指定的幸存者或特感在结束检查点区域时返回true |
| `L4D_IsPositionInFirstCheckpoint()` | vecPos - 要检查的向量位置 | bool | 当给定向量在起始检查点区域内时返回true |
| `L4D_IsPositionInLastCheckpoint()` | vecPos - 要检查的向量位置 | bool | 当给定向量在结束检查点区域内时返回true |
| `L4D_GetCheckpointFirst()` | 无 | int | 返回第一个安全门的实体索引（如果可用） |
| `L4D_GetCheckpointLast()` | 无 | int | 返回最后一个安全门的实体索引（如果可用） |
| `L4D2_IsReachable()` | client - 用于测试的客户端ID<br>vecPos - 要测试的向量坐标 | bool | 检查世界位置是否可被幸存者机器人访问（仅L4D2） |
| `L4D2_NavAreaTravelDistance()` | startPos - 起始位置向量<br>endPos - 结束位置向量<br>ignoreNavBlockers - 是否忽略检查时的阻塞区域 | float | 返回两个区域之间的导航距离 |
| `L4D2_NavAreaBuildPath()` | nav_startPos - 起始位置的导航区域地址<br>nav_endPos - 结束位置的导航区域地址<br>flMaxPathLength - 两点之间允许的最大距离<br>teamID - 为哪个队伍验证路径<br>ignoreNavBlockers - 是否忽略导航阻塞器 | bool | 测试两个向量位置是否可到达（仅L4D2）|
| `L4D_IsValidSurvivor()` | client - 检查的客户端索引 | bool | 验证客户端是否为有效的幸存者玩家 |
| `L4D_IsValidSpecialInfected()` | client - 检查的客户端索引 | bool | 验证客户端是否为有效的特感 |
| `L4D2_ShouldSpawnInFinalArea()` | client - 客户端索引 | bool | 检查客户端是否应该在最终区域生成（仅L4D2） |
| `L4D2_IsSpecialInfectedDominating()` | client - 特感的客户端索引 | bool | 检查特感是否正在控制幸存者（仅L4D2） |
| `L4D_IsSurvivorIncapped()` | client - 幸存者客户端索引 | bool | 检查幸存者是否被击倒 |
| `L4D_IsSurvivorPinned()` | client - 幸存者客户端索引 | bool | 检查幸存者是否被特感控制 |
| `L4D_IsSurvivorDead()` | client - 幸存者客户端索引 | bool | 检查幸存者是否死亡 |
| `L4D_IsSurvivorIncapacitated()` | client - 幸存者客户端索引 | bool | 检查幸存者是否处于无法行动状态 |
| `L4D_IsSurvivorIncapacitated2()` | client - 幸存者客户端索引 | bool | 与L4D_IsSurvivorIncapacitated相同，仅为兼容性 |
| `L4D_IsSurvivorStaggered()` | client - 幸存者客户端索引 | bool | 检查幸存者是否处于摇晃状态 |
| `L4D2_IsSurvivorGettingUp()` | client - 幸存者客户端索引 | bool | 检查幸存者是否正在站起来（仅L4D2） |
| `L4D2_IsSurvivorOnLedge()` | client - 幸存者客户端索引 | bool | 检查幸存者是否在边缘悬挂（仅L4D2） |
| `L4D_IsSurvivorReviving()` | client - 幸存者客户端索引 | bool | 检查幸存者是否正在救治队友 |
| `L4D_IsSurvivorReachable()` | client - 幸存者客户端索引 | bool | 检查幸存者是否可以被其他幸存者接触到 |
| `L4D2_IsSurvivorInWater()` | client - 幸存者客户端索引 | bool | 检查幸存者是否在水中（仅L4D2） |
| `L4D2_IsPlayerInGhostState()` | client - 客户端索引 | bool | 检查玩家是否处于幽灵状态（仅L4D2） |
| `L4D2_GetCurrentWeaponID()` | client - 客户端索引 | int | 获取当前武器的ID |
| `L4D2_GetCurrentWeaponSlot()` | client - 客户端索引 | int | 获取当前武器的槽位 |
| `L4D2_GetWeaponID()` | weapon - 武器实体 | int | 获取武器的ID |
| `L4D2_GetWeaponSlot()` | weapon - 武器实体 | int | 获取武器的槽位 |
| `L4D2_GetWeaponName()` | weapon - 武器实体 | const char[] | 获取武器的名称 |
| `L4D2_GetEquippedMelee()` | client - 客户端索引 | any | 获取装备的近战武器 |
| `L4D2_GetEquippedPrimary()` | client - 客户端索引 | any | 获取装备的主武器 |
| `L4D2_GetEquippedSecondary()` | client - 客户端索引 | any | 获取装备的副武器 |
| `L4D2_SetWeaponUpgrade` | client - 客户端索引<br>slot - 武器槽位<br>upgrade - 升级类型 | void | 设置武器升级 |
| `L4D2_RemoveWeaponUpgrade` | client - 客户端索引<br>slot - 武器槽位<br>upgrade - 升级类型 | void | 移除武器升级 |
| `L4D2_GetWeaponUpgradeCount` | client - 客户端索引<br>slot - 武器槽位<br>upgrade - 升级类型 | int | 获取武器升级数量 |
| `L4D2_IsWeaponUpgraded` | client - 客户端索引<br>slot - 武器槽位<br>upgrade - 升级类型 | bool | 检查武器是否已升级 |
| `L4D2_CheckAndApplyWeaponUpgrade` | weapon - 武器实体<br>upgrade - 升级类型 | bool | 检查并应用武器升级 |
| `L4D2_CheckAndRemoveWeaponUpgrade` | weapon - 武器实体<br>upgrade - 升级类型 | bool | 检查并移除武器升级 |
| `L4D2_CheckPlayerHasWeaponUpgrade` | client - 客户端索引<br>upgrade - 升级类型 | bool | 检查玩家是否拥有特定武器升级（仅L4D2） |
| `L4D2_IsTankControlled()` | tank - Tank实体 | bool | 检查Tank是否被控制 |
| `L4D2_GetMobID()` | client - 客户端索引 | int | 获取特感的MobID |
| `L4D2_SetMobID()` | client - 客户端索引<br>mobID - 设置的MobID | void | 设置特感的MobID |
| `L4D2_GetSpecialInfectedCount()` | 无 | int | 获取当前特感的数量（仅L4D2） |
| `L4D2_AllowLedgeGrab()` | client - 客户端索引<br>bool - 是否允许攀爬边缘 | void | 允许/禁止幸存者攀爬边缘 |
| `L4D2_RemovePlayerFromCrawl()` | client - 客户端索引 | bool | 将玩家从爬行状态移除 |
| `L4D2_SetSurvivorBotMaxPathLength` | client - 客户端索引<br>length - 路径长度 | void | 设置幸存者机器人的最大路径长度 |
| `L4D2_StartBoomerVomit()` | client - 客户端索引 | void | 让Boomer开始呕吐（仅L4D2） |
| `L4D2_StopBoomerVomit()` | client - 客户端索引 | void | 停止Boomer的呕吐（仅L4D2） |
| `L4D2_StartChargerCharge()` | client - 客户端索引<br>target - 目标索引 | void | 让Charger开始冲刺（仅L4D2） |
| `L4D2_StopChargerCharge()` | client - 客户端索引 | void | 停止Charger的冲刺（仅L4D2） |
| `L4D2_StartHunterPounce()` | client - 客户端索引<br>target - 目标索引 | void | 让Hunter开始跳跃（仅L4D2） |
| `L4D2_StopHunterPounce()` | client - 客户端索引 | void | 停止Hunter的跳跃（仅L4D2） |
| `L4D2_StartJockeyRide()` | client - 客户端索引<br>target - 目标索引 | void | 让Jockey开始骑乘（仅L4D2） |
| `L4D2_StopJockeyRide()` | client - 客户端索引 | void | 停止Jockey的骑乘（仅L4D2） |
| `L4D2_StartSmokerDrag()` | client - 客户端索引<br>target - 目标索引 | void | 让Smoker开始拖拽（仅L4D2） |
| `L4D2_StopSmokerDrag()` | client - 客户端索引 | void | 停止Smoker的拖拽（仅L4D2） |
| `L4D2_StartSpitterSpit()` | client - 客户端索引 | void | 让Spitter开始喷射（仅L4D2） |
| `L4D2_StopSpitterSpit()` | client - 客户端索引 | void | 停止Spitter的喷射（仅L4D2） |
| `L4D2_StartTankRock()` | client - 客户端索引<br>target - 目标索引 | void | 让Tank开始扔石头（仅L4D2） |
| `L4D2_StopTankRock()` | client - 客户端索引 | void | 停止Tank扔石头（仅L4D2） |
| `L4D2_StartWitchScream()` | witch - Witch实体<br>victim - 受害者客户端索引 | void | 让Witch开始尖叫（仅L4D2） |
| `L4D2_StopWitchScream()` | witch - Witch实体 | void | 停止Witch的尖叫（仅L4D2） |
| `L4D2_IsScriptSpawnBlocked()` | scriptname - 脚本名 | bool | 检查指定脚本的生成是否被阻止（仅L4D2） |
| `L4D2_BlockScriptSpawn()` | scriptname - 脚本名<br>block - 是否阻止 | void | 阻止或取消阻止指定脚本的生成（仅L4D2） |
| `L4D2_IsScriptInUse()` | scriptname - 脚本名 | bool | 检查指定脚本是否正在使用中（仅L4D2） |
| `L4D2_StartScript()` | scriptname - 脚本名<br>targetname - 目标名 | bool | 启动指定脚本（仅L4D2） |
| `L4D2_StopScript()` | scriptname - 脚本名 | bool | 停止指定脚本（仅L4D2） |
| `L4D2_AllowBoomerBile()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Boomer胆汁效果（仅L4D2） |
| `L4D2_AllowChargerCharge()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Charger冲刺（仅L4D2） |
| `L4D2_AllowHunterPounce()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Hunter跳跃（仅L4D2） |
| `L4D2_AllowJockeyRide()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Jockey骑乘（仅L4D2） |
| `L4D2_AllowSmokerDrag()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Smoker拖拽（仅L4D2） |
| `L4D2_AllowSpitterSpit()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Spitter喷射（仅L4D2） |
| `L4D2_AllowTankRock()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Tank扔石头（仅L4D2） |
| `L4D2_AllowTankMelee()` | client - 客户端索引<br>allow - 是否允许 | void | 允许或禁止Tank近战（仅L4D2） |
| `L4D2_AllowWitchScream()` | witch - Witch实体<br>allow - 是否允许 | void | 允许或禁止Witch尖叫（仅L4D2） |
| `L4D2_OnTakeDamage()` | victim - 受害者<br>inflictor - 攻击者<br>attacker - 攻击者<br>Float:damage - 伤害值<br>&weapon - 武器引用 | void | 伤害计算的前处理钩子（仅L4D2） |
| `L4D2_OnWeaponFire()` | client - 客户端索引<br>weapon - 武器实体<br>iSlot - 武器槽位<br>&iBulletCount - 子弹数量引用<br>&iClipSize - 弹夹大小引用<br>&iReserveAmmo - 备用弹药引用 | void | 武器开火的前处理钩子（仅L4D2） |
| `L4D2_OnWeaponSecondaryFire()` | client - 客户端索引<br>weapon - 武器实体<br>iSlot - 武器槽位 | void | 武器副开火的前处理钩子（仅L4D2） |
| `L4D2_OnPlayerRunCmd()` | client - 客户端索引<br>buttons - 按钮状态<br>impulse - 脉冲值<br>Float:vel[3] - 速度<br>Float:angles[3] - 角度<br>Float:forwardmove - 前向移动<br>Float:sidemove - 侧移<br>Float:upmove - 上移<br>Float:maxspeed - 最大速度<br>Float:clientmaxspeed - 客户端最大速度<br>&weapon - 武器引用<br>&sndtarget - 声音目标引用 | void | 玩家命令处理的前处理钩子（仅L4D2） |
| `L4D2_GetFurthestSurvivorFlow()` | 无 | float | 获取任何幸存者达到的最大流动距离（仅L4D2） |
| `L4D_FindRandomSpot()` | NavArea - NavArea地址<br>vecPos[3] - 存储有效位置的向量数组 | void | 在给定的导航区域中返回随机选择的生成位置 |
| `L4D2_IsVisibleToPlayer()` | client - 客户端索引<br>team - 客户端队伍<br>team_target - 目标点队伍<br>NavArea - 目标的NavArea<br>vecPos[3] - 目标位置的向量 | bool | 检查玩家是否可以看到指定位置（仅L4D2） |
| `L4D2_GetSpecialInfectedDominatingMe()` | victim - 受害者客户端索引 | int | 返回正在控制受害者的特感客户端索引（仅L4D2） |
| `L4D_WarpToValidPositionIfStuck()` | client - 客户端索引 | void | 如果玩家卡住，将其传送到有效位置 |
| `L4D_HasAnySurvivorLeftSafeArea()` | 无 | bool | 当任何幸存者离开起始区域或对抗模式中安全门自动打开时返回true |
| `L4D_IsAnySurvivorInStartArea()` | 无 | bool | 当任何幸存者在起始检查点区域时返回true |
| `L4D_IsAnySurvivorInCheckpoint()` | 无 | bool | 当任何幸存者在起始或结束检查点区域时返回true |
| `L4D_AreAllSurvivorsInFinaleArea()` | 无 | bool | 当所有幸存者都在最终区域时返回true |
| `L4D_IsInFirstCheckpoint()` | client - 客户端索引 | bool | 检查指定幸存者或特感是否在起始检查点区域 |
| `L4D_IsInLastCheckpoint()` | client - 客户端索引 | bool | 检查指定幸存者或特感是否在结束检查点区域 |
| `L4D_IsPositionInFirstCheckpoint()` | vecPos[3] - 要检查的向量位置 | bool | 检查给定向量是否在起始检查点区域内 |
| `L4D_IsPositionInLastCheckpoint()` | vecPos[3] - 要检查的向量位置 | bool | 检查给定向量是否在结束检查点区域内 |
| `L4D_GetCheckpointFirst()` | 无 | int | 返回第一个安全门的实体索引，如果不可用则返回-1 |
| `L4D_GetCheckpointLast()` | 无 | int | 返回最后一个安全门的实体索引，如果不可用则返回-1 |
| `L4D2_IsReachable()` | client - 客户端索引<br>vecPos[3] - 要测试的向量坐标 | bool | 检查世界位置是否可被幸存者机器人访问（仅L4D2） |
| `L4D2_NavAreaTravelDistance()` | startPos[3] - 起始位置<br>endPos[3] - 结束位置<br>ignoreNavBlockers - 是否忽略阻塞区域 | float | 返回两个区域之间的导航距离 |
| `L4D2_NavAreaBuildPath()` | nav_startPos - 起始位置的NavArea地址<br>nav_endPos - 结束位置的NavArea地址<br>flMaxPathLength - 两点之间允许的最大距离<br>teamID - 验证路径的队伍<br>ignoreNavBlockers - 是否忽略导航阻塞器 | bool | 测试两个向量位置是否可以到达（仅L4D2） |
| `L4D2_CommandABot()` | entity - 要命令的机器人或感染者<br>target - 目标特感<br>type - 命令类型（BOT_CMD枚举）<br>vecPos[3] - 移动位置 | bool | 使用VScript "CommandABot"函数命令机器人攻击、移动、撤退或重置之前的命令（仅L4D2） |
| `L4D_HasPlayerControlledZombies()` | 无 | bool | 返回玩家是否可以控制感染者 |
| `L4D_DetonateProjectile()` | entity - 要引爆的投射物实体 | void | 引爆活动的手榴弹投射物 |
| `L4D_TankRockPrj()` | client - 归属伤害的客户端索引<br>vecPos[3] - 投射物创建位置<br>vecAng[3] - 投射物方向<br>vecVel[3] - 投射物速度 | int | 创建激活的Tank石头投射物 |
| `L4D_PipeBombPrj()` | client - 归属伤害的客户端索引<br>vecPos[3] - 投射物创建位置<br>vecAng[3] - 投射物方向<br>effects - 是否创建引信/光粒子<br>vecVel[3] - 投射物速度<br>vecRot[3] - 投射物角速度冲量 | int | 创建激活的破片手榴弹投射物 |
| `L4D_MolotovPrj()` | client - 归属伤害的客户端索引<br>vecPos[3] - 投射物创建位置<br>vecAng[3] - 投射物速度和方向<br>vecVel[3] - 投射物速度<br>vecRot[3] - 投射物角速度冲量 | int | 创建激活的燃烧瓶投射物 |
| `L4D2_VomitJarPrj()` | client - 归属伤害的客户端索引<br>vecPos[3] - 投射物创建位置<br>vecAng[3] - 投射物速度和方向<br>vecVel[3] - 投射物速度<br>vecRot[3] - 投射物角速度冲量 | int | 创建激活的胆汁瓶投射物（仅L4D2） |
| `L4D2_GrenadeLauncherPrj()` | client - 归属伤害的客户端索引<br>vecPos[3] - 投射物创建位置<br>vecAng[3] - 投射物速度和方向<br>vecVel[3] - 投射物速度<br>vecRot[3] - 投射物角速度冲量<br>bIncendiary - 投射物的燃烧效果 | int | 创建激活的榴弹发射器投射物（仅L4D2） |
| `L4D2_SpitterPrj()` | client - 归属伤害的客户端索引<br>vecPos[3] - 投射物创建位置<br>vecAng[3] - 投射物速度和方向<br>vecVel[3] - 投射物速度<br>vecRot[3] - 投射物角速度冲量 | int | 创建Spitter黏液投射物（仅L4D2） |
| `L4D2_UseAdrenaline()` | client - 客户端索引<br>fTime - 屏幕效果持续时间<br>heal - 是否提供健康益处<br>event - 是否触发"adrenaline_used"事件 | void | 为玩家提供肾上腺素效果和健康益处（仅L4D2） |
| `L4D_RespawnPlayer()` | client - 要复活的客户端索引 | void | 从死亡状态复活玩家 |
| `L4D_SetHumanSpec()` | bot - 要设置为观察者的机器人索引<br>client - 观察者的客户端索引 | bool | 设置人类观察者接管幸存者机器人 |
| `L4D_TakeOverBot()` | client - 应该接管的客户端索引 | bool | 接管幸存者机器人 |
| `L4D_CanBecomeGhost()` | client - 客户端索引 | bool | 当屏幕上显示"You will enter Spawn Mode in X seconds"文本时返回true |
| `L4D_SetBecomeGhostAt()` | client - 客户端索引<br>time - 时间 | void | 设置死亡特感玩家过渡到幽灵状态的时间 |
| `L4D_GoAwayFromKeyboard()` | client - 客户端索引 | bool | 将客户端设置为空闲、离开键盘状态 |
| `L4D2_AreWanderersAllowed()` | 无 | bool | 返回是否允许游荡的女巫（仅L4D2） |
| `L4D_IsFinaleEscapeInProgress()` | 无 | bool | 当救援车辆离开直到屏幕淡出和字幕开始时返回true |
| `L4D2_GetCurrentFinaleStage()` | 无 | any | 返回当前最终阶段类型（仅L4D2） |
| `L4D2_ForceNextStage()` | 无 | void | 强制ScriptedMode阶段前进到下一阶段（仅L4D2） |
| `L4D2_GetSurvivalStartTime()` | 无 | int | 返回生存模式开始前的设置倒计时时间（仅L4D2） |
| `L4D2_SetSurvivalStartTime()` | time - 时间 | void | 设置生存模式开始前的倒计时时间（仅L4D2） |
| `L4D_ForceVersusStart()` | 无 | void | 强制游戏以对抗模式开始 |
| `L4D_ForceSurvivalStart()` | 无 | void | 强制游戏以生存模式开始 |
| `L4D2_ForceScavengeStart()` | 无 | void | 强制游戏以夺药模式开始（仅L4D2） |
| `L4D2_IsTankInPlay()` | 无 | bool | 当任何Tank在地图上时返回true（仅L4D2） |
| `L4D2_DefibByDeadBody()` | client - 要复活的客户端<br>reviver - 执行复活的人<br>nopenalty - 是否将此复活添加到队伍使用的除颤器数量中 | void | 通过除颤器复活死亡玩家，播放起身动画（仅L4D2） |
| `L4D2_GetDirectorScriptScope()` | level - 作用域级别 | int | 返回导演脚本作用域句柄（仅L4D2） |
| `L4D_ScavengeBeginRoundSetupTime()` | 无 | int | 重新开始夺药模式的设置计时器（仅L4D2） |
| `L4D2_SpawnAllScavengeItems()` | 无 | void | 生成地图中所有夺药罐（仅L4D2） |
| `L4D_ResetMobTimer()` | 无 | void | 重置自然尸潮计时器（仅L4D2） |
| `L4D_GetPlayerSpawnTime()` | player - 玩家索引 | float | 获取特感的剩余生成时间（仅L4D2） |
| `L4D_SetPlayerSpawnTime()` | player - 玩家索引<br>time - 时间<br>bReportToPlayer - 是否通知玩家 | void | 设置特感的剩余生成时间（仅L4D2） |
| `L4D_RestartScenarioFromVote()` | map - 地图名称 | int | 重新开始回合，必要时切换地图 |
| `L4D_GetVersusMaxCompletionScore()` | 无 | int | 获取地图的最大对抗完成分数 |
| `L4D_SetVersusMaxCompletionScore()` | score - 分数 | int | 设置地图的最大对抗完成分数 |
| `L4D_GetTeamScore()` | logical_team - 逻辑队伍ID<br>campaign_score - 是否获取战役分数 | int | 获取队伍分数（已弃用） |
| `L4D_SetCampaignScores()` | scoreA - 队伍A分数<br>scoreB - 队伍B分数 | void | 设置当前战役分数 |
| `L4D_IsFirstMapInScenario()` | 无 | bool | 检查是否为战役的第一张地图 |
| `L4D_IsMissionFinalMap()` | anyMap - 是否检查任意结局地图 | bool | 检查是否为战役的最后一张地图 |
| `L4D_NotifyNetworkStateChanged()` | 无 | void | 通知CGameRulesProxy游戏状态已更改 |
| `L4D_StaggerPlayer()` | target - 目标玩家<br>source_ent - 来源实体<br>vecSource[3] - 来源位置 | void | 触发目标玩家的踉跄行为 |
| `L4D2_SendInRescueVehicle()` | 无 | void | 呼叫救援车辆（仅L4D2） |
| `L4D2_ChangeFinaleStage()` | finaleType - 结局阶段类型<br>arg - 参数 | void | 更改结局阶段（仅L4D2） |
| `L4D_ReplaceTank()` | tank - 当前坦克玩家<br>newtank - 新坦克玩家 | void | 替换坦克控制权 |
| `L4D2_SpawnTank()` | vecPos[3] - 生成位置<br>vecAng[3] - 面向角度 | int | 生成坦克（仅L4D2） |
| `L4D2_SpawnSpecial()` | zombieClass - 特感类型<br>vecPos[3] - 生成位置<br>vecAng[3] - 面向角度 | int | 生成特感（仅L4D2） |
| `L4D2_SpawnWitch()` | vecPos[3] - 生成位置<br>vecAng[3] - 面向角度 | int | 生成女巫（仅L4D2） |
| `L4D2_SpawnWitchBride()` | vecPos[3] - 生成位置<br>vecAng[3] - 面向角度 | int | 生成女巫新娘（仅L4D2） |
| `L4D_LobbyUnreserve()` | 无 | void | 移除服务器大厅保留 |
| `L4D_LobbyIsReserved()` | 无 | bool | 检查服务器是否为大厅保留 |
| `L4D_GetLobbyReservation()` | reservation - 存储保留ID的字符串<br>maxlength - 最大长度 | void | 获取大厅保留ID |
| `L4D_SetLobbyReservation()` | reservation - 保留ID | void | 设置大厅保留ID |
| `L4D_SetPlayerIntensity()` | client - 客户端索引<br>intensity - 紧张度(0.0-1.0) | void | 设置玩家紧张度 |
| `L4D2_VScriptWrapper_GetMapNumber()` | 无 | int | 返回新战役后已玩地图数量（仅L4D2） |
| `L4D2_VScriptWrapper_HasEverBeenInjured()` | client - 客户端索引<br>team - 队伍ID | bool | 检查角色是否曾被特定队伍成员伤害（仅L4D2） |
| `L4D2_VScriptWrapper_GetAliveDuration()` | client - 客户端索引 | float | 返回角色存活时间（仅L4D2） |
| `L4D2_VScriptWrapper_IsDead()` | client - 客户端索引 | bool | 检查玩家是否死亡且可观察他人（仅L4D2） |
| `L4D2_VScriptWrapper_IsDying()` | client - 客户端索引 | bool | 检查玩家是否死亡但尚未可观察他人（仅L4D2） |
| `L4D2_VScriptWrapper_UseAdrenaline()` | client - 客户端索引<br>time - 时间 | bool | 触发肾上腺素效果（仅L4D2，已弃用） |
| `L4D2_VScriptWrapper_ReviveByDefib()` | client - 客户端索引 | bool | 通过除颤器复活死亡玩家（仅L4D2） |
| `L4D2_VScriptWrapper_ReviveFromIncap()` | client - 客户端索引 | bool | 复活被击晕的玩家（仅L4D2） |
| `L4D2_VScriptWrapper_GetSenseFlags()` | bot - 机器人索引 | any | 获取机器人感知标志（仅L4D2） |
| `L4D2_VScriptWrapper_NavAreaBuildPath()` | startPos[3] - 起始位置<br>endPos[3] - 结束位置<br>flMaxPathLength - 最大路径长度<br>checkLOS - 检查视线<br>checkGround - 检查地面<br>teamID - 队伍ID<br>ignoreNavBlockers - 忽略导航阻塞 | bool | 测试两个向量位置是否可达（仅L4D2，已弃用） |
| `L4D2_VScriptWrapper_NavAreaTravelDistance()` | startPos[3] - 起始位置<br>endPos[3] - 结束位置<br>flMaxPathLength - 最大路径长度<br>checkLOS - 检查视线<br>checkGround - 检查地面 | float | 计算两个区域之间的距离（仅L4D2） |
| `L4D2_GetScriptValueInt()` | key - 变量名<br>value - 默认值 | int | 返回指定导演变量的整数值（仅L4D2） |
| `L4D2_GetScriptValueFloat()` | key - 变量名<br>value - 默认值 | float | 返回指定导演变量的浮点数值（仅L4D2） |
| `L4D2_HasConfigurableDifficultySetting()` | 无 | bool | 检查是否有可配置的难度设置（仅L4D2） |
| `L4D2_GetSurvivorSetMap()` | 无 | int | 返回地图默认的幸存者组设置（仅L4D2） |
| `L4D2_GetSurvivorSetMod()` | 无 | int | 返回当前幸存者组设置（可能已被覆盖）（仅L4D2） |
| `L4D2_IsGenericCooperativeMode()` | 无 | bool | 检查当前游戏模式是否为合作/写实模式（仅L4D2） |
| `L4D_IsCoopMode()` | 无 | bool | 检查当前游戏模式是否为合作模式 |
| `L4D2_IsRealismMode()` | 无 | bool | 检查当前游戏模式是否为写实模式（仅L4D2） |
| `L4D_IsSurvivalMode()` | 无 | bool | 检查当前游戏模式是否为生存模式 |
| `L4D2_IsScavengeMode()` | 无 | bool | 检查当前游戏模式是否为夺药模式（仅L4D2） |
| `L4D_IsVersusMode()` | 无 | bool | 检查当前游戏模式是否为对抗模式 |
| `L4D_GetCampaignScores()` | &scoreA - 队伍A分数<br>&scoreB - 队伍B分数 | int | 获取当前存储在Director中的战役分数（已弃用） |
| `L4D_GetMobSpawnTimerRemaining()` | 无 | float | 获取下一次导演尸潮前的剩余时间（已弃用） |
| `L4D_GetMobSpawnTimerDuration()` | 无 | float | 获取尸潮计时器设置的持续时间（已弃用） |
| `L4D2_GetTankCount()` | 无 | int | 获取当前游戏中的坦克数量（仅L4D2） |
| `L4D2_GetWitchCount()` | 无 | int | 获取当前游戏中的女巫数量（仅L4D2） |
| `L4D_GetCurrentChapter()` | 无 | int | 返回当前战役的地图章节号 |
| `L4D_GetMaxChapters()` | 无 | int | 返回当前游戏模式的最大章节数 |
| `L4D_IsInIntro()` | 无 | int | 返回介绍动画是否正在播放 |
| `L4D_GetAllNavAreas()` | aList - 存储所有导航区域地址的ArrayList | void | 返回所有导航区域地址 |
| `L4D_GetNavAreaID()` | area - 导航区域地址 | int | 根据地址返回导航区域ID |
| `L4D_GetNavAreaByID()` | id - 导航区域ID | Address | 根据ID返回导航区域地址 |
| `L4D_GetNavAreaPos()` | area - 导航区域地址<br>&vecPos[3] - 存储位置的向量 | void | 返回指定导航区域的原点 |
| `L4D_GetNavAreaCenter()` | area - 导航区域地址<br>&vecPos[3] - 存储中心位置的向量 | void | 返回指定导航区域的中心 |
| `L4D_GetNavAreaSize()` | area - 导航区域地址<br>&vecSize[3] - 存储大小的向量 | void | 返回指定导航区域的大小 |
| `L4D_NavArea_IsConnected()` | area1 - 第一个导航区域地址<br>area2 - 第二个导航区域地址<br>direction - 检查方向 | bool | 检查两个导航区域是否在指定方向相连 |
| `L4D_GetNavArea_AttributeFlags()` | pTerrorNavArea - 导航区域指针 | int | 返回导航区域的属性标志 |
| `L4D_SetNavArea_AttributeFlags()` | pTerrorNavArea - 导航区域指针<br>flags - 要设置的属性标志 | void | 设置导航区域的属性标志 |
| `L4D_GetNavArea_SpawnAttributes()` | pTerrorNavArea - 导航区域指针 | int | 返回导航区域的生成属性标志 |
| `L4D_SetNavArea_SpawnAttributes()` | pTerrorNavArea - 导航区域指针<br>flags - 要设置的生成属性标志 | void | 设置导航区域的生成属性标志 |
| `L4D2_GetVersusCampaignScores()` | scores[2] - 存储战役分数的数组 | void | 获取存储在对抗导演中的战役分数（仅L4D2） |
| `L4D2_SetVersusCampaignScores()` | scores[2] - 要设置的战役分数数组 | void | 设置对抗导演中的战役分数（仅L4D2） |
| `L4D2_GetVersusTankFlowPercent()` | tankFlows[2] - 存储坦克生成流程百分比的数组 | void | 获取两个对抗回合中坦克生成的流程百分比（仅L4D2） |
| `L4D2_SetVersusTankFlowPercent()` | tankFlows[2] - 要设置的坦克生成流程百分比数组 | void | 设置两个对抗回合中坦克生成的流程百分比（仅L4D2） |
| `L4D2_GetVersusWitchFlowPercent()` | witchFlows[2] - 存储女巫生成流程百分比的数组 | void | 获取两个对抗回合中女巫生成的流程百分比（仅L4D2） |
| `L4D2_SetVersusWitchFlowPercent()` | witchFlows[2] - 要设置的女巫生成流程百分比数组 | void | 设置两个对抗回合中女巫生成的流程百分比（仅L4D2） |
| `L4D2_CTimerReset()` | timer - 要重置的倒计时计时器 | void | 重置指定的倒计时计时器 |
| `L4D2_CTimerStart()` | timer - 要启动的倒计时计时器<br>duration - 计时器持续时间 | void | 启动指定的倒计时计时器并设置持续时间 |
| `L4D2_CTimerInvalidate()` | timer - 要失效的倒计时计时器 | void | 使指定的倒计时计时器失效 |
| `L4D2_CTimerHasStarted()` | timer - 要检查的倒计时计时器 | bool | 检查指定的倒计时计时器是否已启动 |
| `L4D2_CTimerIsElapsed()` | timer - 要检查的倒计时计时器 | bool | 检查指定的倒计时计时器是否已过期 |
| `L4D2_CTimerGetElapsedTime()` | timer - 要获取的倒计时计时器 | float | 获取指定倒计时计时器的已用时间 |
| `L4D2_CTimerGetRemainingTime()` | timer - 要获取的倒计时计时器 | float | 获取指定倒计时计时器的剩余时间 |
| `L4D2_CTimerGetCountdownDuration()` | timer - 要获取的倒计时计时器 | float | 获取指定倒计时计时器的持续时间 |
| `L4D2_ITimerStart()` | timer - 要启动的间隔计时器 | void | 启动指定的间隔计时器 |
| `L4D2_ITimerInvalidate()` | timer - 要失效的间隔计时器 | void | 使指定的间隔计时器失效 |
| `L4D2_ITimerHasStarted()` | timer - 要检查的间隔计时器 | bool | 检查指定的间隔计时器是否已启动 |
| `L4D2_ITimerGetElapsedTime()` | timer - 要获取的间隔计时器 | float | 获取指定间隔计时器的已用时间 |
| `L4D_GetWeaponID` | weaponName - 武器类名 | int | 返回特定类名的武器ID，找不到返回-1 |
| `L4D2_IsValidWeapon` | weaponName - 武器名称 | bool | 检查给定武器字符串是否存在于WeaponInformationDatabase中 |
| `L4D2_GetIntWeaponAttribute` | weaponName - 武器名称<br>attr - 要读取的属性 | any | 读取武器的整数类型属性 |
| `L4D2_GetFloatWeaponAttribute` | weaponName - 武器名称<br>attr - 要读取的属性 | float | 读取武器的浮点类型属性 |
| `L4D2_SetIntWeaponAttribute` | weaponName - 武器名称<br>attr - 要修改的属性<br>value - 要设置的值 | void | 设置武器的整数类型属性 |
| `L4D2_SetFloatWeaponAttribute` | weaponName - 武器名称<br>attr - 要修改的属性<br>value - 要设置的值 | void | 设置武器的浮点类型属性 |
| `L4D2_GetMeleeWeaponIndex` | weaponName - 武器名称 | int | 从近战武器数据库中检索给定近战武器的索引 |
| `L4D2_GetIntMeleeAttribute` | id - 近战武器ID<br>attr - 要读取的属性 | int | 读取近战武器的整数类型属性 |
| `L4D2_GetFloatMeleeAttribute` | id - 近战武器ID<br>attr - 要读取的属性 | float | 读取近战武器的浮点类型属性 |
| `L4D2_GetBoolMeleeAttribute` | id - 近战武器ID<br>attr - 要读取的属性 | bool | 读取近战武器的布尔类型属性 |
| `L4D2_SetIntMeleeAttribute` | id - 近战武器ID<br>attr - 要修改的属性<br>value - 要设置的值 | void | 设置近战武器的整数类型属性 |
| `L4D2_SetFloatMeleeAttribute` | id - 近战武器ID<br>attr - 要修改的属性<br>value - 要设置的值 | void | 设置近战武器的浮点类型属性 |
| `L4D2_SetBoolMeleeAttribute` | id - 近战武器ID<br>attr - 要修改的属性<br>value - 要设置的值 | void | 设置近战武器的布尔类型属性 |
| `L4D2Direct_GetTankCount` | 无 | int | 获取导演存储的当前Tank数量 |
| `L4D2Direct_GetPendingMobCount` | 无 | int | 返回等待生成的感染者数量 |
| `L4D2Direct_SetPendingMobCount` | count - 数量 | void | 设置等待生成的感染者数量 |
| `L4D2Direct_GetMobSpawnTimer` | 无 | CountdownTimer | 获取导演自然生成尸潮的CountdownTimer引用 |
| `L4D2Direct_GetSIClassDeathTimer` | class - SI类别 | IntervalTimer | 获取从给定SI类别最后死亡开始计数的IntervalTimer引用 |
| `L4D2Direct_GetSIClassSpawnTimer` | class - SI类别 | CountdownTimer | 获取从导演最后一次尝试生成SI开始计数的CountdownTimer引用 |
| `L4D2Direct_GetTankPassedCount` | 无 | int | 获取Tank传递给玩家的次数 |
| `L4D2Direct_SetTankPassedCount` | passes - 传递次数 | void | 设置Tank传递给玩家的次数 |
| `L4D2Direct_GetVSCampaignScore` | teamNumber - 队伍编号(0或1) | int | 读取导演存储的给定队伍的战役分数 |
| `L4D2Direct_SetVSCampaignScore` | teamNumber - 队伍编号(0或1)<br>score - 要设置的分数 | void | 设置导演存储的给定队伍的战役分数 |
| `L4D2Direct_GetVSTankFlowPercent` | roundNumber - 回合编号 | float | 读取对抗模式下给定回合的Tank生成流程百分比 |
| `L4D2Direct_SetVSTankFlowPercent` | roundNumber - 回合编号<br>flow - 流程百分比 | void | 设置对抗模式下给定回合的Tank生成流程百分比 |
| `L4D2Direct_GetVSTankToSpawnThisRound` | roundNumber - 回合编号 | bool | 检查给定回合是否会生成Tank |
| `L4D2Direct_SetVSTankToSpawnThisRound` | roundNumber - 回合编号<br>spawn - 是否生成 | void | 告诉导演是否为给定回合生成基于流程距离的Tank |
| `L4D2Direct_GetVSWitchFlowPercent` | roundNumber - 回合编号 | float | 读取对抗模式下给定回合的Witch生成流程百分比 |
| `L4D2Direct_SetVSWitchFlowPercent` | roundNumber - 回合编号<br>flow - 流程百分比 | void | 设置对抗模式下给定回合的Witch生成流程百分比 |
| `L4D2Direct_GetVSWitchToSpawnThisRound` | roundNumber - 回合编号 | bool | 检查给定回合是否会生成Witch |
| `L4D2Direct_SetVSWitchToSpawnThisRound` | roundNumber - 回合编号<br>spawn - 是否生成 | void | 告诉导演是否为给定回合生成基于流程距离的Witch |
| `L4D2Direct_GetVSStartTimer` | 无 | CountdownTimer | 获取对抗模式开始倒计时器的引用 |
| `L4D2Direct_GetScavengeRoundSetupTimer` | 无 | CountdownTimer | 获取夺药模式回合设置倒计时器的引用 |
| `L4D2Direct_GetScavengeOvertimeGraceTimer` | 无 | CountdownTimer | 获取夺药模式加时赛宽限倒计时器的引用 |
| `L4D2Direct_GetMapMaxFlowDistance` | 无 | float | 获取当前地图的最大流程距离（以流程单位计） |
| `L4D2Direct_GetSpawnTimer` | client - 客户端索引 | CountdownTimer | 获取跟踪SI玩家下次可以生成时间的CountdownTimer引用 |
| `L4D2Direct_GetInvulnerabilityTimer` | client - 客户端索引 | CountdownTimer | 获取跟踪幸存者玩家因"无敌帧"而无敌的CountdownTimer引用 |
| `L4D2Direct_GetTankTickets` | client - 客户端索引 | int | 查找客户端进入Tank抽签的票数 |
| `L4D2Direct_SetTankTickets` | client - 客户端索引<br>tickets - 票数 | void | 设置玩家进入Tank抽签的票数 |
| `L4D2Direct_GetShovePenalty` | client - 客户端ID | int | 获取客户端的推搡惩罚值（已废弃，使用GetEntProp替代） |
| `L4D2Direct_SetShovePenalty` | client - 客户端ID<br>penalty - 推搡惩罚值 | void | 设置客户端的推搡惩罚值（已废弃，使用SetEntProp替代） |
| `L4D2Direct_GetNextShoveTime` | client - 客户端ID | float | 获取幸存者可以执行下一次+attack2的时间 |
| `L4D2Direct_SetNextShoveTime` | client - 客户端ID<br>time - 游戏时间 | void | 设置幸存者可以执行下一次+attack2的时间 |
| `L4D2Direct_GetPreIncapHealth` | client - 客户端ID | int | 获取幸存者在被 incapacitated 之前的生命值（可能仅适用于悬挂的玩家） |
| `L4D2Direct_SetPreIncapHealth` | client - 客户端ID<br>health - 新的 pre-incap 生命值 | void | 设置幸存者在被 incapacitated 之前的生命值（可能仅适用于悬挂的玩家） |
| `L4D2Direct_GetPreIncapHealthBuffer` | client - 客户端ID | int | 获取幸存者在被 incapacitated 之前的临时生命值（可能仅适用于悬挂的玩家） |
| `L4D2Direct_SetPreIncapHealthBuffer` | client - 客户端ID<br>health - 新的 pre-incap 临时生命值 | void | 设置幸存者在被 incapacitated 之前的临时生命值（可能仅适用于悬挂的玩家） |
| `L4D2Direct_GetInfernoMaxFlames` | entity - 实体ID | int | 获取 CInferno 允许生成的最大火焰数量 |
| `L4D2Direct_SetInfernoMaxFlames` | entity - 实体ID<br>flames - 火焰数量 | void | 设置 CInferno 允许生成的最大火焰数量 |
| `L4D2Direct_GetScriptedEventManager` | 无 | any | 返回 CDirectorScriptedEventManager 地址 |
| `L4D2Direct_GetTerrorNavArea` | pos[3] - 位置数组<br>beneathLimit - 下方限制（默认120.0） | Address | 获取包含特定位置的 TerrorNavArea |
| `L4D2Direct_GetTerrorNavAreaFlow` | pTerrorNavArea - TerrorNavArea 指针 | float | 查找 TerrorNavArea 在地图中的流程单位距离 |
| `L4D2Direct_TryOfferingTankBot` | client - Tank 的客户端索引<br>bEnterStasis - 是否将 Tank 置于停滞状态 | bool | 强制导演传递 Tank |
| `L4D2Direct_GetFlowDistance` | client - 客户端ID | float | 获取玩家在流程单位中的距离 |
| `L4D2Direct_DoAnimationEvent` | client - 要执行动画的客户端ID<br>event - 动画索引（PlayerAnimEvent_t）<br>variant_param - 变体参数（默认0） | void | 为玩家播放指定的动画 |
| `L4DDirect_GetSurvivorHealthBonus` | client - 客户端ID | int | 获取客户端的生命值奖励 |
| `L4DDirect_SetSurvivorHealthBonus` | client - 客户端ID<br>health - 生命值奖励数量<br>recompute - 如果为true，设置后调用L4DDirect_RecomputeTeamScores() | void | 设置客户端的生命值奖励 |
| `L4DDirect_RecomputeTeamScores` | 无 | void | 计算记分板上的分数 |
| `CTimer_Reset` | timer - 要重置的 CountdownTimer | void | 重置 CountdownTimer，使其从现在开始重新计算到原始持续时间 |
| `CTimer_Start` | timer - 要启动的 CountdownTimer<br>duration - CountdownTimer 使用的持续时间（秒） | void | 从现在开始为给定的持续时间启动 CountdownTimer |
| `CTimer_Invalidate` | timer - 要使其失效的 CountdownTimer | void | 使 CountdownTimer 失效，使其被视为未运行 |
| `CTimer_HasStarted` | timer - 要检查的 CountdownTimer | bool | 确定 CountdownTimer 是否已开始倒计时 |
| `CTimer_IsElapsed` | timer - 要检查的 CountdownTimer | bool | 确定 CountdownTimer 是否已过期 |
| `CTimer_GetElapsedTime` | timer - 要检查的 CountdownTimer | float | 检查 CountdownTimer 已运行多长时间 |
| `CTimer_GetRemainingTime` | timer - 要检查的 CountdownTimer | float | 检查 CountdownTimer 过期前剩余的时间 |
| `CTimer_GetCountdownDuration` | timer - 要检查的 CountdownTimer | float | 获取 CountdownTimer 使用的倒计时持续时间 |
| `ITimer_Reset` | timer - 要重置的 IntervalTimer | void | 重置 IntervalTimer，使其从现在开始重新计数 |
| `ITimer_Start` | timer - 要启动的 IntervalTimer | void | 启动 IntervalTimer，使其从现在开始计数（与重置相同） |
| `ITimer_Invalidate` | timer - 要使其失效的 IntervalTimer | void | 使 IntervalTimer 失效，使其被视为未运行 |
| `ITimer_HasStarted` | timer - 要检查的 IntervalTimer | bool | 检查 IntervalTimer 是否已启动 |
| `ITimer_GetElapsedTime` | timer - 要检查的 IntervalTimer | float | 获取 IntervalTimer 的已用时间 |
| `CTimer_GetDuration` | timer - 要检查的 CountdownTimer | float | 读取 CTimer 中的持续时间变量 |
| `CTimer_SetDuration` | timer - 要设置的 CountdownTimer<br>duration - 要设置的持续时间 | void | 设置 CTimer 中的持续时间变量 |
| `CTimer_GetTimestamp` | timer - 要检查的 CountdownTimer | float | 读取 CTimer 中的时间戳变量 |
| `CTimer_SetTimestamp` | timer - 要设置的 CountdownTimer<br>timestamp - 要设置的时间戳 | void | 设置 CTimer 中的时间戳变量 |
| `ITimer_GetTimestamp` | timer - 要检查的 IntervalTimer | float | 读取 ITimer 中的时间戳变量 |
| `ITimer_SetTimestamp` | timer - 要设置的 IntervalTimer<br>timestamp - 要设置的时间戳 | void | 设置 ITimer 中的时间戳变量 |
| `L4D_CTerrorPlayer_OnVomitedUpon` | client - 要影响的人的客户端ID<br>attacker - 造成失明的客户端ID | void | 在幸存者或特感身上创建 boomer 呕吐效果 |
| `L4D2_CTerrorPlayer_OnHitByVomitJar` | client - 要影响的人的客户端ID<br>attacker - 造成失明的客户端ID | void | 在幸存者或特感身上创建胆汁瓶呕吐效果（仅L4D2） |
| `L4D2_Infected_OnHitByVomitJar` | entity - 要影响的普通感染者的实体ID<br>attacker - 造成失明的客户端ID | void | 在普通感染者身上创建胆汁瓶呕吐效果（仅L4D2） |
| `L4D2_CTerrorPlayer_Fling` | client - 要影响的人的客户端ID<br>attacker - 造成攻击的客户端ID<br>vecDir[3] - 抛出玩家的向量方向 | void | 将玩家甩到地上，就像被 Charger 击中一样（仅L4D2） |
| `L4D_CancelStagger` | client - 要影响的人的客户端ID | void | 取消玩家的蹒跚状态 |
| `L4D_FindUseEntity` | client - 要检查的人的客户端ID<br>players - 是否只搜索玩家（默认false）<br>range - 搜索可用实体的最大距离（默认96.0） | int | 查找可用的客户端/实体 |
| `L4D_ForceHunterVictim` | victim - 要影响的幸存者的客户端索引<br>attacker - 攻击幸存者的客户端索引 | void | 强制 Hunter 扑倒受害者 |
| `L4D_ForceSmokerVictim` | victim - 要影响的幸存者的客户端索引<br>attacker - 攻击幸存者的客户端索引 | void | 强制 Smoker 用舌头抓住受害者 |
| `L4D2_ForceJockeyVictim` | victim - 幸存者的客户端索引<br>attacker - 攻击幸存者的客户端索引 | void | 强制Jockey扑倒受害者（仅L4D2） |
| `L4D2_Jockey_EndRide` | victim - 幸存者的客户端索引<br>attacker - Jockey的客户端索引 | void | 让Jockey停止骑乘幸存者（仅L4D2） |
| `L4D2_Charger_ThrowImpactedSurvivor` | victim - 幸存者的客户端索引<br>attacker - 攻击者的客户端索引 | void | 像被附近Charger撞击一样抛出幸存者（仅L4D2） |
| `L4D2_Charger_StartCarryingVictim` | victim - 幸存者的客户端索引<br>attacker - Charger的客户端索引 | void | 让Charger携带幸存者（仅L4D2） |
| `L4D2_Charger_PummelVictim` | victim - 幸存者的客户端索引<br>attacker - Charger的客户端索引 | void | 让Charger殴打幸存者（仅L4D2） |
| `L4D2_Charger_EndPummel` | victim - 幸存者的客户端索引<br>attacker - Charger的客户端索引 | void | 让Charger停止殴打幸存者（仅L4D2） |
| `L4D2_Charger_EndCarry` | victim - 幸存者的客户端索引<br>attacker - Charger的客户端索引 | void | 让Charger停止携带幸存者（仅L4D2） |
| `L4D_Hunter_ReleaseVictim` | victim - 幸存者的客户端索引<br>attacker - Hunter的客户端索引 | void | 让Hunter结束对幸存者的扑倒 |
| `L4D_Smoker_ReleaseVictim` | victim - 幸存者的客户端索引<br>attacker - Smoker的客户端索引 | void | 让Smoker停止用舌头悬挂幸存者 |
| `L4D_CreateRescuableSurvivors` | 无 | void | 在可救援房间中生成所有死亡的幸存者 |
| `L4D_StopBeingRevived` | client - 受影响者的客户端ID<br>vocalize - 是否让玩家发出停止的声音（默认为false） | void | 停止复活被 incapacitated 的幸存者，也适用于悬挂在边缘的情况 |
| `L4D_ReviveSurvivor` | client - 受影响者的客户端ID | void | 复活被 incapacitated 的幸存者，也适用于悬挂在边缘的情况 |
| `L4D2_GetVersusCompletionPlayer` | client - 受影响者的客户端ID | int | 获取客户端的地图流程进度百分比（0-100）（仅L4D2） |
| `L4D_GetHighestFlowSurvivor` | 无 | int | 返回在流程中最靠前的客户端ID |
| `L4D_GetInfectedFlowDistance` | entity - 普通感染者ID | float | 获取指定普通感染者的地图流程距离 |
| `L4D2_SwapTeams` | 无 | void | 在对抗模式中交换队伍（仅L4D2） |
| `L4D2_AreTeamsFlipped` | 无 | bool | 返回对抗模式队伍是否翻转（已废弃，使用GameRules_GetProp替代） |
| `L4D_EndVersusModeRound` | countSurvivors - 幸存者是否到达安全屋 | void | 结束对抗模式回合 |
| `L4D2_StartRematchVote` | 无 | void | 开始对抗模式重赛投票（仅L4D2） |
| `L4D2_Rematch` | 无 | void | 通过对抗模式重赛投票（仅L4D2） |
| `L4D2_FullRestart` | 无 | void | 像"mp_restartgame"一样重新开始章节，在对抗模式中队伍会翻转（仅L4D2） |
| `L4D2_HideVersusScoreboard` | 无 | void | 隐藏回合结束记分板（仅L4D2） |
| `L4D2_HideScavengeScoreboard` | 无 | void | 隐藏回合结束记分板（仅L4D2） |
| `L4D2_HideScoreboard` | 无 | void | 隐藏回合结束记分板（仅L4D2） |
| `L4D_TakeOverZombieBot` | client - 接管控制的特感的客户端ID<br>target - 失去控制的特感的客户端ID | void | 接管另一个特感 |
| `L4D_ReplaceWithBot` | client - 失去控制的玩家的客户端ID | void | 用机器人替换玩家 |
| `L4D_CullZombie` | client - 要杀死的玩家的客户端ID（非普通感染者） | void | 杀死玩家，将他们的视角传送到随机幸存者 |
| `L4D_CleanupPlayerState` | client - 受影响的客户端ID | void | 重置玩家状态，相当于死亡时的状态 |
| `L4D_SetClass` | client - 要更改的玩家的客户端ID（非普通感染者）<br>zombieClass - 要更改为的特感类别编号 | void | 设置玩家的特感类别，可以在活着时更改特感！有效值L4D1: 1-3, L4D2: 1-6 |
| `L4D_MaterializeFromGhost` | client - 要实体化的玩家的客户端ID | int | 从幽灵状态生成特感，返回客户端的"m_customAbility"武器，或错误时返回-1 |
| `L4D_BecomeGhost` | client - 受影响的玩家的客户端ID | bool | 将活着的玩家转变为幽灵状态，成功返回true，错误或已处于幽灵状态返回false |
| `L4D_State_Transition` | client - 受影响的玩家的客户端ID<br>state - 状态值 | void | 进入幽灵/死亡模式，一些状态值可能有不同的结果 |
| `L4D_RegisterForbiddenTarget` | entity - 实体ID | int | 为对象设置汽车警报（似乎不起作用） |
| `L4D_UnRegisterForbiddenTarget` | entity - 实体ID | void | 移除对象的汽车警报（似乎不起作用） |
| `L4D_IsEntitySaveable` | entity - 要检查的实体，通常是道具，不应该是刷子等 | void | 查看实体是否可保存以过渡到下一张地图 |
| `L4D_Timer_EnableTimer` | entity - 计时器实体索引<br>enable - 是否启用 | void | 启用或禁用计时器 |
| `L4D_Timer_ResetTimer` | entity - 计时器实体索引 | void | 重置计时器 |
| `L4D_Timer_GetTimeLeft` | entity - 计时器实体索引 | float | 获取计时器剩余时间（秒） |
| `L4D_Timer_SetTimeLeft` | entity - 计时器实体索引<br>time - 剩余时间（秒） | void | 设置计时器剩余时间 |

## 类映射接口

### PlayerAnimState 类映射

#### 方法

| 方法名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `PlayerAnimState::FromPlayer` | client - 玩家索引 | PlayerAnimState | 获取玩家的PlayerAnimState实例 |
| `GetMainActivity` | 无 | int | 获取玩家动画的主要活动，与"left4dhooks_anim.inc"中的枚举匹配 |
| `ResetMainActivity` | 无 | void | 重新开始并重新计算主要活动 |

#### 属性

| 属性名 | 类型 | 描述 |
|-------|------|------|
| `m_bIsCustomSequence` | bool | 仅在"CTerrorPlayerAnimState::SetCustomSequence"后为True |
| `m_bIsDead` | bool | 玩家是否死亡 |
| `m_bIsHealing` | bool | 玩家是否正在治疗 |
| `m_bIsResurrection` | bool | 玩家是否正在复活 |
| `m_bIsHitByCharger` | bool | 玩家是否被Charger击中（也称为多次冲锋，保龄球） |
| `m_bIsPummeled` | bool | 玩家是否被殴打 |
| `m_bIsSlammedIntoWall` | bool | 玩家是否被撞到墙上 |
| `m_bIsSlammedIntoGround` | bool | 玩家是否被撞到地上 |
| `m_bIsStartPummel` | bool | 与Charger殴打动画相关 |
| `m_bIsPounded` | bool | 殴打后起身 |
| `m_bIsCarriedByCharger` | bool | 玩家是否被Charger携带 |
| `m_bIsPunchedByTank` | bool | 玩家是否被Tank拳打（石头起身也共享此属性） |
| `m_bIsSpitting` | bool | 玩家是否正在吐痰 |
| `m_bIsPouncedOn` | bool | 玩家是否被扑到 |
| `m_bIsTongueAttacked` | bool | 玩家是否被舌头攻击 |
| `m_bIsStartChainsaw` | bool | 玩家是否开始使用电锯 |
| `m_bIsIsPouncing` | bool | 玩家是否正在扑击 |
| `m_bIsRiding` | bool | 玩家是否在骑乘 |
| `m_bIsJockeyRidden` | bool | 玩家是否被Jockey骑乘 |
| `m_bIsTonguing` | bool | 玩家是否正在使用舌头 |
| `m_bIsCharging` | bool | 玩家是否正在冲锋 |
| `m_bIsPummeling` | bool | 玩家是否正在殴打 |
| `m_bIsPounding` | bool | 玩家是否正在猛击 |
| `m_bIsTongueReelingIn` | bool | 舌头是否正在收回 |
| `m_bIsTongueAttacking` | bool | 舌头是否正在攻击 |

### ConVarPtrWrapper 类映射

#### 构造函数

| 构造函数 | 参数 | 返回值 | 描述 |
|---------|------|-------|------|
| `ConVarPtrWrapper` | p - ConVar的指针（地址） | ConVarPtrWrapper | 接受C++指针的构造函数 |

#### 方法

| 方法名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `GetInt` | 无 | int | 检索convar的整数值 |
| `GetFloat` | 无 | float | 检索convar的浮点数值 |
| `GetSMHandle` | 无 | ConVar | 检索SourceMod的ConVar句柄 |

#### 属性

| 属性名 | 类型 | 描述 |
|-------|------|------|
| `m_pszName` | Address | 检索convar的C字符串指针 |
| `m_pParent` | ConVarPtrWrapper | 检索父convar（不要直接使用此属性） |
| `m_fValue` | float | 检索convar结构体中存储的浮点值（不要直接使用此属性） |
| `m_nValue` | int | 检索convar结构体中存储的整数值（不要直接使用此属性） |

### Ammo_t 类映射

#### 方法

| 方法名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `GetName` | buffer - 缓冲区<br>maxlength - 最大长度 | void | 获取弹药名称 |

#### 属性

| 属性名 | 类型 | 描述 |
|-------|------|------|
| `nDamageType` | int | 伤害类型 |
| `eTracerType` | int | 弹道类型 |
| `physicsForceImpulse` | float | 物理冲击力 |
| `nMinSplashSize` | int | 最小飞溅尺寸 |
| `nMaxSplashSize` | int | 最大飞溅尺寸 |
| `nFlags` | int | 标志 |
| `pPlrDmg` | int | 玩家伤害值（如果设置了整数，则覆盖CVars） |
| `pNPCDmg` | int | NPC伤害值（如果设置了整数，则覆盖CVars） |
| `pMaxCarry` | int | 最大携带数量（如果设置了整数，则覆盖CVars） |
| `pPlrDmgCVar` | ConVarPtrWrapper | 玩家伤害的CVar |
| `pNPCDmgCVar` | ConVarPtrWrapper | NPC伤害的CVar |
| `pMaxCarryCVar` | ConVarPtrWrapper | 最大携带数量的CVar |

### AmmoDef 类映射

#### 静态方法

| 方法名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `AmmoDef::GetAmmoIndex` | 无 | int | 检索弹药索引（m_nAmmoIndex），从索引1开始，减1得到总弹药类型数 |
| `AmmoDef::GetAmmoOfIndex` | nAmmoIndex - 弹药索引 | Ammo_t | 返回指定索引的弹药指针 |
| `AmmoDef::Index` | psz - 弹药名称 | int | 返回弹药名称的索引，找不到则返回-1 |
| `AmmoDef::MaxCarry` | nAmmoIndex - 弹药索引 | int | 检索玩家可以携带的最大弹药数量 |
| `AmmoDef::PlrDamage` | nAmmoIndex - 弹药索引 | int | 检索玩家伤害值 |
| `AmmoDef::NPCDamage` | nAmmoIndex - 弹药索引 | int | 检索NPC伤害值 |
| `AmmoDef::DamageType` | nAmmoIndex - 弹药索引 | int | 检索伤害类型 |
| `AmmoDef::Flags` | nAmmoIndex - 弹药索引 | int | 检索标志 |
| `AmmoDef::MinSplashSize` | nAmmoIndex - 弹药索引 | int | 检索最小飞溅尺寸 |
| `AmmoDef::MaxSplashSize` | nAmmoIndex - 弹药索引 | int | 检索最大飞溅尺寸 |
| `AmmoDef::TracerType` | nAmmoIndex - 弹药索引 | int | 检索弹道类型 |
| `AmmoDef::DamageForce` | nAmmoIndex - 弹药索引 | float | 检索伤害力 |

## 工具函数接口

以下接口在 `left4dhooks_silver.inc` 中定义，提供了各种实用工具函数：

### 引擎检测

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_IsEngineLeft4Dead()` | 无 | bool | 检查是否为Left 4 Dead引擎 |
| `L4D_IsEngineLeft4Dead1()` | 无 | bool | 检查是否为Left 4 Dead 1引擎 |
| `L4D_IsEngineLeft4Dead2()` | 无 | bool | 检查是否为Left 4 Dead 2引擎 |

### 流程控制

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_GetFlowFromPoint()` | float point[3] - 位置向量 | float | 返回指定位置的流程距离 |
| `L4D_IsEnoughFlow()` | client - 客户端索引<br>float given - 给定值 | bool | 检查玩家的流程距离是否大于给定值 |

### 门控制

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_GetDoorState()` | entity - "prop_door*"实体索引 | int | 返回指定门的状态，使用"DOOR_STATE_*"枚举 |
| `L4D_GetDoorFlag()` | entity - "prop_door*"实体索引 | int | 返回指定门的标志，使用"DOOR_FLAG_*"枚举 |

### 实体操作

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_GetPlayerCurrentWeapon()` | client - 客户端索引 | int | 获取玩家当前使用的武器实体索引 |
| `L4D_GetPlayerCustomAbility()` | client - 客户端索引 | int | 获取玩家的自定义能力实体索引 |
| `L4D_GetPlayerUseTarget()` | client - 客户端索引 | int | 获取玩家正在使用的目标实体索引 |
| `L4D_EntityParent()` | entity - 实体索引 | int | 获取实体的父实体索引，无父实体返回-1 |
| `IsUsingMinigun()` | client - 客户端索引 | bool | 检查玩家是否正在使用加特林 |
| `StopUsingMinigun()` | client - 客户端索引 | void | 停止玩家使用加特林 |
| `L4D_IsPlayerOnFire()` | client - 客户端索引 | bool | 检查玩家是否着火 |
| `L4D_IsPlayerBurning()` | client - 客户端索引 | bool | 检查玩家是否正在燃烧 |
| `L4D_IsTankProp()` | entity - 实体索引 | bool | 检查实体是否为Tank可投掷的道具 |

### 普通感染者控制

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_ForcePanicEvent()` | 无 | void | 创建panic event尸潮（受尸潮冷却计时器限制） |
| `L4D_GetCommonsCount()` | 无 | int | 获取当前普通感染者的数量 |
| `L4D_SpawnCommonInfected()` | vPos - 生成位置向量<br>vAng - 生成角度向量（可选） | int | 在指定位置生成普通感染者，失败返回-1 |

### 感染者-幸存者交互

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_GetVictimHunter()` | client - 特感玩家索引 | int | 获取Hunter正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetVictimSmoker()` | client - 特感玩家索引 | int | 获取Smoker正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetVictimCharger()` | client - 特感玩家索引 | int | 获取Charger正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetVictimCarry()` | client - 特感玩家索引 | int | 获取Carrier(Boomer/Spitter/Jockey)正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetVictimJockey()` | client - 特感玩家索引 | int | 获取Jockey正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetAttackerHunter()` | attacker - 特感玩家索引 | int | 获取Hunter正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetAttackerSmoker()` | attacker - 特感玩家索引 | int | 获取Smoker正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetAttackerCharger()` | attacker - 特感玩家索引 | int | 获取Charger正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetAttackerCarry()` | attacker - 特感玩家索引 | int | 获取Carrier(Boomer/Spitter/Jockey)正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetAttackerJockey()` | attacker - 特感玩家索引 | int | 获取Jockey正在攻击的幸存者索引，无攻击目标返回0 |
| `L4D_GetPinnedInfected()` | survivor - 幸存者索引 | int | 获取正在压制该幸存者的感染者索引 |
| `L4D_GetPinnedSurvivor()` | infected - 感染者索引 | int | 获取该感染者正在压制的幸存者索引 |
| `L4D2_IsMultiCharged()` | charger - Charger索引<br>victim - 幸存者索引 | bool | 检查Charger是否多重撞击了幸存者 |
| `L4D_IsPlayerPinned()` | client - 客户端索引 | bool | 检查玩家是否被压制 |
| `L4D_HasReachedSmoker()` | victim - 幸存者索引<br>smoker - Smoker索引 | bool | 检查幸存者是否到达了Smoker的攻击范围 |

### 生命值和状态管理

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_SetPlayerIncapped()` | client - 客户端索引<br>bool:incapacitate | void | 设置玩家是否被击倒 |
| `L4D_SetPlayerIncappedDamage()` | client - 客户端索引<br>attacker - 攻击者索引（可选） | void | 通过给予100.0伤害来击倒幸存者 |
| `L4D_GetPlayerReviveTarget()` | client - 客户端索引 | int | 获取玩家正在救治的目标索引，无目标返回0 |
| `L4D_GetPlayerReviveOwner()` | client - 客户端索引 | int | 获取正在救治该玩家的救援者索引，无救援者返回0 |
| `L4D_StopReviveAction()` | client - 客户端索引 | void | 停止玩家的救治动作 |

### 玩家状态检查

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_IsPlayerStaggering()` | client - 客户端索引 | bool | 检查幸存者是否正在蹒跚 |
| `L4D1_GetMainActivity()` | client - 客户端索引 | int | 获取Left 4 Dead 1中玩家的主活动ID |

### 随机玩家选择

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `GetAnyRandomClient()` | 无 | int | 返回随机的游戏中客户端索引，无客户端返回0 |
| `GetRandomSurvivor()` | alive - 生存状态（-1=任意，0=仅死亡，1=仅存活）<br>bots - 机器人状态（-1=任意，0=仅真实玩家，1=仅机器人） | int | 返回随机的幸存者索引，无匹配幸存者返回0 |
| `GetRandomInfected()` | alive - 生存状态（-1=任意，0=仅死亡，1=仅存活）<br>bots - 机器人状态（-1=任意，0=仅真实玩家，1=仅机器人） | int | 返回随机的特感索引，无匹配感染者返回0 |
| `GetRandomClient()` | team - 队伍（-1=任意，1=观察者，2=幸存者，3=特感，5=幸存者和特感）<br>alive - 生存状态（-1=任意，0=仅死亡，1=仅存活）<br>bots - 机器人状态（-1=任意，0=仅真实玩家，1=仅机器人） | int | 返回随机的游戏中客户端索引，无匹配客户端返回0 |

### Charger队列攻击相关函数

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D2_GetQueuedPummelStartTime()` | charger - Charger索引 | float | 获取队列攻击开始的时间戳，无队列攻击返回-1.0 |
| `L4D2_SetQueuedPummelStartTime()` | charger - Charger索引<br>timestamp - 时间戳 | void | 设置队列攻击开始的时间戳 |
| `L4D2_IsInQueuedPummel()` | charger - Charger索引 | bool | 检查Charger是否处于队列攻击状态 |
| `L4D2_GetQueuedPummelVictim()` | client - 客户端索引 | int | 获取处于队列攻击中的Charger的受害者索引，无受害者返回-1 |
| `L4D2_SetQueuedPummelVictim()` | client - 客户端索引<br>target - 目标索引 | void | 设置队列攻击中的Charger的受害者 |
| `L4D2_GetQueuedPummelAttacker()` | client - 客户端索引 | int | 获取处于队列攻击中的幸存者的攻击者索引，无攻击者返回-1 |
| `L4D2_SetQueuedPummelAttacker()` | client - 客户端索引<br>target - 目标索引 | void | 设置队列攻击中的幸存者的攻击者 |
| `L4D2_OffsQueuedPummelInfo()` | 无 | int | （静态函数）获取队列攻击字段起始偏移量 |

### 悬崖悬挂相关函数

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_IsPlayerHangingFromLedge()` | client - 客户端索引 | bool | 检查幸存者是否悬挂在悬崖边缘 |
| `L4D_CanPlayerLedgeHang()` | client - 客户端索引 | bool | 检查幸存者是否可以悬挂在悬崖边缘 |
| `L4D_LedgeHangEnable()` | client - 客户端索引 | void | 允许幸存者悬挂在悬崖边缘 |
| `L4D_LedgeHangDisable()` | client - 客户端索引 | void | 禁止幸存者悬挂在悬崖边缘 |

## 粒子和特效接口

以下接口在 `left4dhooks_lux_library.inc` 中定义，提供了粒子效果和特效相关功能：

### 实体位置和物理

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `GetOSType()` | &hGamedata - gamedata句柄（可选） | OS_Type | 获取服务器的操作系统类型（Windows、Linux或Mac） |
| `SetAbsOrigin()` | iEntity - 实体索引<br>const float vec[3] - 原点坐标 | bool | 设置实体的绝对位置（比TeleportEntity更好，保持客户端插值移动） |
| `SetAbsVelocity()` | iEntity - 实体索引<br>const float vec[3] - 速度向量 | bool | 设置实体的绝对速度（保持客户端插值移动） |
| `SetAbsAngles()` | iEntity - 实体索引<br>const float vec[3] - 角度向量 | bool | 设置实体的绝对角度（保持客户端插值移动） |
| `GetAttachmentVectors()` | iEntity - 实体索引<br>char[] attachmentName - 附加点名<br>float vecOrigin[3] - 原点坐标<br>float vecAngles[3] - 角度向量 | bool | 获取实体附加点的向量信息 |
| `LookupAttachment()` | iEntity - 实体索引<br>char[] attachmentName - 附加点名 | int | 查找实体附加点的索引 |
| `GetAttachment()` | iEntity - 实体索引<br>iAttachment - 附加点索引<br>float vecOrigin[3] - 原点坐标<br>float vecAngles[3] - 角度向量 | bool | 获取实体附加点的信息 |
| `IsPositionInWater()` | float vecOrigin[3] - 位置坐标 | bool | 检查位置是否在水中（注意：当前可能不太可靠） |
| `GetAbsOrigin()` | iEntity - 实体索引<br>vecOrigin[3] - 用于存储原点的向量<br>bCenter - 是否获取世界空间中心 | void | 获取实体的世界空间原点 |
| `PhysicsExplode()` | vecOrigin[3] - 爆炸原点<br>iMagnitude - 爆炸强度（限制为100）<br>flRadius - 爆炸半径<br>bDamage - 是否伤害道具<br>flInnerRadius - 内部半径 | void | 创建不影响玩家的物理爆炸效果 |
| `TE_SetupExplodeForce()` | vecOrigin[3] - 爆炸原点<br>flRadius - 爆炸半径<br>flMagnitude - 爆炸强度 | void | 设置不可见爆炸力以推动客户端物理对象（L4D2专用） |
| `TE_SetupPhysicsProp()` | vecModelOrigin[3] - 模型原点<br>iPrecacheModel - 预缓存模型索引<br>vecModelAngles[3] - 模型角度<br>vecVelocity[3] - 速度<br>iFlags - 标志<br>iEffects - 效果<br>iSkin - 皮肤<br>RGB[3] - 颜色 | void | 创建客户端物理道具 |
| `TE_SetupDynamicLight()` | vecOrigin[3] - 光源原点<br>RGB[3] - 颜色<br>flRadius - 半径<br>flTime - 时间<br>flDecay - 衰减速度<br>exponent - 亮度 | void | 设置动态光源（注意：每个客户端tick只能存在一个） |

### 内部工具函数

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `GetGameData()` | &hGamedata - gamedata句柄 | void | 加载游戏配置文件并检查加载结果（静态内部函数） |
| `__FindStringIndex2()` | iStringTable - 字符串表索引<br>const char[] sName - 字符串名称 | int | 查找字符串表中的索引（静态内部函数） |
| `EmitMixedAmbientSoundToAll()` | sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数 | void | 向所有玩家播放混合环境音效 |
| `EmitMixedAmbientSoundToAll_FallBack()` | sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数<br>sample2[] - 备选音效<br>level2 - 备选级别<br>pitch2 - 备选音调 | void | 向所有玩家播放带备选的混合环境音效 |
| `EmitMixedAmbientSound()` | client - 客户端索引<br>sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数 | void | 向特定玩家播放混合环境音效 |
| `EmitMixedAmbientSound_FallBack()` | client - 客户端索引<br>sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数<br>sample2[] - 备选音效<br>level2 - 备选级别<br>pitch2 - 备选音调 | void | 向特定玩家播放带备选的混合环境音效 |

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `GetGameData()` | &hGamedata - gamedata句柄 | void | 加载游戏配置文件并检查加载结果（静态内部函数） |
| `__FindStringIndex2()` | iStringTable - 字符串表索引<br>const char[] sName - 字符串名称 | int | 查找字符串表中的索引（静态内部函数） |

### 粒子效果

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `TE_SetupParticle()` | iParticleIndex - 粒子索引<br>vecParticleStartPos[3] - 起始位置<br>vecParticleEndPos[3] - 结束位置<br>vecParticleAngles[3] - 角度<br>iEntity - 实体所有者 | void | 设置临时粒子效果 |
| `TE_SetupParticleFollowEntity()` | iParticleIndex - 粒子索引<br>iEntIndex - 实体索引<br>vecParticleAngles[3] - 角度 | void | 设置跟随实体原点的粒子效果 |
| `TE_SetupParticleAttachment()` | iParticleIndex - 粒子索引<br>iAttachmentIndex - 附加点索引<br>iEntIndex - 实体索引<br>bFollow - 是否跟随附加点 | void | 设置附加到实体的粒子效果 |
| `TE_SetupStopAllParticles()` | iEntIndex - 实体索引 | void | 设置停止实体上的所有粒子效果 |
| `TE_SetupParticleFollowEntity_MaintainOffset()` | iParticleIndex - 粒子索引<br>iEntIndex - 实体索引<br>vecParticleStartPos[3] - 起始位置<br>vecParticleAngles[3] - 角度 | void | 设置跟随实体并保持偏移的粒子效果（L4D2专用） |
| `TE_SetupParticle_ControlPoints()` | iParticleIndex - 粒子索引<br>iEntIndex - 实体索引<br>vecParticleStartPos[3] - 起始位置 | void | 设置附加到模型预定义控制点的粒子效果 |
| `TE_SetupParticleFollowEntity_Name()` | sParticleName[] - 粒子名称<br>iEntIndex - 实体索引<br>vecParticleAngles[3] - 角度 | bool | 通过名称设置跟随实体的粒子效果 |
| `TE_SetupParticleFollowEntity_MaintainOffset_Name()` | sParticleName[] - 粒子名称<br>iEntIndex - 实体索引<br>vecParticleStartPos[3] - 起始位置<br>vecParticleAngles[3] - 角度 | bool | 通过名称设置跟随实体并保持偏移的粒子效果 |
| `TE_SetupParticle_Name()` | sParticleName[] - 粒子名称<br>vecParticleStartPos[3] - 起始位置<br>vecParticleEndPos[3] - 结束位置<br>vecParticleAngles[3] - 角度<br>iEntity - 实体所有者 | bool | 通过名称设置临时粒子效果 |
| `TE_SetupParticleAttachment_Names()` | sParticleName[] - 粒子名称<br>sAttachmentName[] - 附加点名称<br>iEntIndex - 实体索引<br>bFollow - 是否跟随附加点 | bool | 通过名称设置附加到实体的粒子效果 |
| `GetParticleIndex()` | const char[] name - 粒子名称 | int | 获取粒子系统索引或延迟预缓存 |
| `Precache_Particle_System()` | const char[] name - 粒子名称 | int | 预缓存粒子系统 |
| `L4D_TE_Create_Particle()` | fParticleStartPos[3] - 起始位置<br>fParticleEndPos[3] - 结束位置<br>iParticleIndex - 粒子索引<br>iEntIndex - 实体索引<br>fDelay - 延迟<br>SendToAll - 是否发送给所有客户端<br>sParticleName[] - 粒子名称<br>iAttachmentIndex - 附加点索引<br>fParticleAngles[3] - 角度<br>iFlags - 标志<br>iDamageType - 伤害类型<br>fMagnitude - 强度<br>fScale - 缩放<br>fRadius - 半径 | bool | 创建临时粒子效果（已废弃，仅用于向后兼容） |
| `L4D_TE_Stop_Particle()` | fParticleStartPos[3] - 起始位置<br>fParticleEndPos[3] - 结束位置<br>iParticleIndex - 粒子索引<br>iEntIndex - 实体索引<br>fDelay - 延迟<br>SendToAll - 是否发送给所有客户端<br>sParticleName[] - 粒子名称<br>iAttachmentIndex - 附加点索引<br>fParticleAngles[3] - 角度<br>iFlags - 标志<br>iDamageType - 伤害类型<br>fMagnitude - 强度<br>fScale - 缩放<br>fRadius - 半径 | bool | 停止临时粒子效果（已废弃，仅用于向后兼容） |

### 音效和视觉效果

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `Terror_SetPendingDspEffect()` | iClient - 客户端索引<br>flDelay - 延迟时间<br>dspEffectType - DSP效果类型 | void | 设置客户端的DSP音效效果（参考scripts/dsp_presets.txt） |
| `Terror_SetAdrenalineTime()` | iClient - 客户端索引<br>flDuration - 肾上腺素持续时间 | void | 设置玩家的肾上腺素效果持续时间（仅限L4D2） |
| `Terror_GetAdrenalineTime()` | iClient - 客户端索引 | float | 获取玩家剩余的肾上腺素时间，无效果时返回-1.0（仅限L4D2） |
| `Terror_ReviveDeathModel()` | iRevivee - 被救治的玩家索引<br>iReviver - 救治者索引<br>iDeathModel - 死亡模型索引 | bool | 通过除颤器复活死亡模型 |
| `TE_SetupExplodeForce()` | vecOrigin[3] - 爆炸原点<br>flRadius - 爆炸半径<br>flMagnitude - 爆炸强度 | void | 设置爆炸力效果（L4D2专用） |
| `TE_SetupPhysicsProp()` | vecModelOrigin[3] - 模型原点<br>iPrecacheModel - 预缓存模型索引<br>vecModelAngles[3] - 模型角度<br>vecVelocity[3] - 速度<br>iFlags - 标志<br>iEffects - 效果<br>iSkin - 皮肤<br>RGB[3] - 颜色 | void | 创建客户端物理道具 |
| `TE_SetupDynamicLight()` | vecOrigin[3] - 光源原点<br>RGB[3] - 颜色<br>flRadius - 半径<br>flTime - 时间<br>flDecay - 衰减速度<br>exponent - 亮度 | void | 设置动态光源 |
| `TE_SetupTracerSound()` | vecParticleStartPos[3] - 起始位置<br>vecParticleEndPos[3] - 结束位置 | void | 设置跟踪声音效果 |
| `TE_SetupEntityDecal()` | vecOrigin[3] - 贴花原点<br>vecStart[3] - 起始点<br>iTarget - 目标实体<br>iHitbox -  hitbox索引<br>iPrecacheDecal - 预缓存贴花索引 | void | 设置实体贴花 |
| `TE_SetupWorldDecal()` | vecOrigin[3] - 贴花原点<br>iPrecacheDecal - 预缓存贴花索引 | void | 设置世界贴花 |
| `TE_SetupDecal_FromTrace()` | hTR - 跟踪句柄<br>sDecalName[] - 贴花名称 | bool | 从跟踪射线设置贴花 |
| `GetDecalIndex()` | sDecalName[] - 贴花名称 | int | 获取贴花索引或延迟预缓存 |
| `EmitMixedAmbientSoundToAll()` | sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数 | void | 向所有玩家播放混合环境音效 |
| `EmitMixedAmbientSoundToAll_FallBack()` | sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数<br>sample2[] - 备选音效<br>level2 - 备选级别<br>pitch2 - 备选音调 | void | 向所有玩家播放带备选的混合环境音效 |
| `EmitMixedAmbientSound()` | client - 客户端索引<br>sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数 | void | 向特定玩家播放混合环境音效 |
| `EmitMixedAmbientSound_FallBack()` | client - 客户端索引<br>sample[] - 音效文件路径<br>origin[3] - 发射位置<br>entity - 发射实体<br>level - 音效级别<br>pitch - 音调<br>sndChannel - 声音通道<br>rangeMin - 最小范围<br>rangeCurve - 范围曲线<br>levelBoost - 级别提升<br>exponent - 指数<br>sample2[] - 备选音效<br>level2 - 备选级别<br>pitch2 - 备选音调 | void | 向特定玩家播放带备选的混合环境音效 |

## 实用工具函数

以下接口在 `left4dhooks_stocks.inc` 中定义，提供了各种实用工具函数：

### 团队管理

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_GetClientTeam()` | client - 玩家索引 | L4DTeam | 获取玩家的队伍 |
| `L4D_ChangeClientTeam()` | client - 玩家索引<br>team - 目标队伍 | void | 修改玩家的队伍 |

### 特感类管理

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D1_GetPlayerZombieClass()` | client - 玩家索引 | L4D1ZombieClassType | 获取L4D1中特感玩家的类型（仅限L4D1） |
| `L4D1_SetPlayerZombieClass()` | client - 玩家索引<br>class - 特感类型 | void | 设置L4D1中特感玩家的类型（仅限L4D1） |
| `L4D2_GetPlayerZombieClass()` | client - 玩家索引 | L4D2ZombieClassType | 获取L4D2中特感玩家的类型（仅限L4D2） |
| `L4D2_SetPlayerZombieClass()` | client - 玩家索引<br>class - 特感类型 | void | 设置L4D2中特感玩家的类型（仅限L4D2） |
| `L4D1_GetZombieClassname()` | type - 僵尸类型 | char[] | 根据L4D1僵尸类型获取类名（仅限L4D1） |
| `L4D2_GetZombieClassname()` | type - 僵尸类型 | char[] | 根据L4D2僵尸类型获取类名（仅限L4D2） |

### 玩家状态和属性

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_IsPlayerGhost()` | client - 玩家索引 | bool | 检查特感玩家是否为幽灵状态 |
| `L4D_SetPlayerGhostState()` | client - 玩家索引<br>isGhost - 是否为幽灵 | void | 设置特感玩家的幽灵状态 |
| `L4D_GetPlayerGhostSpawnState()` | client - 玩家索引 | int | 获取特感玩家的幽灵生成状态位 |
| `L4D_SetPlayerGhostSpawnState()` | client - 玩家索引<br>bits - 生成状态位 | void | 设置特感玩家的幽灵生成状态位 |
| `L4D_IsPlayerCulling()` | client - 玩家索引 | bool | 检查特感玩家是否正在被剔除 |
| `L4D_SetPlayerCullingState()` | client - 玩家索引<br>isCulling - 是否被剔除 | void | 设置特感玩家的剔除状态 |
| `L4D_IsPlayerIncapacitated()` | client - 玩家索引 | bool | 检查玩家是否被击倒（注意：坦克玩家在死亡动画时也会返回true） |
| `L4D_SetPlayerIncapacitatedState()` | client - 玩家索引<br>isIncapacitated - 是否被击倒 | void | 设置玩家的击倒状态 |
| `L4D_GetPlayerShovePenalty()` | client - 玩家索引 | int | 获取幸存者玩家的推搡惩罚值 |
| `L4D_SetPlayerShovePenalty()` | client - 玩家索引<br>shovePenalty - 推搡惩罚值 | void | 设置幸存者玩家的推搡惩罚值 |
| `L4D_GetTankFrustration()` | client - 玩家索引 | int | 获取坦克玩家的挫折值 |
| `L4D_SetTankFrustration()` | client - 玩家索引<br>frustration - 挫折值 | void | 设置坦克玩家的挫折值 |
| `L4D_IsPlayerIdle()` | client - 玩家索引 | bool | 检查幸存者玩家是否处于空闲状态 |
| `L4D_GetBotOfIdlePlayer()` | client - 玩家索引 | int | 获取对应空闲玩家的幸存者机器人索引，未找到返回-1 |
| `L4D_GetIdlePlayerOfBot()` | bot - Bot索引 | int | 获取Bot对应的空闲玩家索引 |
| `L4D_GetResourceEntity()` | 无 | int | 获取资源实体索引 |
| `L4D_GetPlayerResourceData()` | client - 客户端索引<br>type - 资源类型 | int | 获取玩家资源数据 |
| `L4D_SetPlayerResourceData()` | client - 客户端索引<br>type - 资源类型<br>value - 值 | bool | 设置玩家资源数据 |
| `L4D_GetPlayerReviveCount()` | client - 客户端索引 | int | 获取玩家被救治次数 |
| `L4D_SetPlayerReviveCount()` | client - 客户端索引<br>count - 次数 | void | 设置玩家被救治次数 |
| `L4D_GetPlayerIntensity()` | client - 客户端索引 | float | 获取玩家紧张度 |
| `L4D_GetAvgSurvivorIntensity()` | 无 | float | 获取平均幸存者紧张度 |
| `L4D_IsPlayerCalm()` | client - 客户端索引 | bool | 检查玩家是否冷静 |
| `L4D_SetPlayerCalmState()` | client - 客户端索引<br>isCalm - 是否冷静 | void | 设置玩家冷静状态 |
| `L4D_HasVisibleThreats()` | client - 客户端索引 | bool | 检查玩家是否有可见威胁 |
| `L4D_IsPlayerOnThirdStrike()` | client - 客户端索引 | bool | 检查玩家是否第三次被击倒 |
| `L4D_SetPlayerThirdStrikeState()` | client - 客户端索引<br>onThirdStrike - 是否第三次 | void | 设置玩家第三次被击倒状态 |
| `L4D_IsPlayerGoingToDie()` | client - 客户端索引 | bool | 检查玩家是否即将死亡 |
| `L4D_SetPlayerIsGoingToDie()` | client - 客户端索引<br>isGoingToDie - 是否即将死亡 | void | 设置玩家即将死亡状态 |
| `L4D_GetPlayerTempHealth()` | client - 客户端索引 | int | 获取玩家临时生命值 |
| `L4D_SetPlayerTempHealth()` | client - 客户端索引<br>tempHealth - 临时生命值 | void | 设置玩家临时生命值 |
| `L4D_SetPlayerTempHealthFloat()` | client - 客户端索引<br>tempHealth - 临时生命值(浮点) | void | 设置玩家临时生命值(支持超过200) |

### 武器操作

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_GetWeaponSlot()` | client - 玩家索引<br>slot - 槽位索引 | int | 获取玩家指定槽位的武器实体索引 |
| `L4D_GetWeaponNameBySlot()` | slot - 槽位索引 | char[] | 获取指定槽位的武器类名 |
| `L4D1_GetWeaponSlot()` | weapon - 武器实体索引 | L4D1WeaponSlot | 获取L4D1中武器的槽位类型（仅限L4D1） |
| `L4D2_GetWeaponSlot()` | weapon - 武器实体索引 | L4D2WeaponSlot | 获取L4D2中武器的槽位类型（仅限L4D2） |
| `L4D1_GetWeaponName()` | slot - 槽位类型 | char[] | 获取L4D1中指定槽位类型的武器类名（仅限L4D1） |
| `L4D2_GetWeaponName()` | slot - 槽位类型 | char[] | 获取L4D2中指定槽位类型的武器类名（仅限L4D2） |
| `L4D1_GetMeleeWeaponSlot()` | weapon - 武器实体索引 | int | 获取L4D1中近战武器的槽位索引（仅限L4D1） |
| `L4D2_GetMeleeWeaponSlot()` | weapon - 武器实体索引 | int | 获取L4D2中近战武器的槽位索引（仅限L4D2） |
| `L4D1_WeaponIsRifle()` | weapon - 武器实体索引 | bool | 检查L4D1中的武器是否为步枪（仅限L4D1） |
| `L4D2_WeaponIsRifle()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为步枪（仅限L4D2） |
| `L4D1_GetShotgunNeedPump()` | weapon - 武器实体索引 | bool | 检查L4D1中的霰弹枪是否需要泵动（仅限L4D1） |
| `L4D1_GetWeaponSlotString()` | slot - 槽位类型 | char[] | 获取L4D1中槽位类型的字符串表示（仅限L4D1） |
| `L4D2_GetWeaponSlotString()` | slot - 槽位类型 | char[] | 获取L4D2中槽位类型的字符串表示（仅限L4D2） |
| `L4D2_GetWeaponName()` | weaponId - 武器ID | char[] | 获取L4D2中武器ID对应的武器名称（仅限L4D2） |
| `L4D2_GetWeaponModel()` | weaponId - 武器ID | char[] | 获取L4D2中武器ID对应的武器模型路径（仅限L4D2） |
| `L4D2_GetUpgradeSlot()` | weaponId - 武器ID<br>upgradeId - 升级ID | int | 获取L4D2中武器升级对应的槽位（仅限L4D2） |
| `L4D2_IsWeaponPrimary()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为主武器（仅限L4D2） |
| `L4D2_IsWeaponSecondary()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为副武器（仅限L4D2） |
| `L4D2_IsWeaponMelee()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为近战武器（仅限L4D2） |
| `L4D2_IsWeaponGrenade()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为投掷武器（仅限L4D2） |
| `L4D2_IsWeaponPistol()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为手枪（仅限L4D2） |
| `L4D2_IsWeaponShotgun()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为霰弹枪（仅限L4D2） |
| `L4D2_IsWeaponSMG()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为冲锋枪（仅限L4D2） |
| `L4D2_IsWeaponSniperRifle()` | weapon - 武器实体索引 | bool | 检查L4D2中的武器是否为狙击步枪（仅限L4D2） |
| `L4D2_GetWeaponUpgradeInfo()` | weaponId - 武器ID<br>upgradeId - 升级ID | L4D2WeaponUpgradeInfo | 获取L4D2中武器升级的信息（仅限L4D2） |
| `L4D2_ApplyWeaponUpgrade()` | weapon - 武器实体索引<br>upgradeId - 升级ID | bool | 为L4D2中的武器应用升级（仅限L4D2） |

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_RemoveWeaponSlot()` | client - 客户端索引<br>slot - 武器槽位 | void | 移除玩家特定槽位的武器 |
| `L4D_RemoveAllWeapons()` | client - 客户端索引 | void | 移除玩家所有武器 |
| `L4D2_IsWeaponUpgradeCompatible()` | weapon - 武器实体索引 | bool | 检查武器是否支持升级 |
| `L4D2_GetWeaponUpgradeAmmoCount()` | weapon - 武器实体索引 | int | 获取武器升级弹药数量 |
| `L4D2_SetWeaponUpgradeAmmoCount()` | weapon - 武器实体索引<br>count - 数量 | void | 设置武器升级弹药数量 |
| `L4D2_GetWeaponUpgrades()` | weapon - 武器实体索引 | int | 获取武器升级位掩码 |
| `L4D2_SetWeaponUpgrades()` | weapon - 武器实体索引<br>upgrades - 升级位掩码 | void | 设置武器升级位掩码 |
| `L4D2_GetWeaponId()` | weapon - 武器实体索引 | L4D2WeaponId | 获取武器ID |
| `L4D2_GetWeaponNameByWeaponId()` | weaponId - 武器ID<br>dest - 目标缓冲区<br>destlen - 缓冲区长度 | int | 根据武器ID获取武器名称 |
| `L4D2_GetWeaponIdByWeaponName()` | weaponName - 武器名称 | L4D2WeaponId | 根据武器名称获取武器ID |

### 感染者-幸存者交互

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D2_GetInfectedAttacker()` | client - 幸存者客户端索引 | int | 获取正在压制该幸存者的感染者索引（仅限L4D2） |
| `L4D2_GetSurvivorVictim()` | client - 感染者客户端索引 | int | 获取该感染者正在压制的幸存者索引（仅限L4D2） |
| `L4D2_WasPresentAtSurvivalStart()` | client - 客户端索引 | bool | 检查幸存者是否在生存模式开始时在场（仅限L4D2） |
| `L4D2_SetPresentAtSurvivalStart()` | client - 客户端索引<br>wasPresent - 是否在场 | void | 设置幸存者在生存模式开始时的在场状态（仅限L4D2） |

### 玩家使用动作

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D2_GetPlayerUseAction()` | client - 客户端索引 | L4D2UseAction | 获取玩家当前的使用动作（仅限L4D2） |
| `L4D2_GetPlayerUseActionTarget()` | client - 客户端索引 | int | 获取玩家使用动作的目标实体索引（仅限L4D2） |
| `L4D2_GetPlayerUseActionOwner()` | client - 客户端索引 | int | 获取玩家使用动作的所有者实体索引（仅限L4D2） |

### 游戏状态

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_IsFinaleActive()` | 无 | bool | 检查最终章节是否激活 |
| `L4D_HasAnySurvivorLeftSafeAreaStock()` | 无 | bool | 检查是否有幸存者离开安全区域 |
| `L4D_GetPendingTankPlayer()` | 无 | int | 获取即将成为Tank的玩家索引 |
| `L4D_IsPlayerUsingMountedWeapon()` | client - 客户端索引 | bool | 检查玩家是否使用固定武器 |
| `L4D2_StopInstructorHint()` | client - 客户端索引 | void | 停止L4D2中玩家的教练提示（仅限L4D2） |

### 游戏信息

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D_IsMissionFinalMap()` | 无 | bool | 检查当前是否为任务的最后一张地图 |
| `L4D_IsCampaignFinalMap()` | 无 | bool | 检查当前是否为战役的最后一张地图 |
| `L4D_GetMissionMode()` | 无 | L4DMissionMode | 获取当前游戏模式 |
| `L4D_GetMissionState()` | 无 | L4DMissionState | 获取当前任务状态 |
| `L4D_GetCampaignName()` | buffer - 输出缓冲区<br>maxlen - 缓冲区大小 | void | 获取当前战役名称 |
| `L4D_GetMapName()` | buffer - 输出缓冲区<br>maxlen - 缓冲区大小 | void | 获取当前地图名称 |
| `L4D_GetGameDescription()` | buffer - 输出缓冲区<br>maxlen - 缓冲区大小 | void | 获取当前游戏描述（如战役名） |

### 视觉效果

| 函数名 | 参数 | 返回值 | 描述 |
|-------|------|-------|------|
| `L4D2_SetEntityGlow()` | entity - 实体索引<br>type - 发光类型<br>range - 发光范围<br>minRange - 最小发光范围<br>colorOverride[3] - 颜色覆盖<br>flashing - 是否闪烁 | bool | 设置实体发光效果 |
| `L4D2_SetEntityGlow_Type()` | entity - 实体索引<br>type - 发光类型 | void | 设置实体发光类型 |
| `L4D2_SetEntityGlow_Range()` | entity - 实体索引<br>range - 发光范围 | void | 设置实体发光范围 |
| `L4D2_SetEntityGlow_MinRange()` | entity - 实体索引<br>minRange - 最小发光范围 | void | 设置实体最小发光范围 |
| `L4D2_SetEntityGlow_Color()` | entity - 实体索引<br>colorOverride[3] - 颜色覆盖 | void | 设置实体发光颜色 |
| `L4D2_SetEntityGlow_Flashing()` | entity - 实体索引<br>flashing - 是否闪烁 | void | 设置实体发光闪烁状态 |
| `L4D2_GetEntityGlow_Type()` | entity - 实体索引 | L4D2GlowType | 获取实体发光类型 |
| `L4D2_GetEntityGlow_Range()` | entity - 实体索引 | int | 获取实体发光范围 |
| `L4D2_GetEntityGlow_MinRange()` | entity - 实体索引 | int | 获取实体最小发光范围 |
| `L4D2_GetEntityGlow_Flashing()` | entity - 实体索引 | bool | 获取实体发光闪烁状态 |
| `L4D2_RemoveEntityGlow()` | entity - 实体索引 | bool | 移除实体发光效果 |
| `L4D2_RemoveEntityGlow_Color()` | entity - 实体索引 | void | 移除实体发光颜色覆盖 |
| `L4D2_IsPlayerSurvivorGlowEnable()` | client - 客户端索引 | bool | 检查玩家幸存者发光是否启用 |
| `L4D2_SetPlayerSurvivorGlowState()` | client - 客户端索引<br>enabled - 是否启用 | void | 设置玩家幸存者发光状态 |
| `L4D2_CreateInstructorHint()` | name - 提示名称<br>target - 目标实体<br>caption - 标题<br>color[3] - 颜色<br>iconOnScreen - 屏幕内图标<br>iconOffScreen - 屏幕外图标<br>binding - 按键绑定<br>iconOffset - 图标偏移<br>range - 范围<br>timeout - 超时时间<br>allowNoDrawTarget - 允许不可见目标<br>noOffScreen - 无屏幕外显示<br>forceCaption - 强制显示标题<br>flags - 标志 | bool | 创建教学提示 |
| `L4D2_StopInstructorHint()` | name - 提示名称 | bool | 停止教学提示 |
| `L4D_FlashScreen()` | client - 客户端索引<br>duration - 闪光持续时间<br>alpha - 闪光透明度 | void | 使玩家屏幕闪光 |
| `L4D1_ClientInFirstPerson()` | client - 客户端索引 | bool | 检查L4D1中玩家是否处于第一人称视角（仅限L4D1） |
| `L4D2_ClientInFirstPerson()` | client - 客户端索引 | bool | 检查L4D2中玩家是否处于第一人称视角（仅限L4D2） |
| `L4D_ClientInFirstPerson()` | client - 客户端索引 | bool | 检查玩家是否处于第一人称视角（通用） |
| `L4D1_SetClientFirstPerson()` | client - 客户端索引<br>firstPerson - 是否为第一人称 | void | 设置L4D1中玩家的视角模式（仅限L4D1） |
| `L4D2_SetClientFirstPerson()` | client - 客户端索引<br>firstPerson - 是否为第一人称 | void | 设置L4D2中玩家的视角模式（仅限L4D2） |
| `L4D_SetClientFirstPerson()` | client - 客户端索引<br>firstPerson - 是否为第一人称 | void | 设置玩家的视角模式（通用） |
| `L4D1_PlayVersusWinSound()` | team - 胜利队伍 | void | 播放L4D1中的对抗模式胜利音效（仅限L4D1） |
| `L4D2_PlayVersusWinSound()` | team - 胜利队伍 | void | 播放L4D2中的对抗模式胜利音效（仅限L4D2） |
| `L4D_PlayVersusWinSound()` | team - 胜利队伍 | void | 播放对抗模式胜利音效（通用） |
| `L4D_ClearClientExplosions()` | client - 客户端索引 | void | 清除玩家的爆炸效果 |

## 动画常量

`left4dhooks_anim.inc` 文件定义了大量的动画常量，用于标识游戏中的各种动画动作。这些常量主要分为以下几类：

### L4D1_ACT_* 常量

L4D1_ACT_* 常量定义了 Left 4 Dead 1 中的各种动画动作，包括：
- 基本动作（闲置、走路、跑步、蹲伏等）
- 武器动作（装弹、瞄准、射击等）
- 特殊动作（救援、被击倒、死亡等）
- 次要武器动作（手枪、近战武器等）
- 投掷武器动作（燃烧瓶、土制炸弹等）
- 手势动作（指向、感谢等）

### L4D2_ACT_* 常量

L4D2_ACT_* 常量定义了 Left 4 Dead 2 中的各种动画动作，包括：
- 基本动作（闲置、走路、跑步、蹲伏等）
- 武器动作（手枪、步枪、霰弹枪、冲锋枪、狙击枪、榴弹发射器等）
- 近战武器动作（斧头、棒球棍、武士刀、平底锅、吉他等）
- 特殊动作（救援、被击倒、死亡、攀爬等）
- 物品交互动作（使用医疗包、止痛药、肾上腺素等）

## 注意事项

- 某些接口仅在特定游戏版本中可用（L4D1 或 L4D2），请在使用前检查兼容性
- 使用钩子时，注意返回值的含义，以正确控制游戏行为
- 对于性能敏感的功能，建议使用本地函数（native）而不是股票函数（stock）
- 在修改游戏行为时，请确保不会破坏游戏平衡或导致游戏崩溃

---
