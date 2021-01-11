# CH1 Javascript Object

>p8 **9 種原生建構函式**

* Number,String,Boolean,Object,Array,Function,Date,RegExp,Error()
* Math 是 static object 靜態物件，就是 隨時都可以拿來用 不用 new

>p19 object reference 依據

    var myObject={};
    var x = myObject;
    myObject.foo = 'bar';
    console.log(myObject, x); // output  Object { foo="bar"} Object { foo="bar"}

由以上得知 x 是**參考**了 myObject 的位址，而不只是複製

> p20 物件的比較是以 記憶體位址來比較，即使兩個物件 內容物相同

    var objA = {str : 'hello'};
    var objB = {str : 'hello'};
    
    console(objA===objB); //output false
    
    var x = {foo : 'bar'};
    var y = x;
    
    console(x===y); // output true

----

# CH2 Object property

>p31 句點標記法(dot notation) and 括號標記法(bracket notation)

    var x = { foo : 'bar',
              foo1: 'bar1'
    };
    var y = 1;
    console.log(x.foo);      // output bar
    console.log(x['foo1']);  // output bar1
    console.log(x['foo' + y]); // output bar1 句點標記法 較難如此組合 ( 括號標記法的好處 ) p33.
    
----

>p37 hasOwnProperty and in usage , 前者 只找 原型鏈 , 後者 會去往下找 複合鏈

hasOwnProperty ex:

    var obj = {foo:'bar'};
    console(obj.hasOwnProperty('foo')); // output true
    console(obj.hasOwnProperty('toString')); // output false
----

in ex:

    var obj = {foo:'bar'};
    console('toString' in obj); // output true
----

> p41 extend JS usability with Underscore.js

----
# CH4 Function

 * function constructor 建構式 , declaration 陳述式 , expression 表達式
 * call and apply 的不同 [apply MDN def](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) v.s [call MDN def](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
 * fun.call(thisArg[, arg1[, arg2[, ...]]]) v.s. fun.apply(thisArg, [argsArray])
 * new 會在自動建構 完整的物件 prototype , JS 支援的各種物件都是如此 Object,Array,String,Number...
 * () 代表 立即執行該 function, 目的是避免一些 不必要的問題
 
----

# CH6 this 關鍵字

    var foo='foo';
    var sayFoo= function(){
      console.log(this['foo']);
    };
    //before sayFoo() output is undefined , after () output is foo , undefined
    //bcz this scope is refered to sayFoo function , not window
    sayFoo();

    // the same as 
    var sayFoo= function(){
      console.log(this['foo']);
    }();

----

# CH8 prototype

    var x = 'string';
    // 定義 x 時, JS 就自動幫 此物件 建立成 複合物件並擁有 prototype.toString() 方法
    console(x.toString());

----

> p94 ** 自原型繼承屬性的實例，一定會取得最新的值 **
         物件參考問題1

    var Foo = function Foo(){};
    Foo.prototype.x = 1;
    var FooInstance = new Foo();
    console.log(FooInstance.x);// output 1
    Foo.prototype.x = 2
    console.log(FooInstance.x);// output 2
    
----

> p95 ** prototype 屬性換成新的物件，無法更新之前的實例(instance) **
物件參考問題2 ( 只參考 new 的時候那個物件的狀態，建立複(製)的版本 )

    var Foo = function Foo(){};
    Foo.prototype.x = 1;
    var FooInstance = new Foo();
    console.log(FooInstance.x);// output 1

    Foo.prototype = {x:2};
    console.log(FooInstance.x);// still 1
    
    var NewFooInstance = new Foo(); // 重新取得覆寫 prototype 之後的複本
    console.log(NewFooInstance.x);// output 2

----

# CH9 Array ( 需熟練 )

## Array.prototype

+ property
  + constructor,index,input,length
+ method
  + pop,push,reverse,shift,sort,splice,unshift,concat,join,slice
  
----

> p105  遍歷迴圈 with while()

    var array = ['a','b','c','d'];
    var counter = 0;
    while(counter < array.length) { // same as counter < array['length'] 
      console.log(array[counter]);
      counter++;      
    }

# CH13 String, Number and Boolean

>p120 有趣的使用

    console.log((1234).toString()   ); // ouput 1234
    console.log( 1234['toString']() ); // ouput 1234
    console.log((true).toString()   ); // true
    console.log( true['toString']()  ); // true

>p121 object check with **typeof**

    console.log(typeof new Number(1) ); // object
    console.log(typeof 1); // number
    console.log(typeof null); //object
    