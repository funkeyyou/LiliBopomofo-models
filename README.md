# 狸注音模型資產

[狸注音（LiliBopomofo）](https://github.com/funkeyyou/LiliBopomofo) 的裝置端打分模型，
以及 app 讀取的簽章 manifest。

## 檔案

| 檔案 | 用途 |
|---|---|
| `manifest.json` | app 讀的清單：模型網址、sha256、RAM 門檻、重排參數 |
| `manifest.json.sig` | 上面那個檔的 Ed25519 簽章（64 bytes，raw） |
| Releases 的 `.gguf` | 模型本體 |

## 為什麼要簽章

manifest **同時攜帶模型網址與 α/β 重排權重**，所以它是一個「能靜默改變輸入法行為」
的攻擊面。app 內 pin 住公鑰，只接受對應私鑰簽出來的 manifest；驗的是
`manifest.json` 的**原始位元組**，不是重新序列化後的 JSON。

也就是說：**`manifest.json` 一旦被任何工具重新格式化（縮排、排序、換行），簽章就失效**。
要改內容請重新簽，不要手動編輯後直接推。

模型下載完之後還會再驗一次 sha256，**驗過才搬進載入路徑**——
順序是刻意的，反過來會讓壞檔短暫出現在會被載入的位置。

## 授權

模型由 [Qwen/Qwen3.5-0.8B-Base](https://huggingface.co/Qwen)（Apache-2.0）
量化並剪裁詞彙表而來，授權不變。剪裁工具與判定見主 repo 的
`Eval/tools/prune_vocab.py` 與 `Eval/M5-VOCAB-PRUNE-GATE.md`。
