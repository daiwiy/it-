# it-
我所学到的
浮动和inline-block的区别和清除浮动

以及inline和block的使用

空隙产生的原因

元素被当成行内元素排版的时候，元素之间的空白符（空格、回车换行等）都会被浏览器处理，根据white-space的处理方式（默认是normal，合并多余空白），原来HTML代码中的回车换行被转成一个空白符，在字体不为0的情况下，空白符占据一定宽度，所以inline-block的元素之间就出现了空隙。这些元素之间的间距会随着字体的大小而变化，当行内元素font-size:16px时，间距为8px。







方法6 ： 给父元素设置display：flex，



浮动：

1.浮动不是任意的，其还是在父元素的范围之中，不能脱离于父元素的内容区域。

2.若浮动元素比它的父元素还高，那么它就会溢出父元素外面

3.脱离文档流（普通流）

4.浮动有可能会造成父元素的高度坍塌





清除浮动：

1.直接给父元素定高：解决浮动元素脱离文档流导致的高度坍塌

2.给父元素加overflow:hidden属性触发bfc（关于bfc后面会详谈）
3.给元素添加display：inline-block（原理也是触发bfc）

4.使用伪类

5.在浮动元素后添加空标签并使用clear：both这个是不允许有浮动元素在哪个位置both是左右（clear只能清除该元素之前的浮动。 ）



bfc：

BFC的布局规则是什么？

1.内部的box会在垂直方向，一个接一个地放置（可以看作BFC中有一个的常规流）。

2.Box垂直方向的距离有margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠

3.每个元素的margin box 的左边，会包含块border box的左边相接触（对于从左往右的格式化，否则相反），即使存在浮动也是如此

4.BFC的区域不会与float box 重叠

5.BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此

6.计算BFC的高度时，浮动元素也参与计算



那些情况会产生新的BFC/如何创建BFC？

⑴根元素或其它包含它的元素

⑵浮动 (元素的 float 不为 none)

⑶绝对定位元素 (元素的 position 为 absolute 或 fixed)

⑷行内块 inline-blocks (元素的 display: inline-block)

⑸表格单元格 (元素的 display: table-cell，HTML表格单元格默认属性)

⑹表格标题 (元素的 display: table-caption, HTML表格标题默认属性)

⑺overflow 的值不为 visible的元素

⑻弹性盒 flex boxes (元素的 display: flex 或 inline-flex)


由bfc延伸至高度坍塌：

父元素高度自适应，子元素 float 后，造成父元素高度为0，称为高度塌陷问题。

float 脱离了普通流，并且创建了新的BFC，而父元素不具备产生 BFC 的条件，所以它的高度为0。


通过了解BFC的特性我们知道，BFC会把它包含的浮动元素高度也算在里面，也就是闭合浮动。

拿 overflow: auto 举例：

overflow: auto 并不会闭合浮动，而是 overflow: auto 会创建一个新的BFC，避免浮动的元素侵入其他元素。

和clear：both很像



由bfc又延伸到margin重叠：
http://lesson.jnshu.com/l/subjectContent/1120/?id=&lobtn=2



css权重：





flex布局：

行内元素：inline-flex

Webkit 内核的浏览器，必须加上-webkit前缀。

注意，设为 Flex 布局以后，子元素的float、clear和vertical-align（基线对齐方式）属性将失效。

具体属性：

flex-direction属性决定主轴的方向（即项目的排列方向）。

flex-wrap属性定义，如果一条轴线排不下，如何换行。

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

justify-content属性定义了项目在主轴上的对齐方式。

align-items属性定义项目在交叉轴上如何对齐。

align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0

align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch



什么是z-index？



w3school给出的定义是：z-index 属性设置元素的堆叠顺序。拥有更高堆叠顺序的元素总是会处于堆叠顺序较低的元素的前面。



层叠顺序：



正z-index>z-index:0/auto>inline/inline-block盒子>float盒子>block盒子>负z-index>background/border



注意：最重要的一点就是这个层叠顺序的前提是在同一个层叠上下文元素中！

谁大谁上：当具有明显的层叠水平标示的时候，如识别的z-indx值，在同一个层叠上下文领域，层叠水平值大的那一个覆盖小的那一个。

后来居上：当元素的层叠水平一致、层叠顺序相同的时候，在DOM流中处于后面的元素会覆盖前面的元素。

每个层叠上下文和兄弟元素独立，也就是当进行层叠变化或渲染的时候，只需要考虑后代元素。



每个层叠上下文是自成体系的，当元素发生层叠的时候，整个元素被认为是在父层叠上下文的层叠顺序中。



关于display：和visibility的区别和2者的用法：

display：neno不显示但是可以使用javascrpt去操作原理是因为：浏览器在最开始渲染时解析html标签时将它在dom树里面生成了相应的Dom但是在解析css之后生成渲染树时没有生成相应的盒子模型所以后面的布局渲染都不存在

display：none有继承性且和opacity一样，相当强力，强制要求，

visibility：hidden也具有继承性但是子元素可以通过修改visibility：visible从而显示；

display：none的元素因为没有在渲染树上不存在所以无法获取焦点和事件：

那我就很好奇，lable和input绑定之后在使input消失：display：none的情况下  input是如何获取到焦点的？？？



虽然不显示且不能响应事件但是可以在form表单里提交好神奇啊

并且display变化会触发reflow（回流）回流和repaint重绘会影响性能

且display：none之后其所在的位置会有其他的标签占据

而visibility：hidden则是：

不显示之后任占据之前的空间，

也无法获取焦点

.和display:none一样不妨碍form表单的提交

.CSS中的counter（计数器）不会忽略

Transition对visibility的变化有效

.visibility变化不会触发reflow
由于从visible设置为hidden时，不会改变元素布局相关的属性，因此不会触发reflow，只是静静地和其他渲染变化一起等待浏览器定时重绘界面。

在冒泡阶段响应事件
由于设置为visibility:hidden的元素其子元素可以为visibility:visible，因此隐藏的元素有可能位于事件冒泡的路径上因此下面代码中，将鼠标移至.visible时，.hidden会响应hover事件显示。




浏览器的渲染机制：

浏览器的渲染原理：浏览器会解析HTML标签生成DOM Tree，解析CSS生成CSSOM，然后将DOM Tree和CSSOM合成生成Render Tree，元素在Render Tree中对应0或多个盒子，然后浏览器以盒子模型的信息布局和渲染界面。而设置为display:none的元素则在Render Tree中没有生成对应的盒子模型，因此后续的布局、渲染工作自然没它什么事了，至于DOM操作还是可以的。








还有：rgba和opacity的区别和用法：

rgba不会继承是指元素的背景或者颜色最后那个a是个通道：

Alpha通道的参数是透明值



opacity是会继承的指的是一个元素的透明度级别。

这个属性会继承，但是如果子元素的opacity的值比父元素小那么它将继承自己的属性值；


自己重新熟悉了一下flex布局的各种细节和属性；

然后看了一下关于浏览器渲染和js引擎的关系：

https://segmentfault.com/a/1190000014018604

印象很深刻





关于问题为什么操作dom很耗费性能：看了关于js引擎线程和Gui渲染线程的执行机制之后从别人那边的出的结论



可能浏览器有自己的考虑，呵呵呵











关于回流和重绘还是比较简单的看了一下



这个是link和@import的区别和优缺点比较



还有关于面试里的问题比较多

文档内巨量的基础知识

https://www.cnblogs.com/autismtune/p/5210116.html

XML dom 和html dom的关系大概是继承（这个是很久以前的东西，没找到答案）

XHTML 是html的版本并不是XML

对XML具体参考：

https://www.w3school.com.cn/xml/xml_intro.asp

收获：

重新学习了关于dom的概念并进行深究：

首先dom是个标准是个规范：“W3C 文档对象模型 （DOM） 是中立于平台和语言的接口，它允许程序和脚本动态地访问和更新文档的内容、结构和样式。”

W3C文档对象模型也是dom；

编程接口也是dom的一种：定义了HTML和XML文档的逻辑结构和文档操作的编程接口。

总结：DOM是一种标准，他定义了html和xml文档的逻辑结构和文档操作的编程接口，这种接口是中立于平台和语言的，它允许程序和脚本动态地访问和更新文档的内容、结构和样式。”

如果要简单好记：dom是一个标准，这个标准规定了文档对象怎么解析成dom树的，所以又被称为文档对象模型，编程接口则是对象方法和对象属性，它允许程序和脚本动态地访问和更新文档的内容、结构和样式。


HTML DOM 是：

HTML 的标准对象模型，html
HTML 的标准编程接口，xml
W3C 标准



HTML DOM appendChild() 方法
appendChild() 方法可向节点的子节点列表的末尾添加新的子节点。

提示：如果文档树中已经存在了 newchild，它将从文档树中删除，然后重新插入它的新位置。如果 newchild 是 DocumentFragment 节点，则不会直接插入它，而是把它的子节点按序插入当前节点的 childNodes[] 数组的末尾。

你可以使用 appendChild() 方法移除元素到另外一个元素。


语法
node.appendChild(node)
参数
参数	类型	描述
node	节点对象	必须。你要添加的节点对象。
返回值
类型	描述
节点对象	添加的节点
技术细节
DOM 版本	Core Level 1 Node Object






HTML DOM removeChild() 方法
removeChild() 方法指定元素的某个指定的子节点。以 Node 对象返回被删除的节点，如果节点不存在则返回 null。


语法
node.removeChild(node)
参数
参数	类型	描述
node	节点对象	必须。 你要移除的节点对象。
返回值
类型	描述
节点对象	移除的节点
技术细节
DOM 版本	Core Level 1 Node Object



HTML DOM createElement() 方法

定义和用法
createElement() 方法通过指定名称创建一个元素

语法
document.createElement(nodename)
参数
参数	类型	描述
nodename	String	必须。创建元素的名称。
返回值
类型	描述
元素对象	创建的元素节点
技术细节
DOM 版本	Core Level 1 Document Object


HTML DOM replaceChild() Method

定义和用法
replaceChild() 方法可将某个子节点替换为另一个。

新节点可以是文本中已存在的，或者是你新创建的。

语法
node.replaceChild(newnode,oldnode)
参数
参数	类型	描述
newnode	Node 对象	必须。你要插入的节点对象。
oldnode	Node object	必须。你要移除的节点对象。
返回值
类型	描述
Node object	替换的节点
技术细节
DOM 版本	Core Level 1 Node Object






HTML DOM childNodes 属性
定义和用法

childNodes 属性返回包含被选节点的子节点的 NodeList。

提示： 如果选定的节点没有子节点，则该属性返回不包含节点的 NodeList。如需循环子节点列表，使用 nextSibling 属性，要比使用父对象的 childNodes 列表效率更高。

浏览器支语法
element.childNodes
技术细节
返回值：	NodeList 对象, 代表节点集合。
DOM 版本	Core Level 1


这个返回值：是xml dom里的NodeList 对象所以每次使用都要打印出来看下，xml和html还是有不同




原生js修改html文本使用innerHtml，修改属性使用.style.属性 进行修改

（权重值高于内联但是小于！important）使用原生js获取css属性并修改：

判断的原因是ie不支持getcomputestyle而是有自己的currentStyle：

function getStyle(element, attr) {

        if(element.currentStyle) {

                return element.currentStyle[attr];

        } else {

                return getComputedStyle(element, false)[attr];

        }

}


从资源到dom树的构成的过程：













自适应和响应式的区别：

自适应：需要开发多套界面适应不同的屏幕宽度；响应式开发一套界面适应全部的屏幕宽度


理论上来说，响应式布局在任何情况下都比自适应布局好一些，但在某些情况下自适应布局更切实际。

自适应布局可以让你的设计更加可控，因为你只需要考虑几种状态就万事大吉了。

但在响应式布局中你可能需要面对非常多状态——是的，大部分状态之间的区别很小，但它们又的确是不同的，这样一来就很难确切搞清你的设计会是什么样。

HTML DOM setAttribute() 方法





定义和用法
setAttribute() 方法添加指定的属性，并为其赋指定的值。

如果这个指定的属性已存在，则仅设置/更改值。

语法
element.setAttribute(attributename,attributevalue)
参数
参数	类型	描述
attributename	String	必需。您希望添加的属性的名称。
attributevalue	String	必需。您希望添加的属性值。
返回值
无返回值。



伪类：

CSS 伪类(Pseudo-classes)
CSS伪类是用来添加一些选择器的特殊效果。



css计数器：

js的全军方法

typeof (变量) === （数据类型）：判断数据类型却不报错 



parseInt：parseInt方法用于将字符串转为整数。
如果字符串头部有空格，空格会被自动去除。

如果parseInt的参数不是字符串，则会先转为字符串再转换。

字符串转为整数的时候，是一个个字符依次转换，如果遇到不能转为数字的字符，就不再进行下去，返回已经转好的部分

如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回NaN

如果字符串以0x或0X开头，parseInt会将其按照十六进制数解析。

parseInt('0x10') // 16

如果字符串以0开头，将其按照10进制解析。

parseInt('011') // 11



对于那些会自动转为科学计数法的数字，parseInt会将科学计数法的表示方法视为字符串，因此导致一些奇怪的结果。

parseInt(1000000000000000000000.5) // 1

// 等同于

parseInt('1e+21') // 1

parseInt(0.0000008) // 8

// 等同于

parseInt('8e-7') // 8



parseInt方法还可以接受第二个参数（2到36之间），表示被解析的值的进制，返回该值对应的十进制数。默认情况下，parseInt的第二个参数为10，即默认是十进制转十进制。

但是这个要慎用因为科学计数法和种种js数字的特殊性及其容易出问题：

如果要用先看一遍文档：

https://wangdoc.com/javascript/types/number.html





parseFloat:parseFloat方法用于将一个字符串转为浮点数

parseFloat('3.14') // 3.14



如果字符串符合科学计数法，则会进行相应的转换。


parseFloat('314e-2') // 3.14

parseFloat('0.0314E+2') // 3.14



如果字符串包含不能转为浮点数的字符，则不再进行往后转换，返回已经转好的部分。

parseFloat('3.14more non-digit characters') // 3.14




parseFloat方法会自动过滤字符串前导的空格。

parseFloat('\t\v\r12.34\n ') // 12.34


如果参数不是字符串，或者字符串的第一个字符不能转化为浮点数，则返回NaN。




上面代码中，尤其值得注意，parseFloat会将空字符串转为NaN。

这些特点使得parseFloat的转换结果不同于Number函数。






字符串：

字符串就是零个或多个排在一起的字符，放在单引号或双引号之中

单引号字符串的内部，可以使用双引号。双引号字符串的内部，可以使用单引号。

'key = "value"'

"It's a long journey"



如果要在单引号字符串的内部，使用单引号，就必须在内部的单引号前面加上反斜杠，用来转义。双引号字符串内部使用双引号，也是如此。

'Did she say \'Hello\'?'

// "Did she say 'Hello'?"



连接运算符（+）可以连接多个单行字符串，将长字符串拆成多行书写，输出的时候也是单行。

果想输出多行字符串，有一种利用多行注释的变通方法。

(function () { /*

line 1

line 2

line 3

*/}).toString().split('\n').slice(1, -1).join('\n')

// "line 1

// line 2

// line 3"



length属性返回字符串的长度，该属性也是无法改变的。





对象：
对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。



键名：
如果键名是数值，会被自动转为字符串。


上面代码中，对象obj的所有键名虽然看上去像数值，实际上都被自动转成了字符串。

如果键名不符合标识名的条件（比如第一个字符为数字，或者含有空格或运算符），且也不是数字，则必须加上引号，否则会报错。

对象的每一个键名又称为“属性”（property），它的“键值”可以是任何数据类型。如果一个属性的值为函数，通常把这个属性称为“方法”，它可以像函数那样调用。

var obj = {

  p: function (x) {

    return 2 * x;

  }

};

obj.p(1) // 2

上面代码中，对象obj的属性p，就指向一个函数。

如果属性的值还是一个对象，就形成了链式引用。



var o1 = {};

var o2 = { bar: 'hello' };

o1.foo = o2;

o1.foo.bar // "hello"

上面代码中，对象o1的属性foo指向对象o2，就可以链式引用o2的属性。

对象的属性之间用逗号分隔，最后一个属性后面可以加逗号（trailing comma），也可以不加。


























函数的重复声明 # 
如果同一个函数被多次声明，后面的声明就会覆盖前面的声明。

function f() {

  console.log(1);

}

f() // 2

function f() {

  console.log(2);

}

f() // 2

上面代码中，后一次的函数声明覆盖了前面一次。而且，由于函数名的提升（参见下文），前一次声明在任何时候都是无效的，这一点要特别注意。





总之，函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域。

很容易犯错的一点是，如果函数A调用函数B，却没考虑到函数B不会引用函数A的内部变量







　这里有一个地方需要注意，函数内部声明变量的时候，一定要使用var命令。如果不用的话，你实际上声明了一个全局变量！
 3种跳出循环的方式的区别：

3个关键词的含义和比较

在 break,continue和return 三个关键字中， break,continue是化为一类的，return 是函数返回语句，但是返回的同时也将函数停止。

相同之处：三个都会将此时进行的语句停止。

不同之处：

1、break：是立即结束语句，并跳出语句，进行下个语句执行。

2、continue：是停止当前语句，并从头执行该语句。

3、return：停止函数。

4、使用的语句环境不一样，break和continue是用在循环或switch语句中，return是用在函数语句中。





break用于完全结束一个循环，跳出循环体。不管是哪种循环，一旦在循环体中遇到break，系统将完全结束循环，开始执行循环之后的代码。 break不仅可以结束其所在的循环，还可结束其外层循环。此时需要在break后紧跟一个标签，这个标签用于标识一个外层循环。



continue的功能和break有点类似，区别是continue只是中止本次循环，接着开始下一次循环。而break则是完全中止循环。



return关键字并不是专门用于跳出循环的，return的功能是结束一个方法。 一旦在循环体内执行到一个return语句，return语句将会结束该方法，循环自然也随之结束。与continue和break不同的是，return直接结束整个方法，不管这个return处于多少层循环之内。
函数的属性和方法：

toString() # 
函数的toString方法返回一个字符串，内容是函数的源码。

length 属性
函数的length属性返回函数预期传入的参数个数，即函数定义之中的参数个数。

name 属性
函数的name属性返回函数的名字。

函数的变量提升

函数的作用域在其声明的位置而不是调用的位置：

函数的闭包：

原因就在于inc始终在内存中，而inc的存在依赖于createIncrementor，因此也始终在内存中，不会在调用结束后，被垃圾回收机制回收。

闭包的另一个用处，是封装对象的私有属性和私有方法。

注意，外层函数每次运行，都会生成一个新的闭包，而这个闭包又会保留外层函数的内部变量，所以内存消耗很大。因此不能滥用闭包，否则会造成网页的性能问题。



function Person(name) {

  var _age;

  function setAge(n) {

    _age = n;

  }

  function getAge() {

    return _age;

  }

  return {

    name: name,

    getAge: getAge,

    setAge: setAge

  };

}

var p1 = Person('张三');

p1.setAge(25);

p1.getAge() // 25



eval命令接受一个字符串作为参数，并将这个字符串当作语句执行。

如果参数字符串无法当作语句运行，那么就会报错。

放在eval中的字符串，应该有独自存在的意义，不能用来与eval以外的命令配合使用。举例来说，下面的代码将会报错。

如果eval的参数不是字符串，那么会原样返回。

eval没有自己的作用域，都在当前作用域内执行，因此可能会修改当前作用域的变量的值，造成安全问题。





数组的属性和方法以及细节：

数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。

除了在定义时赋值，数组也可以先定义后赋值。

任何类型的数据，都可以放入数组。（包括function和object以及Boolean）

如果数组的元素还是数组，就形成了多维数组。

数组的本质：

本质上，数组属于一种特殊的对象。typeof运算符会返回数组的类型是object。

数组的特殊性体现在，它的键名是按次序排列的一组整数（0，1，2...）。

所以，数组的键名其实也是字符串。之所以可以用数值读取，是因为非字符串的键名会被转为字符串。

一个值总是先转成字符串，再作为键名进行赋值。


数组的方法和属性：

数组的length属性，返回数组的成员数量。

length属性是可写的。如果人为设置一个小于当前成员个数的值，该数组的成员会自动减少到length设置的值。

清空数组的一个有效方法，就是将length属性设为0。

如果人为设置length大于当前元素个数，则数组的成员数量会增加到这个值，新增的位置都是空位。


var a = ['a'];

a.length = 3;

a[1] // undefined





上面代码表示，当length属性设为大于数组个数时，读取新增的位置都会返回undefined。

如果人为设置length为不合法的值，JavaScript 会报错。

使用delete命令删除一个数组成员，会形成空位，并且不会影响length属性。







对数据类型的改变：

强制转换主要指使用Number()、String()和Boolean()三个函数，手动将各种类型的值，分别转换成数字、字符串或者布尔值。











对象有两种读取成员的方法：点结构（object.key）和方括号结构（object[key]）。但是，对于数值的键名，不能使用点结构。


in 运算符
检查某个键名是否存在的运算符in，适用于对象，也适用于数组。

for...in 循环和数组的遍历
for...in循环不仅可以遍历对象，也可以遍历数组，毕竟数组只是一种特殊对象。

var a = [1, 2, 3];for (var i in a) {  console.log(a[i]); }



对象的基本特性和方法属性：


查看一个对象本身的所有属性，可以使用Object.keys方法。

var obj = {

  key1: 1,

  key2: 2

};

Object.keys(obj);

// ['key1', 'key2']





delete命令用于删除对象的属性，删除成功后返回true。

var obj = { p: 1 };

Object.keys(obj) // ["p"]

delete obj.p // true

obj.p // undefined

Object.keys(obj) // []






定时器的this一直指向window
对象的原型是：__proto__

函数的原型是：prototype

使用new命令时，它后面的函数依次执行下面的步骤。

创建一个空对象，作为将要返回的对象实例。

将这个空对象的原型，指向构造函数的prototype属性。：
将这个对象的__proto__指向构造函数的prototype属性或者说使__proto__的键值等于构造函数的prototype属性的键值又或者说2者指向同一个堆内存里的地址

将这个空对象赋值给函数内部的this关键字。
或者说使this指向的对象变为这个空对象：简单来说进行了一次赋值

开始执行构造函数内部的代码。
输出这个实例对象；

这个从堆栈内存的角度解释很简单；

https://www.bilibili.com/video/BV1Kt411w7MP?p=29







问：原型链怎么形成？

答：每个对象都有一个内部链接到另一个对象， 称为它的原型 prototype。该原型对象有自己的原型，等等，直到达到一个以null为原型的对象。 根据定义，null没有原型，并且作为这个原型链prototype chain中的最终链接。

问：constructor 是什么？

答：构造函数的prototype 属性指向原型对象，原型对象也生成一个对应的constructor属性指向构造函数。所以constructor用来执行对应的 构造函数。







JS在创建对象（不论是普通对象还是函数对象）的时候，都有一个叫做__proto__的内置属性，用于指向创建它的函数对象的原型对象prototype，我们把这个有__proto__串起来的直到Object.prototype.__proto__为null的链叫做原型链

关于作用域变量的查找机制：

函数在当前作用域中无法找到某个变量时，js引擎就会在外层嵌套的作用域中进行查找，直到找到该变量或者抵达最外层作用域（一般是全局作用域）为止。

而对象的成员（继承的属性和方法是实例成员，实例或者构造函数只可通过自身的来操作的叫静态成员）查找机制

则是通过原型链去查找：

每个对象都有一个proto属性指向自己的原型对象prototype如果在这个对象的原型上找不到自己在搜索的属性或者方法















什么是执行环境？

执行环境（execution context，为简单起见，有时也称为“环境”）是JavaScript

中最为重要的一个概念。执行环境定义了变量或函数有权访问的其他数据，决定了它们各自的行为。——《JavaScript高级程序设计（第3版）》

什么是作用域呢？


每个函数都有自己的执行环境，当代码在执行环境中执行时，就会创建变量对象的作用域链。作用域链保证了对执行环境有权访问所有变量和函数的有序访问。作用域链的前端，始终都是当前执行的代码所在的环境的变量对象，如果环境是一个函数，那么它的变量对象就是该函数的活动对象。作用域链的下一个变量对象来自包含（外部）环境，再下一个变量对象来自下一个包含环境。这样一直延续到全局执行环境，记住，全局执行环境的变量对象永远是作用域中的最后一个对象。

（2）知识剖析：

程序执行时，环境栈与执行环境的关系,当执行流进入一个函数时，即该函数正在执行，函数的执行环境就会被推入一个环境栈中，所有处在执行流的执行环境将有次序地保存在环境栈中，在函数执行之后， 栈将其执行环境弹出，把控制权交给原来的执行环境。所以在程序执行中，环境栈是不断变化的，伴随着执行环境的出入.

（3）常见问题：

js中执环境和作用域的区别在哪里?

（4）解决方案：



1.执行环境：执行环境是JS中最重要的一个概念；它定义了变量和函数有权访问的其他数据；2.全局执行环境：最外围的一个执行环境，根据ECMAScript实现所在的宿主环境不同而不同，在Web浏览器中，全局执行环境被认为是window对象；</p>

3.作用域链：当代码在环境中执行时，会创建变量对象的一个作用链；作用域链的作用是保证对执行环境有权访问的所有变量和函数的有序访问；







关于深拷贝数组的骚操作：

通过数组方法concat去复制一个数组并返回一个副本的特性

声明一个变量在把副本数组赋值给变量

具体链接：https://www.h5course.com/a/20160329399.html

