### 導讀 

  + 第四章 頗重要...就是 UX 本身..如何說服團隊不同角色的人,接受與認識 UX
  + 其實從小米的產品,就可以看出 它們重視 UX 這個點.
  + 看到第四章, 有種感覺是...疑, 有點像是在討論 日本人對於任何產品的追求,
    198x 年代, 我去日本的時候就有這種感覺, 他們的飯店就有給人一種很特別的"感覺",
    只不過這種現象從實際商品轉向了網站(頁)上了,日本人很擅長這種"埋彩蛋"的商品設計,
    埋彩蛋做的好可以增加使用者對於商品的黏著性,FF3(太空戰士3)在1980年代就以常常
    埋下一些刻意的bug(用某種特定的方法才能開啟)著名.
  + 抽象科學(學科)

### Ch3 p.25 前端工程 8 流程

  + Topic comfirmation
  + User flow & UX design
  + Wireframe
  + Specification
  + Division of work
  + Front-end developement
  + Issue tracking
  + Testing

### CH4 
  
  能夠感動人的東西, 才能留下好的經驗

### p.41 專家陷阱

  使用者想的與開發者(設計師與工程師)常常有很大的出入,期待的東西也不盡相同.
  
### P.45 新的系統開發流程(P.63對照)

  + 加入UX的系統開發流程
  
需求訪談 => 系統分析與設計 => 系統開發 => 系統上線
   |            |            |          |
   =>      系統雛型設計   系統經驗測試  系統經驗修正
   
### P.47 前端工程師需要被理解, 說服其他角色使團隊走向正循環的理由.

### P.49 UI & UX Difference

### P.52 UX 設計 所需的能力對照與階段

  三種都需要溝通能力
  
  + 前期: 使用者特性研究 - 田野調查, 觀察能力, 把觀察變成文件的能力(文件力)
  + 中期: 使用者介面設計 - 設計能力, prototype(建立雛形)的能力, GUI 知識
  + 後期: 使用者經驗測試 - 記錄能力, Q&A(總結歸納)能力
  
### P.53 誰適合擔任 UX經驗 設計師

### P.63 UX 設計階段

  + 一般網頁 專案流程
    確認產品需求=>設計資訊架構=>介面與互動設計=>程式設計與QA=>系統上線
  
  + UX 專案流程
    使用者特性研究=>確認使用情境=>使用者認知研究=>系統功能測試=>持續收集反饋與修正
    
### P.66 任務1 - 使用者訪談

  + 蠻像在做 碩士論文的 前(後)測....

### P.67 任務2 - 確認使用情境

  + 傳統資訊架構的 UML 設計,忽略了"人"的層面, 少了這一塊, 讓很多即使是系統設計專家,
  卻一再設計出"能用,卻不好用"的系統.

### P.71 任務3 - 使用者認知研究
  
  + 工具 - Balsamiq
  介面與互動, 是使用者是否會愛上這個系統的關鍵因素,這時候最適合的工具, 就是製作系統 wireframe.
  wireframe 應該專注在每個頁面應該顯示的資訊, 如何將大量的訊息做區分與如何讓這些元素帶給使用者價值.
  而不是浪費時間在視覺的呈現, 因為那是確認流程後才需要做的事情.
  
### P.75 任務4 - 系統測試
  
  盲測是重點, 真實的體驗
  
  + 記錄&追蹤
  + 設計測試任務 - 在旁邊觀察並記錄完成花費的時間 與 所有碰到的問題
  
### P.76 持續收集反饋與修正

  + A/B Test - 讓數字(使用者)說話,而不是你自己說了算
  
### P.79 7E 概念

  + 容易學習 Easy to learn
  + 有用的 Effective
  + 有效的 Efficient
  + 容錯 Error tolerant
  + 迷人的 Engaging
  + 使人上癮的 Enchanting
  + 出眾的 Eminent
  
### Ch6 開發工具

  + P.92 程式碼管理.
  + git 工作模式
    + subversion-style workflow
    + integration manager workflow
    + dictator and lieutenant workflow

### *** P.98 JQuery Cheat Sheet ***
  
### P.104 IE 黑歷史

### P.152 CSS3 產生器

### P.160 JS 常用事件類別
  + p.161原生aJax 因為不同瀏覽器而有不同的寫法, 所以 使用 JQuery 的 ajax 會比較好.

### P.162,163 CROS 問題解法
  
  + 在 JQuery 1.2 就有提供 JSONP 這個 CORS 的解法(使用 callback )

### P.164 Callback
  
  + 使用情境 ( 想要分開監聽事件與執行事件以達到邏輯分離 )
  
### P.165 WEB Performance
  
  + 減少 request
  + 壓縮程式碼, 壓縮圖片(可接受的失真率)
  + 改善js不優良的寫法
    + 可以用 css 呈現, 就不要用 js
    + 大量迴圈時, 分段(切細)處理 個別片斷, 再將結果相加
    + 減少使用 try catch
    + 減少使用 global variable
    + 縮短變數名稱
    
### P.167 JS Framework 介紹 - Backbone, Angular,requireJS

### P.172 JQuery 

### P.178 JQuery 的優缺點

  + window.onload() V.S $.ready()
    + onload 是 所有的內容都載入完畢才開始觸發
    + ready 是 DOM 載入完畢就開始觸發
  
### P.182 JQuery Selector

### P.186 優化 JQuery

  + 挑選合適的選擇器 : id > tag > class > attribute
  + 儘量使用原生的 Javascript
  + 將選取出來的元素放到變數中, 不要想到才選取
  + 使用 JQuery CDN
  + 使用 chaining method

### P.190 JQuery 外掛資源 
  
  + JQuery UI,Mobile,UI Effects,flot,Chop Slider3,LazyLoad,Datatables
  
### P.191 JQuery 相關網站

  + 官方永遠不會掛...@@
  + [JQuery for Designers](http://jqueryfordesigners.com) 掛了...
  
### Ch13 學海無涯

  + P.212 學習更多專案知識
    + i18n
    + REST風格 - 具有語意的系統網址服務
      + Representational State Transfer
      + Rest風格的 WebService 範例
    
```

http://product.com/products       READ    GET     取得產品列表
http://product.com/products/123   READ    GET     取得產品 123 的內容
http://product.com/products       CREATE  POST    新增一個產品
http://product.com/products/123   DELETE  DELETE  刪除產品 123
http://product.com/products/123   UPDATE  PUT     更新產品 123

```

    + 持續整合 CI - Continuous Integration
    + MVC 
    + 了解各種資料格式
    + SEO
  
### ** P.217 前端 Framework - Bootstrap **

### Ch13.4 學習更多電腦科學
  
  + 至少一種後端程式語言
  + 重構
    + 重構的進行通常會搭配 單元測試, 如此才能確保在重構的過程中沒有將系統的邏輯破壞掉,確保系統的穩定性.
      而許多 IDE 就有內建重構的功能, 有效提升程式碼品質.
  + TDD - 核心概念是 在 撰寫程式之前, 就先撰寫測試程式碼.
  + Design Pattern
  + 正規表示法 ... 恩, 這是另一本書 :)
  + 網路安全
    + 前後端防呆
    + 程式碼注入 Injection  
      利用 form 提交(submit)一些混合程式碼的內容,而資料庫記錄下之後,這段內容又會在某個地方被呼叫或是執行到
      ,就可能間接的執行到當初提交的惡意程式碼.
    + 跨站請求偽造 - CSRF
    + XSS Cross-site scripting 跨網站指令碼 - 安全漏洞攻擊
    
### Ch13.5 善用各類線上資源
  
### Ch14 基本設計概念

### Ch14.3 常用的設計語言

  + 點陣圖 ( bitmap or raster )
  + 向量圖 ( vector )
  + UCD ( User Center Design ) - 以使用者為中心的設計方法
    + UCD design question
      + 誰是使用者
      + 使用者的認物和目標是甚麼?
      + 使用者的期待, 我們有提供嗎?
      + 使用者期帶從我們這裡得到甚麼?
      + 使用者可能期待的資訊是甚麼?
      + 使用者覺得我們會怎麼做?
  + 留白 - 提升使用者經驗 & 質感
  + CIS - 企業識別系統
  + 惹惱設計師金句 - 呵呵...

### Ch14.5 通知訊息設計

### Ch14.6 設計資源素材

### Ch15 關於字型

  + 襯線與無襯線 sans & seri-sans
  + 中文字型代表的個性 - List
  + 英文字型代表的個性 - List
  + Moo0 FontViewer
  
### Ch16 學習色彩

  + 色彩與心理學
  + 視線流動
  + 色彩的情緒
  + 色彩與感覺
  + 色彩與年齡偏好
  
### Ch16.5 其他色彩議題

  + 為色盲而設計
  + 配色相關網路資源
  
### Ch18 APP 與 行動版網站的取捨

  + P.294 原生app,行動版網頁,Hybrid網頁 app 三種優缺點比較表
    + 原生 app:  
      iOS: Object-C, Android: Java
    + 行動版網頁:  
      HTML5,CSS3,Javascript
    + Hybrid網頁 app  
      HTML5,CSS3,Javascript,WebView,APP 包裝技術(PhoneGap,Sencha Touch)
      
### Ch19 自適性設計
  
### Ch20 少即是多

### Ch21 行動版網頁設計技巧 P.325

  + P.336 型式追隨功能 ( Forms Follow Function )  
    + 過去此概念比較常用在 工業與建築設計上面, 引領設計師門不斷力求做出好看又好用的工業設計作品.
    + 指的是設計本身就是具有功能性,而非單純為了美觀而設計 - 出自 建築大師 路易士沙利文.
  
  + 形式追隨功能的精神特點  
    + 極簡設計
    + 好的產品必須好看又好用
    + LESS IS MORE
    + 美感來自於純粹, 沒有其他裝飾
    + 設計應該注重功能性, 美感是次要考慮
    
  + P.338 打造 "可按" 感覺的技巧整理  
    + 光澤,漸層,陰影 營造立體感
    + 形狀, 模擬一般人所認知的按鈕
    + 區塊與色塊, 提供按鈕不同的狀態
    + 文字輔助提示
    
  ( 下面兩個應該很難形容...通常都是看到有人這樣應用..然後抄襲..)  
  + P.339 打造 "可抽" 感覺的技巧整理
  + P.340 打造 "可捲" 感覺的技巧整理 ( 向下,上滑動捲軸 )