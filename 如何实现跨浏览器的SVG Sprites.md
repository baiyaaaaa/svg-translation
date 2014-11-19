# 如何实现跨浏览器的SVG Sprites #

> 原文链接：[http://webdesign.tutsplus.com/tutorials/how-to-implement-cross-browser-svg-sprites--cms-22427](http://webdesign.tutsplus.com/tutorials/how-to-implement-cross-browser-svg-sprites--cms-22427)

In this tutorial I’m going to demonstrate a basic implementation of some SVG icons, how to provide a fallback, and how to turn them into an SVG sprite.

在这篇教程中我会演示一些SVG图标的基础实现、如何提供兼容，以及如何将它们转换成SVG sprite。

## 基础的SVG实现 ##

For the purpose of this tutorial I’m going to be using a single page, which will act as a kind of online business card. It will briefly introduce me and display three network profiles relevant to my work.

基于本文的目的，我会以一个像个人名片的东西来开始。它会简短地介绍一下我自己以及显示3个和我工作相关的网络档案。

![](dave.png)

From the screenshot above you can see that I’m using icons (for Twitter, Dribbble and GitHub) to symbolically reference my network profiles. I downloaded these icons from flaticon, which has a wide range of icons & symbols in both vector and raster formats. 

从上面的截图你可以看到我使用了三个图标（Twitter，Dribble 和 Github）象征着我的网络档案。这些图标我是从 flaticon 下载到的，这是一个具有各种不同图标和符号的网站，并且每个图标都提供矢量和光栅格式。

### PNG 和 SVG ###

We’re going to begin by using the PNG versions of these icons, for the sake of backward compatibility, then we’ll prepare the SVG versions to use in supporting browsers.

我们会在支持SVG的浏览器中使用SVG的格式，然后使用PNG格式的图标来实现向后兼容。

I used Sketch to output my PNG icons, so I’m going to use it again to prepare my icons for SVG usage.

我使用Sketch来输出我的PNG图标，另外我还会再使用它来输出SVG格式的图标。

![](sketch-screenshot.png)

If you look at the screenshot above you’ll notice that I’ve named all my groups and shapes in the left hand panel appropriately (Adobe Illustrator has a similar view in the Layers panel). It’s important to name all your assets correctly, not only to help you remain organised but also for what we’ll be using them for later in this tutorial. 

在上面的截图中你会注意到我将分组和图形都在左侧面板进行了适当的命名。（Adobe Illustrator在图层面板中有个相似的视图）。将资源正确地命名是很重要的，不仅仅让它们保持组织性更加为了我们后面的使用。

### 输出SVG ###

Now I’ll export the icons as SVGs, which is straightforward with the slicing tool in Sketch. For more information on how this works take a look at Understanding Sketch’s Export Options. I’ll be exporting them as separate files and placing them into the images directory of my project.

现在我会将这些图标输出为SVG，我们可以用Sketch的裁剪工具来轻松地完成这项工作。在Sketch的输出选项中你可以得到更多的信息从而明白它是怎么实现的。我会将它们输出为单独的文件并放置在我项目中的images目录中。

Normally, to show an image on your site you’d reference the asset with a src attributed element or something similar: 

通常地，你要在网站中展示一张图片你需要通过一个元素的src属性中来引入，类似下面这样：

    <img src="path-to-my-image.png" alt="" />

However with SVGs there are a number of different ways we can use them within an HTML document. For example, we can use the actual SVG code inline - here’s what that code might look like:

然而，对于SVG来说我们可以有几种不同的方法来在HTML文档中使用它们。举个例子，我们可以使用直观的SVG代码来描述一张图片。代码可能会是这样：

	<?xml version="1.0" encoding="UTF-8" standalone="no"?>
	<svg width="50px" height="41px" viewBox="0 0 50 41" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns">
	    <!-- Generator: Sketch 3.1 (8751) - http://www.bohemiancoding.com/sketch -->
	    <title>twitter-icon</title>
	    <desc>Created with Sketch.</desc>
	    <defs></defs>
	    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
	        <g id="twitter-icon" sketch:type="MSLayerGroup" fill="#55ACEE">
	            <path d="M0,36.3461306 C0.803663004,36.4417973 1.62142857,36.4907387 2.45054945,36.4907387 C7.26336996,36.4907387 11.6928571,34.8346712 15.2086081,32.0564595 C10.71337,31.9727973 6.91959707,28.9779505 5.61245421,24.8624369 C6.23956044,24.9834054 6.88315018,25.0482297 7.54505495,25.0482297 C8.48205128,25.0482297 9.38956044,24.9217207 10.2516484,24.684955 C5.55201465,23.7334595 2.01117216,19.5466577 2.01117216,14.5276667 C2.01117216,14.4840811 2.01117216,14.4406802 2.01190476,14.397464 C3.3970696,15.1733243 4.98095238,15.6392838 6.66501832,15.693027 C3.90860806,13.8354685 2.09487179,10.6648018 2.09487179,7.07102252 C2.09487179,5.17264865 2.6014652,3.39321171 3.48571429,1.86328378 C8.55238095,8.13037387 16.1217949,12.2543829 24.6595238,12.6863604 C24.4844322,11.9282297 24.3934066,11.1375946 24.3934066,10.3257207 C24.3934066,4.60511261 28.9930403,-0.0328738739 34.6664835,-0.0328738739 C37.6210623,-0.0328738739 40.2908425,1.2251982 42.1648352,3.23844595 C44.5047619,2.77377928 46.7032967,1.91167117 48.6880952,0.724702703 C47.9210623,3.14351802 46.2923077,5.17357207 44.1712454,6.45565315 C46.2492674,6.20522072 48.2291209,5.6483964 50.0714286,4.82451802 C48.6941392,6.90185135 46.952381,8.72635135 44.9454212,10.1868378 C44.9652015,10.6310045 44.9750916,11.0777568 44.9750916,11.5269099 C44.9750916,25.2155541 34.6424908,41 15.7472527,41 C9.9459707,41 4.54615385,39.2852027 0,36.3461306 L0,36.3461306 Z" id="bird" sketch:type="MSShapeGroup"></path>
	        </g>
	    </g>
	</svg>

This is one of the icons I exported, in XML format. This code is pretty much just like HTML (it’s a structural format) which means we can slot this straight into the page. 

这是我上面输出的其中一个图标，基于XML的格式的呈现。这些代码几乎就像一段HTML一样，这意味着我们可以插入这段代码到页面中。

### 在HTML中添加inline SVG ###

Let’s begin with the base HTML page which includes the PNG icons with their anchors, and a container:

让我们以一个基础的HTML页面开始，里面包含了3个赋予了链接的PNG图标，以及它们的容器：

	<div class="section">
	    <a href="http://twitter.com/DavidDarnes" title="Twitter profile">
	        <img alt="Twitter" width="50" height="51" src="img/twitter-icon.png">
	    </a>
	    <a href="http://dribbble.com/DavidDarnes" title="Dribbble profile">
	        <img alt="Dribbble" width="50" height="51" src="img/dribbble-icon.png">
	    </a>
	    <a href="http://github.com/DavidDarnes" title="GitHub profile">
	        <img alt="GitHub" width="50" height="51" src="img/github-icon.png">
	    </a>
	</div>

Now I’m going to copy and paste the SVG code, however I’m going to ignore the top line which refers to the file’s character encoding and other file attribute details. The HTML document contains that information already so we needn’t duplicate it.

现在我会开始复制上面SVG图标代码并黏贴到这里面，但我会忽略这段`<?xml version="1.0" encoding="UTF-8" standalone="no"?>`说明文件编码方式和其他信息的代码。因为在HTML文档中已经包含了这部分的信息，我们无需复制进去。

	<div class="section">
	    <a href="http://twitter.com/DavidDarnes" title="Twitter profile">
	    	<svg width="50px" height="41px" viewBox="0 0 50 41" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns">
		        <!-- Generator: Sketch 3.1 (8751) - http://www.bohemiancoding.com/sketch -->
		        <title>twitter-icon</title>
		        <desc>Created with Sketch.</desc>
		        <defs></defs>
		        <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
		            <g id="twitter-icon" sketch:type="MSLayerGroup" fill="#55ACEE">
		                <path d="M0,36.3461306 C0.803663004,36.4417973 1.62142857,36.4907387 2.45054945,36.4907387 C7.26336996,36.4907387 11.6928571,34.8346712 15.2086081,32.0564595 C10.71337,31.9727973 6.91959707,28.9779505 5.61245421,24.8624369 C6.23956044,24.9834054 6.88315018,25.0482297 7.54505495,25.0482297 C8.48205128,25.0482297 9.38956044,24.9217207 10.2516484,24.684955 C5.55201465,23.7334595 2.01117216,19.5466577 2.01117216,14.5276667 C2.01117216,14.4840811 2.01117216,14.4406802 2.01190476,14.397464 C3.3970696,15.1733243 4.98095238,15.6392838 6.66501832,15.693027 C3.90860806,13.8354685 2.09487179,10.6648018 2.09487179,7.07102252 C2.09487179,5.17264865 2.6014652,3.39321171 3.48571429,1.86328378 C8.55238095,8.13037387 16.1217949,12.2543829 24.6595238,12.6863604 C24.4844322,11.9282297 24.3934066,11.1375946 24.3934066,10.3257207 C24.3934066,4.60511261 28.9930403,-0.0328738739 34.6664835,-0.0328738739 C37.6210623,-0.0328738739 40.2908425,1.2251982 42.1648352,3.23844595 C44.5047619,2.77377928 46.7032967,1.91167117 48.6880952,0.724702703 C47.9210623,3.14351802 46.2923077,5.17357207 44.1712454,6.45565315 C46.2492674,6.20522072 48.2291209,5.6483964 50.0714286,4.82451802 C48.6941392,6.90185135 46.952381,8.72635135 44.9454212,10.1868378 C44.9652015,10.6310045 44.9750916,11.0777568 44.9750916,11.5269099 C44.9750916,25.2155541 34.6424908,41 15.7472527,41 C9.9459707,41 4.54615385,39.2852027 0,36.3461306 L0,36.3461306 Z" id="bird" sketch:type="MSShapeGroup"></path>
		            </g>
		        </g>
	        </svg>
	        <img alt="Twitter" width="50" height="51" src="img/twitter-icon.png">
	    </a>
	    <a href="http://dribbble.com/DavidDarnes" title="Dribbble profile">
	        <img alt="Dribbble" width="50" height="51" src="img/dribbble-icon.png">
	    </a>
	    <a href="http://github.com/DavidDarnes" title="GitHub profile">
	        <img alt="GitHub" width="50" height="51" src="img/github-icon.png">
	    </a>
	</div>

I’ve placed the SVG right above the corresponding PNG icon within the HTML page. For the time being I’m going to wrap the regular PNG image line in a comment tag to stop it appearing next to the SVG version. 

在这个HTML页面中，我已经将SVG放在了PNG图标的正上方。现在我要把PNG图片的代码注释掉防止它再SVG图片后面再出现一次。

### 清理 SVG ###

I’m also going to clean up the code within my SVG. Removing the element attributes is optional as most of the pieces I’m removing won’t change how the SVG will act. Here is a before and after if you wish to do the same with yours:

接着我准备清理一下上面的SVG代码。移除掉那些可选的元素属性因为我要移除的这些属性并不会影响SVG的表现。下面是优化后跟优化前的代码对比，但他们表现效果是一样的：

	<svg width="50px" height="41px" viewBox="0 0 50 41" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:sketch="http://www.bohemiancoding.com/sketch/ns">
	    <!-- Generator: Sketch 3.1 (8751) - http://www.bohemiancoding.com/sketch -->
	    <title>twitter-icon</title>
	    <desc>Created with Sketch.</desc>
	    <defs></defs>
	    <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd" sketch:type="MSPage">
	        <g id="twitter-icon" sketch:type="MSLayerGroup" fill="#55ACEE">
	            <path d="M0,36.3461306 C0.803663004,36.4417973 1.62142857,36.4907387 2.45054945,36.4907387 C7.26336996,36.4907387 11.6928571,34.8346712 15.2086081,32.0564595 C10.71337,31.9727973 6.91959707,28.9779505 5.61245421,24.8624369 C6.23956044,24.9834054 6.88315018,25.0482297 7.54505495,25.0482297 C8.48205128,25.0482297 9.38956044,24.9217207 10.2516484,24.684955 C5.55201465,23.7334595 2.01117216,19.5466577 2.01117216,14.5276667 C2.01117216,14.4840811 2.01117216,14.4406802 2.01190476,14.397464 C3.3970696,15.1733243 4.98095238,15.6392838 6.66501832,15.693027 C3.90860806,13.8354685 2.09487179,10.6648018 2.09487179,7.07102252 C2.09487179,5.17264865 2.6014652,3.39321171 3.48571429,1.86328378 C8.55238095,8.13037387 16.1217949,12.2543829 24.6595238,12.6863604 C24.4844322,11.9282297 24.3934066,11.1375946 24.3934066,10.3257207 C24.3934066,4.60511261 28.9930403,-0.0328738739 34.6664835,-0.0328738739 C37.6210623,-0.0328738739 40.2908425,1.2251982 42.1648352,3.23844595 C44.5047619,2.77377928 46.7032967,1.91167117 48.6880952,0.724702703 C47.9210623,3.14351802 46.2923077,5.17357207 44.1712454,6.45565315 C46.2492674,6.20522072 48.2291209,5.6483964 50.0714286,4.82451802 C48.6941392,6.90185135 46.952381,8.72635135 44.9454212,10.1868378 C44.9652015,10.6310045 44.9750916,11.0777568 44.9750916,11.5269099 C44.9750916,25.2155541 34.6424908,41 15.7472527,41 C9.9459707,41 4.54615385,39.2852027 0,36.3461306 L0,36.3461306 Z" id="bird" sketch:type="MSShapeGroup"></path>
	        </g>
	    </g>
	</svg>

----------

	<svg width="50px" height="41px" viewBox="0 0 50 41" version="1.1" xmlns="http://www.w3.org/2000/svg">
	    <g id="twitter-icon" fill="#55ACEE">
	        <path d="M0,36.3461306 C0.803663004,36.4417973 1.62142857,36.4907387 2.45054945,36.4907387 C7.26336996,36.4907387 11.6928571,34.8346712 15.2086081,32.0564595 C10.71337,31.9727973 6.91959707,28.9779505 5.61245421,24.8624369 C6.23956044,24.9834054 6.88315018,25.0482297 7.54505495,25.0482297 C8.48205128,25.0482297 9.38956044,24.9217207 10.2516484,24.684955 C5.55201465,23.7334595 2.01117216,19.5466577 2.01117216,14.5276667 C2.01117216,14.4840811 2.01117216,14.4406802 2.01190476,14.397464 C3.3970696,15.1733243 4.98095238,15.6392838 6.66501832,15.693027 C3.90860806,13.8354685 2.09487179,10.6648018 2.09487179,7.07102252 C2.09487179,5.17264865 2.6014652,3.39321171 3.48571429,1.86328378 C8.55238095,8.13037387 16.1217949,12.2543829 24.6595238,12.6863604 C24.4844322,11.9282297 24.3934066,11.1375946 24.3934066,10.3257207 C24.3934066,4.60511261 28.9930403,-0.0328738739 34.6664835,-0.0328738739 C37.6210623,-0.0328738739 40.2908425,1.2251982 42.1648352,3.23844595 C44.5047619,2.77377928 46.7032967,1.91167117 48.6880952,0.724702703 C47.9210623,3.14351802 46.2923077,5.17357207 44.1712454,6.45565315 C46.2492674,6.20522072 48.2291209,5.6483964 50.0714286,4.82451802 C48.6941392,6.90185135 46.952381,8.72635135 44.9454212,10.1868378 C44.9652015,10.6310045 44.9750916,11.0777568 44.9750916,11.5269099 C44.9750916,25.2155541 34.6424908,41 15.7472527,41 C9.9459707,41 4.54615385,39.2852027 0,36.3461306 L0,36.3461306 Z" id="bird"></path>
	    </g>
	</svg>

Take note of the elements I’ve removed. The <title>, <desc>, and <defs> elements aren’t needed now, but we may need them later on in this tutorial. There are also a few <g> elements which refer to groups, and correspond to the groups created in my Sketch document. By default Sketch places everything inside a page, hence the group element <g id=”Page-1”… . You can remove this as it doesn’t have a use for us (the group within it is more important). Sketch does provide an option to produce cleaner SVGs upon exporting, however there is no harm in cleaning the code up yourself.

注意我移除的那些元素。 `<title>`, `<desc>`, 和 `<defs>`元素目前是不需要的，但在本文后面我们可能会用到它们。其中代表着分组的`<g>`元素相当于我在Sketch文档中的分组。默认地Sketch是将所有的东西放在一个页面中的，相当于组元素`<g id=”Page-1”…`。你可以把这个元素移除掉因为它对我们来说没有什么作用（在它里面的组元素才是重要的）。Sketch提供了一个选项让我们在输出之前处理SVG的清理工作，但你自己来清理一遍也没多大问题。

The final part of this step is to remove the height and width attributes within the SVG element itself. These will need to be compensated for in my CSS file, as shown below:

这部分的最后一步就是移除掉SVG标签上的`height`和`width`属性。它们会在我的CSS文件中来定义，如下所示：

	<svg viewBox="0 0 50 41" version="1.1" xmlns="http://www.w3.org/2000/svg">
	    <g id="twitter-icon" fill="#55ACEE">
	        <path d="M0,36.3461306 C0.803663004,36.4417973 1.62142857,36.4907387 2.45054945,36.4907387 C7.26336996,36.4907387 11.6928571,34.8346712 15.2086081,32.0564595 C10.71337,31.9727973 6.91959707,28.9779505 5.61245421,24.8624369 C6.23956044,24.9834054 6.88315018,25.0482297 7.54505495,25.0482297 C8.48205128,25.0482297 9.38956044,24.9217207 10.2516484,24.684955 C5.55201465,23.7334595 2.01117216,19.5466577 2.01117216,14.5276667 C2.01117216,14.4840811 2.01117216,14.4406802 2.01190476,14.397464 C3.3970696,15.1733243 4.98095238,15.6392838 6.66501832,15.693027 C3.90860806,13.8354685 2.09487179,10.6648018 2.09487179,7.07102252 C2.09487179,5.17264865 2.6014652,3.39321171 3.48571429,1.86328378 C8.55238095,8.13037387 16.1217949,12.2543829 24.6595238,12.6863604 C24.4844322,11.9282297 24.3934066,11.1375946 24.3934066,10.3257207 C24.3934066,4.60511261 28.9930403,-0.0328738739 34.6664835,-0.0328738739 C37.6210623,-0.0328738739 40.2908425,1.2251982 42.1648352,3.23844595 C44.5047619,2.77377928 46.7032967,1.91167117 48.6880952,0.724702703 C47.9210623,3.14351802 46.2923077,5.17357207 44.1712454,6.45565315 C46.2492674,6.20522072 48.2291209,5.6483964 50.0714286,4.82451802 C48.6941392,6.90185135 46.952381,8.72635135 44.9454212,10.1868378 C44.9652015,10.6310045 44.9750916,11.0777568 44.9750916,11.5269099 C44.9750916,25.2155541 34.6424908,41 15.7472527,41 C9.9459707,41 4.54615385,39.2852027 0,36.3461306 L0,36.3461306 Z" id="bird"></path>
	    </g>
	</svg>

----------
	.icon {
	    max-width: 40px;
	    max-height: 40px;
	    transition: .2s;
	    -webkit-filter: drop-shadow(0 1px 0 #11222d);
	}

If you’ve followed my steps you should be able to see in the browser a sharp and clean vector version of your graphics. 

如果你跟着我的步骤你应该能在浏览器看到一个简洁锐利的矢量图。

Tip: Check if the graphic is actually an SVG by zooming in Command-+ when viewing it in the browser. The graphic should stay sharp no matter how far you zoom in.

提示：你可以通过浏览器的放大缩小来看看这个图片是否为SVG。这个图片不应该会受到你浏览器放大缩小而产生变化。