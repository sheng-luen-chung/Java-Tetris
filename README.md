[English](#english) | [繁體中文](#繁體中文-traditional-chinese)

# English

# Tetris: Java Edition

A Tetris clone developed in Java using standard AWT and Swing libraries. The project implements standard modern Tetris mechanics including the Super Rotation System (SRS) and features a custom rendering engine for block aesthetics and particle effects.

## Features

### Gameplay Mechanics
* **Super Rotation System (SRS)**: Implements standard wall kick data for block rotation near boundaries.
* **Advanced Scoring**: Includes rule sets for T-Spin detection (3-corner rule) and Combo chaining.
* **Modern Controls**: Supports Soft Drop, Hard Drop, and Piece Hold functionality.
* **Ghost Piece**: Displays an indicator at the bottom of the matrix where the piece will land.
* **Game Modes**: Provides Endless Mode and Level Mode (increasing gravity speed).

### Graphics & Interface
* **Custom 3D Rendering**: Uses `Graphics2D` and `GradientPaint` to apply bevel lighting and shadow effects to blocks natively.
* **Particle Effects**: Features physics-based particle spurts on Hard Drop and visual lightning animations on line clears.
* **UI Layout**: Standard three-column layout (Hold, Matrix, Next/Score) with dynamic background animations.

### Audio System
* **Asynchronous SoundManager**: Handles sound effects (SFX) and background music (BGM) in separate threads to prevent blocking the game loop.
* **Format Conversion**: Automatically downsamples unsupported 24-bit/32-bit audio files to 16-bit PCM for compatibility with the Java `Clip` API.
* **State synchronization**: BGM changes seamlessly based on game state (Menu, Playing, Game Over).

### Architecture
* **MVC Pattern**: Separates `GameState` (Model), `GamePanel` (View), and `GameController`/`InputController` (Controller).
* **Game Loop**: A dedicated thread updates the logic and triggers repaints consistently.

## Installation & Usage

### Prerequisites
* Java Runtime Environment (JRE) 8 or higher.

### Running the Game
1. Clone the repository or download the latest release block.
2. Ensure that `Tetris.jar` and the `sounds/` directory are located in the **same directory**.
3. Open a terminal or command prompt, navigate to the directory, and run:
   ```bash
   java -jar Tetris.jar
   ```

### Controls
* **Arrow Left / Right**: Move piece
* **Arrow Up / X**: Rotate Clockwise
* **Z**: Rotate Counter-Clockwise
* **Arrow Down**: Soft Drop
* **Space**: Hard Drop
* **C**: Hold Piece
* **Escape**: Pause / Resume Game
* **Enter**: Confirm Selection (Main Menu)

## Functionality Showcase

### Live Gameplay Interface
![Gameplay Screen](docs/images/image-1.png)
*Showcasing the core gameplay view, including the Ghost Piece dropping accuracy, matrix border gridlines, and dynamic particles.*

### Main Menu and Mode Selection
![Menu Interface](docs/images/image-2.png)
*Demonstrating the graphic-based main menu interface with customized geometric cursors and transparent background animations.*

### Game Over and Scoring
![Game Over Screen](docs/images/image-3.png)
*Presenting the Game Over screen highlighting your total score and high score record updates, while smoothly transitioning the BGM state.*

---

<br>
<br>

# 繁體中文 (Traditional Chinese)

# Tetris: Java Edition

使用標準 AWT 與 Swing 函式庫以純 Java 開發的俄羅斯方塊。本專案實作了現代主流俄羅斯方塊的標準機制（例如超級旋轉系統 SRS），並特別針對方塊美學與粒子特效打造了一套自定義的渲染引擎。

## 核心功能

### 遊戲機制
* **超級旋轉系統 (SRS)**：實作了標準的踢牆判定資料，允許方塊在靠近邊界或狹窄空間時進行特殊旋轉。
* **高階計分法則**：包含 T-Spin（T轉）的三角偵測機制，以及 Combo 連擊的計分加成。
* **現代化操控**：完整支援 Soft Drop（緩降）、Hard Drop（瞬落）以及 Piece Hold（方塊保留）等主流操作。
* **殘影預視 (Ghost Piece)**：在盤面底部顯示落點指示器，精準預判方塊著陸位置。
* **遊戲模式**：提供 Endless Mode (無盡模式) 與 Level Mode (等級挑戰，重力速度將隨等級提升)。

### 視覺渲染與介面
* **自定義 3D 渲染**：利用 `Graphics2D` 與 `GradientPaint` 原生賦予方塊立體斜角高光與陰影特效。
* **物理粒子系統**：加入了 Hard Drop 觸發下的物理四散特效，以及消除行數時的閃電視覺動畫。
* **UI 佈局**：標準的三欄式介面配置（Hold 區、主盤面、Next/分數資訊區），並帶有動態背景。

### 音效引擎
* **非同步 SoundManager**：使用獨立的執行緒分流處理音效 (SFX) 與背景音樂 (BGM) 的播放，絕不阻塞主執行緒。
* **格式自動相容**：自動將無法受 Java `Clip` 原生支援的 24-bit/32-bit 浮點音源降轉為 16-bit PCM 格式播放。
* **狀態同步切換**：BGM 會根據遊戲當前所處的狀態（主選單、遊戲中、遊戲結束）完美順滑地切換與過渡。

### 系統架構
* **MVC 架構設計**：嚴格劃分 `GameState` (模型)、`GamePanel` (視圖) 以及 `GameController`/`InputController` (控制器)。
* **穩定遊戲迴圈**：專屬的獨立執行緒確保邏輯的穩健更新以及畫面的幀數刷新。

## 安裝與遊玩

### 環境環境限制
* Java Runtime Environment (JRE) 8 或更高版本。

### 啟動遊戲
1. 複製 (Clone) 本儲存庫，或是直接下載最新的發行版本打包檔。
2. 請確保 `Tetris.jar` 與 `sounds/` 資料夾位被放置於**同一個目錄**中。
3. 開啟終端機或是命令提示字元，移動到該目錄並執行以下指令：
   ```bash
   java -jar Tetris.jar
   ```

### 預設操作按鍵
* **左 / 右方向鍵**：移動方塊
* **上方向鍵 / X**：順時針旋轉
* **Z**：逆時針旋轉
* **下方向鍵**：Soft Drop 緩降
* **空白鍵 (Space)**：Hard Drop 瞬落
* **C**：Hold 保留方塊
* **Esc**：暫停 / 恢復遊戲
* **Enter**：確認選擇（於主選單時）

## 功能展示

### 實際遊玩介面
![Gameplay Screen](docs/images/image-1.png)
*展示核心的遊戲畫面，包含精準的落點殘影、底層網格保護罩，以及方塊觸底時的動態物理粒子特效。*

### 遊戲大廳主選單
![Menu Interface](docs/images/image-2.png)
*展現純圖像化與幾何游標構成的三欄式選單，同時背後會有緩慢落下的巨型透明俄羅斯方塊背景。*

### 結算與高分顯示
![Game Over Screen](docs/images/image-3.png)
*遊戲無憾結算的結果展示頁面，會結算您的計分與歷史紀錄，同時音樂引擎亦會跟隨畫面自然過渡至結算音效。*