# Process-Long-Subtitles

## 簡介
本程式（Colab 筆記本）用於處理由影片字幕AI生成工具(Rask AI)生成的過長字幕。該工具有時產生的字幕檔裡，會有某行字幕文字過多的狀況。當字幕文字過長時，本程式會自動將其拆分成數行較短的字幕，並根據原始字幕的時長平均分配每行的顯示時間，從而生成更為美觀且易讀的 SRT 字幕檔。

## 功能
- **自動拆行**：檢測字幕中每行的長度，若超過預設的 70 字元，則自動拆分成多行。
- **時間平分**：根據原始字幕的總時長，平均分配每行的開始與結束時間，確保時序連貫。
- **SRT 檔生成**：處理後的字幕將輸出成新的 SRT 文件，方便後續使用。

## 如何使用
1. **開啟 Colab 筆記本**  
   點擊下方按鈕，直接在 Google Colab 中開啟此筆記本：
   
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Chihuah/Process-Long-Subtitles/blob/main/Process_Long_Subtitles_(from_Rask_ai).ipynb)

2. **執行筆記本**  
   筆記本已分成多個 cell，請依序執行每個 cell。  
   - 第一個 cell 會安裝所需的套件 `pysrt`。  
   - 後續的 cell 定義了處理字幕的函數並執行範例程式碼。

3. **上傳輸入檔案**  
   將你要處理的 SRT 字幕檔（例如 `5-2-03_enL.srt`）上傳至 Colab，或根據需要修改檔案路徑。

4. **處理字幕**  
   筆記本將呼叫 `process_file` 函數來讀取、處理並生成新的 SRT 字幕檔。

## 筆記本結構
- **安裝區塊**：安裝 `pysrt` 套件。
- **匯入區塊**：載入 `pysrt` 和 `textwrap` 模組。
- **函數定義**：
  - `process_subtitles(subs, max_length)`：處理字幕，拆分過長的行並重新計算時間。
  - `process_file(input_file, output_file, max_length=70)`：讀取 SRT 檔案、呼叫處理函數並將結果寫入新檔案。
- **使用範例**：展示如何處理範例字幕檔。

## 貢獻
歡迎提交 Issue 或 Pull Request 來改進此工具。如果你有任何建議或發現問題，請隨時提出。

## 授權
本專案採用 [MIT License](LICENSE) 授權，詳細內容請參閱 LICENSE 檔案。

## 聯絡方式
如有任何疑問或建議，請在 GitHub 上發 Issue 與我聯絡。
