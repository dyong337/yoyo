##CSS
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
			* 
		* 相对大小

https://www.jianshu.com/p/aaef5ceb3936