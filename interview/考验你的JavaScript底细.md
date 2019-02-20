## [参考链接](http://sentsin.com/jsquiz.html) 
#### QM 2017/6/26

#### 1. 

    (function(){
        return typeof arguments;
    })();


​    
    A:"object"  
    B:"array"   
    C:"arguments"   
    D:"undefined"

#### 2.

    var f = function g(){ 
        return 23; 
    };
    typeof g();


​    
    A:"number"  
    B:"undefined"   
    C:"function"    
    D:Error

#### 3.

    (function(x){
        delete x;
        return x;
    })(1);
       
    A:1  
    B:null
    C:undefined
    D :Eror

#### 4.

    var y = 1, x = y = typeof x;
    x;
    
    A:1 
    B:"number"  
    C:undefined
    D:"undefined"

#### 5.

    (function f(f){
        return typeof f();
    })(function(){ return 1; });
    
    A:"number"
    B:"undefined"
    C:"function"
    D:Error


​    
#### 6.

    var foo = {
        bar: function() {
        return this.baz; 
    },
        baz: 1
    };
    (function(){
        return typeof arguments[0]();
    })(foo.bar);
    
    A:"undefined"   
    B:"object"  
    C:"number"
    D:"function"

#### 7.

    var foo = {
        bar: function(){
        return this.baz; 
    },
        baz: 1
    }
    typeof (f = foo.bar)();
    
    A:"undefined"   
    B:"object"
    C:"number"
    D:"function"

#### 8.

    var f = (
        function f(){ 
            return "1"; 
        }, 
        function g(){ 
            return 2; 
        }
    )();
    typeof f;
    
    A:"string"
    B:"number"
    C:"function"
    D:"undefined"

#### 9.  不明白

    var x = 1;
    if (function f(){}) {
        x += typeof f;
    }
    x;
    
    A:1 
    B:"1funciton"   
    C:"1undefined"
    D:NaN

#### 10.

    var x = [typeof x, typeof y][1];
    typeof typeof x;
    
    A:"number"
    B:"string"  
    C:"undefined"
    D:"object"

#### 11.

    (function(foo){
        return typeof foo.bar;
    })({ foo: { bar: 1 } });
    
    A:"undefined"
    B:"object"
    C:"number"
    D:Error

#### 12.

    (function f(){
        function f(){ return 1; }
        return f();
        function f(){ return 2; }
    })();
    
    A:1 
    B:2 
    C:Error(e.g "Too much recursion")
    D:undefined

#### 13. 不明白

    function f(){ return f; }
    new f() instanceof f;
    
    A:true
    B:false

#### 14.

    with (function(x, undefined){}) length;
    
    A:1
    B:2
    C:undefined
    D:error


​    
​    
​    
​    
​    
​    




## 答案
1:A  
2:D  
3:A  
4:D     
5:A     
6:A     
7:A     
8:B     
9:C     
10:B        
11:A    
12:B        
13:B    
14:B