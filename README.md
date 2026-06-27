# 🎵 歌詞で学ぶ 日本語

透過喜愛的歌曲學習日文文法的自學網頁工具。

🌐 **線上版本**：https://sharonyen55.github.io/japanese-study/

---

## 功能介紹

- **歌詞頁**：顯示日文歌詞與中文翻譯，漢字自動標注假名（振り仮名）
- **文法頁**：每首歌提取 5 個重點文法句型，附例句與中文解說，可標記已學會
- **學習進度**：首頁顯示整體文法完成率、各 JLPT 等級進度
- **歌手分類**：左側樹狀選單依歌手分類，可展開／收合
- **YouTube 連結**：每首歌附 MV 縮圖，點擊開啟 YouTube（建議搭配子母畫面同步聆聽）
- **手機支援**：響應式版面，手機可正常使用
- **離線可用**：所有資料內嵌於 HTML，不需伺服器

---

## 目前收錄歌曲

### Roselia（BanG Dream!）

| # | 歌名 | 備註 |
|---|------|------|
| 1 | BLACK SHOUT | 團體劇情第一章（Roselia 結成） |
| 2 | LOUDER | 友希那與父親的羈絆 |
| 3 | Re:birth day | 成員間建立信任，如同重生 |
| 4 | 陽だまりロードナイト | 莉莎的主場 |
| 5 | 熱色スターマイン | 夏季煙火大會的熱情 |
| 6 | ONENESS | 五人一心的開端 |
| 7 | Determination Symphony | 紗夜對妹妹日菜的決心 |
| 8 | Opera of the wasteland | 樂團宏大感 |
| 9 | －HEROIC ADVENT－ | 卡片戰鬥主題曲 |
| 10 | 軌跡 | 聲優更換紀念曲 |

### 其他歌手

| # | 歌名 | 歌手 | 備註 |
|---|------|------|------|
| 11 | 感情グラス | 河瀨茉希 | 上伊那ぼたん ED |
| 12 | 芽吹くとき | yonige | 上伊那ぼたん OP |
| 13 | 飛ぼうよ | yama | 黄泉のツガイ ED |

---

## 新增歌曲方法

### 步驟一：準備歌詞

將歌詞存入 `source/` 資料夾，格式為日文與中文交替，空行隔開：

```
# 歌曲名稱

暗(くら)い夜(よる)も
黑暗的夜晚也

迷(まよ)わず進(すす)もう
毫不猶豫地前行吧
```

注音寫法：`漢字(ふりがな)` → 網頁自動轉為漢字上方標注

### 步驟二：加入歌詞資料（index.html）

在 `LR[10]` 之後加入新的歌詞變數：

```javascript
LR[14] = `日文第一句
中文第一句

日文第二句
中文第二句`;
```

### 步驟三：加入歌曲資料（index.html）

在 `SONGS` 陣列最後一首後面加入：

```javascript
{
  id: 14,
  title: "歌曲名稱",
  artist: "演唱者",
  group: "所屬作品或團體",
  youtube: "影片ID",        // youtu.be/ 後面的部分
  note: "備註說明",
  level: "N4",              // 整體難度
  distribution: {N5:30, N4:35, N3:25, N2:8, N1:2},  // 各等級佔比（合計100）
  grammar: [
    {id:"g1", pattern:"〜ている", example:"例句(注音)", meaning:"中文說明", level:"N5", learned:false},
    {id:"g2", pattern:"〜たい",   example:"例句(注音)", meaning:"中文說明", level:"N4", learned:false},
    {id:"g3", pattern:"〜ずに",   example:"例句(注音)", meaning:"中文說明", level:"N3", learned:false},
    {id:"g4", pattern:"〜ように", example:"例句(注音)", meaning:"中文說明", level:"N3", learned:false},
    {id:"g5", pattern:"〜んだ",   example:"例句(注音)", meaning:"中文說明", level:"N4", learned:false}
  ]
}
```

### 步驟四：推送到 GitHub

```bash
cd "D:\Sharon\AI\Life\Jepan"
git add index.html
git commit -m "新增歌曲：歌曲名稱"
git push origin master:main
```

約 1 分鐘後網站自動更新。

---

## 日常更新指令

```bash
cd "D:\Sharon\AI\Life\Jepan"
git add index.html
git commit -m "說明修改內容"
git push origin master:main
```

---

## 技術架構

| 項目 | 說明 |
|------|------|
| 語言 | 純 HTML + CSS + JavaScript，無任何框架 |
| 資料儲存 | 歌詞與文法資料全部內嵌於 HTML |
| 學習進度 | 儲存於瀏覽器 `localStorage`（各裝置獨立） |
| 假名標注 | `漢字(ふりがな)` 格式自動轉換為 `<ruby>` 標籤 |
| 歌曲排序 | 數字 → 英文字母 → 日文五十音 |
| 部署平台 | GitHub Pages（免費） |

---

## JLPT 等級色碼

| 等級 | 色碼 | 程度 |
|------|------|------|
| N5 | 🟢 綠 | 初學者基礎 |
| N4 | 🔵 藍 | 初級 |
| N3 | 🟡 黃 | 中級 |
| N2 | 🟠 橙 | 中高級 |
| N1 | 🔴 紅 | 最高級 |

---

## 學習流程建議

1. **聽歌**：點 MV 縮圖開啟 YouTube，手機使用子母畫面（PiP）邊聽邊學
2. **看歌詞**：切換至「歌詞」頁，對照中文翻譯理解句意，注意假名注音
3. **學文法**：切換至「文法」頁，閱讀各句型說明與例句
4. **標記進度**：點擊文法卡片標記已學會，卡片變綠色
5. **追蹤進度**：點選左上標題回首頁，查看整體完成率

---

*以 Claude Code 輔助開發*
