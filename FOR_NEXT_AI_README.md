# FOR NEXT AI — 快速上手指南

> **给接手的 AI 开发者**: 这是一份 2 分钟快速上手指南。  
> 阅读顺序：**本文件 → PROJECT_MEMORY.md → index.html**

---

## 当前状态（2026-05-08）

**项目**: 仙途 · 放置修仙  
**版本**: v0.1（网页原型阶段）  
**状态**: ✅ 核心循环可玩，需继续迭代

---

## 快速开始（3 步）

### 1. 了解项目
- 打开 `PROJECT_MEMORY.md` 了解完整背景
- 在浏览器打开 `index.html` 试玩 5 分钟
- 按 F12 打开控制台，输入 `resetGame()` 可重置进度

### 2. 关键约束
- **纯前端单文件**: 所有代码在 index.html 中，无外部依赖
- **只用 localStorage**: 无后端，无数据库
- **移动端适配**: UI 需同时支持手机和桌面
- **中文优先**: 游戏面向中国用户

### 3. 你的任务
查看 OPERATION_LOG.md 最后一节了解当前任务。如果没有明确任务，询问用户想要什么。

---

## 代码结构速查

`index.html` 分为三个 `<script>` 区域（通过注释分隔）：

```
// ===== 数据定义 =====      ← REALMS, SKILLS, EQUIPMENT_SLOTS 等配置
// ===== 游戏状态 =====       ← state 对象、loadState/ saveState
// ===== 核心计算 =====       ← getAutoQiPerSec, getClickQi 等
// ===== 操作 =====           ← cultivate, buySkill, attemptBreakthrough 等
// ===== UI 渲染 =====        ← refreshAll, refreshSkills 等
// ===== 初始化 =====         ← init()
```

修改数值 → 改"数据定义"区  
添加新系统 → 在"操作"区加函数，"UI渲染"区加面板

---

## 常用命令（在浏览器控制台执行）

```javascript
// 看当前状态
console.log(state);

// 重置游戏
resetGame();

// 加速测试：直接加灵力
state.qi += 100000;
refreshAll();

// 加速测试：直接突破到某境界（0-23）
state.realmIdx = 10;  // 筑基初期
state.exp = 0;
refreshAll();

// 解锁所有功法
SKILLS.forEach(s => state.ownedSkills.push(s.id));
refreshAll();

// 手动保存
saveState();

// 清除存档
localStorage.removeItem('xiuxian_idle_save');
```

---

## 不要做的事

- ❌ 不要引入外部框架（jQuery/Vue/React），保持零依赖
- ❌ 不要改变核心数据结构（REALMS 数组格式、state 对象键名）
- ❌ 不要删除 localStorage 存档逻辑
- ❌ 不要移除移动端适配
- ❌ 新增功能前先在 PROJECT_MEMORY.md 记录

---

## 需要帮助时

1. 搜索 `index.html` 里的中文注释，已经写得很详细
2. 查看 OPERATION_LOG.md 了解历史操作
3. 如果卡住，告诉用户具体遇到了什么问题

---

> **最后更新**: 2026-05-08
