# [Flexbox](http://learnlayout.com/) Note


## 關於 "display" 屬性 (重要度-五顆星 )

display 是設計 CSS 版面配置中最重要的屬性，**每個 HTML 元素都有一個預設的 display 值**，不同的元素屬性會有不同的預設值。大部分元素的 display 屬性，預設值通常是 block 或 inline 其中一個。若該元素的 display 屬性被標示為 block 就被稱為「區塊元素」，若被標示為 inline 就稱為「行內元素」。 

  + block 
  
  div 是一個標準的區塊元素。一個區塊元素會讓其內容從新的一行開始顯示，並盡可能的撐滿容器。其他常用的區塊元素包括 p 、 form 以及一些 HTML5 新出現的元素，例如：header 、 footer 、 section 等等。
  
  + inline
  
  span 是一個標準的行內元素。一個行內元素可以在段落中 <span> 像這樣 </span> 包裹一些文字片段，透過 CSS 點綴其樣式，且不會打亂段落原本的版面配置。 a 元素是最常見的行內元素，它可以被用作超連結之用。 

  + inline-block
        .box2 {
          display: inline-block;
          width: 200px;
          height: 100px;
          margin: 1em;
        }
  在 較小螢幕下觀看 會自動往下排版
        
  + none
  
  另一個常用的 display 值是 none 。有一些特殊的元素 display 預設值會套用 none 屬性值，例如 script 元素就是個典型的例子。display:none 通常會搭配 JavaScript 一起使用，我們可以透過 JavaScript 動態修改元素的 display 屬性，用以隱藏或顯示該元素，而不是將元素從頁面中刪除或重建。
  
  display 和 visibility 屬性不一樣，把 display 設定成 none 不會保留元素原本該顯示的空間，但是 visibility: hidden; 會讓元素的內容看不見，但會保留原本內容應該顯示的空間，只是看不到內容而已。 

  + 其他 display 值
 
  還有很多其他的 display 值，例如 list-item 和 table 等等，[這裡有一份詳細的列表](https://developer.mozilla.org/en-US/docs/CSS/display)，你可以連進去查看完整的屬性值清單。稍後我們會探討 inline-block 和 flex 這兩個屬性。 
  
### 補充說明

就像我之前說過的，每個元素都有一個預設的 display 屬性，不過你可以隨時隨地地覆蓋這個屬性值。雖然我們把 div 修改成一個「行內元素」好像還蠻怪的，不過實務上來說我們會把某些元素修改掉預設的 display 屬性，好讓它可以呈現有特定語義的元素。其中比較常見的例子就是把 li 元素修改成 inline，以便我們將該元素正確地呈現在水平的選單上。 

## 使用 Flexbox 配置居中的版面

    .vertical-container {
      height: 300px;
      display: -webkit-flex;
      display:         flex;
      -webkit-align-items: center;
              align-items: center;
      -webkit-justify-content: center;
              justify-content: center;
    }
    
## margin: auto;

    #main {
      width: 600px;
      margin: 0 auto; 
    }
    
設定區塊元素的 width 屬性，可以避免該元素從左到右撐滿容器，然後你可以設定左右外邊距（margin-left 與 margin-right）為 auto 來使其水平居中。元素在顯示的時候，只會顯示到你所指定的寬度，然後剩餘的寬度平均的散落在左右兩邊的邊距上。     

## 關於 max-width 屬性

    #main {
      max-width: 600px;
      margin: 0 auto; 
    }
    
 使用 max-width 替代 width 可以更完美的處理當瀏覽器視窗小於元素寬度的情況，這點在行動裝置上顯得更為重要，你現在就可以調整瀏覽器視窗大小看看這頁的變化！

另外，max-width 屬性幾乎在所有的主流瀏覽器都有支援（包括 IE7+ 以後版本），所以各位可以不用擔心有瀏覽器相容性的問題。 

## 關於 box-sizing 屬性

經過了幾個世代的轉變，人們意識到自己運算出元素的寬度實在很無趣，所以終於出現了一個叫做 box-sizing 的 CSS 屬性。當你設定一個元素樣式為 box-sizing: border-box;，這個元素的內距和邊框將不會增加元素本身的寬度。我們用跟上一頁一樣的例子，但我們將兩個元素都設定了 box-sizing: border-box; ：

    // 以下兩個 class 同樣大小 , 因為設定了 border-box;
    .simple {
      width: 500px;
      margin: 20px auto;
      -webkit-box-sizing: border-box;
         -moz-box-sizing: border-box;
              box-sizing: border-box;
    }

    .fancy {
      width: 500px;
      margin: 20px auto;
      padding: 50px;
      border: solid blue 10px;
      -webkit-box-sizing: border-box;
         -moz-box-sizing: border-box;
              box-sizing: border-box;
    }    

### 重新設定所有元素成 border-box

    * {
      -webkit-box-sizing: border-box;
         -moz-box-sizing: border-box;
              box-sizing: border-box;
    }
    
因為 box-sizing 算是個比較新的屬性，所以你還應該還是要加上我之前在例子中使用的 -webkit- 和 -moz- 前綴（Prefixes），這樣才能啟用特定瀏覽器實驗中的 CSS 特性。請記得該屬性從 IE8+ 之後就開始支援。

## Multiple column  多欄文字版面

    .three-column {
      padding: 1em;
      -moz-column-count: 3;
      -moz-column-gap: 1em;
      -webkit-column-count: 3;
      -webkit-column-gap: 1em;
      column-count: 3;
      column-gap: 1em;
    }
    
CSS3 Multiple Columns 是很新的標準，所以你需要使用前綴，並且它不支援 [IE9 以下和 Opera Mini 版本](http://caniuse.com/#search=column)。還有許多和 cloumn-* 相關的屬性，[點擊這裡瞭解更多](http://www.quirksmode.org/css/multicolumn.html)。
