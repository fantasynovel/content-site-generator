# Component Guide — Content Site Generator 組件參考

> 本文件記錄了 `index.html` 中所有可重複使用的 CSS 組件與 HTML 結構。
> **設計風格**：UED AI 簡報風格（藍紫漸層封面、白色內容頁、彩色卡片、橫向長條圖、Ranking、Timeline）。

---

## 目錄

1. [Slide 結構](#1-slide-結構)
2. [排版組件](#2-排版組件)
3. [重點標註](#3-重點標註)
4. [流程圖](#4-流程圖)
5. [表格](#5-表格)
6. [資訊框](#6-資訊框)
7. [統計卡片](#7-統計卡片)
8. [分段橫幅](#8-分段橫幅)
9. [圖表區塊](#9-圖表區塊)
10. [徽章標籤](#10-徽章標籤)
11. [藥丸狀標籤](#11-藥丸狀標籤)
12. [高亮工具](#12-高亮工具)
13. [大號數字](#13-大號數字)
14. [檢查清單](#14-檢查清單)
15. [圖片嵌入](#15-圖片嵌入)
16. [版面寬度切換](#16-版面寬度切換)
17. [Mermaid 互動式圖表](#17-mermaid-互動式圖表)
18. [Mermaid 點擊放大全螢幕](#18-mermaid-點擊放大全螢幕)
19. [UED 封面版型](#19-ued-封面版型)
20. [UED Accent Bar 標題](#20-ued-accent-bar-標題)
21. [UED 卡片系統](#21-ued-卡片系統)
22. [雙欄佈局 two-col](#22-雙欄佈局-two-col)
23. [三欄佈局 three-col](#23-三欄佈局-three-col)
24. [橫向長條圖 bar-chart](#24-橫向長條圖-bar-chart)
25. [Ranking 排行版型](#25-ranking-排行版型)
26. [Timeline 時間軸](#26-timeline-時間軸)
27. [UED 徽章 badge 系統](#27-ued-徽章-badge-系統)
28. [章節過渡頁 section-header](#28-章節過渡頁-section-header)
29. [版型選擇指引](#29-版型選擇指引)

---

## 1. Slide 結構

### 用途
定義單一頁面容器。每個 slide 獨立顯示，通過 JavaScript 切換。

### 基本結構

```html
<!-- Slide 容器 (需要給予 active class 才能顯示) -->
<div class="slide active" data-title="頁面標題" data-num="01">
  <div class="slide-card">
    <!-- 所有內容放在這裡 -->
  </div>
</div>

<!-- 非活躍的 slide -->
<div class="slide" data-title="另一頁面" data-num="02">
  <div class="slide-card">
    <!-- 內容 -->
  </div>
</div>
```

### Attributes

| 屬性 | 用途 |
|------|------|
| `data-title` | 在側邊欄導覽顯示的標題 |
| `data-num` | 幻燈片編號（格式：01, 02, 等） |
| `active` class | 加上此 class 才會顯示該 slide |

### 全屏模式適應

```html
<!-- .slide 會根據 body.fullscreen 自動適應尺寸 -->
<div class="slide active" data-title="..." data-num="...">
  <div class="slide-card">
    <!-- 在全屏模式下自動放大字體 -->
  </div>
</div>
```

---

## 2. 排版組件

### 標題層級

```html
<h2>主標題（Slide 大標題）</h2>
<!-- 字體：1.6rem，權重 700 -->

<h3>副標題（Section 標題）</h3>
<!-- 字體：1.15rem，權重 700 -->

<h4>小標題（Subsection）</h4>
<!-- 字體：1rem，權重 600 -->

<p>一般段落文本</p>
<!-- 字體：0.92rem，顏色 #424245 -->
```

### Subtitle（副標題說明）

```html
<div class="subtitle">Chapter 01 — 運作原則與兩層 AI 架構</div>
<!-- 字體：0.9rem，顏色 #86868b，有下邊框 -->
```

### 列表

```html
<!-- 無序列表 -->
<ul>
  <li>項目 1</li>
  <li>項目 2</li>
</ul>

<!-- 有序列表 -->
<ol>
  <li>第一步</li>
  <li>第二步</li>
</ol>
```

### 粗體與強調

```html
<p>這是 <strong>粗體</strong> 文本。</p>

<p>這是 <span class="hl-blue">藍色高亮</span> 文本。</p>
```

---

## 3. 重點標註

### .key-point — 重點呼籲框

**用途**：突出重要概念或原則。

**樣式**：漸變背景（藍-紫），圓角邊框，1.05rem 字體。

```html
<div class="key-point">
  本團隊採用顛覆傳統的運作模式：<strong>AI 為主，人為輔</strong>。
  人類成員的核心工作不是親手執行任務，而是<span class="bg-blue">操作 AI</span> + <span class="bg-green">驗證產出</span>。
</div>
```

### 變體

```html
<!-- 中等大小 (較小的 key-point) -->
<div class="key-point" style="font-size:0.95rem;">
  需求文件一出來，所有 function 同時啟動，不互等。<br>
  <span style="font-size:0.85rem; color:#636366;">未確定的部分由 AI 生成 <span class="bg-purple">mock</span> 或預留區塊。</span>
</div>

<!-- 置中顯示 -->
<div class="key-point" style="font-size:1.1rem; text-align:center;">
  <strong>需求文件一出來，所有 function 同時啟動，不互等。</strong><br>
  <span style="font-size:0.9rem; color:#636366;">詳細說明文字</span>
</div>
```

---

## 4. 流程圖

### .flow + .flow-step — 線性流程

**用途**：展示序列步驟或決策流程。

**基本結構**：

```html
<div class="flow">
  <span class="flow-step">步驟 1</span>
  <span class="flow-arrow">→</span>
  <span class="flow-step">步驟 2</span>
  <span class="flow-arrow">→</span>
  <span class="flow-step">步驟 3</span>
</div>
```

### 帶顏色的流程步驟

```html
<div class="flow">
  <span class="flow-step blue">Claude Code</span>
  <span class="flow-arrow">·</span>
  <span class="flow-step purple">Copilot</span>
  <span class="flow-arrow">·</span>
  <span class="flow-step green">Gitea + TFS</span>
  <span class="flow-arrow">·</span>
  <span class="flow-step orange">Notion + Trello</span>
</div>
```

### 流程步驟的顏色變體

| Class | 背景色 | 文字色 |
|-------|--------|--------|
| `.flow-step.blue` | #e8f0fe | #0066cc |
| `.flow-step.green` | #e6f9f0 | #00875a |
| `.flow-step.orange` | #fff3e0 | #e67700 |
| `.flow-step.purple` | #f3e8ff | #7b2ff7 |

```html
<div class="flow">
  <span class="flow-step orange">人操作 AI</span>
  <span class="flow-arrow">→</span>
  <span class="flow-step blue">AI 執行</span>
  <span class="flow-arrow">→</span>
  <span class="flow-step green">人驗證</span>
</div>
```

### 多行流程（垂直排列）

```html
<div class="flow" style="flex-direction: column; align-items: flex-start; gap: 12px;">
  <div style="width: 100%; display: flex; align-items: center; gap: 8px;">
    <span class="flow-step orange" style="white-space: nowrap;">1. PM 在 Notion 寫 PRD</span>
    <span class="flow-arrow">→</span>
    <span class="flow-step blue" style="white-space: nowrap;">2. Claude Cowork 讀取</span>
    <span class="flow-arrow">→</span>
    <span class="flow-step green" style="white-space: nowrap;">3. Claude 產出 SDD Spec</span>
  </div>
  <div style="width: 100%; display: flex; align-items: center; gap: 8px;">
    <span class="flow-step purple" style="white-space: nowrap;">4. 存回 Notion</span>
    <span class="flow-arrow">→</span>
    <span class="flow-step orange" style="white-space: nowrap;">5. RD 讀 Spec 生成代碼</span>
  </div>
</div>
```

---

## 5. 表格

### .table-wrap + table — 標準表格

**用途**：結構化展示數據。

**基本結構**：

```html
<div class="table-wrap">
  <table>
    <thead>
      <tr>
        <th>欄位 1</th>
        <th>欄位 2</th>
        <th>欄位 3</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>資料 1.1</td>
        <td>資料 1.2</td>
        <td>資料 1.3</td>
      </tr>
      <tr>
        <td>資料 2.1</td>
        <td>資料 2.2</td>
        <td>資料 2.3</td>
      </tr>
    </tbody>
  </table>
</div>
```

### 帶顏色的表格行

使用 `.row-{color}` 在行首添加左邊框，色碼對應流程步驟。

```html
<div class="table-wrap">
  <table>
    <thead>
      <tr><th>角色</th><th>說明</th></tr>
    </thead>
    <tbody>
      <tr class="row-blue">
        <td><span class="hl-blue">PM</span></td>
        <td>需求管理與排程</td>
      </tr>
      <tr class="row-purple">
        <td><span class="hl-purple">Design</span></td>
        <td>UI/UX 設計</td>
      </tr>
      <tr class="row-green">
        <td><span class="hl-green">RD</span></td>
        <td>程式碼開發</td>
      </tr>
      <tr class="row-orange">
        <td><span class="hl-orange">QA</span></td>
        <td>測試與品質</td>
      </tr>
      <tr class="row-red">
        <td><span class="hl-red">Urgent</span></td>
        <td>高優先緊急項目</td>
      </tr>
    </tbody>
  </table>
</div>
```

### 表格行顏色列表

| Class | 左邊框顏色 | 適用場景 |
|-------|-----------|---------|
| `.row-blue` | #0066cc | 藍色主題 / 工具層 |
| `.row-green` | #00875a | 綠色主題 / 成功狀態 |
| `.row-orange` | #e67700 | 橙色主題 / 警告 |
| `.row-purple` | #7b2ff7 | 紫色主題 / AI Member |
| `.row-red` | #d1242f | 紅色主題 / 高優先 |

### 複雜表格範例

```html
<div class="table-wrap">
  <table>
    <thead>
      <tr>
        <th>項目</th>
        <th>說明</th>
        <th>類型</th>
      </tr>
    </thead>
    <tbody>
      <tr class="row-blue">
        <td><strong>Claude Code</strong></td>
        <td>主力 AI 開發引擎</td>
        <td><span class="pill pill-blue">Max</span></td>
      </tr>
      <tr class="row-green">
        <td><strong>Gitea</strong></td>
        <td>自架 Git Server</td>
        <td><span class="pill pill-green">版控</span></td>
      </tr>
      <tr class="row-orange">
        <td><strong>Notion</strong></td>
        <td>文件管理中心</td>
        <td><span class="pill pill-orange">文檔</span></td>
      </tr>
    </tbody>
  </table>
</div>
```

---

## 6. 資訊框

### .info-box — 藍色資訊框

**用途**：補充說明或提示訊息。

**基本結構**：

```html
<div class="info-box">
  <strong>Tech Lead 不是額外的人</strong>。Tech Lead 是由一位資深 RD <strong>兼任</strong>的角色，主要職責是：
  <ul style="margin-top: 8px; margin-bottom: 0;">
    <li>在需求分析階段與 PM 討論技術可行性</li>
    <li>設定 App Development Skill 和架構規範</li>
    <li>進行高階 Code Review 與架構把關</li>
  </ul>
</div>
```

### .info-box.warn — 橙色警告框

**用途**：警告或重要注意事項。

```html
<div class="info-box warn">
  <strong>重要原則：</strong>AI 產出的 code 一律經過 PR 流程，不允許直推 main/develop。
</div>
```

### 帶背景色的資訊框

```html
<div class="info-box" style="background: #f0f5ff; border-left-color: #0066cc;">
  <strong>AI Member 看得到所有資訊流，但碰不到任何 source code。</strong><br>
  這是刻意的設計：AI Member 是「資訊整合者」和「監督者」，不是「開發者」。
</div>
```

---

## 7. 統計卡片

### .stat-row + .stat-card — 統計卡片組

**用途**：展示關鍵數字或指標。

**基本結構**：

```html
<div class="stat-row">
  <div class="stat-card">
    <div class="stat-value hl-blue">6+1</div>
    <div class="stat-label">人 + AI Member</div>
  </div>
  <div class="stat-card">
    <div class="stat-value hl-purple">SDD</div>
    <div class="stat-label">Spec-Driven Dev</div>
  </div>
  <div class="stat-card">
    <div class="stat-value hl-green">6</div>
    <div class="stat-label">Claude Code 席位</div>
  </div>
  <div class="stat-card">
    <div class="stat-value hl-orange">14</div>
    <div class="stat-label">文件章節</div>
  </div>
</div>
```

### 卡片樣式

| 屬性 | 說明 |
|------|------|
| `.stat-value` | 大號數字（1.8rem），支援顏色 class（`.hl-blue` 等） |
| `.stat-label` | 小號說明（0.78rem），灰色文字 |
| `.stat-row` | 容器，自動換行 |

### 置中排列

```html
<div class="stat-row" style="justify-content:center; max-width:660px; margin:0 auto 40px;">
  <!-- 卡片內容 -->
</div>
```

---

## 8. 分段橫幅

### .section-banner — 漸變橫幅

**用途**：視覺化分割不同段落，突出新章節。

**基本結構**：

```html
<div class="section-banner">
  <h3>AI 執行層</h3>
  <p>核心生產力引擎 — 3 Max + 3 Pro 席位</p>
</div>
```

### 顏色變體

| Class | 漸變色 |
|-------|--------|
| `.section-banner` (default) | 藍 → 紫 (#0066cc → #7b2ff7) |
| `.section-banner.green` | 綠 → 亮綠 (#00875a → #00b894) |
| `.section-banner.orange` | 橙 → 淺橙 (#e67700 → #f0a500) |
| `.section-banner.purple` | 紫 → 淺紫 (#7b2ff7 → #a855f7) |
| `.section-banner.red` | 紅 → 淺紅 (#d1242f → #e55b5b) |

### 使用範例

```html
<!-- 綠色橫幅 -->
<div class="section-banner green">
  <h3>協作與管理層</h3>
  <p>Notion + Trello + Mattermost</p>
</div>

<!-- 紫色橫幅 -->
<div class="section-banner purple">
  <h3>設計層</h3>
  <p>Figma + Axure RP</p>
</div>

<!-- 橙色橫幅 -->
<div class="section-banner orange">
  <h3>版控與 CI/CD</h3>
  <p>Gitea + Gitea Actions + TFS</p>
</div>

<!-- 紅色橫幅 -->
<div class="section-banner red">
  <h3>QA 初始任務</h3>
  <p>測試管理 + AI 品質驗證標準</p>
</div>
```

---

## 9. 圖表區塊

### .diagram — 黑色代碼/圖表區塊

**用途**：展示 ASCII 圖表、架構圖、程式碼片段。

**樣式**：深色背景（#1d1d1f），等寬字體，固定寬度行。

```html
<div class="diagram">                    ┌──────────┐
                    │  Notion  │ ← 知識庫 / 文件中心
                    └────┬─────┘
                         │
┌──────────┐      ┌──────┴──────┐      ┌──────────┐
│  Trello  │ ←──→ │  AI Member  │ ←──→ │Mattermost│
│(任務看板) │      │ (資訊中樞)   │      │(即時通訊) │
└──────────┘      └──────┬──────┘      └──────────┘
                         │
          ┌──────────────┼──────────────┬──────────────┐
          ↓              ↓              ↓              ↓
   ┌────────────┐ ┌────────────┐ ┌───────────┐ ┌──────────┐
   │Claude Code │ │  Figma /   │ │ Gitea/TFS │ │OnePage   │
   │+ Copilot   │ │ Axure RP   │ │ (版控+CI) │ │(分享)    │
   │(AI 開發)   │ │ (設計)      │ │           │ └──────────┘
   └────────────┘ └────────────┘ └───────────┘</div>
```

### 多行代碼或清單

```html
<div class="diagram">Day 0  ｜ Kick-off
       ├─ PM 用 Claude Code 產出 User Story / AC
       ├─ 全員確認工具環境已就位
       └─ AI Member 建立 Notion 專案頁面 + Mattermost channel

Day 1  ｜ Sprint Planning
       ├─ PM 帶著 AI 產出的 User Story 開 Planning
       ├─ RD 用 Claude Code 做技術估點
       ├─ AI Member 記錄會議 → Notion → Trello
       └─ Design 用 Figma/Axure 產出簡易設計稿</div>
```

### 樹狀結構

```html
<div class="diagram">📚 知識庫（Knowledge Base）
├── 📋 PRD & 需求
│   ├─ [Database] 功能需求庫
│   ├─ [DB] SDD Spec 模板版本
│   └─ [Page] 最新 Spec 編輯中
├── 🎨 Design
│   ├─ [DB] Design Token 庫
│   ├─ [Page] UI Kit / 設計規範
│   └─ [Page] Figma 連結與版本管理
├── 💻 Architecture & Code
│   ├─ [Page] App Development Skill
│   ├─ [DB] 架構決策記錄（ADR）
│   └─ [Page] API 契約文件
├── 🧪 QA & Test
│   ├─ [DB] Test Case 庫
│   ├─ [DB] Bug 回報追蹤
│   └─ [Page] 測試報告彙總
└── 📊 AI Member & 運作
    ├─ [DB] 日報記錄
    ├─ [Page] 每日工作流程
    ├─ [Page] Scrum 儀式會議紀錄
    └─ [Page] 團隊指標儀表板</div>
```

---

## 10. 徽章標籤

### .badge — 優先級徽章

**用途**：標示優先級或狀態。

**樣式**：小圓角背景，0.72rem 字體。

```html
<td><span class="badge high">高</span></td>
<td><span class="badge mid">中</span></td>
<td><span class="badge low">低</span></td>
```

### 徽章顏色

| Class | 背景色 | 文字色 | 用途 |
|-------|--------|--------|------|
| `.badge.high` | #fee | #c00 | 高優先 |
| `.badge.mid` | #fff5e6 | #e67700 | 中優先 |
| `.badge.low` | #f0f5ff | #0066cc | 低優先 |

### 在表格中使用

```html
<tr>
  <td>P1</td>
  <td>學會用 Claude Cowork 做需求管理</td>
  <td><span class="badge high">高</span></td>
</tr>
```

---

## 11. 藥丸狀標籤

### .pill + 色彩變體 — 標籤類型

**用途**：標記工具、技術棧或分類。

**樣式**：4px 上下邊距，14px 左右邊距，圓角 20px。

```html
<span class="pill pill-blue">Claude Code</span>
<span class="pill pill-green">Notion</span>
<span class="pill pill-orange">Trello</span>
<span class="pill pill-purple">AI Member</span>
<span class="pill pill-red">Critical</span>
<span class="pill pill-gray">Optional</span>
```

### 藥丸顏色

| Class | 背景色 | 文字色 |
|-------|--------|--------|
| `.pill-blue` | #e8f0fe | #0066cc |
| `.pill-green` | #e6f9f0 | #00875a |
| `.pill-orange` | #fff3e0 | #e67700 |
| `.pill-purple` | #f3e8ff | #7b2ff7 |
| `.pill-red` | #ffeef0 | #d1242f |
| `.pill-gray` | #f0f0f2 | #636366 |

### 在表格中使用

```html
<tr>
  <td>RD-iOS</td>
  <td><span class="pill pill-gray">MacBook</span></td>
  <td>Xcode 僅在 macOS 上運行（必須）</td>
</tr>
```

### 大型藥丸（自訂樣式）

```html
<span class="pill pill-blue" style="font-size:0.85rem; padding:6px 18px;">
  Pilot-S：1 週 / 簡單功能
</span>
<span class="pill pill-purple" style="font-size:0.85rem; padding:6px 18px;">
  Pilot-M：2 週 / 中等複雜度
</span>
```

---

## 12. 高亮工具

### 內聯高亮 — .hl-{color}

**用途**：強調文字顏色而不改變背景。

**樣式**：粗體，顏色變化。

```html
<span class="hl-blue">藍色高亮</span>
<span class="hl-green">綠色高亮</span>
<span class="hl-orange">橙色高亮</span>
<span class="hl-purple">紫色高亮</span>
<span class="hl-red">紅色高亮</span>
```

### 背景高亮 — .bg-{color}

**用途**：帶有背景色的高亮，更顯眼。

**樣式**：淺色背景 + 深色文字，自動圓角。

```html
<span class="bg-blue">主題藍</span>
<span class="bg-green">主題綠</span>
<span class="bg-orange">主題橙</span>
<span class="bg-purple">主題紫</span>
<span class="bg-red">主題紅</span>
```

### 在段落中混合使用

```html
<p>
  本團隊採用顛覆傳統的運作模式：<strong>AI 為主，人為輔</strong>。
  人類成員的核心工作不是親手執行任務，而是<span class="bg-blue">操作 AI</span>
  + <span class="bg-green">驗證產出</span>。
</p>
```

### 在標題中使用

```html
<h2 style="background: linear-gradient(135deg, #0066cc, #7b2ff7);
           -webkit-background-clip: text;
           -webkit-text-fill-color: transparent;">
  AI Scrum Team 建置計畫
</h2>
```

---

## 13. 大號數字

### .big-num — 超大數字

**用途**：展示重要的大型指標或數字。

**樣式**：2.4rem 字體，權重 800，字間距 -0.03em。

```html
<div class="big-num">6+1</div>

<div class="stat-value hl-blue">6+1</div>
<!-- 或在統計卡片中搭配 .hl-{color} -->
```

### .medium-text — 中號文字

**用途**：標準強調文字。

**樣式**：1.1rem 字體。

```html
<p class="medium-text">這是中等大小的強調文字。</p>
```

---

## 14. 檢查清單

### .checklist + .checked — 待辦清單

**用途**：展示可檢查的清單項目，支援已完成狀態。

**基本結構**：

```html
<ul class="checklist">
  <li class="checked">已完成的項目</li>
  <li>未完成的項目</li>
  <li>另一個待做項目</li>
</ul>
```

### 樣式說明

- `.checklist` = 無序列表，移除預設標籤
- `li::before` = 自訂複選框（初始狀態：淺灰邊框）
- `li.checked::before` = 已勾選（深藍背景 + 白色✓）

### 實際範例

```html
<ul class="checklist">
  <li class="checked">AI Member 具體職責清單 → 見 Chapter 12</li>
  <li>Scrum 流程細節與 AI 參與方式</li>
  <li>資訊流設計與 Notion 同步機制</li>
  <li class="checked">SDD Spec 模板正式版</li>
  <li>Pilot-S / Pilot-M 的實際需求選定</li>
</ul>
```

### 帶搜索的檢查清單

```html
<ul class="checklist">
  <li class="checked">✓ Design 看完 Spec 後，能用 AI 生成 wireframe</li>
  <li class="checked">✓ App RD 看完 Spec 後，能用 AI 生成頁面骨架 + mock data</li>
  <li class="checked">✓ Backend RD 看完 Spec 後，能用 AI 生成 API 骨架 + mock response</li>
  <li class="checked">✓ QA 看完 Spec 後，能用 AI 生成 test case 初版</li>
</ul>
```

---

## 15. 圖片嵌入

> **重要**：所有 `<img>` 標籤一律加上 `class="zoomable"`，啟用點擊放大（lightbox）功能。唯一例外是 lightbox overlay 自身的 `<img id="lightboxImg">`。

### 基本圖片嵌入

```html
<img class="zoomable" src="/path/to/image.png" alt="描述文字" style="max-width: 100%; height: auto; margin: 20px 0; border-radius: 10px;">
```

### 圖片搭配說明

```html
<figure style="margin: 20px 0; text-align: center;">
  <img class="zoomable" src="/path/to/screenshot.png" alt="系統架構圖" style="max-width: 100%; border-radius: 10px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
  <figcaption style="font-size: 0.85rem; color: #86868b; margin-top: 8px;">
    圖片說明：展示 AI-First Scrum Team 架構
  </figcaption>
</figure>
```

### 響應式圖片容器

```html
<div style="max-width: 600px; margin: 20px auto;">
  <img class="zoomable" src="/path/to/image.png" alt="描述" style="width: 100%; height: auto; display: block; border-radius: 12px;">
</div>
```

### 圖片在側邊排列

```html
<div style="display: flex; gap: 20px; align-items: flex-start; margin: 20px 0;">
  <img class="zoomable" src="/path/to/image.png" alt="描述" style="width: 300px; height: auto; border-radius: 10px; flex-shrink: 0;">
  <div>
    <h4>圖片旁邊的文字標題</h4>
    <p>詳細說明文字可以放在這裡...</p>
  </div>
</div>
```

### Lightbox 點擊放大機制

HTML template 已內建完整的 lightbox 機制（CSS + JS + overlay HTML），包含：

- `.zoomable` class：`cursor: zoom-in` + hover 透明度變化
- 點擊後開啟全畫面遮罩並顯示放大圖片
- 右上角關閉按鈕 + 點擊遮罩關閉 + `Esc` 鍵關閉

只需在 `<img>` 加上 `class="zoomable"` 即可啟用，無需額外撰寫 CSS 或 JavaScript。

---

## 組合使用範例

### 完整的功能區塊

```html
<div class="slide-card">
  <h2>標題</h2>
  <div class="subtitle">說明文字 — 時間或版本</div>

  <!-- 重點標註 -->
  <div class="key-point">
    核心要點說明
  </div>

  <!-- 流程圖 -->
  <div class="flow">
    <span class="flow-step blue">步驟 1</span>
    <span class="flow-arrow">→</span>
    <span class="flow-step green">步驟 2</span>
  </div>

  <!-- 分段橫幅 -->
  <div class="section-banner">
    <h3>子段落標題</h3>
    <p>段落說明</p>
  </div>

  <!-- 表格 -->
  <div class="table-wrap">
    <table>
      <thead>
        <tr>
          <th>欄 1</th>
          <th>欄 2</th>
        </tr>
      </thead>
      <tbody>
        <tr class="row-blue">
          <td><span class="hl-blue">項目 A</span></td>
          <td><span class="pill pill-blue">標籤</span></td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- 資訊框 -->
  <div class="info-box">
    補充說明文字
  </div>
</div>
```

### 統計與視覺化區塊

```html
<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin: 20px 0;">
  <div style="padding: 16px 20px; border-radius: 10px; background: #f0f5ff; border: 1px solid #d6e4ff;">
    <div class="hl-blue" style="margin-bottom: 4px;">指標名稱</div>
    <div style="font-size: 0.82rem; color: #636366;">描述文字</div>
  </div>
  <div style="padding: 16px 20px; border-radius: 10px; background: #e6f9f0; border: 1px solid #b7ebd8;">
    <div class="hl-green" style="margin-bottom: 4px;">另一個指標</div>
    <div style="font-size: 0.82rem; color: #636366;">描述文字</div>
  </div>
</div>
```

---

## CSS 色彩系統參考

### 主色系

| 名稱 | 深色 | 淺色 | 背景 |
|------|------|------|------|
| 藍色 | #0066cc | 淺藍 | #e8f0fe / #f0f5ff |
| 綠色 | #00875a | 淺綠 | #e6f9f0 |
| 橙色 | #e67700 | 淺橙 | #fff3e0 |
| 紫色 | #7b2ff7 | 淺紫 | #f3e8ff |
| 紅色 | #d1242f | 淺紅 | #ffeef0 |

### 灰色系

| 用途 | 色碼 |
|------|------|
| 文字主色 | #1d1d1f |
| 文字次色 | #636366 |
| 文字弱色 | #86868b |
| 邊框 | #e5e5e7 |
| 淺灰背景 | #f5f5f7 |
| 更淺灰背景 | #fafafa |

---

## 全屏模式特殊考慮

在全屏模式下（`body.fullscreen` class），以下元素會自動放大：

```css
body.fullscreen .slide-card h2 { font-size: 2.2rem; }
body.fullscreen .slide-card h3 { font-size: 1.3rem; }
body.fullscreen .slide-card p,
body.fullscreen .slide-card li { font-size: 1rem; }
body.fullscreen .diagram { font-size: 0.88rem; }
body.fullscreen .stat-card .stat-value { font-size: 2.2rem; }
```

建議在設計大量文字或圖表的 slide 時，預留全屏模式的額外空間。

---

## 響應式設計提示

### 移動設備適應（768px 以下）

```css
@media (max-width: 768px) {
  .sidebar { transform: translateX(-100%); }
  .main { margin-left: 0; }
  .slide-card { padding: 28px 24px; }
  .flow { flex-wrap: wrap; }
  .stat-row { flex-direction: column; }
}
```

### 自訂響應式佈局建議

```html
<!-- 桌面版：2 欄 -->
<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
  <!-- 內容 -->
</div>

<!-- 或使用 flex wrap -->
<div style="display: flex; gap: 20px; flex-wrap: wrap;">
  <!-- 內容 -->
</div>
```

---

## 複製黏貼快速範本

### 新增 Slide 範本

```html
<div class="slide" data-title="新頁面" data-num="99">
  <div class="slide-card">
    <h2>頁面標題</h2>
    <div class="subtitle">Chapter XX — 副標題說明</div>

    <h3>第一個小節</h3>
    <p>內容段落...</p>

    <h3>第二個小節</h3>
    <div class="table-wrap">
      <table>
        <thead><tr><th>欄位</th><th>說明</th></tr></thead>
        <tbody>
          <tr><td>項目</td><td>描述</td></tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
```

### 完整頁面框架

```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>頁面標題</title>
  <style>
    /* 從 index.html 複製 CSS */
  </style>
</head>
<body>
  <div class="slide-area">
    <div class="slide active" data-title="..." data-num="01">
      <div class="slide-card">
        <!-- 內容 -->
      </div>
    </div>
  </div>
</body>
</html>
```

---

## 16. 版面寬度切換

### .width-toggle — 內容寬度切換控制

**用途**：讓使用者在閱讀模式下切換內容區域寬度，適應不同螢幕大小與閱讀偏好。

**三種寬度模式**：

| 按鈕 | Body Class | Slide max-width | 適用場景 |
|------|-----------|----------------|---------|
| 中 | `width-mid` | 860px | 文字為主的章節，提升閱讀舒適度 |
| 大 | `width-lg` | 1200px | 表格、流程圖等需要較寬空間的內容 |
| Full | `width-full` | 100% | 全寬顯示，適合大型圖表或寬表格 |

### HTML 結構

寬度切換控制放在 topbar 的 `.nav-arrows` 區域內，位於前後頁按鈕的左側：

```html
<div class="nav-arrows">
  <div class="width-toggle" id="widthToggle">
    <button data-width="mid" title="適中寬度 (860px)">中</button>
    <button data-width="lg" title="寬版 (1200px)">大</button>
    <button data-width="full" class="active" title="全寬">Full</button>
  </div>
  <button id="prevBtn" onclick="prevSlide()">&#8592;</button>
  <button id="nextBtn" onclick="nextSlide()">&#8594;</button>
  <button class="fullscreen-btn" onclick="toggleFullscreen()">&#9654;</button>
</div>
```

### CSS 樣式

```css
/* ── Width Toggle ── */
.width-toggle {
  display: flex;
  align-items: center;
  gap: 2px;
  background: #f5f5f7;
  border-radius: 8px;
  padding: 2px;
  margin-right: 8px;
}
.width-toggle button {
  padding: 4px 12px;
  border: none;
  border-radius: 6px;
  background: transparent;
  cursor: pointer;
  font-size: 0.75rem;
  font-weight: 500;
  color: #86868b;
  transition: all 0.2s;
  white-space: nowrap;
}
.width-toggle button:hover {
  color: #1d1d1f;
}
.width-toggle button.active {
  background: #fff;
  color: #0066cc;
  font-weight: 600;
  box-shadow: 0 1px 3px rgba(0,0,0,0.08);
}
body.fullscreen .width-toggle { display: none; }

/* Content width modes */
body.width-mid .slide { max-width: 860px; }
body.width-lg .slide { max-width: 1200px; }
body.width-full .slide { max-width: 100%; }
```

### JavaScript

```javascript
// ── Content width toggle ──
(function initWidthToggle() {
  const saved = localStorage.getItem('contentWidth') || 'full';
  setContentWidth(saved);
  document.getElementById('widthToggle').addEventListener('click', function(e) {
    const btn = e.target.closest('button[data-width]');
    if (!btn) return;
    setContentWidth(btn.dataset.width);
  });
})();

function setContentWidth(mode) {
  document.body.classList.remove('width-mid', 'width-lg', 'width-full');
  document.body.classList.add('width-' + mode);
  document.querySelectorAll('#widthToggle button').forEach(function(b) {
    b.classList.toggle('active', b.dataset.width === mode);
  });
  localStorage.setItem('contentWidth', mode);
}
```

### 行為特性

- **持久化**：使用 `localStorage` 記住使用者的選擇，跨頁面重載保持一致
- **預設值**：預設為 `full`（全寬），若 localStorage 無記錄則套用此預設
- **全螢幕自動隱藏**：進入 fullscreen 簡報模式時，寬度切換按鈕自動隱藏（全螢幕固定 100%）
- **Active 狀態**：當前選中的按鈕以白底藍字 + 陰影突顯

### 自訂預設寬度

若需更改預設寬度（例如預設為「中」），調整 JavaScript 中的 fallback 值：

```javascript
const saved = localStorage.getItem('contentWidth') || 'mid'; // 改為 'mid' 或 'lg'
```

同時更新 HTML 中的 `class="active"` 位置：

```html
<button data-width="mid" class="active" title="適中寬度 (860px)">中</button>
<button data-width="lg" title="寬版 (1200px)">大</button>
<button data-width="full" title="全寬">Full</button>
```

---

---

## 17. Mermaid 互動式圖表

### 用途

用於**架構圖**類型的內容：系統架構、元件關係、流程圖（含決策分支）、甘特圖、序列圖。不適用於純文字清單、樹狀結構或少於 3 步的簡單步驟（這些應使用 `.diagram`）。

### 何時使用 Mermaid vs .diagram

| 使用 Mermaid（`.mermaid-wrap`） | 使用 `.diagram`（ASCII 文字） |
|-------------------------------|---------------------------|
| 系統架構圖（元件關係與層級） | 純文字時間軸 / 時程列表 |
| 流程圖（決策與步驟走向） | 樹狀目錄結構 |
| Gantt 甘特圖 | 簡單步驟列表（< 3 步） |
| 序列圖（系統間互動） | 表格式比較 |

### 基本結構

```html
<div class="mermaid-wrap">
  <div class="mermaid">
graph TD
  A[Component A] --> B[Component B]
  B --> C[Component C]
  </div>
  <div class="mermaid-label">▲ 圖表標題</div>
</div>
```

### CSS 樣式

```css
/* ── Mermaid ── */
.mermaid-wrap {
  background: #f8f9fa;
  border: 1px solid #e5e5e7;
  border-radius: 10px;
  padding: 24px 16px;
  margin: 16px 0 24px;
  overflow-x: auto;
}
.mermaid-wrap .mermaid {
  width: 100%;
  min-height: 200px;
}
.mermaid-wrap .mermaid svg {
  width: 100% !important;
  max-width: 100%;
  height: auto !important;
  min-height: 200px;
}
.mermaid-label {
  font-size: 0.72rem;
  color: #86868b;
  text-align: right;
  margin-top: 6px;
}

/* 全螢幕模式 */
body.fullscreen .mermaid-wrap {
  max-width: 100%;
  padding: 32px 24px;
}
body.fullscreen .mermaid-wrap svg {
  min-height: 400px;
  max-height: 70vh;
}
```

### 支援的圖表類型

**Flowchart（流程圖 / 架構圖）**
```html
<div class="mermaid-wrap">
  <div class="mermaid">
graph TD
  HW[Mac Mini] --> SUP[Supervisor Agent]
  SUP --> A[Agent A]
  SUP --> B[Agent B]
  SUP --> C[Agent C]

  classDef blue fill:#e8f0fe,stroke:#0066cc,color:#1d1d1f
  classDef purple fill:#f3e8ff,stroke:#7b2ff7,stroke-width:2px,color:#1d1d1f
  class HW blue
  class SUP purple
  class A,B,C blue
  </div>
  <div class="mermaid-label">▲ Multi-Agent 架構</div>
</div>
```

**Flowchart LR（左到右流程）**
```html
<div class="mermaid-wrap">
  <div class="mermaid">
flowchart LR
  START((Start)) --> A[Step 1]
  A --> B[Step 2]
  B --> C{Decision}
  C -- Yes --> D[Result A]
  C -- No --> E[Result B]
  </div>
</div>
```

**Gantt（甘特圖）**
```html
<div class="mermaid-wrap">
  <div class="mermaid">
gantt
  title Project Timeline
  dateFormat HH:mm
  axisFormat %H:%M
  section Phase 1
    Task A        :active, a1, 09:00, 60min
  section Phase 2
    Task B        :a2, 10:00, 120min
    Task C        :a3, 10:00, 120min
  section Phase 3
    Task D        :a4, 12:00, 60min
  </div>
  <div class="mermaid-label">▲ 時程甘特圖</div>
</div>
```

**Sequence Diagram（序列圖）**
```html
<div class="mermaid-wrap">
  <div class="mermaid">
sequenceDiagram
  participant U as User
  participant A as API
  participant DB as Database
  U->>A: Request
  A->>DB: Query
  DB-->>A: Result
  A-->>U: Response
  </div>
</div>
```

### 撰寫規則（踩坑紀錄）

這些規則來自實際踩坑經驗，違反時會造成 SVG 渲染失敗：

1. **不要使用 Emoji** — SVG 渲染器無法正確計算 emoji 字元寬度，會導致 `<rect> attribute width: negative value` 錯誤。
   ```
   ❌ HW["🖥 Mac Mini"]
   ✅ HW[Mac Mini]
   ```

2. **避免 `\n` 換行** — 多行文字在部分版本造成排版計算異常。改用 ` - ` 連接。
   ```
   ❌ A["第一行\n第二行"]
   ✅ A[第一行 - 第二行]
   ```

3. **避免特殊符號** — 全形括號 `（）`、雙向箭頭 `⇄`、中間點 `·` 等會導致解析錯誤。
   ```
   ❌ SYN["Sync Agent（同步）"]
   ✅ SYN[Sync Agent]
   ```

4. **使用 `classDef` 批量設定樣式** — 比逐一 `style` 指令更穩定且易維護。
   ```
   ❌ style A fill:#e8f0fe,stroke:#0066cc
      style B fill:#e8f0fe,stroke:#0066cc
   ✅ classDef blue fill:#e8f0fe,stroke:#0066cc,color:#1d1d1f
      class A,B blue
   ```

5. **CDN 版本必須確認存在** — 使用前用 `curl -sI <URL> | head -3` 驗證回應 200。目前使用 v11.12.0。

### 配色參考

與本站配色系統一致的 classDef 定義：

```
classDef blue fill:#e8f0fe,stroke:#0066cc,color:#1d1d1f
classDef purple fill:#f3e8ff,stroke:#7b2ff7,stroke-width:2px,color:#1d1d1f
classDef orange fill:#fff3e0,stroke:#e68a00,color:#1d1d1f
classDef green fill:#e6f9f0,stroke:#00875a,color:#1d1d1f
classDef gray fill:#f5f5f7,stroke:#d1d1d6,color:#636366
classDef red fill:#ffeef0,stroke:#d1242f,color:#1d1d1f
```

### 技術注意：隱藏 DOM 的渲染問題

`.slide` 預設 `display: none`，Mermaid 在隱藏容器中計算文字寬度會得到 0，扣掉 padding 後產生負寬度錯誤。HTML template 中的 `initMermaid()` 已處理這個問題：渲染前暫時讓所有 slide 設為 `display:block; visibility:hidden; position:absolute`，渲染完成後恢復。渲染完成後會自動呼叫 `_mermaidInjectExpandButtons()` 注入放大按鈕（見 § 18）。不需要額外處理。

---

## 18. Mermaid 點擊放大全螢幕

### 用途

所有 `.mermaid-wrap` 圖表自動支援**點擊放大全螢幕**顯示。hover 時右上角出現 ↗ 放大按鈕，點擊後以毛玻璃遮罩 + 白色卡片（94vw × 92vh）展示放大的 SVG 圖表。此功能已內建於 HTML template，無需額外撰寫 CSS 或 JavaScript。

### 互動行為

- **hover 提示**：滑鼠移入 `.mermaid-wrap` 時，右上角淡入 SVG 放大圖示按鈕，外框出現淡灰陰影
- **全螢幕顯示**：點擊圖表或放大按鈕後，overlay 佔滿視窗，SVG 自動縮放填滿可用空間
- **關閉方式**：右上角 ✕ 按鈕 / ESC 鍵 / 點擊深色背景
- **自動注入**：放大按鈕由 `_mermaidInjectExpandButtons()` 在 Mermaid 渲染完成後動態注入，不需手動加入 HTML

### CSS 樣式

```css
/* 放大按鈕 — 動態注入到每個 .mermaid-wrap */
.mermaid-expand-btn {
  position: absolute;
  top: 8px;
  right: 8px;
  width: 30px;
  height: 30px;
  border: none;
  background: rgba(0,0,0,0.05);
  border-radius: 6px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.2s ease, background 0.15s;
  z-index: 2;
  padding: 0;
}
.mermaid-wrap:hover .mermaid-expand-btn { opacity: 1; }
.mermaid-expand-btn:hover { background: rgba(0,0,0,0.1); }

/* 按鈕內 SVG 圖示 — 必須覆蓋尺寸，避免被 .mermaid svg 規則干擾 */
.mermaid-expand-btn svg {
  width: 16px !important;
  height: 16px !important;
  min-height: 0 !important;
  fill: none;
  stroke: #636366;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* 全螢幕 Overlay */
.mermaid-overlay { display: none; position: fixed; inset: 0; z-index: 100000; background: rgba(0,0,0,0.75); backdrop-filter: blur(6px); }
.mermaid-overlay.active { display: flex; justify-content: center; align-items: center; }
.mermaid-overlay-inner { background: #fff; border-radius: 14px; width: 94vw; height: 92vh; padding: 24px 32px 16px; display: flex; flex-direction: column; }
.mermaid-overlay-content { width: 88vw; height: 78vh; display: flex; align-items: center; justify-content: center; overflow: auto; }
.mermaid-overlay-content svg { width: 100% !important; height: 100% !important; max-width: 88vw; max-height: 78vh; min-height: 0 !important; }
```

### HTML 結構

overlay HTML 位於 `</body>` 之前（已內建於 template）：

```html
<div class="mermaid-overlay" id="mermaidOverlay">
  <div class="mermaid-overlay-inner" id="mermaidOverlayInner">
    <button class="mermaid-overlay-close" id="mermaidOverlayClose">&times;</button>
    <div class="mermaid-overlay-content" id="mermaidOverlayContent"></div>
    <div class="mermaid-overlay-label" id="mermaidOverlayLabel"></div>
  </div>
  <div class="mermaid-overlay-hint">按 ESC 或點擊外部關閉</div>
</div>
```

### JavaScript

overlay 邏輯和按鈕注入的 JS 也已內建於 template。核心流程：

1. Mermaid 渲染完成 → 呼叫 `_mermaidInjectExpandButtons()`
2. 為每個 `.mermaid-wrap` 注入一個 `.mermaid-expand-btn`（含 SVG 圖示）
3. 點擊時 clone 原始 SVG、移除 `width`/`height`/`style` 屬性，放入 overlay 容器使其自由縮放

### 注意事項

- `.mermaid-expand-btn svg` 必須用 `!important` 覆蓋 `width`/`height`/`min-height`，否則會被 `.mermaid-wrap .mermaid svg` 規則干擾導致按鈕變形
- 全螢幕時 clone SVG 並移除原始尺寸屬性，讓圖表根據容器大小自動縮放
- overlay 的 `z-index: 100000` 確保在所有 UI 元件之上（含 sidebar、topbar、fullscreen 簡報模式）
- 此功能與圖片的 lightbox 機制獨立運作，互不衝突

---

## 19. UED 封面版型

### .slide-cover — 漸層封面

**用途**：每個文件的第一張 Slide，全幅漸層背景搭配置中標題。

**顏色**：青綠 → 藍 → 紫 (UED 品牌漸層)

```html
<div class="slide active" data-title="封面" data-num="00">
  <div class="slide-cover">
    <div class="cover-inner">
      <div class="cover-eyebrow">部門名稱 / 團隊</div>
      <h1 class="cover-title">文件主標題</h1>
      <p class="cover-subtitle">副標題或一句話摘要</p>
      <div class="cover-date-pill">v1.0 · 2026-03</div>
    </div>
  </div>
  <!-- 封面下方可放摘要卡片 -->
  <div class="slide-card" style="margin-top:0; border-radius:0 0 16px 16px;">
    <div class="stat-row" style="justify-content:center;">
      <div class="stat-card">
        <div class="stat-value">5</div>
        <div class="stat-label">章節</div>
      </div>
    </div>
    <div class="info-box">使用左側導覽或方向鍵 ← → 瀏覽。</div>
  </div>
</div>
```

---

## 20. UED Accent Bar 標題

### .slide-title-wrap + .accent-bar — 左側漸層條

**用途**：所有非封面 Slide 的主標題，左側加上 4px 藍紫漸層條作為視覺錨點。

```html
<div class="slide-title-wrap">
  <div class="accent-bar"></div>
  <h2>這裡是 Slide 主標題</h2>
</div>
<div class="subtitle">Chapter 01 — 副標題說明</div>
```

**規則**：每張內容 Slide 都應使用此模式取代純 `<h2>`。

---

## 21. UED 卡片系統

### .card — 圓角色塊容器

**用途**：取代純文字段落，給內容加上顏色背景，增加視覺分組感。

```html
<!-- 顏色變體 -->
<div class="card card-blue">   藍色卡片 — 主要資訊、工具 </div>
<div class="card card-purple"> 紫色卡片 — AI 功能、進階  </div>
<div class="card card-green">  綠色卡片 — 成果、完成事項 </div>
<div class="card card-orange"> 橙色卡片 — 警告、注意事項 </div>
<div class="card card-yellow"> 黃色卡片 — 提示、備注     </div>
<div class="card card-white">  白色卡片 — 有陰影的白底   </div>
```

### 左邊框變體（card + border）

```html
<div class="card card-blue card-border-blue">
  藍色左邊框強調
</div>
<div class="card card-white card-border-purple">
  白底紫色左邊框
</div>
```

| Class | 背景色 | 適用場景 |
|-------|--------|---------|
| `.card-blue`   | #EEF3FF | 主要說明、工具導入 |
| `.card-purple` | #EDE9FE | AI 功能、自動化   |
| `.card-green`  | #ECFDF5 | 成果、正面資訊    |
| `.card-orange` | #FFF7ED | 警告、待辦事項    |
| `.card-yellow` | #FEFCE8 | 補充說明、備注    |
| `.card-white`  | #FFFFFF | 中性內容、表單    |

---

## 22. 雙欄佈局 two-col

### .two-col — 兩欄並排

**用途**：並排展示兩個對應主題、Before/After 比較、左說明右圖表。

```html
<div class="two-col">
  <div class="card card-blue">
    <span class="badge badge-blue" style="display:inline-block;padding:4px 14px;border-radius:999px;font-size:0.78rem;font-weight:600;margin-bottom:12px;">左欄標題</span>
    <p style="font-size:0.88rem;color:#374151;">左欄說明文字內容。</p>
  </div>
  <div class="card card-purple">
    <span class="badge badge-purple" style="display:inline-block;padding:4px 14px;border-radius:999px;font-size:0.78rem;font-weight:600;margin-bottom:12px;">右欄標題</span>
    <p style="font-size:0.88rem;color:#374151;">右欄說明文字內容。</p>
  </div>
</div>
```

**常見組合**：
- `card-blue` + `card-purple`：功能對比
- `card-blue` + `card-white`：說明 + 數據
- `card-orange` + `card-green`：Before + After

---

## 23. 三欄佈局 three-col

### .three-col — 三欄並排

**用途**：展示三個類別、三個階段、三個維度的資訊。

```html
<div class="three-col">
  <div class="card card-blue">
    <span class="badge badge-blue" style="display:inline-block;padding:4px 12px;border-radius:999px;font-size:0.75rem;font-weight:600;margin-bottom:8px;">工具導入</span>
    <p style="font-size:0.85rem;color:#374151;margin-top:8px;">第一類核心內容說明。</p>
  </div>
  <div class="card card-purple">
    <span class="badge badge-purple" style="display:inline-block;padding:4px 12px;border-radius:999px;font-size:0.75rem;font-weight:600;margin-bottom:8px;">自動化</span>
    <p style="font-size:0.85rem;color:#374151;margin-top:8px;">第二類核心內容說明。</p>
  </div>
  <div class="card card-green">
    <span class="badge badge-green" style="display:inline-block;padding:4px 12px;border-radius:999px;font-size:0.75rem;font-weight:600;margin-bottom:8px;">設計決策</span>
    <p style="font-size:0.85rem;color:#374151;margin-top:8px;">第三類核心內容說明。</p>
  </div>
</div>
```

---

## 24. 橫向長條圖 bar-chart

### .bar-row + .bar-track + .bar-fill — 水平進度條

**用途**：調查結果、使用比例、時間節省統計。

```html
<div class="card card-blue" style="padding:20px 24px;">
  <div class="bar-row">
    <span class="bar-label">創意發想</span>
    <div class="bar-track">
      <div class="bar-fill" style="width: 80%"></div>
    </div>
    <span class="bar-value">80%</span>
  </div>
  <div class="bar-row">
    <span class="bar-label">文字整理</span>
    <div class="bar-track">
      <div class="bar-fill" style="width: 65%"></div>
    </div>
    <span class="bar-value">65%</span>
  </div>
  <div class="bar-row">
    <span class="bar-label">程式生成</span>
    <div class="bar-track">
      <div class="bar-fill" style="width: 55%"></div>
    </div>
    <span class="bar-value">55%</span>
  </div>
</div>
```

**與 two-col 搭配（左圖表 + 右洞察）**：

```html
<div class="two-col">
  <div class="card card-blue">
    <!-- bar rows here -->
    <div class="highlight-box">
      <p style="font-size:0.8rem;color:#6B7280;">最高使用情境</p>
      <p class="stat-number">80%</p>
    </div>
  </div>
  <div class="card card-white">
    <p style="font-size:1rem;font-weight:700;color:#4A7CF7;">整體節省時間達</p>
    <div class="stat-number" style="margin-top:8px;">42%</div>
  </div>
</div>
```

---

## 25. Ranking 排行版型

### .rank-item — 金銀銅排行

**用途**：工具排行、貢獻排序、Q3/Q4 對比排名。

```html
<div class="two-col">
  <div class="card card-blue">
    <span class="badge badge-blue" style="display:inline-block;padding:4px 14px;border-radius:999px;font-size:0.78rem;font-weight:600;margin-bottom:16px;">Q3 省時幅度最大</span>
    <div class="rank-item">
      <div class="rank-medal">🥇</div>
      <div>
        <span class="badge badge-orange" style="display:inline-block;padding:3px 10px;border-radius:999px;font-size:0.72rem;font-weight:600;margin-bottom:4px;">最高等級</span>
        <div class="rank-title">Cursor + Claude</div>
        <div class="rank-note">寫 code 不再是設計師的阻力</div>
      </div>
    </div>
    <div class="rank-item">
      <div class="rank-medal">🥈</div>
      <div>
        <span class="badge badge-teal" style="display:inline-block;padding:3px 10px;border-radius:999px;font-size:0.72rem;font-weight:600;margin-bottom:4px;">高效率</span>
        <div class="rank-title">工具名稱 B</div>
        <div class="rank-note">短描述說明</div>
      </div>
    </div>
    <div class="rank-item">
      <div class="rank-medal">🥉</div>
      <div>
        <div class="rank-title">工具名稱 C</div>
        <div class="rank-note">短描述說明</div>
      </div>
    </div>
  </div>
  <div class="card card-purple">
    <!-- Q4 ranking 放這裡 -->
  </div>
</div>
```

---

## 26. Timeline 時間軸

### .timeline + .tl-step + .tl-line — 橫向時間軸

**用途**：展示專案階段、里程碑、流程推進。

```html
<!-- 時間軸（橫向）-->
<div class="timeline">
  <div class="tl-step">
    <div class="tl-dot tl-dot-orange"></div>
    <div class="tl-label">探索問題<br><span style="font-size:0.72rem;color:#6B7280;">需求釐清</span></div>
  </div>
  <div class="tl-line"></div>
  <div class="tl-step">
    <div class="tl-dot tl-dot-blue"></div>
    <div class="tl-label">收斂方案<br><span style="font-size:0.72rem;color:#6B7280;">流程設計</span></div>
  </div>
  <div class="tl-line"></div>
  <div class="tl-step">
    <div class="tl-dot tl-dot-purple"></div>
    <div class="tl-label">品質把關<br><span style="font-size:0.72rem;color:#6B7280;">上線準備</span></div>
  </div>
  <div class="tl-line"></div>
  <div class="tl-step">
    <div class="tl-dot tl-dot-green"></div>
    <div class="tl-label">持續優化<br><span style="font-size:0.72rem;color:#6B7280;">監控回饋</span></div>
  </div>
</div>

<!-- 時間軸下方配合 three-col 卡片 -->
<div class="three-col">
  <div class="card card-yellow" style="border:2px solid #FCD34D;">
    <h3 style="font-size:1rem;font-weight:700;color:#1B2559;margin:0 0 8px;">初期規劃</h3>
    <span class="badge badge-gold" style="display:inline-block;padding:3px 10px;border-radius:999px;font-size:0.72rem;font-weight:600;margin-bottom:8px;">目標</span>
    <ul style="font-size:0.85rem;color:#374151;margin-left:16px;margin-top:8px;">
      <li>確認需求範圍</li>
      <li>建立規格文件</li>
    </ul>
  </div>
  <div class="card card-orange" style="border:2px solid #F97316;">
    <h3 style="font-size:1rem;font-weight:700;color:#1B2559;margin:0 0 8px;">中期執行</h3>
    <ul style="font-size:0.85rem;color:#374151;margin-left:16px;margin-top:8px;">
      <li>開發實作</li>
      <li>測試驗收</li>
    </ul>
  </div>
  <div class="card card-purple" style="border:2px solid #8B72F5;">
    <h3 style="font-size:1rem;font-weight:700;color:#1B2559;margin:0 0 8px;">後期上線</h3>
    <ul style="font-size:0.85rem;color:#374151;margin-left:16px;margin-top:8px;">
      <li>部署與監控</li>
      <li>使用者回饋</li>
    </ul>
  </div>
</div>
```

**dot 顏色對應**：

| Class | 顏色 | 使用時機 |
|-------|------|---------|
| `.tl-dot-blue`   | #4A7CF7 實心 | 當前節點 / 完成 |
| `.tl-dot-orange` | #F97316 空心 | 起點 / 探索階段 |
| `.tl-dot-purple` | #8B72F5 空心 | 關鍵里程碑     |
| `.tl-dot-green`  | #10B981 空心 | 終點 / 成果    |

---

## 27. UED 徽章 badge 系統

### 實色徽章（白色文字）

```html
<span class="badge badge-blue"   style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">工具導入</span>
<span class="badge badge-purple" style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">自動化</span>
<span class="badge badge-green"  style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">設計決策</span>
<span class="badge badge-teal"   style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">新功能</span>
<span class="badge badge-orange" style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">注意</span>
<span class="badge badge-gold"   style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">最佳</span>
<span class="badge badge-red"    style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">重要</span>
```

### 輪廓徽章（灰色文字）

```html
<span class="badge badge-outline" style="display:inline-block;padding:3px 12px;border-radius:999px;font-size:0.78rem;font-weight:600;">Before</span>
<span class="badge badge-outline" style="display:inline-block;padding:3px 12px;border-radius:999px;font-size:0.78rem;font-weight:600;">After</span>
```

**注意**：badge 類別只定義顏色，需搭配 `style` 或在全域加入 `.badge { display:inline-block; padding:5px 16px; border-radius:999px; font-size:0.78rem; font-weight:600; }` 基礎樣式。

---

## 28. 章節過渡頁 section-header

### .slide-section-bg — 漸層過渡頁

**用途**：大章節之間的分隔頁，帶出下一段落主題。

```html
<div class="slide" data-title="第一章" data-num="01">
  <div class="slide-section-bg">
    <div class="section-inner">
      <span class="badge badge-blue" style="display:inline-block;padding:5px 16px;border-radius:999px;font-size:0.78rem;font-weight:600;">SECTION 01</span>
      <div class="section-big-title">章節大標題</div>
    </div>
  </div>
</div>
```

---

## 29. 版型選擇指引

根據內容類型選擇最合適的版型：

| 內容類型 | 推薦版型 | 元件組合 |
|---------|---------|---------|
| 章節封面 | cover | `.slide-cover` + `.cover-inner` |
| 章節轉場 | section-header | `.slide-section-bg` + `.section-big-title` |
| 一般說明 | standard | `accent-bar` 標題 + `.key-point` + 段落 |
| 兩項對比 | two-col | `.two-col` + `.card` × 2 |
| 三類分群 | three-col | `.three-col` + `.card` × 3 |
| 調查數據 | bar-chart | `.bar-row` + `.bar-track` + `.bar-fill` |
| 工具排行 | ranking | `.rank-item` + `.rank-medal` + `.rank-title` |
| 流程階段 | timeline | `.timeline` + `.tl-step` + `.tl-line` + `.three-col` |
| 功能截圖 | screenshot | `.two-col` + `.screenshot-box` |
| 統計總覽 | stats-mixed | `.two-col` + bar-chart + `.stat-number` |
| 工具清單 | icon-grid | `.three-col` + `.icon-grid` + `.stat-medium` |

---

**最後更新**：2026-03-24
**版本**：v2.0 — UED AI 設計風格全面升級（封面漸層、accent bar、卡片系統、12 種新版型）

