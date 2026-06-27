# 日文歌曲學習網頁 — 專案說明

## 檔案位置
- 主網頁：`D:\Sharon\AI\Life\Jepan\index.html`（自含式，所有資料內嵌）
- 歌詞來源：`D:\Sharon\AI\Life\Jepan\source\`
- 線上網址：https://sharonyen55.github.io/japanese-study/

---

## 關鍵字觸發流程

### 當我說「新增歌曲」或「加歌曲」時：

**我需要你提供（必填）：**
- 歌名（日文）
- 歌手／演唱者
- 所屬作品或團體
- 日文歌詞（原文即可，**不需要注音或中文翻譯**，我來處理）

**可後補（留空也能先新增）：**
- YouTube 影片 ID（網址 `?v=` 或 `youtu.be/` 後面的部分）
- 備註說明

**我負責處理：**
- 漢字標注假名 `漢字(ふりがな)`
- 每句歌詞的中文翻譯
- 5 個文法句型（pattern、example、exampleZh、meaning、JLPT 等級）
- 整體難度與各等級佔比（distribution 合計 100）

**執行步驟：**

1. **讀取 index.html**，找出目前最大的歌曲 id，新歌 id = 最大值 + 1

2. **整理歌詞**：為日文歌詞加上假名注音與中文翻譯，格式：
   ```
   日文第一句（漢字(ふりがな)）
   中文翻譯第一句
   
   日文第二句
   中文翻譯第二句
   ```

3. **在 index.html 的 `/* ── Raw lyrics ── */` 區塊末尾**加入：
   ```javascript
   LR[新id] = `歌詞內容`;
   ```

4. **在 SONGS 陣列末尾**加入新歌物件

5. **推送到 GitHub**：
   ```
   git add index.html
   git commit -m "新增歌曲：歌名"
   git push origin master:main
   ```

**文法例句注意事項：**
- `example` 必須實際包含 pattern 核心字串（去掉開頭 `〜`、去掉 `（...）`、去掉中間 `〜` 或 `／` 後的部分）
- 允許中間夾注音，例如 `届(とど)かずに` 可以被 `ずに` 比對到
- 從歌詞中選有出現該文法用字的句子，不要自創不在歌詞裡的例句

---

### 當我說「查看歌曲」或「目前有幾首」時：

讀取 index.html 的 SONGS 陣列，列出：
- 總歌曲數
- 依歌手分組的清單（id、歌名、等級）

---

### 當我說「推上去」或「更新網站」時：

執行：
```
git add index.html
git commit -m "更新內容"
git push origin master:main
```
並告知推送完成，約 1 分鐘後網站更新。

---

## 技術備忘

- 假名注音格式：`漢字(ふりがな)` → 自動轉為 `<ruby>` 標籤
- 歌曲排序：數字 → 英文 → 日文五十音（`localeCompare('ja')`）
- 學習進度存於瀏覽器 `localStorage`，key 為 `jplearn_v2`
- Git 遠端：`origin` = `https://github.com/sharonyen55/japanese-study.git`
- 本地分支 `master`，推送到遠端 `main`：`git push origin master:main`
