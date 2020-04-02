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

