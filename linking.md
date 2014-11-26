# Linking #
在互联网中，资源通过IRI来标识。举个例子，一个位于http://example.com中名为`someDrawing.svg`的SVG文件可能会具有以下的IRI：

	http://example.com/someDrawing.svg

一个IRI可以通过其自身的IRI片段标识符来访问一个XML文档中的特定元素。一个包含片段标识符的IRI组成中包含了一个可选的位于“#”号字符后面的基础IRI。例如，下面的IRI可以用来指定位于someDrawing.svg中的一个ID为“Lamppost”的元素。

	http://example.com/someDrawing.svg#Lamppost

## 语法形式: IRI 和 FuncIRI ##

IRIs 被用在`xlink:href`属性中。一些属性同时允许IRI和文字字符串作为内容。为了从相对IRI中消除文字字符串，`<FuncIRI>`得到了应用。这是一个被限定为功能符的简单的IRI。**注意：**由于历史原因，其分隔符被设计为`url(` 何 `)`，以此来兼容CSS的规范。FuncIRI的一般用于[呈现属性](http://www.w3.org/TR/SVG/styling.html#StylingUsingPresentationAttributes)中

SVG广泛地将绝对和相对的IRI引用应用于其他元素中。举个例子，为了用线性渐变来填充一个矩形，你可以先定义一个`linearGradient`元素并赋予它一个ID。如下所示：

	<linearGradient xml:id="MyGradient">...</linearGradient>

然后将这个线性渐变引用到矩形的`fill`属性当中。

	<rect fill="url(#MyGradient)"/>

SVG 支持两种类型的IRI引用：

- [本地IRI引用](http://www.w3.org/TR/SVG/intro.html#TermLocalIRIReference)，指的是一个IRI引用中不包含绝对路径的IRI或相对路径的IRI。然后仅仅包含一个片段标识符（如，`#<elementID>` or `#xpointer(id<elementID>)`）
- [非本地IRI引用](http://www.w3.org/TR/SVG/intro.html#TermNonLocalIRIReference),一个包含了绝对或相对路径IRI的IRI引用。