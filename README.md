# 狸注音 — 模型散布

本 repo 只做一件事：散布[狸注音（LiliBopomofo）](https://github.com/funkeyyou/LiliBopomofo)
在裝置端 AI 重排功能所使用的語言模型，以及**簽章過的** manifest。

## 這裡有什麼

- **模型檔（GGUF）**：放在 [Releases](../../releases)。
- **`manifest.json` 與 `manifest.json.sig`**：輸入法先驗簽章才會採用。
  公鑰編譯在 app 內；驗不過就一律拒絕。

## 為什麼 manifest 要簽章

manifest 同時攜帶**模型下載網址**與**打分權重**。若不驗簽，
任何能改動這裡回應的人都能靜默改變輸入法的行為，甚至讓它去下載別的檔案。
輸入法端沒有「跳過驗證」的路徑。

## 隱私

模型下載後**完全在使用者的電腦上運算**。打字內容、選字記憶、使用統計
都不會離開裝置。AI 功能預設關閉，使用者主動啟用並同意後才會下載。

## 模型來源與授權

| 模型 | 上游 | 授權 |
|---|---|---|
| `qwen3-0.6b-base-q4_k_m` | [Qwen/Qwen3-0.6B-Base](https://huggingface.co/Qwen/Qwen3-0.6B-Base) | Apache-2.0 |
| `qwen35-0.8b-base-q4_k_m` | [Qwen/Qwen3.5-0.8B-Base](https://huggingface.co/Qwen/Qwen3.5-0.8B-Base) | Apache-2.0 |

本 repo 散布的是上述模型經 llama.cpp 轉換為 GGUF 並以 Q4_K_M 量化後的**衍生產物**。
原始模型著作權歸 Qwen 團隊（阿里巴巴集團）所有，依 Apache License 2.0 釋出；
授權條款全文見 [`NOTICE`](NOTICE)。本 repo 與 Qwen 團隊無隸屬關係。

狸注音本體以 MIT 授權釋出，基於 openvanilla/McBopomofo（小麥注音）開發。
