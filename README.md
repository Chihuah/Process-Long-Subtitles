# Process Long Subtitles

一個 Python 工具，用來將 AI 產生（如 Rask.ai、Whisper）的過長 SRT 字幕拆分成多行，並自動均分時間軌，提升字幕可讀性。

本版本在原始的「依字數硬切」基礎上，升級為**語意感知斷句（semantic-aware splitting）**：優先在標點與連接詞等自然語意邊界處切分，讓每一行字幕讀起來更通順、更貼近語句的自然停頓。

## 功能特色

- **語意斷句**：依下列優先順序尋找斷點，而非單純按字數硬切
  1. 強標點（`. ! ? ; :`）之後
  2. 弱標點（`,`、`—`、`-`）之後
  3. 連接詞（and, but, or, because, which, that, when …）之前
  4. 以上皆無時，退而在空白處切分（不會切斷英文單字）
- **長度控制**：每段長度盡量不超過 `max_length`（預設 100 字元，可自訂）
- **時間軌自動均分**：拆分後的多段字幕，依段數比例重新分配起訖時間
- **跨分鐘安全**：時間計算以總毫秒數（`ordinal`）為基準，避免長字幕跨分鐘時的時間錯位

## 環境需求

- Python 3
- [`pysrt`](https://pypi.org/project/pysrt/)

```bash
pip install pysrt
```

## 使用方式

於 Jupyter Notebook 或 Google Colab 開啟 `Process_Long_Subtitles.ipynb`，依序執行各 cell，最後呼叫：

```python
process_file('input.srt', 'output.srt', max_length=100)
```

- `input_file`：來源 SRT 檔路徑
- `output_file`：輸出 SRT 檔路徑
- `max_length`：每行字幕的字元數上限（預設 100）

## 參數調整

- **`max_length`**：依字幕呈現寬度調整。畫面較窄或字體較大時可調小。
- **`CONJUNCTIONS`**：連接詞清單可自行增減。若發現某些字幕常斷在不理想處，調整此清單最直接。

## 運作說明

工具會逐句讀取 SRT，對超過 `max_length` 的行進行語意斷句，再將原本一句的時間區間依拆分後的段數平均分配給各段。斷句邏輯為「先確保每段不超過長度上限，再盡量切在自然語意邊界」，因此偶爾相鄰兩段長度會有落差，這是為了不超出長度上限的取捨。

## 版本說明

- `Process_Long_Subtitles.ipynb`：**目前版本**，語意斷句強化版。
- `Process_Long_Subtitles_(from_Rask_ai).ipynb`：早期版本，僅依字數硬切（`textwrap.wrap`），已棄用。

## 授權

MIT License
