---
title: VS Code 的相關設置
date: 2023-07-20
description: 介紹了如何設定在 VS Code 中可以執行 C/C++ 的方法，適用於 Windows 環境，還有一些 MinGW 編譯器相關的介紹。
path: blog/vscoode-setting
draft: true
taxonomies:
  categories: 
    - Coding
  tags: 
    - VS Code
---

強烈建議 : 不確定正確與否的設定不要亂設，不然解除安裝都改不回來，改了什麼設定要記得紀錄下來。以下部分驗證後確定沒問題。

---

## 終端機輸出中文出現亂碼問題
參考自[解決VScode（C/C++）終端輸出中文亂碼的問題](https://blog.csdn.net/qq_46323094/article/details/118069069)

依次點選“檔案”–“喜好設定”–“設定”–“使用者”–“功能”–“終端機”–“在settings.json中編輯(Integrated >Automation Profile : Windows)”;

```json
//新增下面這一段進去
"terminal.integrated.profiles.windows": {
        "PowerShell": {
        "source": "PowerShell",
        "overrideName": true,
        "args": ["-NoExit", "/c", "chcp 65001"],
        "icon": "terminal-powershell",
        "env": {
            "TEST_VAR": "value"
        }
        }
    },
    "terminal.integrated.defaultProfile.windows": "PowerShell",
```




## 字體大小設定更改

參考自[Day03 | VSCode使用者與工作區設定](https://ithelp.ithome.com.tw/articles/10238252)

## 開啟檔案出現亂碼

參考自[vscode中文亂碼怎麼解決 vscode輸出亂碼怎麼解決](https://iter01.com/683056.html)