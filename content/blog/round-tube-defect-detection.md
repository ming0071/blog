---
title: 圓管缺陷檢測
date: 2024-01-29
description: 藉由極座標轉換的方法做圓管的缺陷檢測，並用 C++ 結合 opencv 函式庫的方式實現
path: blog/round-tube-defect-detection
draft: false
taxonomies:
  categories: 
    - Coding
  tags: 
    - open cv
    - circle defect
---
在碩一上的自動光學檢測這門課的做了一個期末專案，目的是要檢測出排列好在桌上的圓管缺陷，看否有凹陷、突起的情況發生，藉由光學檢測的形式標記 NG 品出來，本專案的程式也有公開在[github](https://github.com/ming0071/112-1_AOI-final-project)提供有興趣的人使用。

專案方法是由工業相機對金屬圓管取像之後，再由 C++ 結合 opencv 函式庫進行後續的影像處理，本篇文章主要對於軟體上影像處理的過程進行說明。<br>
以下是專案中的圓管的實際照片試例:<br>
<a href="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/tube.png" data-fancybox data-caption="tube">
  <img src="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/tube.png" loading="lazy" alt="tube" width="520"/>
</a><br>
程式流程圖:<br>
<a href="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/circle.png" data-fancybox data-caption="code-flow">
  <img src="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/circle.png" loading="lazy" alt="code-flow" width="520"/>
</a><br>

## 圖片預處理

第一步讀取經由工業相機拍攝之後的照片，後續經由中值濾波、二值化、開運算等基本影像處理後，接著提取出最外輪廓去除(即最大面積輪廓)，得到僅保留內圓輪廓的效果，確保後續的霍夫測圓可以只抓取內圓的特徵做後續的影像辨識。<br>
由下圖比較可以發現去除最外輪廓之後可以得到更好的結果。
<a href="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/pre-process.png" data-fancybox data-caption="pre-process">
  <img src="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/pre-process.png" loading="lazy" alt="pre-process" width="520"/>
</a><br>

## 以極座標轉換做輪廓檢測

一開始先是由霍夫轉換得到每個圓的圓心座標、半徑，對其結果進行上到下、左而右的排序，確保每次經由霍夫計算後得到的圓是固定的順序，接下來就可以對每個圓抓取 ROI 並開始極座標輪廓檢測的過程。<br>
1. 極座標轉換
2. 均值濾波，以(3,501)的濾波核進行濾波，得到假想的完美圓，即沒有缺陷
3. 差值計算，以極座標轉換和假想圓做差值計算，這樣得到的結果就會是缺陷的特徵
4. 缺陷特徵二值化
5. 缺陷特徵輪廓抓取
6. 反極座標轉換

<a href="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/process.png" data-fancybox data-caption="process">
  <img src="https://github.com/ming0071/112-1_AOI-final-project/blob/main/docs/process.png" loading="lazy" alt="process" width="520" />
</a>

而缺陷的判定就可以藉由計算每個圓內缺陷區域內的像素面積而得，當大於設定的閥值即為 NG、小於設定的閥值即為 OK

## 實時的讀取影片進行辨識

當改以非照片形式做缺陷辨識時需要改變先前的判定邏輯，因為以照片為輸入做霍夫測圓而得到的影像光影是固定的，不太會有什麼變化產生，但是改以影片作為輸入時，每幀影像的光影都有些微的差別，而這些細微的差別就使的每次霍夫檢測的圓心、半徑特徵有所變化，讓極座標的過程不穩定，會使判定的結果不斷地閃爍，而不是穩定的輸出。

而影片新的缺陷辨識邏輯大致與圖片相同，每幀影像依舊是以缺陷區域內的像素面積為參數，看他使否大於設定的閥值判定 NG 與否，當判定 NG 一次時，就會給該圓的結果減 1；反之， OK 則加 1，這樣的一次過程就是算一次的投票。

而每幀都會經過一次這樣的投票過程 ，依據這樣的結果決定顯示該圓是 NG 或是 OK，避免了輸出結果閃爍的可能性，當經過多次的運算之後會使的輸出結果穩定，就算過程中出現少數的失誤判斷也不會影響結果的顯示。