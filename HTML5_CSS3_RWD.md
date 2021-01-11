###  W3C 制定規格流程

  + p.12 草案 => 最終草案 => 建議案候補 => 建議案 => 建議  
  Working Draft => Last Call Working Draft => Candidate Recommendation => Proposed Recommendation => Recommendation
  
### Ch1
  + 這個網頁真的是經典 !!! 過了幾年 竟然還有更新 新版的 !!! 上面的圖 視窗縮小 竟然會根據 css 更換 src ( 人會疊起來 !! )
  原始碼(break-down):
  
```

  <picture>
    <source srcset="/d/_made/d/misc-images/rwd-4_450_736_81.jpg 1x, /d/_made/d/misc-images/rwd-4_1362_2227_81.jpg 2x" media="(max-width: 450px)">
    <source srcset="/d/_made/d/misc-images/rwd-3_960_690_81.jpg 1x, /d/_made/d/misc-images/rwd-3_1500_1078_81.jpg 2x" media="(max-width: 960px)">
    <source srcset="/d/_made/d/misc-images/rwd-2_1400_761_81.jpg 1x, /d/_made/d/misc-images/rwd-2_2049_1114_81.jpg 2x" media="(max-width: 1400px)">
    <source srcset="/d/_made/d/misc-images/rwd-1_2577_1165_81.jpg 1x, /d/_made/d/misc-images/rwd-1_2577_1165_81.jpg 2x">
    <img src="/d/_made/d/misc-images/rwd-4_450_736_81.jpg" srcset="/d/_made/d/misc-images/rwd-4_450_736_81.jpg" alt="" itemprop="contentUrl">
  </picture>
  
  
  + p.17 1.2-1 RWD 是於 2010 年由 Ethan Marcotte 所倡導的網頁製作手法 『[A List Apart](http://www.alistapart.com/articles/responsive-web-design/)』的報導裡,整理了所有有關RWD網頁設計的基本思維。
  此外,該篇報導可隨著裝置螢幕的寬度變更版面,等同是RWD網頁設計的範例。
### Ch2
  + p.43 這邊 更換 iconmenu 的位置 S 的時候 將 menu 換到下方
  
``` csscode

  #container {
    position: relative;    
  }
  #iconmenu {
    position: absolute;
    right: 8px;
    bottom: 6px;
  }
  #footer {/* 這邊刻意加深底部的高度*/
    padding-bottom: 60px;
  }
  #site,#iconmenu {
    float:none;
  }
    
```
  + css 有時候在設計上,本來就會藏有一些 heck(trick), 但過一陣子可能就不適用..@@...
  + 這邊 css position 有些 細微的不同, 可以參考[這裡](http://zh-tw.learnlayout.com/position.html)了解  
  + p.81 設定 thumbnail 的圖片 max-width: 35%,height:auto  
  達到 當 視窗大小改變的時後, 圖片本身的最大寬度 是 外框的 35%
  
### Ch3 Media Query
  
  + p.96  
  2012.6.19 被 w3c 以最終的 推薦 標準發佈,成為標準規格
  + 瀏覽器 是否支援 某些特性.

  + 撰寫 css MediaQuery 的三種方式

    + HTML內 <link rel="stylesheet" href="example.css" media="only 媒體類型 and (特性)">
    + css 內直接寫  
      @media only 媒體類型 and (特性) {
    
      }
    + css 內匯入  
      @import url("example.css") only 媒體類型 and (特性);
  
  + p.97 媒體類型
  
  + p.119 使用 Modernizr 進行功能判定 支援程度
  + p.123 若是不支援某功能 , 會在 <html> 標籤後自動嵌入 no-xxx 的class值  

    ex:
  ```html
  
  <html class="no-touch canvas geolocation postmessage websqldatabase indexeddb hashchange history draganddrop websockets rgba multiplebgs"></html>
  
 ```
 
  + 當有不支援的情況的時候, 就需 另外設定 不支援css 的 style

### Ch5 高解析度裝置的設定

  + p.174 圖片處理(render) 使用的演算法
    + 雙線性內插法 bilinear interpolation (平滑處理)
    + 鄰近點內插法 nearest neighbor
  + SVG 的使用 p.176...這個項目基本上 一本專書來講也不為過...可大可小...
  + 網路字型服務 - Google Web Fonts


### Ch6 技術性範例 (最實用的一章)

  + p.184 使用 HTML5 表現更明確的網頁邏輯架構  
  HTML5 Tags List:( TODO )
  + p.185 使用 article 可讓 瀏覽器 出現 閱讀器(div, section, article 的差異)
  + p.210 有效率的編排橫向排列的選單(蠻重要...)  
  使用 modernizr (flexbox屬性),
  傳統在排列上 都是用 float:left or right => display: -webkit-box;
  + p.218 這邊設計了三種排版樣式, 分別給 small,medium,large 這三種螢幕大小  
  現在 bootstrap3 的方式來看, 只要在 每個 div 規劃欄寬時 設定 col-xs-3 col-sm-6之類的 class, 讓已經設計好的 class 按照規劃走.
  + p.235 利用  html5 標籤 summary,detail 完成折疊式標題與內容
  + p.237 [動畫效果](http://www.w3schools.com/cssref/css3_pr_animation-keyframes.asp) 這邊直接看範例比較快...這邊的範例並不好...
  [CSS-Tricks](https://css-tricks.com/snippets/css/keyframe-animation-syntax/)