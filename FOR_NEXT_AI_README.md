# FOR NEXT AI — 快速上手指南 (v0.2)

> **给接手的 AI 开发者**: 阅读顺序：**本文件 → PROJECT_MEMORY.md → index.html**

---

## 当前状态（2026-05-08）

**项目**: 仙途 · 放置修仙  
**版本**: v0.2（重制版，有战斗+掉落+突破演出+随机事件）  
**状态**: ✅ 核心玩法完整，可玩性大幅提升

---

## v0.2 相比 v0.1 的核心变化

| 系统 | v0.1 | v0.2 |
|------|------|------|
| 修炼 | 点按钮 | 点击角色(暴击动画) + 自动灵力粒子 |
| 战斗 | ❌ 无 | ✅ 16种敌人自动生成+战斗 |
| 掉落 | ❌ 占位 | ✅ 5级稀有度装备掉落系统 |
| 突破 | 简单弹窗 | 全屏闪电+紧张条赌博演出 |
| 事件 | ❌ 无 | ✅ 6种随机事件，2选1风险决策 |
| 粒子 | ❌ 无 | ✅ 修炼/战斗/突破三种粒子特效 |

---

## 代码结构速查

`index.html` 关键变量和函数：

```javascript
// ===== 核心数据 =====
S (state)          // 游戏状态对象
REALMS[]           // 24层境界配置 (n=名称, exp=所需经验, qi=每秒灵力, atk=攻击力, bt=突破率, cost=突破花费)
SKILLS[]           // 12种功法
ENEMIES[]          // 16种敌人 (minR=最低境界要求)
EQUIP_POOL{}       // 装备库 (weapon/armor/accessory × 5稀有度)
EVENTS[]           // 6种随机事件

// ===== 关键函数 =====
tick()             // 100ms游戏主循环
spawnEnemy()       // 生成敌人
attackEnemy(dmg)   // 攻击敌人
killEnemy()        // 击杀敌人 → 掉落判定
manualAttack()     // 点击角色
useSkill()         // ⚡技能
openBreakthrough() // 打开突破覆盖层
triggerBreakthrough() // 执行突破(3秒紧张条)
triggerEvent()     // 触发随机事件
spawnQiParticles(count) // 生成修炼粒子
```

---

## 调试命令（浏览器控制台）

```javascript
S       // 查看完整状态
S.qi += 50000       // 加灵力
S.realm = 10        // 跳境界（0-23）
S.equip.weapon = EQUIP_POOL.weapon[7]  // 给诛仙剑
S.equip.armor = EQUIP_POOL.armor[7]    // 给不灭金身
getAtk()            // 看当前攻击力
qiMult()            // 看灵力倍率
btChance()          // 看突破率
localStorage.removeItem('xx2_save')  // 清除存档
```

---

## 不要做的事

- ❌ 不要改成纯点击器（v0.2的核心价值在于非点击玩法）
- ❌ 不要移除粒子系统（这是视觉可玩性的关键）
- ❌ 不要简化突破演出（赌博感是留存的关键）
- ❌ 不要引入外部依赖

---

## 已知问题

1. iOS Safari 粒子性能未测试
2. 技能冷却显示有时延迟一帧
3. 突破 UI 在超小屏幕(<320px)可能溢出
4. 没有音效（可考虑 Web Audio API 简单音效）

---

> **最后更新**: 2026-05-08 (v0.2)
