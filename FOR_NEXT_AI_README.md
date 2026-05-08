# FOR NEXT AI — 快速上手指南

> 阅读顺序：**本文件 → PROJECT_MEMORY.md → index.html**

---

## 当前状态（2026-05-08 会话结束）

**项目**: 仙途 · 放置修仙 (xiuxian-idle)  
**版本**: v0.2.1  
**状态**: ✅ 核心循环完整，bug已修复，用户正在玩

**用户类型**: 挂机玩家。喜欢打开游戏放着、偶尔回来看。不需要操作类游戏。

---

## 今天发生了什么（极简版）

1. **v0.1** — 点击按钮修仙 → 用户：太无聊
2. **v0.2** — 加了战斗/掉落/突破演出/事件（大量bug）
3. **Bug修复** — 致命bug修了6个
4. **中途又做了两个失败尝试**：嘴替大师（问卷不是游戏）、叠塔（操作类不适合）
5. **用户最终确认**：修仙放置 v0.2.1 是对的。他就喜欢挂机。

**教训**：不要猜用户喜欢什么。直接问。本用户是挂机党，不是操作党。

---

## 如何接手

```bash
# 项目位置
cd "/mnt/c/Users/911/OneDrive/AI/project/xiuxian-idle"

# 查看历史
git log --oneline

# 在浏览器打开游戏
# 双击 index.html 或用浏览器打开它
```

---

## 代码结构速查

```
index.html (~980行)
├── <style>  CSS（暗色主题 + 粒子动画）
├── <body>   游戏UI结构
└── <script> JS游戏逻辑
    ├── 数据定义: REALMS[], SKILLS[], ENEMIES[], EVENTS[], EQUIP_POOL{}
    ├── 游戏状态: S (state对象，存档key: xx2_save)
    ├── 核心计算: qiMult(), clickMult(), btBonus(), getAtk(), btChance()
    ├── 游戏循环: tick() — 每100ms执行
    ├── 战斗系统: spawnEnemy(), attackEnemy(), killEnemy(), manualAttack(), useSkill()
    ├── 突破系统: openBreakthrough(), triggerBreakthrough()
    ├── 事件系统: triggerEvent(), resolveEvent()
    ├── UI渲染: refreshAll(), refreshHUD(), refreshPanel(), refreshSkillCD()
    └── 初始化: init() → setInterval(tick, 100)
```

---

## 调试命令（浏览器控制台）

```javascript
S                    // 查看完整状态
S.qi += 50000        // 加灵力
S.realm = 10         // 跳境界（0-23）
S.equip.weapon = EQUIP_POOL.weapon[7]  // 给诛仙剑
localStorage.removeItem('xx2_save')     // 清除存档
```

---

## 下一步做什么

**不要自己决定加什么功能。先问用户。** 用户可能在挂机过程中发现了想改进的地方，也可能想加新系统。让用户主导节奏。

如果用户没想法，可以提议：
- 装备系统完善（对比/自动替换/强化）
- 更多敌人/事件/功法
- 宗门/宠物/炼丹系统
- 后端 + 排行榜 + 微信小程序

---

> **最后更新**: 2026-05-08 (v0.2.1)
