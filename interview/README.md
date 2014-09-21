js
================



# 面试基础题目


#js#
##一、基本知识##

###1.基本类型和引用类型###
基本类型就是那些字符串、数字、布尔值以及null和Undefine，他们在传递数值的时候只进行值传递；
引用类型就是除了上面这些基本类型之外的那些对象，他在传递的过程中，采用的是引用的传递，类似java中的两种类型的值一样

###2.null && undefine###
null是一个对象，指代的是一个对象不存在；一般应用在函数的参数来判断不是对象，或者是在原型链中的终点
typeof null -> object
undefine则是一个预定全局变量，表明的是一个变量没有初始化，可以理解就是声明的一个变量但是还没给这个变量赋值的那些情况；
typeof undefine -> undefine

###3. 执行环境和作用域###
执行环境：是一个函数可以访问到的变量和函数
作用域：是一个函数在执行过程中可以访问到的变量和函数的一个对象链


###4. 垃圾回收###
当一个函数执行完毕的时候，正常情况下，他内部声明的变量和函数会在函数执行结束后进行释放，常见的有两种处理垃圾回收的方法：一种是引用计数（就是计算引用一个变量的次数，当一个变量他的引用的次数为0的时候就代表了没有其他变量引用他，便可以进行垃圾回收）；还有一种是标记清除（利用一个标记为来清除）


###5. this###
关于this的指向分为四种，分别对应了函数的四种用法
1. 当函数作为构造函数的时候，比如new A()，那么此时函数A内部的this指向的是构造函数返回的那个新的实例；
2. 函数作为一个对象的方法进行调用，比如p.A()，那么此时函数A中的this指向的是该对象P
3. 函数作为一个普通的函数进行调用，比如就是A()，那么此时A内部的this指向的是全局的window
4. 函数作为call,apply的方法调用，比如A.call(o,a)，那么此时函数A内部的this指向的是绑定后的对象o


###6. 闭包###
闭包的作用有两个
1. 可以读取到函数内部的数值
2. 可以让一些变量始终保存在内存中（私有变量）

关于第一点正常的函数由于作用域链的限制，他只能访问到本身以及他的上一级的函数内部定义的变量，但是不能访问在他内部定义的函数内的变量信息，通过闭包可以将这些信息返回出来

关于第二点正常的函数在执行结束之后，由于内部的变量的引用计数都是0，所有函数在执行完毕之后要进行回收，所以执行一次之后就没有了，但是通过闭包，可以将一个变量在结束返回的时候将其返回，那么在函数结束的时候，他的引用计数没有清零，所有将不会被回收掉，这样可以达到可以让他一直存在内存中

比如一些全局的计数可以用这个方法来实现

###7. 面向对象 ###



###8. arguments###

是一个类数组，表示符arguments表示的是指向实参对象的引用，还有一个是aguments.callee指代的是当前正在执行的函数，可以使用这个方法来下实现递归的函数调用

###9. Array和String基本用法###
1. Array
    * slice():从某个已有的数组返回选定的元素
    * join():把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。
    * splice():从数组中添加/删除项目，然后返回被删除的项目
2. String
    * slice()方法可提取字符串的某个部分，并以新的字符串返回被提取的部分
    * split()把字符串分割为字符串数组
    * substring() 方法用于提取字符串中介于两个指定下标之间的字符

###10. Object.create###
        Object.create(prototype, descriptors)
第一个参数是原型链上的属性,后面的参数是挂在对象上的,EC５的功能
可以通过模拟类似实现（可以再加一些对类似的判断）

        var f = function(){};
        f.prototype = obj;
        retunrn new f();
        
不过只是类似模拟，因为有种object.create(null)没有原型的也可以


###11. AJAX和Promise/Deferred###

###12.###

##二、 问题##
###1. js脚本延迟###
js程序在浏览器端的执行分两个步骤：
1. 载入文档，并执行<\script\>中的代码
2. 执行异步事件 这个时候就是监听浏览上发生的事件



在script中有两个属性在支持他们的浏览中可以运行
1. defer：浏览器延迟脚本的执行，直到文档的载入和解析完成
2. async：浏览器尽快执行脚本，而不用在下载脚本时阻塞文档解析

可以动态创建一个。然后再插入DOM中

###2. 写一个通过的事件处理的函数###
就是要处理下IE的事件处理跟其他的事件处理的兼容
target在事件流的目标阶段；currentTarget在事件流的捕获，目标及冒泡阶段。只有当事件流处在目标阶段的时候，两个的指向才是一样的， 而当处于捕获和冒泡阶段的时候，target指向被单击的对象而currentTarget指向当前事件活动的对象（一般为父级）。

###3. 常见的http错误代码###
200 - 服务器成功返回网页
404 - 请求的网页不存在
503 - 服务不可用
304 - Not Modified 如果客服端已经完成一个有条件的请求并且请求是允许的，但是这个文档并没有改变，服务器应该返回304状态
403 - Forbidden 服务器接受请求，但是被拒绝处理。

响应码分五种类型，由它们的第一位数字表示：
1.1xx：信息，请求收到，继续处理
2.2xx：成功，行为被成功地接受、理解和采纳
3.3xx：重定向，为了完成请求，必须进一步执行的动作
4.4xx：客户端错误，请求包含语法错误或者请求无法实现
5.5xx：服务器错误，服务器不能实现一种明显无效的请求

###4. new一个对象过程中发生的事情###
自定义构造函数，在new过程中发生的事情

   * 创建一个空对象，将它的引用赋给this，并继承函数的原型。
   * 通过this将属性和方法添加至这个对象。
   * 最后返回this指向的新对象（如果没有手动返回其他的对象）。

###5. **bind函数**###
函数绑定一个简单的bind函数接受一个函数和一个环境，并返回一个在给定环境中调用给定函数的函数，并且就让那个所有参数不变地传过去

    function bind(fn,context){
        return function(){
            return fn.apply(context,argument);
        }
    }
###6. function与New　Function的区别###
1. new Function()允许js在运行时动态创建并编译函数
2. 每次调用都会先解析函数体并创建新的函数对象，所以执行的效率比较低（比如在一个循环体中这个定义，每次都会进行解析，而function不用）
3. Function的作用域在顶层(全局作用域)

注：貌似之前在博客中看到过，有一些模版引擎就是通过这个来实现的

###7. js创建一个table###
可能一开始的想法会是如下

        var _table = document.createElement("table");
        _table.innerHTML = "...";

其实这样是有问题的，在于table的innerHTML是只读的属性，（ IE下 COL, COLGROUP, FRAMESET, HTML, STYLE, TABLE, TBODY, TFOOT, THEAD, TITLE, TR 这些元素的 innerHTML 属性都是只读的，不能直接操作）不可以写，提供几个方法
1. 老老实实的先创建一个table，然后在创建一个tbody，然后试用table.appendChild(tbody)这样来
2. 在table外面裹一个div，那么直接对那个div进行innerHTML

[附上第一种方法的代码](https://developer.mozilla.org/zh-CN/docs/%E4%BD%BF%E7%94%A8Javascript%E5%92%8CDOM_Interfaces%E6%9D%A5%E5%A4%84%E7%90%86HTML)

###8. 关于跨域的方法###
1. postMessage
2. 修改window.domain
3. 修改window.name
4. 修改hash

具体可以参考之前整理的[博文](http://tankpt.github.io/2014/05/28/20140528_cors/)

###9. get 和post方式的区别###
原理上
1. 根据http规范，GET用于信息获取，而且是安全和幂等
get应该指的是用于获取信息而不是修改信息，
2. 根据http规范，POST表示可能修改服务器上的资源请求

表面现象
1. GET请求的数据会附在URL之后（就是把数据放置在HTTP协议头中），以?分割URL和传输数据，参数之间以&相连；而POST把提交的数据则放置在是HTTP包的包体中。
2. "GET方式提交的数据最多只能是1024字节，理论上POST没有限制，可传较大量的数
(1)其实GET是通过URL提交数据，那么GET可提交的数据量就跟URL的长度有直接关系了 
(2)理论上讲，POST是没有大小限制的，HTTP协议规范也没有进行大小限制，说“POST数据量存在80K/100K的大小限制”是不准确的，POST数据是没有限制的，起限制作用的是服务器的处理程序的处理能力。

3. 解析的方法不同
(1)在ASP中，服务端获取GET请求参数用Request.QueryString，获取POST请求参数用Request.Form
(2)在JSP中，用request.getParameter(\"XXXX\")来获取，虽然jsp中也有request.getQueryString()方法，但使用起来比较麻烦，比如：传一个test.jsp?name=hyddd&password=hyddd，用request.getQueryString()得到的是：name=hyddd&password=hyddd
(3)在PHP中，可以用_GET和_POST分别获取GET和POST中的数据，而_REQUEST则可以获取GET和POST两种请求中的数据。值得注意的是，JSP中使用request和PHP中使用$_REQUEST都会有隐患

4. POST的安全性要比GET的安全性高。注意：这里所说的安全性和上面GET提到的“安全”不是同个概念。上面“安全”的含义仅仅是不作数据修改，而这里安全的含义是真正的Security的含义，比如：通过GET提交数据，用户名和密码将明文出现在URL上，因为(1)登录页面有可能被浏览器缓存，(2)其他人查看浏览器的历史纪录，那么别人就可以拿到你的账号和密码了，除此之外，使用GET提交数据还可能会造成Cross-site request forgery攻击。

###10. js深拷贝###
主要的点在于js对象的赋值，是引用的赋值

        function clone(myObj){
            //传入参数必须对对象才能实现clone出新对象
            if(typeof(myObj) != 'object' || myObj == null)                   return myObj;
            var newObj = new Object();
            for(var i in myObj){
              newObj[i]＝clone(myObj[i]);
              //对于对象中含有对象情况使用递归调用。
            }
            return myNewObj;
        }

###11. url中取参数###
貌似很多地方都会出现这个问题，写了个自己的

        var getParament = function (_url) {
            var paramentArray =  _url.split("?")[1].split("&"),
                tmpObj = {};
            for(var i=0 ,len = paramentArray.length;i<len;i++)
            {
                    var tmp = paramentArray[i].split("=");
                    tmpObj[tmp[0]] = tmp[1];
            }
            return tmpObj;
        };
        var regetPara = function(_url){
            var pattern = /(\?|&)\w+=\w+/g,
               _paraArray = _url.match(pattern),
                tmpObj = {};
            for(var j= 0,len2 = _paraArray.length;j<len2;j++)
            {
                var　tmp=_paraArray[j].substring(1).split("=");
                tmpObj[tmp[0]] = tmp[1];
            }
            return tmpObj;
        }


###12. 从dom查找class###

写了两种方法，一种是用ducoment.getElementsByTagName("*")；还有一种是基于递归的方法来实现，两种方法见整理的[js-common中element](https://github.com/Tankpt/learning/blob/master/js-common/src/element.js)


###13. innerText、textContent区别###
刚好看到这个。然后搜了下网上找到一个[不错的答案](http://stackoverflow.com/questions/19030742/difference-between-innertext-and-innerhtml-in-javascript)
大概的就是说了下
1. innerHTML
(1)微软在IE中引入，在一些旧的ff浏览器上不支持，其他浏览器都支持
(2)对样式比较敏感，返回的时候会忽略那些隐藏的元素，这包括了visible:hiddern和display:none的元素
(3)不会返回那些script标签之间的内容;而且返回的内容会企图保留原来表格的格式
(4)**对css的样式敏感，会触发一次回流**
2. textContent
(1)对样式不敏感，所以那些被隐藏的元素也会一起被返回
(2)不会触发一次回流，所以在性能上更为好
(3)会返回标签内的所有内容，包括了script里面的内容

    
补充:innerHTML的性能不错，效率比那些createElement(**)，再append　DOM中的方法性能要很好多

写了一个比较兼容的方法
见整理的[js-common中element](https://github.com/Tankpt/learning/blob/master/js-common/src/element.js)

###14. 用innerHTML来实现outerHTML###
主要的思想就是创建一个临时的容器，里面放着需要的node的一份拷贝内容，在插入的时候则是利用结点在移动的时候，他会自动从一个地方移动到另一个地方，原来的地方不需要手动清除
见整理的[js-common中element](https://github.com/Tankpt/learning/blob/master/js-common/src/element.js)

###15. 模拟jquery中的append insertBefore的方法###

主要是思路就是通过原生的这append 和insertBefore来实现，insertAfter、insertBefore、append、pretend
见整理的[js-common中element](https://github.com/Tankpt/learning/blob/master/js-common/src/element.js)

###16. 模拟事件###
对于事件的绑定和解绑，所要注意的就是IE下的attachEvent与非IE下的addEventListener,之前看到的一个简单的版本如下

        _v._$dispatchEvent = function(_node,_event){
            try{
                if(_node.dispatchEvent){
                    var _eventObj = document.createEvent("HTMLEvents");
                    _eventObj.initEvent(_event,true,true);
                    _node.dispatchEvent(_eventObj);
                }else if(_node.fireEvent){
                    var evt = document.createEventObject();
                    _node.fireEvent('on'+_event,evt);
                }
            }catch(e){}
    };

但是存在的一个问题就是不能模拟冒泡这样的事件了，他只是模拟了这个动作，但是跟实际点击这个动作的效果不一样

        /**
         * 事件触发器
         * @param { Object } DOM元素
         * @param { String / Object } 事件类型 / event对象
         * @param { Array }  传递给事件处理函数的附加参数
         * @param { Boolean } 是否冒泡
         */
        trigger : function( elem, event, data, isStopPropagation ){
            var type = event.type || event,
                // 冒泡的父元素，一直到document、window
                parent = elem.parentNode ||　elem.ownerDocument || 
                    elem === elem.ownerDocument && win,
                eventHandler = $.data( elem, type + 'Handler' );
            isStopPropagation = typeof data === 'boolean' ? 
                data : (isStopPropagation || false);
            data = data && isArray( data ) ? data : [];
            // 创建自定义的event对象        
            event = typeof event === 'object' ? 
                    event : {
                        type : type,
                        preventDefault : noop,
                        stopPropagation : function(){
                            isStopPropagation = true;
                        }
                    };
            event.target = elem;        
            data.unshift( event );
            if( eventHandler ){
                eventHandler.call( elem, data );
            }
            // 递归调用自身来模拟冒泡
            if( parent && !isStopPropagation ){
                data.shift();
                this.trigger( parent, event, data );
            }
        }

里面有几点做的很赞，一个就是依次遍历递归到顶部的这个方法；还有一个就是判断parent的方法（这个之前都没有设计到过）

参考的博文[事件触发器](http://stylechen.com/trigger.html)

补充：**在event对象中，有俩属性target和currentTarget，其中target始终指向触发该事件的元素；currentTarget则是始终指向绑定事件的元素，而且在事件处理函数中的this 也是指向绑定事件的元素**

###17. 模拟jQuery中的ready方法###
主要是来监听document的DOMContentLoad（表示文档加载完毕，但是可能图片或延迟的js还没加载好）,还有监听document的readystatechange事件，以及监听load　

#css#
##一、基本知识##
1. font的缩写可以按照下面的规则
    
            font-style
            font-variant
            font-weight
            font-size/line-height
            font-family
2. em和strong区别：em表示强调，strong表示更强烈的强调。em用来局部强调，strong 则是全局强调。从视觉上考虑，em的强调是有顺序的，阅读到某处时，才会注意到。strong的强调则是一种随意无顺序的，看见某文时，立刻就凸显出来的关键词句em 表示内容的着重点（stress emphasis），strong 表示内容的重要性（strong importance），strong 不会改变所在句子的语意，em 则会改变所在句子的语义

3. 清除浮动比较优雅的一个方法
    
        .f-cb:after{display:block;clear:both;visibility:hidden;height:0;overflow:hidden;content:".";}
        .f-cb{zoom:1}
4. text-decoration 分别有哪几种值
    none、underline、overline、line-through、blink
5. 

##问题##
1. css常见的hack
 关于hack的介绍：
（１）属性前缀法(即类内部Hack)：例如 IE6能识别下划线"_"和星号" * "，IE7能识别星号"*"，但不能识别下划线"_"，IE6~IE10都认识"\9"，但firefox前述三个都不能认识。
（２）选择器前缀法(即选择器Hack)：例如 IE6能识别*html.class{}，IE7能识别*+html.class{}或者*:first-child+html .class{}。
（３）IE条件注释法(即HTML条件注释Hack)：针对所有IE(注：IE10+已经不再支持条件注释)： <!--[if IE]>IE浏览器显示的内容<![endif]-->，针对IE6及以下版本：<!--[if lt IE 6]>只在IE6-显示的内容<![endif]-->。这类Hack不仅对CSS生效，对写在判断语句里面的所有代码都会生效。

        background-color:gray\9; /* IE6, IE7, IE8, IE9, IE10*/
        background-color:purple\0; /* IE8, IE9, IE10 */  
        background-color:orange\9\0;/*IE9, IE10*/  
        *background-color:black;  /* ie 6/7 - for ie7 */  
        _background-color:green;  /* ie 6 - for ie6 */   
2. 

#html#

##基础##
1.  Doctype? 严格模式与混杂模式-如何触发这两种模式，区分它们有何意义? 
标准模式和混杂模式（quirks mode）。在标准模式中，浏览器根据规范呈现页面；在混杂模式中，页面以一种比较宽松的向后兼容的方式显示。
[详见](http://blog.sina.com.cn/s/blog_5f245b8a01019uy7.html)
2.  void的空元素
[见博文](http://ourjs.com/detail/531b2ce89144f4934f00000b)
3.  

#其他#

##cookie##
1. cookie的作用域是通过文档源和文档路径来确定的；而且默认情况下，于创建他的web页面有关，并对该web页面以及和该页面同目录或者子目录的其他web页面可见
2. 不过cookie可以设置他的作用域


##兼容问题##
1. 写出几种IE6 BUG的解决方法

        a  双边距BUG float引起的 使用display
        b  像素问题 使用float引起的 使用dislpay:inline -3px
        c  超链接hover 点击后失效 使用正确的书写顺序 linkvisited hover activen  Ie z-index问题 给父级添加position:relative
        d  Png 透明 使用js代码改
        e  Min-height 最小高度 ！Important 解决’
        f  select 在ie6下遮盖 使用iframe嵌套
        g  为什么没有办法定义1px左右的宽度容器(IE6默认的行高造成的，使用over:hidden,zoom:0.08line-height:1px)
