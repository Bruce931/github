### 導讀

  [ES6(ECMAScript2015)](https://goo.gl/CAQXKC)(看完應該好幾個月後了@@ - 就算快速掃過也大概要一個月以上...)  
  (*) 表示 重要  
  (s) 表示 速記

### ES6 新功能

   + [overview of well-known symbols](https://goo.gl/VZoZRQ)
    + 调用Symbol.for(string)。这种方式会访问symbol注册表，其中存储了已经存在的一系列symbol。  
    这种方式与通过Symbol()定义的独立symbol不同，symbol注册表中的symbol是共享的。  
    如果你连续三十次调用Symbol.for("cat")，每次都会返回相同的symbol。  
    注册表非常有用，在多个web页面或同一个web页面的多个模块中经常需要共享一个symbol。      
      + 只有用 Symbol.for() 找出來的 Symbol 才會是一樣的
      + 簡單講, Symbol 就是用來抽取(象)出共用變數的一種方法
      
### 3.18 Function Overloading

  JavaScript functions don’t have typed signatures
  which means they can’t do overloading•
  When you define multiple functions with the same name,
  the one that appears last in your code replaces any previous ones
  
  Check for named arguments to simulate overloading

    ``` JS     
    function sayMessage(message) {
      console.log(message);
    }

    function sayMessage() {
      console.log("Default message");
    }

    function sayMessage(message) {
      if (message === undefined) console.log("Default message");
      else console.log(message);
    }
    sayMessage("Hello!"); // => Hello sayMessage(); // => Default message  
    ```

### 3.20 Dynamically Defining Functions
  
  Functions are usually defined with function keyword 
  
  ```
  var f = function (x, y) { return x * y; };
  ```
  
  Functions can also be defined with Function constructor (they will be anonymous)
    •Expects any number of string arguments
    •The last argument is the function body, others are arguments 

  ```
  var f = new Function("x", "y", "return x * y;");
  ```
  
  Always defined as if they were top-level functions i.e. with global scope  

### 3.21 Documenting for IntelliSense

  Use brackets FuncDocr pplugin ( Ctrl+Alt+D ) extract parameters to document


### 3.22 Understanding Function Parameter Documentation
  
  Note that because JavaScript is very flexible with passing arguments, the documentation describes which parameters are required or optional
  
  ```
  JQuery.get(url[,data][,success(data,textString,jqXHR)][,dataType])
  ```
  
### 3.25 document and window Events

  ```
  // a custom function to hide IE weirdness
  function addEvent(obj, eventName, listener) {
    if (obj.addEventListener) {
      obj.addEventListener(eventName, listener, false);
    } else {
      // IE 8 and earlier 
      obj.attachEvent("on" ### eventName, listener);
    }
  }
  ```
### 3.27 Event Object (*)

  + Some useful properties
    + currentTarget: the element whose listeners caught the event
    + target: the element that triggered the event
    + cancelable: can an event have its default action prevented
    + eventPhase: one of the event phase constants:
    + CAPTURING_PHASE (1), AT_TARGET (2), BUBBLING_PHASE (3)
  + Some useful methods
  
    + preventDefault(): any default action normally taken (要作 override 時 => a tag 模擬 click 事件卻不連結 href ( 預設 a tag 會有的動作))    
    + stopPropagation(): prevent further capturing/bubbling (停止 callback)
    + [understanding return false] (https://goo.gl/oPCYuo)
      + 理解return false，尽量避免使用它，请用event.preventDefault()替代return false。
    
### 3.30 Catching and Throwing Errors

```
try {
    try {
        console.log("Nested try running...");
        // to throw a custom error pass unique number and string 
        throw new Error(301, "an error message");
    } catch (error) {
        // number, description, message properties
        if (error.number === 301) console.log("my error");
        console.log("Nested catch " ### error.message);
        throw error; // rethrow 
    } finally { /* clean up */ }
} catch (e) {
    console.log("Outer catch " ### e.message);
} finally {
    console.log("Outer finally running");
}
```

### 3.31 Null-Coalescing Operator (s)

  ```
  if (x) { 
    // if x is usable, i.e. NOT undefined, 
    answer = x; 
    // null, false, etc., then use it 
  } else { 
  // otherwise, use some default value 
    answer = someDefault; 
  }
  // equal to the code below

  answer = x || someDefault;
  ```

### 3.32 this in functions (*)

  If you define a variable or function in the global scope in a browser,
  this is the window
  
  ```
  // this is the window object
  function thisExamples(parameter) { 
    this.number = 1; 
    console.log(this.number); // => 1 
    number = 2; // same as this.number 
    console.log(this.number); // => 2 
    console.log(parameter); // => 4 
    this.parameter = 3; // different from parameter 
    console.log(this.parameter); // => 3 
    console.log(parameter); // => 4 
  }
  
  thisExamples(4); 
  console.log(this.parameter); // => 3 
  console.log(this.number); // => 2
  ```
### 3.33 this in Event Handlers (*)

  ```
  $("div").click(function () {
    // this will be the DOM element for the div that was clicked, 
    // so you could (for instance) set its foreground color: 
    this.style.color = "red"; 
  });
  ```
  
### 3.34 this in Event Handlers (*)

  + What does this refer to in doSomething?
  ```
  function doSomething() {
    alert('clicked: ' + this);
  }
  ```
  
  In JavaScript this always refers to the “owner” of the function,  
  usually the object that a function is a method of
  
  In the example above, window is the owner of doSomething()

  + An onclick property, though, is owned by the HTML element it belongs to, so if we do this, this now refers to the element
  
  ```
  element.onclick = doSomething; // reassigns ‘this’ to the element
  ```
  
  + **BUT inline event handling doesn’t have the same effect!**
  
  ```
  <h2 onclick="doSomething();">
  ```

### 3.35 this in Event Handlers (*)

  + **Avoid the problem by explicitly passing this**
  
  ```
  function doSomething(element) {
    // element now refers to the HTML element 
    element.style.color = '#cc0000';
  }
  ```
  
  <span onclick="doSomething(this)">Click Me</span>
  
### 3.36 OLN and JSON

  Object Literal Notation - Putting property names in quotes does NOT mean you are using JSON
  
  [MDN - Stringify](https://goo.gl/UUMn0C)
  ```
  var point = { x: 5, y: 12 }; 
  var book = { "main title": "Exam 70-480", 
               subtitle: "Programming with HTML5", 
               "for": "Beginners"
  };
  ```
  
  (JSON) is when a JavaScript object is serialized into a string using JSON.stringify()
  
  ```
  o = { x: 1, y: { z: [false, null, ""] } }; 
  s = JSON.stringify(o); // s is '{"x":1,"y":{"z":[false,null,""]}}' 
  p = JSON.parse(s); // p is a deep copy of o
  ```
  
  ```
  
  function replacer(key, value) {
    // Filtering out properties
    if (typeof value === "string") {
      return undefined;
    }
    return value;
  }

  var foo = {foundation: "Mozilla", model: "box", week: 45, transport: "car", month: 7};
  JSON.stringify(foo, replacer);
  // '{"week":45,"month":7}'
  ```
    
  MDN 有提到 JSON 的字串問題(換行和換段落字元), 使用以下函式跳脫該字元  
  ```  
  function jsFriendlyJSONStringify (s) {
    return JSON.stringify(s).
      replace(/\u2028/g, '\\u2028').
      replace(/\u2029/g, '\\u2029');
  }
  ```
  MDN例子 - localStorage 與 JSON.stringify 合併使用(*)
  ```
// Creating an example of JSON
var session = {
  'screens': [],
  'state': true
};
session.screens.push({ 'name': 'screenA', 'width': 450, 'height': 250 });
session.screens.push({ 'name': 'screenB', 'width': 650, 'height': 350 });
session.screens.push({ 'name': 'screenC', 'width': 750, 'height': 120 });
session.screens.push({ 'name': 'screenD', 'width': 250, 'height': 60 });
session.screens.push({ 'name': 'screenE', 'width': 390, 'height': 120 });
session.screens.push({ 'name': 'screenF', 'width': 1240, 'height': 650 });

// Converting the JSON string with JSON.stringify()
// then saving with localStorage in the name of session
localStorage.setItem('session', JSON.stringify(session));

// Example of how to transform the String generated through 
// JSON.stringify() and saved in localStorage in JSON object again
var restoredSession = JSON.parse(localStorage.getItem('session'));

// Now restoredSession variable contains the object that was saved
// in localStorage
console.log(restoredSession);
```

### 3.38 Binding a Function to this(做類似 wrapper 的事情)

```
var originalObject = { 
  minimum: 50, // some properties 
  maximum: 100, 
  checkNumericRange: function (numberToCheck) { // a method 
    if (typeof numberToCheck !== 'number') 
      return false; 
    else 
      return numberToCheck >= this.minimum &&  
             numberToCheck <= this.maximum; 
  } 
} 
var result1 = originalObject.checkNumericRange(15); 
console.log(result1); // => false 
var newObject = { minimum: 10, maximum: 20 }; // “duck” type 
var newFunction = originalObject.checkNumericRange.bind(newObject); 
var result2 = newFunction(15); // does not affect original method 
console.log(result2); // => true 20
```

### 3.39 classList

  classList returns a token list of the class attribute of the element
  + classList is a convenient alternative to accessing an element’s list of classes as a space-delimited string via element.className
```
<div id="kermit" class="foo bar"></div>
var div = document.getElementById("kermit");
// if visible is set, then remove it, otherwise add it
div.classList.toggle("visible");
div.classList.add("anotherclass");
div.classList.remove("foo");
```

### 3.40 What is jQuery? 

Created by John Resig, January 2006
  + Light-weight (32kB), CSS3 compliant, cross-browser, feature-rich (DOM manipulation, eventing, Ajax, animation) library
  
jQuery function is aliased to use dollar sign $() or jQuery()

Two major version branches
  + jQuery 1.x (version 1.11.0 on 24th March 2014)
  + jQuery 2.x (version 2.1.0 on 24th March 2014)

2.x has the same API, but does not support Microsoft Internet Explorer 6, 7, or 8 so use the 1.x version unless you are certain no IE 6/7/8 users are visiting your site

+ 3.43 Attribute Selectors

###

### 4.6 progress and meter
### 4.7 output

### 4.9 Detecting HTML5 Input Support
  Modernizr does this for you (and more efficiently)
  
    If your browser doesn’t support that type it will ignore the value and revert to “text”

### 4.13 Regular Expressions(Basics)

Regular expressions can validate and process text 
When validating input, include the leading caret and 
trailing dollar to avoid security vulnerabilities 
+ ^ means start of input; $ means end of input 
+ \d{4} means four digits, but would also match DROP table;1234 
+ ^\d{4}$ means only four digits

{…} is a quantifier, […] is a set (or range) of characters

### 4.14 Regular Expressions(Common Characters)
|shorthand | description | shorthand | description |
|	^	|	Start of line/string	|	$	|	End of line/string		|
|	\t	|	Tab	|	\n	|	New line		|
|	\b	|	Boundary of word	|	\B	|	Non-boundary		|
|	*	|	Zero or more times	|	+	|	One or more times		|
|	?	|	Zero or one time	|	x|y	|	Either x or y		|
|	.	|	Single character	|	[^aeiou]	|	Not in set of chars		|
|	[xyz]	|	Any of the enclosed characters	|	[a-z]	|	A range of characters		|
|	\d \D	|	Digit Non-digit	|	\w \W	|	Word character non-word character		|
|	\s \S	|	White space / non-white space	|	\G	|	Match at point previous match ended		|
|	\040	|	ASCII as octal	|	\u0020	|	Unicode as hex		|

### 4.15 Common Examples

  [8 Regular Expressions You Should Know](http://net.tutsplus.com/tutorials/other/8-regular-expressions-you-should-know/)
  
### Module 5 Communicating with a Remote Server

### 5.4 Sanitizing Encoding and Decoding

  [What is the difference between decodeURIComponent and decodeURI?](http://stackoverflow.com/questions/747641/what-is-the-difference-between-decodeuricomponent-and-decodeuri)
  
### 5.5 $.get function

  jQuery.get( url [, data ] [, success(data, textStatus, jqXHR) ] [, dataType ] )
  
  + success(data, textStatus, jqXHR)
    + The success callback function is passed the returned data, which will be an XML root element, text string, JavaScript file, or JSON object, depending on the MIME type of the response
    + It is also passed the text status of the response
    
### 5.7-9 $.ajax settings object properties1 (1/3~3/3)

  |	Name	|	Description	|	Default	|	additional description	|
  |	accepts	|	What kind of response it will accept	|	Depends on dataType	|		|
  |	async	|	If you need synchronous requests, set this option to false (cross-domain requests and dataType: "jsonp"3 requests do not support synchronous operation)	|	TRUE	|	deprecated	|
  |	cache	|	If set to false, it will force requested pages not to be cached by the browser. Setting cache to false will only work correctly with HEAD and GET requests	|	true, except for datatype 'script' and 'jsonp'	|		|
  |	contentType	|	When sending data to the server, use this content type	|	'application/x-www-form-urlencoded; charset=UTF-8'	|		|
  |	context	|	This object will be made the context of all Ajax-related callbacks	|	$.ajaxSettings merged with settings passed to $.ajax	|		|
  |	data	|	Data to be sent to the server, converted to a query string, if not already a string (appended to the url for GET-requests)	|		|		|
  |	crossDomain	|	If you wish to force a crossDomain request (such as JSONP) on the same domain, set the value to true	|	false for same-domain requests, true otherwise	|	Cross Domain Requests	|
  |	dataFilter	|	A function to be used to sanitize the raw response	|	None	|		|
  |	dataType	|	The type of data that you’re expecting back from the server	|	Intelligent guess	|	If dataType is jsonp, type must be GET	|
  |	headers	|	"An object of additional header 
  key/value pairs to send"	|	{}	|		|
  |	jsonp	|	Override the callback function name in a jsonp request	|		|	Cross Domain Requests	|
  |	username, password	|	A username and password to be used with XMLHttpRequest in response to an HTTP access authentication request	|		|		|
  |	statusCode	|	An object of numeric HTTP codes and functions to be called when the response has the corresponding code e.g. statusCode: {404: function() { ... } }	|	{}	|		|
  |	complete	|	Function called if request finishes (after error and success)	|	None	|	deprecated => use always	|
  |	error	|	Function called if request fails	|	None	|	deprecated => use fail	|
  |	success	|	Function called if request succeeds	|	None	|	deprecated => use done	|
  |	timeout	|	Set a timeout (in milliseconds)	|		|		|
  |	type	|	The type of request to make ("POST")	|	'GET'	|		|
  |	url	|	The URL to which the request is sent	|	The current page	|		|

### 5-10 Should I Use success or Done?

  There are two ways to continue after an AJAX call  
  + success has been the traditional name of the success callback in jQuery, defined as an option in the ajax call
    
  ```

  $.ajax({
    //... 
    success: function(data) {
      /* ... */ 
      } 
  });

  ```
    
  + Since the implementation of $.Deferreds, done is the preferred way to implement success callbacks
    
  ```
  $.ajax({
    /* ... */ 
    }).done(function (data) { 
      /* ... */
    });
  ```

### 5.11 What is this Inside jQuery Ajax Calls? (*)

  If you want to refer to this in an Ajax callback
  ```
  var tempThis = this; 
  $.ajax({ 
    //... 
    success: function (data) { 
      $(tempThis).addClass("cool"); 
    } 
  });
  ```
  Or set the context property
  ```
  $.ajax({ 
    //... 
    context: this, 
    success: function (data) { 
      $(this).addClass("cool"); 
  } 
  });
  ```
  [$(this) inside of AJAX success not working ](http://stackoverflow.com/questions/6394812/this-inside-of-ajax-success-not-working)
  
### 5.13 Event Handlers for Ajax Operations ( html5 ajaxUploader 實作了每個方法 )

  |	Method	|	Description	|
  |	ajaxStart	|	When an Ajax operation begins and none are already active	|
  |	ajaxSend	|	When an Ajax operation begins	|
  |	ajaxComplete	|	When an Ajax operation finishes	|
  |	ajaxSuccess	|	When an Ajax operation finishes successfully	|
  |	ajaxError	|	When an Ajax operation has an error	|
  |	ajaxStop	|	When all Ajax operations have finished	|

### 5.14 Serializing Forms (*)

  [serialize()](http://api.jquery.com/serialize/); // encoded into a string 
  [serializeArray()](http://api.jquery.com/serializeArray/) // encoded into an array

### 5.15 Parsing XML

  If you’re lucky, the services you call will return JSON
  + If not, you might have to parse XML
```
var x = "<!-- lots of XML to process -->"; 
if (window.DOMParser) { 
  parser = new DOMParser(); 
  xmlDoc = parser.parseFromString(x, "text/xml"); 
} else { // Internet Explorer 
  xmlDoc = new ActiveXObject("Microsoft.XMLDOM"); 
  xmlDoc.async = false; 
  xmlDoc.loadXML(x); 
} 
```

### Module 6 Styling HTML5 by Using CSS3 ( 去看 CSS 專書更好, 這邊講的 不太清楚...要測試也試不太出來@@ )

### 6.11 Enabling Flex Layout (apply to container) (*)
### 6.12 flex-direction (apply to container)
### 6.13 flex-wrap (apply to container)
### 6.14 justify-content (apply to container)

### 6.20 Grid Block Style ( 挺怪異的使用方式... )


### Module 7 Creating Objects and Methods by Using JavaScript (*)

### 7.4 Block Scope using let
  
  JavaScript 1.7 and later allow block scope using let  
  意思就是 1.7 版以前沒有 let 的時候 都是 直接覆蓋前面的值.(如果是閉包那又會保留...一整個混亂 @@)

### 7.6 Hoisting Functions (*) 升天函式(因為它真的升..上...去....了.....)

  Hoisting with functions differs depending on if you are using a named or anonymous function  
  函數的提昇 只會使的 具名函式 獲得提昇(匿名函式不會)  
  匿名函式 就是 為了要保持程序的封裝性.
  
  ```originSourceCode
  function test() { 
    foo(); // TypeError "foo is not a function" 
    bar(); // "this will run!" 
    var foo = function () { 
        alert("this won't run!"); 
    } 
    function bar() {  
        alert("this will run!"); 
    }
  }
  test();
  // 直譯器解析這個函式的順序為
  // 1. 先把所有的變數 拉到前面 變成一個 var
  // 2. 然後把所有的 "具名"函式 依照原來的順序 拉到 前面.
  // 這邊回到原始 Javascript 對於 First Class Function 的定義
  // 它先把具名函式 優先拉到前面, 等於 先建立了索引, 讓後面呼叫的時候可以直接引用 
  function test() { 
      var foo; 
      function bar() { 
          alert("this will run!"); 
      } 
      foo(); // TypeError "foo is not ... 
      bar(); // "this will run!" 
      foo = function () { 
          alert("this won't run!"); 
      } 
  }
  ```

### 7.7 Terms 使用名詞介紹. (*)

  + Native object (*)
   + Defined by ECMAScript specification 
   + e.g. arrays, functions, dates, and regular expressions 
  + Host object (*)
   + Defined by host environment (typically the web browser) 
   + e.g. DOM, window 
  + User-defined object 
   + Any object defined by the execution of code “Own” and “inherited” properties 
  + “Own” and “inherited” properties (自有屬性 與 繼承屬性) (*)
   + An own property is defined directly on an object
   + An inherited property is defined by an object’s prototype chain
### 7.11 Objects Three Ways to Create an Object

  + Object literal Notation
    ```
    var emptyObject = {}; 
    var point = { x: 5, y: 12 };
    var book = { 
      // for names with spaces 
      "main title": "Exam 70-480",
      subtitle: "Programming with HTML5", 
      "for": "Beginners" 
    };
    // or reserved keywords
    ```
  + new Constructor
  ```
  var o = new Object(); // prototype is Object.prototype 
  var d = new Date(); // prototype is Date.prototype 
  var a = new Array(); // prototype is Array.prototype 
  var r = new RegExp("[dh]og"); // prototype is RegExp.prototype
  ```
  + Object.create(prototype)
  ```
  var o1 = Object.create(point); // inherits x and y 
  var o2 = Object.create(null); // no inherited properties 
  var o3 = Object.create(Object.prototype); // like new Object or {}
  ```

### 7.12 Object Literal Syntax Quirks

  ```
  var point = {
    x: 5, y: 12, // <= this comma SHOULD be allowed in all browsers 
  };
  ```
  IE 8 will not pass !
  
### 7.19 Testing for Properties
  ```
  var o = { x: 1, y: 2 };
  ```
  + Use in operator to check for own and inherited
    ```
    console.log("x" in o); // => true (own)
    console.log("z" in o); // => false
    console.log("toString" in o); // => true (inherited)
    ```
  + Use hasOwnProperty() to check for own
    ```
    console.log(o.hasOwnProperty("x")); // => true (own) 
    console.log(o.hasOwnProperty("z")); // => false 
    console.log(o.hasOwnProperty("toString")); // => false (inherited)
    ```
  + Check if it has enumerable properties
    ```
    console.log(o.propertyIsEnumerable("toString")); // => false 
    console.log(o.propertyIsEnumerable("x")); // => true
    ```
  + Iterate through all enumerable properties using for…in
    ```
    for (var p in o) 
      console.log(p); // prints x, y, and z, but not toString
    ```
### 7.20 Property Descriptors and Defining Properties ( 非常少機會用的到...@@ )

  + Object.getOwnPropertyDescriptor, Object.defineProperty
    當初使化一個物件的時候 JS 就自動啟動了自我描述的  
    機制,意即 會自動幫你產生一些 輔助性的 屬性(7.13)(property)與方法(valueOf,toSource,toString)    
    
    ```
    自我描述機制
    當使用了這個指令:
    var r = new RegExp("[dh]og");
    // 下面是他的原型鏈的樣子
    
    Object.prototype      RegExp.prototype                    r.prototype
    hasOwnProperty            exec
    isPrototypeOf      =>     test
    toString                toString (overridden) 被覆寫的方法
    valueOf     
    ```
    7.14 Object.prototype 有提到 Object 原型鏈內有的成員 , 如下表   
    
    // 以下為 可(會)繼承 [透過產生物件 直譯後] 隨即產生的 Object 原型方法  
    // (Almost) all objects chain back to Object.prototype so share these inherited methods
    + hasOwnProperty  
    Returns a boolean indicating whether an object
    contains the specified property as a direct property 
    of that object and not inherited through the 
    prototype chain
    
    + isPrototypeOf  
    Returns a boolean indication whether the specified 
    object is in the prototype chain of the object this 
    method is called upon 
    
    + propertyIsEnumerable  
    Returns a boolean indicating if the internal 
    ECMAScript DontEnum attribute is set 
    
    + toLocaleString  
    Returns an object converted to a string based on the current locale
    
    + toString  
    Returns a string representation of the object
    
    + valueOf  
    Returns the primitive value of the specified object  
    
    // 7.15 Object
    //以下為不可繼承的方法  
    + create  
    Creates a new object with the specified prototype object and properties
    
    + defineProperty, defineProperties  
    Adds the named property(ies) described by given descriptor(s) to an object
    
    + getOwnPropertyDescriptor  
    Returns a property descriptor for a named property on an object
    
    + getOwnPropertyNames  
    Returns an array containing the names of all of the given object’s own enumerable and non-enumerable properties
    
    + freeze, seal, preventExtensions  
    “Lock” an object (see slide 7.6)
    
    + isFrozen, isSealed, isExtensible  
    Check if an object is “locked”
    
    + getPrototypeOf, setPrototypeOf*(Experimental and very slow!)  
    Returns the prototype of the specified object
    
    // 而建立 一級函式後 會立即產生的 原型鏈方法為  
    // apply(後面接 arrays), call(後面接 ,), toSource, toString  
    // call uses commas, apply uses array [7.22]
    ```
    f.call(o, 1, 2); // pass parameters comma-separated 
    f.apply(o, [1, 2]); // pass parameters as single array
    ```
  ```
  var o = { x: 1 }; 
  var desc = Object.getOwnPropertyDescriptor(o, "x"); 
  console.log(desc.value);        // => 1 
  console.log(desc.writable);     // => true 
  console.log(desc.enumerable);   // => true 
  console.log(desc.configurable); // => true 
  ```
  
  7.20 範例程式碼 有提到 [use strict](https://goo.gl/ATVt7l) 嚴格模式 (*)  
  
    ```
    Object.defineProperty(o, "y", { writeable: false }); 
    o.y = 3; // silently fails unless "use strict" 
    console.log(o.y); // => 2 
    
    Object.defineProperty(o, "y", { value: 3 });
    console.log(o.y); // => 3
    ```
    w3c :  
    + The syntax, for declaring strict mode,   
    was designed to be compatible with older versions of JavaScript.  
    
    + Strict mode makes it easier to write "secure" JavaScript.
    Strict mode changes previously accepted "bad syntax" into real errors.
    
    + In normal JavaScript, a developer will not receive any error feedback assigning values to non-writable properties.  
      非嚴格模式下 , coder
    + In strict mode, any assignment to a non-writable property, a getter-only property, a non-existing property, a non-existing variable, or a non-existing object, will throw an error.
    講中文: 就是要與舊版 JS app 相容,寫出更安全的 JS app,找出可能會有問題的舊的程式碼.
    w3c 有很多範例...很值得看!!
    
    很重要的一個部份(雖然只是幾個字,但是代表新舊功能的並行),  
    當你碰到不常碰到的問題的時候就該到這邊來看一下,  
    尤其是 新舊程式的轉換並行 與 新程式的開發的初期就該使用這樣的模式(避免某些問題)

### 7.22 Invoking Functions

  + functions is different from methods
    ```
    //as function
    function f() { /* ... */ }; 
    f(); // invoke function
    //as method
    o.m = f;
    o.m(); // invoke method
    //as constructor (*)
    var o = new Object(); // invoke constructor 
    var o2 = new Object; // allowed if no parameters
    ```
  + Through their call() and apply() methods
  ```
  f.call(o, 1, 2); // pass parameters comma-separated 
  f.apply(o, [1, 2]); // pass parameters as single array
  //call uses commas, apply uses array
  ```

### 7.24~7.25 (*)
    Inheritance with Factories (not recommended) 
    Inheritance with Constructors

### 7.33 Subclasses (*)

  + The key to subclasses in JavaScript is proper initialization of the prototype object  
    講中文: 正確的初始化 原型鏈物件 是 存取子類別的關鍵
### 7.34 Chaining Constructors and Methods (*)

  + When you define a new constructor for a new class,  
  it needs to perform all the work to initialize the object  
  講中文: 如果你"自己定義"了一個物件的建構子,  
  那你要自己去定義 要初始化物件所需做的事情.
  + 較省力的作法
  ```  
  function Person(name) { // constructor for Person 
    this.name = name;  
  }
  function Student(name, subject) {  // constructor for Student 
    Person.apply(this, arguments); // call base constructor 
    this.subject = subject; 
  }
  Student.prototype = Object.create(Person.prototype);
  Student.prototype.constructor = Student; 
  
  Student.prototype.toString = function () { 
    return Person.prototype.toString.apply(this, arguments) + " (BSc. Hons.)"; 
  };
  ```
  
### 7.35-36 Chaining Constructors Example (*)

### 7.37 JSON Deserialization and Re-associating prototype (*)

  通常這個步驟 已經有人幫我們寫好了, 因為常常會碰到@@...  
  有了 JSON 就會有各種 以前都已經用過的方法想要轉移到 JSON 這個新的東西上...
  新的應用通常都是 BaseOn 以前已經有的事物上, 只是換了一種形式(Form).
  
### 8 Module 8 Creating Interactive Web Pages by Using HTML5 APIs

  + Implement HTML5 APIs - Implement Geolocation API
  + Write code that interacts with UI controls - Implement media controls
  
### 8.5 Geolocation - How to Get Your Location
  + To get your location once
   + navigator.geolocation.getCurrentPosition(success[, error[, options]]) 
  [Geolocation.getCurrentPosition()](https://goo.gl/8Lgrhn)  
  ```
  navigator.geolocation.getCurrentPosition( 
  successCallback, errorCallback, 
  { enableHighAccuracy: true, timeout: 2000 }); 
  ```
  // getCurrentPosition() 與 watchPosition()  
  均可容納 1 組成功回呼、1 組錯誤回呼 (選填)、1 組 PositionOptions 物件 (選填)  
  // 中文: https://goo.gl/NBM8ON
  + To get your location at a regular interval
  ```
  var id = navigator.geolocation.watchPosition( 
    successCallback, errorCallback, 
    { enableHighAccuracy: true, maximumAge: 5000 }); 
  navigator.geolocation.clearWatch(id); // to stop receiving events
  ```
  + handle successCallback and errorCallback
  ```
  error.message, error.code 
• error.PERMISSION_DENIED 
• error.POSITION_UNAVAILABLE 
• error.TIMEOUT 
  function successCallback(e) { 
    // e.coords.latitude 
    // e.coords.longitude 
  function errorCallback(error) { 
    if(error.code === error.TIMEOUT) { 
      alert(error.message);
  }
  ```
  
### 9.2 Adding Offline Support to Web Applications
  
  + Storage APIs
    + localStorage and sessionStorage both extend Storage
    + different: sessionStorage is non-persistence
  + AppCache API
   + ApplicationCache(9.5)
   + Any page the user navigates to that includes a manifest will be  
   implicitly added to the application cache
   + You can see the urls that are controlled by the application cache by visiting  
   chrome://appcache-internals/ in Chrome
   + If the manifest or a resource specified in it fails to download, the entire cache  
   update process fails

OR
  + [lawnchair: simple json storage](http://brian.io/lawnchair/)
  
### 9.6  manifest Example
```
Example 
CACHE MANIFEST 
# 2010-06-18:v2 
 
# Explicitly cached 'master entries'. 
CACHE: 
/favicon.ico 
index.html 
stylesheet.css 
images/logo.png 
scripts/main.js 
 
# Resources that require the user to be online. 
NETWORK: 
* 
 
# static.html will be served if main.py is inaccessible 
# offline.jpg will be served in place of all images in images/large/ 
# offline.html will be served in place of all other .html files 
FALLBACK: 
/main.py /static.html 
images/large/ images/offline.jpg 
/ /offline.html 4 
```

### 9.7 Updating the Cache ( 快取[緩存]的更新 )
  + Once an application is offline it remains cached until one of the following happens:  
  講中文: 如果 app 離線 , 他將使用 快取機制 存取部份 離線資源 直到 以下兩件事情發生:
    + The user clears their browser’s data storage for your site  
    講中文: 使用者清除了瀏覽器的資料
    + The manifest file is modified  
    講中文:保存清單被修改後
  + To programmatically check for updates to the manifest, first call applicationCache.update()  
  講中文: 用程序檢查保存清單 並且 執行applicationCache.update() 作手動更新
    + When the applicationCache.status is in its UPDATEREADY state,  
    calling applicationCache.swapCache() will swap the old cache for the new one
    
### 9.8 applicationCache Events 

```
Event                                Description   

cached              Fired after the first cache of the manifest 

checking            Checking for an update 

downloading         An update was found; the browser is fetching resources 

error               The manifest returns 404 or 410, the download failed,
                    or the manifest changed while the download was in progress 
                    
noupdate            Fired after the first download of the manifest 

obsolete            Fired if the manifest file returns a 404 or 410 which
                    results in the application cache being deleted 
                    
progress            Fired for each resource listed in the manifest as it is  
                    being fetched 
                    
updateready         Fired when the manifest resources have been newly  
                    redownloaded, so you can now call swapCache()
                    
```

### 10 Implementing an Adaptive User Interface (*)
  講中文: 實作一個 自適應的 使用者界面
  
### 10.7 Media Queries

```
// html example 那一邊寫都可以 , 因為 media query 會自己找到 符合的
<link rel='stylesheet' media='only screen and (max-width: 700px)' href='css/narrow.css' />

<link rel='stylesheet' media='only screen and (min-width: 701px) and (max-width: 900px)' href='css/medium.css' />

// css file example
@media screen and (max-width: 995px), screen and (max-height: 700px) {

/* rules for either media query */

}
```

### 10.8 "Conditional Comments" Not Supported in Internet Explorer 10 and later
  講中文: 條件式註解 在 IE10 以後都不支援(為了相容性)
  ```
  <!--[if IE]>
    This content is ignored in Internet Explorer 10 and other browsers.
    In older versions of Internet Explorer, it renders as part of the page.
    //講中文: 在舊版的IE上,使用"條件式註解" 會將這些內容渲染成網頁的內容.
  <![endif]-->  
  ```

### 11 Creating Advanced Graphics
  講中文: ( 跳過...因為 圖論 是一門專門的學問...懂這些皮毛 對你的人生並不會有多少影響 @@ )
  + HTML5 canvas and SVG graphics
### 12 Animating the User Interface
  講中文: 這邊可以做的很酷炫...但那應該也是講"天份"的...如果只是抄襲(包括修改)別人的  
  效果, 那還是不會有機會出師的, 動態效果通常會需要有主體故事內容和劇本,這兩個都是專門的學問...
  
  如果只是單純的一頁裡面那種動來動去, 放大看整個網站之後 會缺乏 整理規劃 與 設計感.
  這種功力都是必須經年累月才能夠 表達出來, 當然也有瞬間頓悟那種...
  
  [Using transitions to make JavaScript functionality smooth](http://jsfiddle.net/RwtHn/5/)

### 12.6 Animation with Keyframes (*)

  + To make h1 slide in from right-to-left 
    + Optionally, add a keyframe so that three quarters of the way
  
  + through the animation it tripple the size of the font 
    + Optionally, add an iteration count and direction to repeat the animation 

  ex: [線上範例](https://goo.gl/Tolv6b)
  
  ```
  h1 { 
      animation-duration: 3s; 
      animation-name: slidein; 
  } 
  @keyframes slidein {
      from {
        margin-left: 100%;
        width: 300%; 
      }    
      75% {
        font-size: 300%;
        margin-left: 25%;
        width: 150%;
      }
      to {
        margin-left: 0%;
        width: 100%;
      }
  }
  
  ```
  
### 13 Web Sockets - Implementing Real-time Communication by Using Web Sockets
  
### 13.3 When To Use Web Sockets
    
  + Achieving zero-lag connectivity between Web clients and servers requires going beyond the HTTP protocol  
    講中文: 希望達到 網路服務無延遲, 需要使用更多超越Http協定能給予的服務
    
  + The new WebSocket Protocol aims to overcome a structural limitation of the HTTP protocol that makes it inefficient for Web applications hosted in browsers to stay connected to the server over a persistent connection  
    講中文: 為了改善 目前 網路連線的結構性的限制 以及 長時間連線的沒效率
    
  + [Understanding the Power of WebSockets](http://msdn.microsoft.com/en-us/magazine/hh975342.aspx)
### 13.4 webSockets example - Server Side

    ```
    using Microsoft.Web.WebSockets;
    
    public class ChatController : ApiController { 
      public HttpResponseMessage Get(string username) { 
        HttpContext.Current.AcceptWebSocketRequest(new ChatWebSocketHandler()); 
        return Request.CreateResponse(HttpStatusCode.SwitchingProtocols); 
      } 
      class ChatWebSocketHandler : WebSocketHandler { 
        public ChatWebSocketHandler() { 
        } 
        public override void OnOpen() { 
        } 
        public override void OnMessage(string message) { 
        } 
      } 
    } 
    ```
### 13.5 webSockets example - Client Side

    ```
    $(document).ready(function () { 
        websocket = new WebSocket('ws://localhost/api/ChatController'); 
        websocket.onopen = function () { 
        }; 
        websocket.onerror = function (event) { 
        }; 
        websocket.onmessage = function (event) { 
        }; 
        websocket.send('Hello'); 
        websocket.close(); 
    }); 
    ```

### 14 Web Workers - Performing Background Processing by Using Web Workers

  + Start and stop a web worker  
    初始化
  + Pass data to a web worker  
    傳遞初始參數給 web worker
  + Configure timeouts and intervals on the web worker  
    在 web worker 上配置超時和間隔
  + Register an event listener for the web worker  
    註冊監聽事件
  + Limitations of a web worker  
    web worker的限制
    

  [example](https://msdn.microsoft.com/library/hh673568)
  + 瀏覽器傳統上是單一執行緒，強制應用程式中所有的指令碼在單一 UI 執行緒中一起執行。雖然您可以使用文件物件模型 (DOM) 事件與 setTimeout API 讓使用者產生數個事件同時發生的錯覺，但只要執行一個需要大量電腦資源的工作，使用者就會覺得螢幕停滯不動。
  
  + Web 工作者 API 提供一個方式讓 Web 應用程式作者能夠產生可與主頁面平行執行的背景指令碼。您可以一次產生數個執行緒，供長期執行的工作使用。新的工作者物件需要 .js 檔案，對伺服器發出非同步要求即可產生此檔案。

### 14.4 Web Workers - What Can You Use Inside a Web Worker?

  + Worker has a Global scope separate from the page  
  獨立於 該網頁的程式碼區塊
  + Major limitations
    + Worker code cannot access the DOM or window
    + Worker has a single thread, so if it could have multiple messages posted to it simultaneously, it should process and return as quickly as possible, otherwise the messages will be queued up (or the worker could spawn additional workers)

### Appendix A - jQuery,HTML5, CSS3 Reference( 還蠻重要的, 類似速查表,你看到 標題就知道裡面在講啥 代表你已經知道了這個東西... )

比較重要的是
  
  + jQuery DOM Insertion, Inside
    + .append() and .aapendTo()
    + .html()
    + .prepend() and .prependTo() 在元素前面插入...用於表現 即時(實時)新聞之類的元素
    + .text() 
  + jQuery DOM Insertion, Outside
    + .after()
    + .before()
    + .insertafter()
    + .insertBefore()
  + jQuery DOM Insertion, Around  
  好處是可以不用管裡面裝什麼東西,直接打(解)包...類似封裝的概念,  
  但是前提是 內部結構要夠明確 才不會亂掉
    + .unwrap()
      解包
    + [.wrap()](http://api.jquery.com/wrap/)  
      打包  
      把select出來的元素用 後面的元素包起來
    + .wrapAll() 
    + .wrapInner()
  + jQuery General Attribute
    + .attr()
    + .prop()
    + .removeAttr()
    + .removeProp()
    + .val()
  + jQuery Helper Functions
    + .param()
    + .serialize()
    + .serializeArray()
  + jQuery Events (這邊 成對的事件 比較好記憶...)
    + live() and die() - 取代了 (un)delegate() , 但仍可用
    + bind() and unbind()
    + click() and dblclick()
    + focus() and hover()
    + proxy()
    + key and mouse event    
    + on and off and one()
    + scroll, select, submit, toggle, trigger, resize, ready, 
    + load and unload    
  + jQuery Ajax Methods
    + ajaxComplete()
    +
  + jQuery Prototype Methods
  + jQuery Selectors
  + jQuery Node Methods
  
### HTML5 New Input Type

  + color,date(year, month and day),
  + datetime(year, month, day, hour, minute, second, and fraction of a second, based on UTC time zone)
  + datetime-local
  + email,number
  + range,tel,time,url,week

### Differences between SVG and Canvas
+ SVG
  + 不需依靠解析度  
    Resolution independent
  + 可以綁定事件  
    Support for event handlers
  + 大面積  
    Best suited for applications with large rendering areas (Google Maps)
  + 複雜的圖就別用...比如遊戲這種需要細緻的圖  
    Slow rendering if complex (anything that uses the DOM a lot will be slow)
  + 不適用於遊戲  
  Not suited for game applications
+ Canvas
  + Resolution dependent
  + No support for event handlers
  + Poor text rendering capabilities
  + You can save the resulting image as .png or.jpg
  + Well suited for graphic-intensive games

### Appendix B - Unit Testing JavaScript
