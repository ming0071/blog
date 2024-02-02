---
title: 在 vscode 上執行 opencv 的 json 檔設定
date: 2024-02-01
description: 介紹了如何設定在 VS Code 中可以執行 opencv 的方法，適用於 Windows、MinGW 環境，主要是在 json 檔的設定。
path: blog/vscoode-opencv-setting
draft: true
taxonomies:
  categories: 
    - Coding
  tags: 
    - VS Code
    - opencv
---

## 先對本機端電腦的環境進行設定

1. 安裝好mingw64、vscode
2. 下載安裝opencv，這裡有 2 種方法，但我建議自使用第一個方法，比較不會出錯 :
  - 從[官網](https://opencv.org/releases/)下載後再自己用 CMake 編譯
  - 直接使用其他人編譯好的文件
    - [huihut](https://github.com/huihut/OpenCV-MinGW-Build)，注意規格是否相符於安裝好的 mingw64 與作業系統
    - [Kirigaya](https://gitee.com/kirigaya/opencv_built_by_gcc_on_-windows)
3. 把 opencv 的 bin 資料夾放到環境變數裡面
4. 把 opencv include 裡面的opencv2 資料夾複製到 mingw64 的 include  資料夾裡面
5. 把 opencv lib 資料夾內的內容複製到 mingw64 的 lib 資料夾裡面


# 對 vscode 的環境進行設定

vscode 之中有很多

1. 使用 code runner ，可以簡單使用 code runner 直接編譯
