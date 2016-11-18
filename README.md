# JavaScript 知识点整理
JavaScript 是按照CEMAScript 标准设计和实现的, 后文说的javaScript 语法起始就是ES5的标准实现.  
先说说有哪些基础语法?  
# 最基础的语法有哪些?   
基础语法几乎所有的语言差异不大,无非数据类型/操作符/控制语句/函数等,简单列举下.  
五中基本数据类型&1中复杂的数据类型  
javaScriptba包含5种基本数据类型,分别是undefined /null/boolean/number/string,基本数据类型就这五种,没有其他的!  
javaScript包含一种复杂的数据类型,就是Object类型,Object类型是所有其他对象的基类.  
注意:javaScript并不区分浮点数和整数,都是用Number来表示.  

前面提到的5种基本数据类型,以及这儿的一种复杂数据类型,这就是数据类型的全部了!  
基本操作符  
这个是常识,知道怎么回事就好.  
常用的操作符包括: 算数操作符. 关系操作符. 布尔操作符.赋值操作符等.  
控制语句  
这就是我们常说的If-else之类的控制语句  
常用的并不多: If语句 switch语句 for语句 while语句 for-in语句.  
函数  
函数就是一个小段的逻辑的封装,理论上逻辑越独立越好.
javaScript函数可以接受任意数量的参数,并且可以通过argunments对象来访问这些参数.  
任何一门语言的基础语法都是想通的 , 除开一些细节差异,大致就是上面这些了:数据类型.操作符.控制语句.函数.模块等等.  
接下来介绍稍微复杂的一些概念. 
# 变量. 作用域. 内存问题
变量 
javaScript变量分为两种:基本类型和引用类型.其中基本类型就是前面提到的5中基本数据类型,引用类型就是前面提到的Object以及基于它的其他复杂数据类型. 
 
基本类型:在内存中占据实际大小的空间,赋值的时候,会在内存中创建一份新的副本.保存在内存中. 
引用类型:指向对象的指针而不是对象本身,赋值的时候,只是创建一个新的指针指向对象.保存在堆内存中. 


变量内存分配 
一句话就是,基本类型在内存中是实际的值;而应用类型在内存中就是一个指针,指向一个对象,多个引用类型可能同时指向同一个对象. 
那么,如何确定某个变量是那种数据类型呢? 
确定一个变量是那个基本类型用typeof操作符. 
确定一个变量是那种引用类型用Instanceofl操作符. 
这个别忘了! 
 作用域
变量是在某一个特定的作用域中声明的,作用域决定了这些变量的生命周期,以及哪些代码可以访问其中的变量 

javaScript作用域只包括全局作用域和函数作用域,并不包含块级作用域! 
作用域可以嵌套,从而形成作用域链.由于作用域链的存在,可以让变量的查找向上追溯,即子函数可以访问父函数的作用域=>祖先函数的作用域=>直到全局作用域,这种函数 
我们也成为闭包,后文会介绍,
```javascript
  var color='red';
  function changeColor(){
  var antherColor='red';
  function swapColors(){
  var tempColor =antherCorlor;
  anotherColor =color;
  color=tempColor;
  //这里可以范根color,anotherColor tempColor
  }
  //这里可以访问color,anotherColor,但不能访问tempColor
  swapColors();
  }
  //这里只能访问color  changeColor();
```
每个作用域能够访问到的变量以及嵌套的的作用域可向上追溯.
 
作用域链 
作用域的概念看着简单, 实际使用会有不少问题, 遇到问题要细心分析. 
内存问题 
javaScript引擎具有自动垃圾回收机制,不需要太关注内存分配和垃圾回收的问题,这里就不做展开了. 
引用类型 
刚才也提过,Object是唯一的复杂数据类型,引用类型都是从Object类型上继承而来.
array:数据类型 
date:日期类型 
regExp:正则表达式类型, 这个多学学有好处! 
等等~~~~
 那么问题来了,我们用的最多的函数是什么数据类型呢?答案是Function类型!
 唉,好像发现了点什么? 由于Funtion是应用类型,而Javascirpt又可以往引用类型上加属性和方法.那么,函数也可以! 这也是javaScript函数强大和复杂的地方.也就是说:函数也可以拥有自定义方法和属性! 
此外,javaScript对前面提到的5种基本类型的其中3种也做了引用类型封装, 分别是Boolean, Number,String,但其实使用不多,了解就行, 
在所有代码执行之前,作用域就内置了两个对象,分别是Glodal和Math,其中浏览器的Global就是window. 
到此为止,Javascript中基础概念都差不多接胡搜啊了,其中函数和作用域会复杂一点点, 其他都比较浅显. 
接下里,介绍下JavaScript中一些稍微复杂一些的概念:面向对象. 
# 面向对象编程 
javaScript本身并没有类和接口的概念了,面向对象都是基于原型实现的, 
为了简单, 我们只分析面向对象的两个问题: 
如何定义一个类? 
如何实现类的继承 
定义一个类 
不扯其他的, 直接告诉你.我们使用构造函数+原型的方式和定义一个类. 
使用构造函数创建自定义类, 然后使用New操作符来创建类的实例,但是构造函数上的方法和属性在每一个示例上都存在,不能共享,于是我们引入原型来实现方法和属性的共享. 
原型 最后我们将需要共享的方法和属性定义的元素上,把专属于示例的方法和属性放到构造函数中,到这,我们就通过构造函数+原型的方式定义了一个类. 
```javaScript
  //构造函数 
  function Person(name,age,job){
  this.name= name;
  this,age.=age;
  this.job =job;
  this.friends= ['Shelby','Court'];
  }
  //原型 
  Person.prototype={
  constructor:Person,
  sayName:function(){
  return this.nama;
  }
  }
  //实例化
  var person1 =new Person('Nicholas',29,'software ENGineer');
  var person2 =new Person('Greg',27,'DECTOR');
  person1,frinds.push('van');
  alert(person1,frinds);   //输出'Shelby,Count,van'
  alert(person2.frinds);  //输出'Shelby,Count'
  alert(person1.friedns ===person2.friends)  //输出false
  alert(person1.staName ===person2.sayName);//输出true
```
实现继承 
前文讲了如何定义一个类, 那现在定义一个父类 ,一个子类. 
如何让子类继承父类,javaScript通过原型链来实现继承!  
如何构造原型链?将父类实例赋值给子类构造函数的原型即可.好绕,但是千万得记住~!!! 
原型链继承 
构造原型链之后, 子类就可以范根父类的所有属性和方法! 
```javaScript
//父类 
function SuperType(){
  this.property=true;
}
SuperType.prototype.getSuperValue=function(){
return this.property;
};
//子类
function SubType(){
this.subproperty =false;
}
//子类继承父类
SubType.prototype = new SuperType();
//给子类添加新方法 
SubType.prototype.getSubValue = function(){
  return this.subproperty;
}
//重写父类的方法
SubType.prototype.getSuperValue =function(){
return false;
};
//实例化 
var instance =new SubType();
console.log(instance.getSuperValue());输出false
```
面向对象的知识可以用一本书来写,这知识简单介绍下最基础最常用的概念.
# 函数表达式 
javaScript 中有两种定义函数的方式:函数声明和函数表达式.
使用函数表达式无序对函数命名,从而实现动态编程,也即匿名函数,有了匿名函数, 
javaScript函数有了更强大的用处. 
递归 
递归是一种很常见的算法,进店例子就是阶乘. 
```javaScript
  //最佳实践,函数表达式
  var factorial =(funtionf(num){
  if(num<=1){
  return 1;}else{
  return num * f(nume-1);
  }
  })
  //缺点: 
  //factorial存在被修改的可能 
  //导致return num*factorial(num -1)报错 
  function factorial(num){
  if (num<=1){ return 1;}else{return num*factorial(num-1);}
  }
  //缺点:arguments.callee,规范已经不推荐使用了
```
递归就是这样,很多人还在使用augunment,callee的方式,改回函数表达式把.这才是最佳实践.
其实递归不男鞋,你只要分两个步骤就会很清晰多了..
1. 边界条件,通常是if else
2. 递归调用. 按照这个模式,找几个经典的递归练练手,就熟悉了. 
闭包 
很多人经常觉得闭包很复杂,很容易掉坑里,其实不是的. 
那么闭包是什么呢?如果一个函数可以访问另外一个函数作用域中答辩了,那么前者就是闭包. 
由于javaScript函数可以返回函数,自然,创建闭包的常用方式就是一个函数内部创建另一个函数! 
这个并没有什么,在父函数中定义子函数就可以创建闭包,二子函数可以访问父函数的作用域 
我们通常因为被闭包坑了,才会被闭包吓到,尤其是面试里一堆闭包. 
闭包的定义前面提了, 如何创建闭包也说了, 那么我们数艘数哦闭包的缺陷以及如何解决/
```javascirpt 
  /*
  *我们通过SubFuncs返回函数数组,然后分别调用执行
  *返回函数的数组subFuncs而这些函数对superFunc的变量有引用
  *这就是一个典型的闭包
  * 那么有什么问题呢?
  *当我们回头执行subFuncs中的函数水滴时候,我们得到的i起始一直都是10为什么?
  *因为当我们返回subFuncs之后,superFunc中的i=10
  *所以当执行subFuncs中的函数的时候,输出i为10.
  * 以上就是闭包最大的坑,一句话理解就是:
  *子函数对富含鼠的变量的引用,是富含鼠运行结束后的变量的状态**/
  function superFunc(){
  var subFuncs =new Array();
  for(var i =0;i<10;i++){
  subFuncs[i] =function(){
  return i;};
  }
  return subFuncs;
  }
  //那么,如何解决上诉的闭包坑呢?
  //其实原理很简单,既然闭包坑的本质是:子函数对父函数变量的引用,是富含鼠运行结束之后的变量的状态
  //那么我们解决这个问题的方式就是:子函数对父函数的变量的引用,使用运行时候的状态 
  //如何做?
  //子啊函数表达式的基础上,加上自执行即可.
  function superFunc(){
  var subFuncs =new Array();
  for(var i=0 ;i<10;i++){
  subFuncs[i] =function(num){
  return function(){
  return num;
  };
  }(i);  }
  return subFuncs;
  }
```
综上,闭包本身就不是什么复杂的机子,就是子函数可以访问父函数的作用域.
而由于javaScript函数的特殊性,我们可以返回函数,如果我们将作为闭包的函数返回,那么该函数引用的父函数变量是父函数运行结束之后的状态, 
而不是运行时的状态,这便是闭包最大的坑,而为了解决这个坑,我们常用的方式就是让函数表达式自执行 
此外由于闭包引用了祖先函数的作用域,所以滥用闭包会有内存问题.
 好像闭包说都有点多了,说的他一无是处,那么闭包有什么用处呢?
  主要还是封装把.
  
# 封装
闭包可以封装私有变量或者黄封装块级作用域.
→封装块级作用域
javsScript 并没有块级作用域的概念,只有全局作用域和函数作用域,那么如果想要创建块级作用域的话,我们可以通过闭包来模拟. 
创建并立即调用一个函数,就可以封装一个块级作用域. 该函数可以立即执行其中的代码, 
内部变量执行结束就会被立即销毁.
```javaScript
  function outputNumbers(count){
  //在函数作用域下,利用闭包封装块级作用域 
  //这样的话,i在外部不可用 变有了类似块级作用域
  (function(){for (var i =0 ;i<coune;i++){alert(i);}})
  alert(i)//导致一个错误!
  }
  //在全局作用域下,利用闭包封装块级作用域 
  //这样的话,代码块不会对全局作用域造成污染
  (function(){
  var now =new Date();
  if(now .getMonth()== 0 && now.getDate()==1){
  alert('happy new year!')};
  })();
  //封装块及作用域的核心就是 函数表达式 +自执行!
  (function(){
  //块级作用域..
  })();
```
封装私有变量 
javaScript也没有私有变量的概念,我们也可以使用闭包来实现公方法,通过隐藏变量暴露方法的方式来实现封装私有变量. 
```javascript
(function(){
//私有变量和私有函数
var privateVariable =10;
function privateFunction(){
return false;}
//构造函数
myObject =function(){};
//公有/特权方法
MyObject.prototype.publicMethod =function(){
privateVariable++;
return privateFunction()
}})();
```


# 总结:
这差不多就是javaScript  的一些基础语法和稍微高级一些的用法,其实所谓的高级. 
都是javaScript不成熟的变现,尤其是面对对象,处于工程化的需要但是javaScript 本并不完美支持,好在ES6最新标准解决了很多问题. 
结合Babel用起来也不用太考虑兼容性问题,如果你是新手的话,建议你直接去ES6+BABEl吧2.

1. javaScript的基础主要包括:5种基本数据类型 1种复杂的数据类型, 操作符 ,控制语句, 函数等.
2. 了解基本的语法后,你还需要学习JavaScript的变量,作用域,作用域链.
3. 常见的引用类型可以边查边用.作为过来人,建议多学学正则,对你代码工地有较大的提升. 
4. 面对对象编程的部分外面有很多种方式,你只需要记住使用构造函数+原型去定义一个雷, 使用原型链去实现继承即可.更多的扩展, 
  多查阅资料翻翻书之类的把.
5. 函数表达式比较好玩的东西. 递归. 闭包.封装.记住递归的最佳实践.闭包的定义及缺陷,闭包的适用场景. 
6. javaScript 作为一门动态语言,和其他语言有较大的差异,这也就是造成很多人学习javaScript时会觉得难学,但是你现在看看前文,虽然与一个简略的总结.  
  但是JS主要的内容就这样了.所以不要被自己吓到了.
     
        
           
     补充一句如果你是新手的话,你直接去撸ES6+BABEL
