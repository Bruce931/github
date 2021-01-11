### Ch3 前進 HTML5
  
  + HTML5 特點
  + HTML5 文件架構(標籤),元素(標籤)
    nav,header,article,section,footer,aside
  + article and section difference
    article 是可獨立表現的 文件主體.
    article 可以增加搜尋引擎的可讀性
  + header,hgroup
  + mark,em,figure
  + detail with summary ( NOT For IE )
  + draggable
  + HTML5 Video,Audio controls
  
### Ch4 樣式
  
  + color 表示法(147 preDefined colors)
  ```    
    #Hex
    rgb(R[0~255],G[0~255],B[0~255])
    rgba(R[0~255],G[0~255],B[0~255],Alpha[0.x~1])
  ```
    
### Ch5 Javascript & JSON
  
  + p5-5,6 Data Types
    String,Number,Boolean ( 包裹過的 js object type,the same as Java )
    + JS raw types are : number,string,boolean,object,function, undefined
    + differnece between null,undefined,0,1,true,false
  + p5-8 check datatype of variable
    ```
    var index = 5;
    var result = (typeof index ==='number') // true
    ```
  + p5-11 解釋了 == 在 js 會自動轉型成 後面的型態
  
    ```
    var zero = 0;
    var falseVar = false;
    zero == falseVar; // true
    zero === falseVar // false
    ```
  + p5-19 刪除 array 內的資料 需用 splice(deleteIndex,deleteNumber)
    ```
    var array=[1,2,3];
    array.splice(1,1);
    ```
### Ch6 DOM(Document Object Model) 簡介

  + p6-7 EventListener (IE6~8 Not Supported)
    addEventListener(eventName,listenerFunction,bubbles)
    removeEvenListener(eventName,listenerFunction,bubbles)
    attachEvent,DetachEvent(For IE6~8)
    
### Ch7 JQuery

  + JQuery 很重要的元素是 selector, pseudo selector, chain methods, callback(JS basic),
  + p7-11 常用方法列表
    + $(selector).addClass
    + .each,
    + [.show](http://api.jquery.com/show/),
      .hide( [duration ] [, complete ] )
      duration : 400(millisecond) = 0.4s
    + [.hide](http://api.jquery.com/hide/)    
    + [.css](http://api.jquery.com/css/)
    + .eq(index) // index start from 0 
    + .filter
      $(selector).filter( selector );
    + .find
      find element inside the result of JQuery (selector) Object 
    + method: first, last(), next(), prev()
    + evnet handle:
      + [.focus,focusin,focusout](http://api.jquery.com/focus/)
      + [.click,dbclick,error]
      + [.keydown,keyup,keypress]
      + [.hover.mousedown,mouseup,mouseleave,mouseout,mouseover,mousemove]
      + [.load,unload,ready]
        注意: ajax 特有方法 done,fail[p9-13]
        ```
        $.ajax({options
          }).done(function(){
          
          }).fail(function(){
          
          });
        ```
          
      + [.select]
      
### Ch8 HTML5 Form Validation

  + p8-4 新增 optgroup 選項大標的標籤
    ```
    <select id="xx" name="yy">
      <optgroup label="optgroup1">
        <option value="val1">lbl1</option>
        <option value="val2">lbl2</option>
      </optgroup>
      <optgroup label="optgroup2">
        <option value="val1">lbl1</option>
        <option value="val2">lbl2</option>
      </optgroup>
    </select>
    ```
  + p8-5 新增 datalist [ 推薦清單 ]
  + p8-8 新增 input types
    + number => min and max ( step遞增數 )
    + email
    + url [ 可配合 pattern 在行內驗證 ]
  + p8-9 新增 input 屬性( properties )
    + autofocus
    + autocomplete
    + required
    + **pattern**(配合正規表示法)
    + placeholder
    + **title** ( 輸入錯誤後的提是訊息)
    ```html5
    ex:
      只能輸入英文字 的 pattern :      
      <input type="text" required title="只能輸入大寫英文字" pattern="[A-Z]+" />
      ```
  + p8-14 正規表達式 簡介.
  
### Ch9 AJAX

  + p9-14 資料表單序列化.
  
### Ch10 CSS3 with HTML5

  + p10-24 pseudo-classes,pseudo-elements
    + ::first-letter
    + ::first-line
    + ::before,::after
    + ::selectiopn
  + p-28 應用於 form 的 pseudo classes
    input:enabled,disabled,checked,focus,hover

### ***Ch11*** train your Javascript with Good habit [30 pages]
  
  + p11-2 ***這邊的範例與觀念很重要*** hoisting(變數提升), scope(變數的可視域)
    變數提升這邊的範例在於強調 {} 這個是用來區分 程式碼的 Block definition sign
    只要在 { } 內的都是 區域變數範圍.( **any** {} block include **if block** )
  + p11-3 管理全域命名空間
    + iif(JQuery使用),Namespaces,strict mode
  + p11-5 單體 singleton
    在使用單體時, 有時會有人使用 延遲載入(lazy loading)來達到某些目的(non-Blocking).
    ex: Math class(global static object)
      + [MDN Network](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects)
  + p11-6 自訂物件 ( 比較 p11-4 利用命名空間的方式 )
    Javascript利用了 this 關鍵字(相對於 Java 的 private存取子)來模擬物件導向的封裝(閉包使用),
    讓外界不能(不可存取)這個物件的屬性或方法
    (不同於 Java 使用 public,protected,private,default存取子來控制) 物件的可視性,
  + p11-12,13 使用建構子,prototype
  + p11-16 Object.create()
  + **p11-28,29** 這兩個範例很重要
    常見的js誤用: 要在 callback 函視內存取外部(這個block之外都算)變數:
    
    ex:
      ```javascript
      var Obj = {
        var that = this,
        this.funcA = function(opt){
          ...  
        };
        
        $.get('data.xml',function(){
          that.funcA(optB); // 不使用 that 會錯 !!
        });
      };
      ```
### Ch12 HTML5 API 
  
  + p12-5 範例 : custom event handler
    ex: 
      event.stopPropagation(); // 不要 stacked callback bubble up;
      event.preventDefault();  // 不使用 預設返回方法;
      
### Ch13 offLine support
  
  + 傳統: cookie, session,
    cookie: 20組/4kb 的 key/pair objects
    session: 存在於 Server, 有隱匿性 但可偽造.
  + ***HTML5 新增 localStorage(10 mb),sessionStorage*** // 需判斷是否 有支援 (js modernizer library)
  + p13-15 ***Indexed Database API***
    ```    
    var db,
      idb = indexedDB.open(dbName);
    idb.onsuccess = function(event) {
      // 此處 event 也可以省略不寫, 改寫成 idb.result
      db = event.target.result;
    };
    idb.onerror = function(event) {
      // 此處 event 也可以省略不寫, 改寫成 idb.errorCode
      alert("error: " + event.target.errorCode );
    };
    ```
  + p13-16 add delete method
  + p13-17,19 範例1-index簡單搜尋,範例2-標籤雲(範例有點難,做標籤雲有很多種實作方式 QQ)
  + **p13-19~34** 自訂物件結合 正規表示法 (不錯的範例)
    split( /\s*,\s*/ ) // 代表 要依照 前後不管有多少空格, 只要中間有一個 , (逗號)
    這樣的 pattern 來切割字串成陣列.
  + p13-46 測試網路連線寫法.
    navigator.onLine ( true or false )
    
### Ch14 RWD
  
  + p14-5 wbr v.s br ( for english only )
    wbr: 依照音節來斷字
    br : 自行斷行
  + p14-8 caniuse.com 了解各瀏覽器支援 各個 html properties 的支援程度
    + 友善列印版本的 css
      ( 去掉大圖,頁首,尾,menu,動畫,flash,背景色[灰階或深色時],超連結換成網址 )
      p14-18 有範例
      
  + p14-9 media types
    + 設計各種 media(媒體) 的 css
      + ex: 手機就 字大一點,排版欄位較少
  + p14-12 Media Queries
    + 加強了 css(CSS3) 檔案內 具有邏輯選擇性的可能性
    + 兩種作法
      1. 直接在 html檔案內的 link tag 內做分類
        // 襯線 就是 字體的 邊角處 不圓滑 ( 看起來較工整 ), sans 法文意為 "無(沒有)"
        // 當 media queries 查詢到是使用於 一般螢幕時, 使用 無襯線(字)的版本的 css
        <link rel="stylesheet" type="text/css" media="screen" href="sans-serif.css">
        // 當 media queries 查詢到是使用於 列印 時, 使用 有襯字的版本的 css
        <link rel="stylesheet" type="text/css" media="print" href="serif.css">
      2. 在 css 內做查詢並分類
      ```
        @media screen and (max-device-width:480px) and ( resolution:300dppi)
        {
          ...(略)
        }
        ```
  + p14-15 透過註解的方式偵測舊版的IE瀏覽器(這也只針對 css )
  + p14-19 設定列印版本的左右邊界

### CH15~16 SVG & Canvas ( 跳過~ 有點難~ 這麼難用遲早會被淘汰 @@ )

### CH17 CSS Transition ( 跳過 again ~~)

### ***Ch18*** web socket 即時通訊 ( 沒做過相關的練習過@@ )

### ***Ch19*** web workers 背景處理程序( 沒做過相關的練習過@@ )
