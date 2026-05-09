# FOR NEXT AI — 快速上手指南

> 阅读顺序：**本文件 → PROJECT_MEMORY.md → index.html**

---

## 当前状态（2026-05-09 会话结束）

**项目**: 仙途 · 放置修仙 (xiuxian-idle)  
**版本**: v0.3.0 — 大境界质变版  
**状态**: ✅ 六大质变系统全部实现，用户正在玩

**用户类型**: 挂机玩家。喜欢打开游戏放着、偶尔回来看。

---

## 今天做了什么（极简版）

用户反馈 v0.2.1 核心问题：**境界升级只是改称号，玩法/装备/功法/画面全不变**。

实施的 v0.3 改造：

1. **大境界分组** — 10大境界(凡人→真仙)，每个解锁新机制
2. **灵根觉醒** — 金丹境五选一灵根(金木水火土)，永久改变玩法
3. **装备强化** — 0~+15升星系统，有爆装风险
4. **神通树** — 元婴境解锁6大神通，分支选择
5. **转世系统** — 真仙飞升重置进度但保留灵根+永久加成
6. **视觉进化** — 角色大小/颜色/光环/粒子随境界变化
7. **更多内容** — 高阶敌人、境界专属事件、鸿蒙品质装备

---

## 如何接手

```bash
# 项目位置
cd "/mnt/c/Users/911/OneDrive/AI/project/xiuxian-idle"

# 查看历史
git log --oneline

# 在浏览器打开游戏
# 双击 index.html
```

---

## 代码结构速查

```
index.html (~1400行)
├── <style>  CSS（暗色主题 + 阶段视觉 + 强化/灵根面板）
├── <body>   游戏UI（新增灵根觉醒覆盖层、解锁提示条）
└── <script> JS游戏逻辑
    ├── 数据: STAGES[], REALMS[], LINGGEN{}, SKILLS[], SHENTONG[], ENEMIES[], EQUIP_POOL{}
    ├── 游戏状态: S (存档key: xx2_save，向后兼容v0.2)
    │   新增字段: linggen, linggenChosen, prestige, prestigeBonus
    ├── 核心计算: qiMult(), getAtk(), getDef(), getCritChance(), btChance()
    ├── 新系统: chooseLinggen(), enhanceEquip(), buyShentong(), doPrestige()
    ├── 视觉: updateVisuals(), updateUnlockBar(), doStageBreakthrough()
    ├── 游戏循环: tick() — 每100ms
    └── 初始化: init() → setInterval(tick, 100)
```

---

## 调试命令（浏览器控制台）

```javascript
S                    // 查看完整状态
S.realm = 13         // 跳境界
S.qi += 50000        // 加灵力
S.linggen = 'huo'    // 设火灵根
S.linggenChosen = true
S.equip.weapon = {n:'轩辕剑',r:'mythic',a:70,enhance:10}  // 给装备
localStorage.removeItem('xx2_save')     // 清除存档
```

---

## 下一步做什么

**不要自己决定加什么功能。先问用户。**

如果用户没想法，可以提议：
- 宗门系统（单人门派管理、弟子培养）
- 炼丹/炼器系统
- 成就系统
- 更多敌人/事件/功法/神通
- 后端 + 排行榜 + 微信小程序

---

> **最后更新**: 2026-05-09 (v0.3.0)
