# OS AI Agent

> **真正的 Stateful System Control Agent**
> 透過背景長駐 PTY/Process 通道，實現無需每次重複 `cd` 或重新 `export` 環境變數的真·狀態保持終端代理。

`OS AI Agent` 是專為作業系統設計的自動化助理框架（目前優先支援 Windows 系統，並整合遠端 SSH 控制）。支援本地 Ollama 與 OpenAI API 相容模型，具備動態工具擴充能力、Web Console 視覺化介面以及強大的持久化 PowerShell / SSH 指令執行機制。

---

##  為什麼選擇 OS AI Agent？（核心優勢）

市面上許多 AI Agent 在執行 Shell 指令時，背後每次都是開啟全新的 `subprocess`，為了保持目錄，只能在背後偷偷拼接 `cd /path && command`。這種「偽持久化」無法保持記憶體狀態，且背景服務會立刻關閉。

**OS AI Agent 的不同之處：**

*  **真·狀態持久化 (Stateful Long-lived Session)**：採用背景長駐的 PowerShell 進程與 PTY 管道，PID 完全固定。無論中間與 AI 對話多久，`cd` 路徑、環境變數 (`$env:VAR`)、虛擬環境皆完美保留。
*  **原生系統直接控制 (Native System Control)**：不強制隔離於 Docker 沙盒內，可以直接控制宿主實體電腦，進行套件安裝、檔案維護與系統管理。
*  **多通道中央總線 (Central Channel Bus)**：支援同時開闢並切換多個本地 PowerShell 與遠端 Linux SSH 通道，個別維持獨立的 Session Context。
*  **零冗餘動態套件 (Extensible Tools)**：採用 Plugin 模組化設計，自動掃描載入工具，且大部分內建工具使用原生庫，保持極輕量化。

---

## 主要功能特點

1. **雙模型與自訂 API 整合**：支援連接本地 Ollama（如 Gemma、Llama 3 等模型）或 OpenAI API 相容服務，透過設定檔即可一鍵切換。
2. **Web 輕量 Console UI (Port 10000)**：內建輕量 Web 伺服器與好看的 Tailwind CSS 介面，提供流暢的 AI 聊天與指令轉發體驗。
3. **PowerShell 自動化整合**：自動處理 UTF-8 編碼與輸出流，支援 Windows 自動化操作與軟體環境建置。
4. **遠端 Linux SSH 模組**：自動處理 SSH 握手與 Session 保持，登入一次後即可持續發送遠端 Linux 指令。
5. **熱插拔工具機制 (Hot-swappable Tools)**：只需在 `tools/` 資料夾下新增 Python 腳本，系統啟動時即會自動註冊為 AI 可呼叫的 Function。

---

## 🛠️ 系統需求與安裝

### 系統需求
- **作業系統**：Windows 10 / 11（預設須具備 PowerShell 執行權限）
- **Python 版本**：Python 3.10 或以上版本

### 必要套件說明
專案設計追求極輕量，僅依賴少數必要套件：

- `requests`：用於發送 HTTP 請求以進行 API 溝通（包含 Ollama 本地服務、OpenAI API 及天氣查詢工具）。

```bash
pip install requests
