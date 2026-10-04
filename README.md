# os-ai-agent

OS AI Agent 是專為作業系統設計的自動化助理工具(目前僅支持windows系統)，支援本地 Ollama 與 OpenAI API 雙模型機制，具備動態工具擴充能力與自動化 PowerShell 指令執行機能。

## 系統需求

- Python 3.10 或以上版本
- Windows 作業系統（預設環境須具備執行 PowerShell 之權限）

## 功能特點

- 雙模型整合支援：支援連接本地部署之 Ollama（如 Gemma、Llama 等模型）或 OpenAI API，並可於設定檔中快速切換。
- 動態工具擴充機制：透過簡單的腳本架構即可完成工具擴充，系統會自動掃描並載入新增之功能模組。
- PowerShell 自動化整合：支援系統指令執行與檔案操作，並具備自動處理字元轉義與執行結果消化之機制。
- 結構化結果回傳：內部執行結果由模型二次整理，僅輸出關鍵資訊與執行摘要。

## 必要套件說明

本專案運作依賴以下 Python 套件：

- `requests`：用於發送 HTTP 請求以進行 API 溝通（包含 Ollama 本地服務、OpenAI API 及 weather 工具）。

