# 前端技術分享專案 Copilot 指引

## 專案概述
這是一個關於「Vibe Coding」技術分享的單頁 HTML 展示網站，使用純 HTML、CSS 和 JavaScript 建構。網站設計為自包含的響應式展示平台，具有流暢動畫和現代化 UI 模式。

## 架構與結構

### 單檔案架構
- **`techTalk.html`**: 完整的自包含展示頁面，內嵌 CSS 和 JavaScript
- 所有樣式都內嵌在 `<style>` 標籤中 (第 7-196 行)
- 所有 JavaScript 都嵌入在 `<script>` 標籤中 (第 350-385 行)
- 無需外部依賴或建置流程

### 設計系統模式

#### 色彩配置
- 主要漸層: `linear-gradient(135deg, #667eea 0%, #764ba2 100%)`
- 主題色: `#667eea` (用於邊框、項目符號、懸停狀態)
- 內容背景: 白色 (`#fff`) 用於區塊，淡灰色用於佔位符
- 文字顏色: `#4a5568` 用於標題，`#718096` 用於佔位符文字

#### 版面組件
```css
.container      // 主要容器 (max-width: 1200px, 置中)
.section        // 內容卡片，具有 fadeInUp 動畫
.nav-menu       // 玻璃擬態導覽，使用 backdrop-filter
.content-placeholder  // 虛線邊框內容區域
.pros-cons      // 優缺點的兩欄網格
.media-section  // 截圖/影片的響應式網格
```

#### 導覽模式
- 分為兩個 `<ul>` 元素 (`.nav-list1`, `.nav-list2`) 進行視覺分組
- 每個導覽項目包含表情符號前綴，建立視覺層次
- 使用 CSS Grid 搭配 `repeat(auto-fit, minmax(200px, 1fr))` 實現響應式

### 內容慣例

#### 區塊結構
每個區塊遵循此模式:
```html
<section id="section-id" class="section">
    <h2>編號. 標題</h2>
    <div class="content-placeholder">
        <ul>
            <li>項目符號內容</li>
        </ul>
    </div>
</section>
```

#### 列表樣式
- 使用 `::before` 偽元素建立自定義項目符號，顏色為 `#667eea`
- 無預設列表樣式 (`list-style-type: none`)
- 20px 左邊距，使用絕對定位的自定義項目符號

#### 響應式斷點
- 手機版斷點: `@media (max-width: 768px)`
- 導覽在手機版切換為單欄
- 字體大小縮小 (3rem → 2rem for h1)
- 區塊內邊距縮小 (40px → 20px)

## 互動模式

### 平滑滾動
- 使用 `href="#section-id"` 的錨點導覽
- JavaScript 處理平滑滾動: `scrollIntoView({ behavior: 'smooth', block: 'start' })`

### 動畫效果
- **滾動淡入**: 使用 IntersectionObserver API 提升效能
- **區塊動畫**: `fadeInUp` 關鍵幀動畫，具有錯開延遲
- **懸停效果**: 導覽項目的 `translateY(-2px)` 效果

## 開發工作流程

### 內容更新
1. 直接在 `.content-placeholder` div 內的 HTML `<li>` 元素中修改內容
2. 透過替換 `.media-placeholder` 內容為 `<img>` 或 `<video>` 標籤來新增媒體
3. 更新 `.nav-list1` 和 `.nav-list2` 中的導覽表情符號和文字

### 樣式變更
- 所有 CSS 都在 `<style>` 區塊中 (第 7-196 行)
- 使用現有的 CSS 自定義屬性模式確保主題一致性
- 維持玻璃擬態效果: `backdrop-filter: blur(10px)` + RGBA 背景

### 語言考量
- 內容為繁體中文 (`lang="zh-TW"`)
- 字體堆疊優先使用 `'Microsoft YaHei'` 進行中文字符渲染
- 確保中文內容使用正確的 UTF-8 編碼

## 重要檔案參考
- **`techTalk.html`** (第 214-385 行): 主要內容區塊 - 在此修改展示更新
- **CSS 動畫** (第 174-185 行): `@keyframes fadeInUp` - 在此擴展新動畫
- **JavaScript** (第 350-385 行): 平滑滾動和交叉觀察器邏輯

## 測試與預覽
- 直接在瀏覽器中開啟 `techTalk.html` (無需建置步驟)
- 在 768px 斷點測試響應式行為
- 驗證所有 6 個區塊間的平滑滾動
- 檢查低階設備上的動畫效能