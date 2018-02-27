##CSS基础
* 派生选(上下文选择器)择器:派生选择器允许你根据文档的上下文关系来确定某个标签的样式
	
		li strong {
		    font-style: italic;
		    font-weight: normal;
		  }
		
		<li><strong>我是斜体字。这是因为 strong 元素位于 li 元素内。</strong></li>
* 后代选择器(要求必须从右向左读选择器,后代选择器有一个易被忽视的方面，即两个元素之间的层次间隔可以是无限的。):
	
		h1 em {color:red;}

		<h1>This is a <em>important</em> heading</h1>
		<p>This is a <em>important</em> paragraph.</p>
* 子元素选择器:只能选择作为某元素子元素的元素。

		h1 > strong {color:red;}
		如果从右向左读，选择器 h1 > strong 可以解释为“选择作为 h1 元素子元素的所有 strong 元素”。
		
		table.company td > p
		上面的选择器会选择作为 td 元素子元素的所有 p 元素，这个 td 元素本身从 table 元素继承，该 table 元素有一个包含 company 的 class 属性。
* 相邻兄弟选择器:如果需要选择紧接在另一个元素后的元素，而且二者有相同的父元素
		
		h1 + p {margin-top:50px;}
		html > body table + ul {margin-top:20px;}
		这个选择器解释为：选择紧接在 table 元素后出现的所有兄弟 ul 元素，该 table 元素包含在一个 body 元素中，body 元素本身是 html 元素的子元素
* id 选择器:选择器可以为标有特定 id 的 HTML 元素指定特定的样式。
	> id 选择器以 "#" 来定义。   
	> /#red {color:red;}  
	> /#green {color:green;}  
	
	* id 选择器和派生选择器  
		> \#sidebar p {  
		font-style: italic;  
		text-align: right;  
		margin-top: 0.5em;  
		}
* CSS 类选择器:类选择器以一个点号显示    		
	*   
		> .center {text-align: center}
	
	* class 也可被用作派生选择器：  
		> .fancy td {   
		color: #f60;  
		background: #666;  
		}
	* 类而被选择  
		> td.fancy {  
		color: #f60;  
		background: #666;  
		}  
		类名为 fancy 的表格单元将是带有灰色背景的橙色。
* 对带有指定属性的 HTML 元素设置样式。
	 * title 属性的所有元素设置样式
	 	> [title]   
	 	> {  
	 	> color: red;  
	 	> }
	 * 属性和值选择器
	 	> [title=W3School]  
	 	> {  
	 	> border:5px solid blue;  
	 	> }
	 * 属性和值选择器 - 多个值
		 > [title~=hello] { color:red; }  
	 * CSS 选择器参考手册
		 > [attribute]	用于选取带有指定属性的元素。  
		 > [attribute=value]	用于选取带有指定属性和值的元素。  
		 > [attribute~=value]	用于选取属性值中包含指定词汇的元素。  
		 > [attribute|=value]	用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。  
		 > [attribute^=value]	匹配属性值以指定值开头的每个元素。  
		 > [attribute$=value]	匹配属性值以指定值结尾的每个元素。  
		 > [attribute*=value]	匹配属性值中包含指定值的每个元素。  
* 创建CSS:
	* 外部样式表  
		
			<head>  
				<link rel="stylesheet" type="text/css" href="mystyle.css" />  
			</head>   
	* 内部样式表  
			
			<head>
				<style type="text/css">
				  hr {color: sienna;}
				  p {margin-left: 20px;}
				  body {background-image: url("images/back40.gif");}
				</style>
			</head>
	* 内联样式
		
			<p style="color: sienna; margin-left: 20px">
			This is a paragraph
			</p>
	* 多重样式(属性值被继承过来，内敛样式 > 内部样式 > 外部样式)
	

* 背景
	* 背景色: background-color属性
		
			p {background-color: gray; padding: 20px;}
	* 背景图像: background-image属性
			
			a.radio {background-image: url(/i/eg_bg_07.gif);}
	* 背景重复:background-repeat 属性

			body
			  { 
			  background-image: url(/i/eg_bg_03.gif);
			  background-repeat: repeat-y;
			  }
	* 背景定位:
		* 关键字：background-position: center|top|bottom|right|left
		* 百分数值:background-position: 50% 50%;
			> 图像的中心点和元素的中心点对齐
		* 长度值：backgournd-posiiton: 50px 50px
			> 图片左上角相对元素左上角偏移值
	* 背景关联:background-attachment:fixed(声明图像相对于可视区是固定的（fixed）)
		> 文档比较长，那么当文档向下滚动时，背景图像也会随之滚动  
		> background-attachment 属性的默认值是 scroll，也就是说，在默认的情况下，背景会随文档滚动。
* CSS 文本
	* 缩进文本(块级元素): text-indent: 5em;
		> 通过使用 text-indent 属性，所有元素的第一行都可以缩进一个给定的长度，甚至该长度可以是负值。  
		> 这个属性最常见的用途是将段落的首行缩进，下面的规则会使所有段落的首行缩进 5 em：
		> 如果想把一个行内元素的第一行“缩进”，可以用左内边距或外边距创造这种效果。
		> text-indent: 20%;（缩进父元素宽度的20%）
		> 继承：属性可以继承(子元素从父元素中继承这个属性)
	* 水平对齐: text-aligin:
		* center： 把文本排列到左边。默认值：由浏览器决定。
		* left ：把文本排列到右边。   
		* right ： 把文本排列到中间。
		* justify ： 实现两端对齐文本效果。 
		* inherit ： 规定应该从父元素继承 text-align 属性的值。 	
	* 字间隔：word-spacing，默认值 normal 与设置值为 0 是一样的
		> p.spread {word-spacing: 30px;}  
		> p.tight {word-spacing: -0.5em;}
	* 字母间隔:letter-spacing
		> h1 {letter-spacing: -0.5em}  
		h4 {letter-spacing: 20px}
	* 字符转换:text-transform:
		* none
		* uppercase
		* lowercase
		* capitalize : 每个单词的首字母大写
	* 文本装饰:text-decoration
		* none
		* underline : 下划线
		* overline ： 上划线
		* line-through ： 中划线
		* blink ：让文本闪烁
	* 处理空白符：white-space：normal|pre 
		* normal:合并空格、回车键，只留一个空格  
		* pre :浏览器不会合并空白符，也不会忽略换行符
		* nowrap：防止元素中的文本换行，除非使用一个br元素
		* pre-wrap：CSS2.1 引入，保留空白符序列，但是文本行会正常地换行。 
		* pre-line:CSS2.1 引入，合并空白符序列，但保留换行符。
	* 文本方向：direction
* [CSS 字体](http://www.w3school.com.cn/css/css_font.asp)
	* CSS 字体系列
	* 指定字体系列:font-family: sans-serif;
		* 使用通用字体系列
			> body {font-family: sans-serif;}
		* 指定字体系列
			> h1 {font-family: Georgia;}  
			> h1 {font-family: Georgia, serif;}
	* 字体风格:font-style
		* normal - 文本正常显示
		* italic - 文本斜体显示
		* oblique - 文本倾斜显示
	* 字体变形:font-variant
		* nomal
		* small-saps 
	* 字体加粗:font-weight
		* bold(700)
		* font-weight:100;
		* 关键字 100 ~ 900 为字体指定了 9 级加粗度；400 等价于 normal，而 700 等价于 bold
	* 字体大小：font-size值可以是绝对或相对值。
		* 绝对值  
		* 相对大小  
		* 使用像素来设置字体大小  
		* 使用 em 来设置字体大小
		* 结合使用百分比和 EM
			> body {font-size:100%;}   
			h1 {font-size:3.75em;}  
			h2 {font-size:2.5em;}  
			p {font-size:0.875em;}  
* CSS 链接
	* 链接的四种状态
		* a:link - 普通的、未被访问的链接
		* a:visited - 用户已访问的链接
		* a:hover - 鼠标指针位于链接的上方
		* a:active - 链接被点击的时刻
		>a:link {color:#FF0000;}		/* 未被访问的链接 */  
		a:visited {color:#00FF00;}	/* 已被访问的链接 */  
		a:hover {color:#FF00FF;}	/* 鼠标指针移动到链接上   */  
		a:active {color:#0000FF;}	/* 正在被点击的链接 */  
* 列表 
	* 列表类型：ist-style-type
		> ul.circle {list-style-type:circle;}  
		ul.square {list-style-type:square;}  
		ol.upper-roman {list-style-type:upper-roman;}  
		ol.lower-alpha {list-style-type:lower-alpha;}
	* 列表项图像:list-style-image		
		> ul li {list-style-image : url(xxx.gif)}
	* 列表标志位置:
		* inside: 列表项目标记放置在文本以内，且环绕文本根据标记对齐。
		* outside:默认值。保持标记位于文本的左侧。列表项目标记放置在文本以外，且环绕文本不根据标记对齐。
		* inherit:规定应该从父元素继承 list-style-position 属性的值。
	* 简写列表样式:将以上 3 个列表样式属性合并为一个方便的属性：list-style
		> li {list-style : url(example.gif) square inside}
* CSS 表格:
	* 表格边框: border 属性。
		> table, th, td  
		  {  
		  border: 1px solid blue;  
		  }
		> 表格具有双线条边框。这是由于 table、th 以及 td 元素都有独立的边框。 
	* 折叠边框:border-collapse 属性设置是否将表格边框折叠为单一边框：
		> table
		  {  
		  border-collapse:collapse;  
		  }  
		   
		> table,th, td  
		  {  
		  border: 1px solid black;  
		  }
		> 注释：如果没有规定 !DOCTYPE，border-collapse 属性可能会引起意想不到的错误。  
		>>  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
	* 表格宽度和高度:width,height
	* 表格文本对齐:
		* text-aligin:水平对齐
			* left、right、center
		* vertical-aligin:垂直对齐方式
			* top、bottom、center
	* 表格内边距:padding 
	* 表格颜色:backgroun-color(背景色)，color(文本颜色)
	* 设置分隔单元格边框的距离：border-spacing： 15px 20px
	* 设置表格标题的位置:caption-side
		* <caption style="caption-side:bottom">表格标题</caption>
	* 是否显示表格中的空单元格：empty-cells
		> table{
		> empty-cells:hide(show);
		> }
	* 单元、行、列的算法：table-layout
		> table{
		> table-layout:fixed(auto);
		> } 
* [轮廓（outline)](http://www.w3school.com.cn/css/css_outline.asp)

## CSS 框模型
* CSS 框模型 
	* 内边距
		* width 和 height 指的是内容区域的宽度和高度。增加内边距、边框和外边距不会影响内容区域的尺寸，但是会增加元素框的总尺寸。
		* 内边距：padding属性
			* 接受长度值或百分比值，但不允许使用负值。
			* padding-top
			* padding-right
			* padding-bottom
			* padding-left
	* 边框 ：border
		* 每个边框有 3 个方面：宽度、样式，以及颜色
		* 边框与背景
		* 边框的样式: border-style
		* 定义多种样式
			* p.aside {border-style: solid dotted dashed double;}
		* 定义单边样式
			* border-top-style
			* border-right-style
			* border-bottom-style
			* border-left-style
		* 边框的宽度:border-width 属性
			* 定长度值如：2px 或 0.1em
			* 关键字：thin 、medium（默认值） 和 thick。
			* 注释：CSS 没有定义 3 个关键字的具体宽度，所以一个用户代理可能把 thin 、medium 和 thick 分别设置为等于 5px、3px 和 2px，而另一个用户代理则分别设置为 3px、2px 和 1px。
				> 所以，我们可以这样设置边框的宽度：  
				>> p {border-style: solid; border-width: 5px;}
		* 定义单边宽度
			> p {border-style: solid; border-width: 15px 5px 15px 5px;}
			* border-top-width
			* border-right-width
			* border-bottom-width
			* border-left-width
		* 边框的颜色:border-color 属性，它一次可以接受最多 4 个颜色值。
			> p {  
			  border-style: solid;  
			  border-color: blue rgb(25%,35%,45%) #909090   red;  
			  }
			* border-top-color
			* border-right-color
			* border-bottom-color
			* border-left-color
		* 透明边框
			* CSS2 引入了边框颜色值 transparent。这个值用于创建有宽度的不可见边框
* [外边距](http://www.w3school.com.cn/css/css_margin.asp)
* 外边距合并

## CSS定位
* [display属性](http://www.w3school.com.cn/cssref/pr_class_display.asp)
	* none： 此元素不会被显示。
	* block：此元素将显示为块级元素，此元素前后会带有换行符。
	* inline：默认。此元素会被显示为内联元素，元素前后没有换行符。 
* CSS 定位机制
	* 普通流
		* 块级框:从上到下一个接一个地排列，框之间的垂直距离是由框的垂直外边距计算出来。
		* 行内框:在一行中水平布置.
			> 由一行形成的水平框称为行框（Line Box），行框的高度总是足以容纳它包含的所有行内框。不过，设置行高可以增加这个框的高度。
	* 浮动
	* 绝对定位
	* [position属性](http://www.w3school.com.cn/cssref/pr_class_position.asp):这个属性定义建立元素布局所用的定位机制
		* absolute:生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。
		元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。
			> h2  
			  {  
			  position:absolute;  
			  left:100px;  
			  top:150px;  
			  }
		* fixed:生成绝对定位的元素，相对于*浏览器窗口*进行定位。
		* [relative](CSS绝对定位absolute详解):生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。
		* static:默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。
		* inherit:规定应该从父元素继承 position 属性的值。
* 相对定位:如果对一个元素进行相对定位，它将出现在它所在的位置上。然后，可以通过设置垂直或水平位置，让这个元素“相对于”它的起点进行移动。		
* 