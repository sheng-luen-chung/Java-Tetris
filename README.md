# Tetris - Java AWT/Swing 現代化俄羅斯方塊

這是一款以 Java AWT/Swing 完全自製、嚴格遵循 **MVC 架構**與**物件導向設計 (OOP)** 打造的現代化俄羅斯方塊引擎。遊戲內建流暢的粒子特效、無停頓的並發音效系統以及殿堂級的動態 UI 介面。本專案從前期基礎核心，一路打磨至符合商業等級標準，所有的功能與介面渲染皆以純程式碼繪製（不仰賴外部遊戲引擎支援）。

---

## 🚀 專案里程碑與功能總覽

本專案跨越了高達 14 個開發階段 (Phase 1 ~ Phase 14.5)，層層堆疊與淬鍊出極具可玩性且極致華麗的系統：

### 初期重點 (Phase 1 ~ Phase 5)：核心法則與架構搭建
*   **MVC 核心架構**：徹底分離介面 (`GamePanel` 等 View)、邏輯狀態 (`GameState` 等 Model) 以及事件流 (`GameController` 等 Controller)，奠定易於擴充的厚實基礎。
*   **10x20 標準盤面與 7-Bag 隨機生成**：導入了現代俄羅斯方塊的 7-Bag 隨機抽選器，確保玩家永不面臨無方塊可解的死亡隨機陷阱。
*   **SRS (Super Rotation System) 踢牆判定**：完整實作了 SRS 的基礎旋轉碰撞與 Kick 邏輯，大幅強化盤面邊緣與深坑操作的容錯率。

### 中期重點 (Phase 6 ~ Phase 10)：極致操作體驗與進階演算法
*   **Lock Delay 鎖定延遲機制**：加入了方塊觸底後 0.5 秒的懸空操作時間（可滑動/旋轉），滿足高階玩家在極限空間的佈局需求。
*   **Ghost Piece 殘影預測**：在盤面底部動態繪製對應半透明的落點殘影，輔助玩家進行高速精準判斷。
*   **進階判定系統**：
    *   **T-Spin 對角演算法判定**：實踐了透過 3-corner 偵測 T-Spin 發動的演算法，並賦予特製的分數獎勵。
    *   **Combo 連擊疊加**：支援連續段數計算，隨著 Combo 越高會有不同規模的視覺浮動回饋 (Floating Text)。
    *   **Soft Drop / Hard Drop**：區分柔軟下放的即時控速與一鍵觸底硬落的快速操作手感。

### 後期重點 (Phase 11 ~ Phase 14.5)：殿堂級視覺特效與音效系統
*   **並發音緒 SoundManager**：自建針對 `javax.sound.sampled` API 的音效管理引擎，支援 BGM 循環與音量漸變，並徹底解決 Java 在某些 Windows 系統播放 24-bit 格式音源崩潰的技術瓶頸。
*   **純代碼繪製 UI 與動態選單**：支援完全由手把/鍵盤操控的主選單大廳系統。
*   **立體與高光渲染機制**：
    *   所有方塊與 UI 邊框 (`GamePanel`) 拋棄原本扁平色塊，採用 `GradientPaint` 融合 `Color` 高光/陰影 bevel 特效打底，形成一體化晶瑩剔透的 3D 感。
    *   純座標向量繪製 (`fillPolygon`) 各種選單與操作說明的 UI 箭頭，捨棄外部字型依賴。
*   **物理微粒與雷電光柱 (Particle Effect System)**：
    *   Hard Drop 觸底時，產生金色破風的物理彈射粒子。
    *   消除多重行數或是觸發 T-Spin 時，於兩側產生高壓細絲雷電特效。
*   **科幻動態景深**：選單擁有無數緩降旋轉的巨型「宇航級」透明 Tetromino，配搭底層 10x20 微光網格保護罩，帶來壓倒性的高階視覺呼吸感。

---

## 🛠 開發過程遭遇的困難與技術解決方案

在將專案推至「商業規格」的過程，開發團隊解決了數個棘手的 Java AWT 框架局限與邏輯衝突，列舉如下：

1.  **高精度音檔無法讀取導致遊戲卡死 (UnsupportedAudioFileException)** 
    *   **現象**：設計師提供的現代高解析度 24-bit/32-bit float BGM 或 SFX 丟入標準 Java 的 `AudioSystem.getAudioInputStream` 時會直接誘發 Crash。
    *   **解法**：在 `SoundManager` 內部建構並攔截 Format 分析，若讀取到不被 Java `Clip` 原生支援的資料深度，透過 `AudioSystem.getAudioInputStream(AudioFormat, AudioInputStream)` 即時建立轉碼管線 (Transcoding Pipeline)，將音樂動態降轉回 16-bit PCM 格式播放，達成零相容性問題。

2.  **字型缺失導致特殊符號破圖 (Font Rendering Missing Glyphs)**
    *   **現象**：原先使用 Unicode 字串符號 (例如 🡨, 🡪, 🡩, 🡫 或 ▶) 繪製 Controls 選單鍵位說明時，發現不同作業系統或 Java Runtime 的預設字型支援度不一，輕則出現排版偏誤，重則直接變成方框亂碼。
    *   **解法**：全面拔除字串符號，自建 `drawArrow(Graphics2D g, ...)` 等向量繪圖 Helper 方法，憑藉 `g.fillPolygon()` 來進行座標層級的手繪三角形與幾何標記，確保像素級的絕對一緻與永不破圖。

3.  **UI 渲染層疊導致畫面溢出與座標錯亂**
    *   **現象**：引入左右三欄式的面板架構時，頻繁對矩陣內部的 `Graphics2D` 呼叫 `g.translate()` 來偏移座標處理 `Board` 以避免越界，卻導致選單、環境微粒跟文字渲染在回退時發生偏移錯誤。
    *   **解法**：嚴格統一了狀態機生命週期的畫面清理策略，且強制規範執行 `g.translate(matrixOffsetX, 0);` 區段後，必須進行相應的 `g.translate(-matrixOffsetX, 0);` 還原，再針對 UI 圖層單獨做絕對座標定位；並同時以常數 `PADDING` 架構將所有版塊切分隔離，保證了 UI 零干涉的高維護性。

4.  **輸入法卡頓與鍵位衝突 (IME Hook Conflict)**
    *   **現象**：設定 `SHIFT` 作為 Hold 功能時，若為 Windows 用戶，會無預警喚醒中文輸入法或鎖定焦點，破壞即時操控遊戲體驗。
    *   **解法**：分析 `InputController` 攔截層，決定移去高風險的 `SHIFT` 輔助鍵綁定，統一由單主體字元鍵 (英文字母 `C` 鍵) 做為 Hold 的常規設定。

---

## 🎮 如何遊玩 (How to Run)

目前已經將專案所有的位元碼打包成為標準執行檔。

1. **依賴環境配置**：
   確保您電腦有安裝 JRE 8 或以上的 Java 執行環境，並且 `sounds` 音效資源資料夾位於本體的相對目錄中。
2. **啟動遊戲**：
   請在終端機或命令提示字元執行下方指令：
   ```bash
   java -jar Tetris.jar
   ```

> *開發團隊追求的是「極致」。享受您無可匹敵的 Tetris 宇宙。*
