# Document Structure #
一个SVG文档片段通过一个SVG元素包裹其子元素来构成。

SVG文档片段可以是很简单的，也可以是很复杂的。简单的SVG片段可以是只包含一个简单的图形元素，复杂的SVG片段则可能包含了许多的容器元素及图形元素。

## 分组：`<g>`元素 ##

**概述**

`<g>`元素是一个容器元素用来将一组相关的图形元素组织在一起。
分组构建SVG时，同时使用 `desc` 和 `title`元素，可以为文档建构和语义提供很好的信息。
示例：

	<?xml version="1.0" standalone="no"?>
	<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
	  "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
	<svg xmlns="http://www.w3.org/2000/svg"
	     version="1.1" width="5cm" height="5cm">
	  <desc>Two groups, each of two rectangles</desc>
	  <g id="group1" fill="red">
	    <rect x="1cm" y="1cm" width="1cm" height="1cm"/>
	    <rect x="3cm" y="1cm" width="1cm" height="1cm"/>
	  </g>
	  <g id="group2" fill="blue">
	    <rect x="1cm" y="3cm" width="1cm" height="1cm"/>
	    <rect x="3cm" y="3cm" width="1cm" height="1cm"/>
	  </g>
	
	  <!-- Show outline of canvas using 'rect' element -->
	  <rect x=".01cm" y=".01cm" width="4.98cm" height="4.98cm"
	        fill="none" stroke="blue" stroke-width=".02cm"/>
	</svg>

一个`<g>`元素可以包含其他的`<g>`元素在里面。因此，下面的代码也是可行的：

	<?xml version="1.0" standalone="no"?>
	<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
	  "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
	<svg xmlns="http://www.w3.org/2000/svg"
	     version="1.1" width="4in" height="3in">
	  <desc>Groups can nest</desc>
	  <g>
	     <g>
	       <g>
	       </g>
	     </g>
	   </g>
	</svg>

## 定义可重用的内容：`<defs>`元素 ##

**概述**

SVG允许定义在预留的可重用的图形元素。它是通过IRI引用来访问这些元素的。举个例子，为了用线性渐变来填充一个矩形，你可以先定义一个`linearGradient`元素并赋予它一个ID。如下所示：

	<linearGradient xml:id="MyGradient">...</linearGradient>

然后将这个线性渐变引用到矩形的`fill`属性当中。

	<rect fill="url(#MyGradient)"/>

某些类型的元素，例如渐变，它本身并不会产生一个图形。它能被方便地放到任何的地方。然而，有时候我们定义一个元素并不是希望直接地将它渲染出来，而是想在需要的地方才将其渲染。基于这个目的，SVG为我们提供了`<defs>`元素，它允许我们预定义一些分组内容。

我们推荐的是，所有引用元素都应该被定义在`<defs>`元素里面。总是被引用的元素包括`<altGlyphDef>`, `<clipPath>`, `<cursor>`, `<filter>`, `<linearGradient>`, `<marker>`, `<mask>`, `<pattern>`, `<radialGradient>` 和 `<symbol>`。这样做可以增加SVG内容的易读性和可访问性。

`<defs>`元素可包含的内容跟`<g>`元素是相同的。

而在`<defs>`中的子元素不会直接地渲染因为他们的`display`属性被设为了`none`，所以它们不会出现在渲染树中。

	<?xml version="1.0" standalone="no"?>
	<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
	<svg width="8cm" height="3cm"
	     xmlns="http://www.w3.org/2000/svg" version="1.1">
	  <desc>Local URI references within ancestor's 'defs' element.</desc>
	  <defs>
	    <linearGradient id="Gradient01">
	      <stop offset="20%" stop-color="#39F" />
	      <stop offset="90%" stop-color="#F3F" />
	    </linearGradient>
	  </defs>
	  <rect x="1cm" y="1cm" width="6cm" height="1cm" 
	        fill="url(#Gradient01)"  />
	
	  <!-- Show outline of canvas using 'rect' element -->
	  <rect x=".01cm" y=".01cm" width="7.98cm" height="2.98cm"
	        fill="none" stroke="blue" stroke-width=".02cm" />
	</svg>

## `<desc>` and `<title>` 元素 ##

每一个容器元素和图形元素都可以为其提供一个`desc`或者`title`元素来作为元素的描述。当SVG片段以视觉媒体的形式出现时，`desc`或者`title`元素并不会被渲染出来。但当指针移动到该元素上面时，浏览器可能会将`title`元素显示为一个气泡悬浮框。

为了遵从文档片段的规范，`title`应该是其父元素的第一个子元素。

下面是一个示例：

	<?xml version="1.0" standalone="no"?>
	<!DOCTYPE svg SYSTEM "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
	<svg xmlns="http://www.w3.org/2000/svg"
	     version="1.1" width="4in" height="3in">
	  <g>
	    <title>Company sales by region</title>
	    <desc>
	      This is a bar chart which shows 
	      company sales by region.
	    </desc>
	    <!-- Bar chart defined as vector data -->
	  </g>
	</svg>

## `<symbol>` 元素 ##

`symbol`元素用于定义一个可通过`use`元素来实例化的图形模板对象。`symbol`元素可为同一个文档中多次使用到的图形增加结构和语义。

`symbol`元素和`g`元素的根本区别：

- `symbol`元素自身并不会渲染，但`symbol`元素的实例会被渲染。
- `symbol`元素可设置`viewBox` 和 `preserveAspectRatio`属性，使得`symbol`元素可通过缩放来适配一个`use`元素引用的矩形视窗。

`symbol`元素永远不会直接地被渲染，即使你将其`display`属性设置为`none`以外的值。

## `<use>` 元素 ##

与`image`元素不同`use`元素不能够引用整一个文件。

`use`元素具有这几个可选元素`x`, `y`, `width` 和 `height`

如果`use`元素引用了一个`symbol`元素：

在生成的内容当中，`use`会被`g`替换，`use`上除了`x`, `y`, `width`， `height` 和 `xlink:href`以外的所有属性都会被转移到生成的`g`元素中。
