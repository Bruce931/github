## JavaScript 設計模式與開發實踐 - 曾探 
- [參考 - 阮一峰的 BLOG - JS](http://www.ruanyifeng.com/blog/javascript)
- [參考 - 阮一峰的 BLOG](http://www.ruanyifeng.com/blog/archives.html)

###  重點摘要
---
##### 第一，三部分算是作者的總整理與體會的部分，範例很多，當然也有些是重複的，看到後面可以理解作者第一部分的故事安排（起承轉合）。

* 前言
    *   iii. 設計模式的定義 : 針對特定問題的簡潔而優雅的解決方案。
    *   vii. 模擬JS版的 Factory Method而把建立物件的步驟延遲到子類別中。實際上，在Java中，讓子類別來建立物件的原因是為了達到DIP(依賴導置原則)，降低耦合，表現物件多態。
* 第一部分重點

    ##### 第一次看會覺得很混亂，因為作者用漸進式的敘述方式，一開始安排的是較不好的實作方式或是較少功能的實作。所以，最好是看兩遍以上，體會作者為什麼這樣寫。
    ---
    *   ch2 this,call and apply [阮一峰的blog參考](http://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html)
    *   ch3 closure and higher order function
        * closure def: 將閒置變數(封閉並)裝在匿名(返回)函數內的行為
        * p44. 封裝變數、延續變數的生命週期
        * highter order function def: 被當作參數傳遞或返回輸出( 回呼[**callback**] 函數 )
            * p.55(P300) 透過原型鏈增加(擴展[extend])函式功能的實例
            * p56 高階函數的應用
                + 部分求值(柯里currying)
                + uncurrying
                + 函數節流
                + 分流
                + 惰性載入函數(lazy loading)
    *   ch8
        *   p129. p134. 發佈-訂閱模式(觀察者模式)實例
        *   p137. 命名衝突的處理.
* 第三部分 (**重點**)
    *   ch18~ch21 (SOLID) [線上參考](http://www.hitripod.com/blog/2011/12/object-oriented-design-five-principles-solid/)
            S: 單一類別單一責任、低耦合。
            O: 開放擴充、封閉修改。
            L: 類別間的相容性。
            I: 介面要特定目的、易懂、可再用性高。
            D: 抽象化。
            
            S: SRP - Single Responsibility Principle 單一職責原則
            O: OCP - Open-Closed Principle 開放 - 封閉原則
            L: LKP - Liskov’s Substitution Principle 子類別必須可以被父類別的所替換
            I: ISP - The Interface Segregation Principle 介面隔離原則
            D: DIP - The Dependency Inversion Principle 依賴導置原則
        *   ch18 SRP - 代理模式,迭代器模式,單例模式,裝飾者模式(ch20.p300)
        *   ch19 LKP - 中介者模式,外觀模式
        *   ch20 OCP - p300. 透過原型鏈增加原有函式的功能.p305. 觀察者模式,範本模式,策略模式,職責鏈模式
        *   ch21 ISP - 命令模式
            * p6-p13 多態, p14-p16 封裝 p22-27 原型繼承,
            * p316 Object.prototype.toString.call([]) === '[object Array]' 判斷變數是否為物件
            * p316 用TypeScript實作 命令模式的介面
    *   ch22 重構(Refactor) （**重構技巧**）
        *   ch22 - DIP - Refactor Tricks.
        
### 個人觀點
---

*   沒有中英文對照：語言開發者通常都是歪國人，所以原文變的相對重要，譯文沒有翻的貼切還不如看原文比較能夠了解。
*   範例蠻多的，值得列入收藏（但是沒有設計模式的使用情況分類）
*   盡信書，不如無書：每個程式設計師都有個人喜好和習慣，沒有絕對的好或壞，我們只能盡量朝著較好的方向去前進。
*   一股腦兒的介紹模式，通常結果都是吸收不良（需要不斷的閱讀和實作才能熟練）