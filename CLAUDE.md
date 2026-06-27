# 日文歌曲學習網頁 — 專案說明

## 檔案位置
- 主網頁：`D:\Sharon\AI\Life\Jepan\index.html`（自含式，所有資料內嵌）
- 歌詞來源：`D:\Sharon\AI\Life\Jepan\source\`
- 線上網址：https://sharonyen55.github.io/japanese-study/

---

## Skills

> 說出關鍵字即可觸發，不需要加 `/`

---

### 新增歌曲

**觸發**：說「新增歌曲」或「加歌曲」

**你只需要提供：**
| 欄位 | 必填 | 說明 |
|------|------|------|
| 歌名 | ✅ | 日文歌名 |
| 歌手 | ✅ | 演唱者名稱 |
| 所屬作品 | ✅ | 所屬團體或動畫名稱 |
| 日文歌詞 | ✅ | 純日文原文即可，不需注音或中文翻譯 |
| YouTube ID | ⬜ | `youtu.be/` 或 `?v=` 後面的部分，可後補 |
| 備註 | ⬜ | 曲子背景說明，可後補 |

**我負責處理：**
- 漢字標注假名 `漢字(ふりがな)`
- 每句歌詞中文翻譯
- 5 個文法句型（pattern、example、exampleZh、meaning、JLPT 等級）
- 整體難度評估與各等級佔比（N5+N4+N3+N2+N1 合計 100）

**執行流程：**
1. 讀取 `index.html`，取得目前最大 id，新歌 id = 最大值 + 1
2. 整理歌詞（加假名注音＋中文翻譯）
3. 在 `/* ── Raw lyrics ── */` 末尾加入 `LR[新id]`
4. 在 `SONGS` 陣列末尾加入新歌物件
5. `git add index.html && git commit -m "新增歌曲：歌名" && git push origin master:main`

**文法例句規則（避免橘色高亮失效）：**
- `example` 必須實際包含 pattern 核心字串
  - 核心 = pattern 去掉開頭 `〜`、去掉 `（...）`、去掉中間 `〜` 或 `／`
  - 例：`〜ずに` → 核心 `ずに`，example 中需有 `ずに`（注音中間夾也算，如 `届(とど)かずに`）
- 從歌詞中選有出現該文法用字的句子，不要自創不在歌詞裡的例句

---

### 查看歌曲

**觸發**：說「查看歌曲」或「目前有幾首」

讀取 `index.html` 的 SONGS 陣列，列出：
- 總歌曲數
- 依歌手分組的清單（id、歌名、JLPT 等級）

---

### 推上去

**觸發**：說「推上去」或「更新網站」

```bash
git add index.html
git commit -m "更新內容"
git push origin master:main
```

告知推送完成，約 1 分鐘後網站更新。

---

## 技術備忘

| 項目 | 說明 |
|------|------|
| 假名注音 | `漢字(ふりがな)` → `<ruby>` 標籤；正則只抓 `[㐀-鿿々〆ヶヵ]+` 漢字範圍，平假名不轉換 |
| 文法高亮 | `ruby(highlightPattern(pattern, example))` 順序不能反；pattern core 要三步驟抽取 |
| 歌曲排序 | 數字 → 英文字母 → 日文五十音（`localeCompare('ja')`） |
| 學習進度 | `localStorage`，key 為 `jplearn_v2` |
| Git | 本地 `master` → 遠端 `main`：`git push origin master:main` |
