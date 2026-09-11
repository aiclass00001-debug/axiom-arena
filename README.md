# AXIOM / ARENA

一款以 Three.js 與 Rapier.js 製作的單檔 HTML5 3D 戰鬥陀螺物理遊戲。

AXIOM / ARENA 的重點不是預錄動畫，而是讓兩個陀螺在深碗形競技場中，透過剛體物理、重力、摩擦力、角速度、碰撞衝量與旋轉能量衰減，產生每一場都不同的戰鬥結果。

## Play

GitHub Pages 部署完成後，開啟：

```text
https://你的帳號.github.io/你的Repository名稱/
```

遊戲使用 CDN 載入 Three.js 與 Rapier.js，因此執行時需要網路連線。

## Features

- 深碗形科幻競技場，斜坡會實際影響陀螺移動
- Rapier.js 動態剛體物理
- 真實角速度與 RPM 下降
- 摩擦、阻尼、碰撞衝量、恢復係數與旋轉能量損失
- 低 RPM 時產生 wobble、傾斜與自然倒地
- 撞牆反彈與陀螺互撞都會影響線速度、角速度與穩定度
- 五種不同物理特性的原創陀螺
- 單人 vs AI
- 雙人同鍵盤對戰
- 玩家名稱、比分與本機排行榜
- 動態旋轉音效與原創電子配樂
- 碰撞火花、能量環、撞擊文字、重擊慢動作與鏡頭震動
- 撞擊方向 3D 箭頭提示
- Ring Out 與 Spin Finish 勝負判定
- 可調整重量、加速度、撞牆反彈與互撞力道
- 可切換自動、全場與跟隨鏡頭

## Battle Tops

| 陀螺 | 類型 | 主要特性 |
| --- | --- | --- |
| CYAN // VECTOR | Balance | 平衡、適合入門 |
| EMBER // HELIX | Attack | 高 RPM、高碰撞輸出、容易失穩 |
| AEGIS // TITAN | Defense | 質量最高、抗擊退、移動較慢 |
| VOLT // RAZOR | Speed | 移動最快、擅長高速切入 |
| VOID // ORBIT | Stamina | 旋轉能量衰減較慢、續航最長 |

每款陀螺具有不同的質量、慣性、重心、初始 RPM、移動速度、穩定度、碰撞損失與 AI 行為。

## Controls

### 單人模式

- 滑鼠拖曳：設定發射方向與力道
- `WASD`／方向鍵：發射前瞄準，發射後施加小幅物理操控力
- `Space`：發射或重新開始
- `C`：切換鏡頭
- `F2`：切換除錯資訊

### 雙人模式

- 玩家 1：`WASD`
- 玩家 2：方向鍵
- 兩位玩家在發射前分別瞄準，按下 `LAUNCH` 後同時發射
- 戰鬥中雙方都只能施加小幅物理力，不會直接控制陀螺位置

## Match Rules

- 陀螺離開有效競技場範圍，立即 Ring Out
- RPM 低於門檻並持續一段時間，判定 Spin Finish
- 勝一局記 1 分，平手不加分
- 單人模式另有以勝利、剩餘 RPM、出界與速勝計算的本機排行榜分數
- 排行榜使用瀏覽器 `localStorage`，不會同步到其他裝置

## Physics Model

每個陀螺都是 Rapier 動態剛體，包含：

- 質量與慣性張量
- 重心高度
- 初始線速度與角速度
- 線性阻尼與角阻尼
- 接觸摩擦與恢復係數
- 碰撞衝量造成的旋轉能量損失
- 傾斜時增加的 wobble 與滾動阻力
- 低 RPM 時的自然失穩與倒地

物理模擬使用固定時間步長與 CCD，並限制極端線速度與角速度，以降低穿透、爆炸、NaN 與永久卡住的機率。

## Impact Feedback

碰撞回饋會依實際碰撞衝量分級：

- `METAL CLASH`：一般互撞
- `HEAVY IMPACT`：較強碰撞、更多火花與鏡頭震動
- `CRITICAL IMPACT`：重擊慢動作、強烈閃光、撞擊方向箭頭與較大能量環
- `RAIL REBOUND`：撞牆反彈

短時間內連續碰撞會顯示 `×2`、`×3` 等 Combo 提示。

## Run Locally

直接雙擊 `index.html` 通常也能開啟，但建議使用本機 HTTP Server：

```bash
python3 -m http.server 4173
```

接著開啟：

```text
http://localhost:4173/
```

## GitHub Pages Deployment

1. 在 GitHub 建立一個新的 Repository。
2. 將 `index.html` 與 `README.md` 上傳到 Repository 根目錄。
3. 開啟 `Settings → Pages`。
4. Source 選擇 `Deploy from a branch`。
5. Branch 選 `main`，資料夾選 `/(root)`。
6. 儲存後等待 GitHub Pages 完成部署。

`index.html` 必須放在發布來源的根目錄，GitHub Pages 才會將它當成網站入口。

## Project Structure

```text
axiom-arena/
├── index.html     # 完整遊戲：HTML、CSS、JavaScript、Three.js、Rapier.js
└── README.md      # 專案說明
```

## Technology

- HTML5
- CSS3
- JavaScript ES Modules
- Three.js `0.170.0`
- Rapier3D Compat `0.17.3`
- Web Audio API
- GitHub Pages

## Original Content

所有陀螺造型、競技場視覺、音效與配樂皆為本專案原創程式化內容，未使用 Beyblade 或其他品牌的模型、標誌、角色與名稱。

## Current Limitations

- AI 排行榜目前是本機排行榜，不是多人線上排行榜
- 遊戲需要 CDN 網路連線才能載入物理與 3D 函式庫
- 音訊需要玩家先點擊「啟用音訊」才能播放，這是瀏覽器自動播放政策限制
- 雙人模式為同一鍵盤的本機對戰，尚未加入網路連線

## License

本專案的遊戲程式與原創視覺內容可作為個人展示、教學與研究用途。若要公開再發佈或商業使用，請另外保留本 README 與原作者資訊。
