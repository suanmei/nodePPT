title: 移动端适配方案
speaker: 李宇
url: https://github.com/ksky521/nodePPT
transition: slide
files: /js/demo.js,/css/demo.css,/js/zoom.js
theme: dark
usemathjax: yes


[slide]
# 移动端适配方案
----

<a href="https://suanmei.github.io"><i class="fa fa-github" aria-hidden="true"></i></a>
<a href="https://www.zhihu.com/people/li-ruo-yu-34/activities" class="font-set">知乎</a>

<style>
.font-set {
  font-size: 20px;
}
.iphone-img {
	
	width: 400px;
	height: 280px;
}
.viewport-img {
	width: 450px;
	height: 300px;
}
</style>


[slide]
# 前言

* 什么是**适配**？ {:&.rollIn}
	* 我们拿到设计师的图之后，需要根据设计图让页面在各种手机上**良好得**呈现出来，这个过程叫做**适配** {:&.rollIn}

* **适配对象**是什么？
	* 不同**屏幕尺寸**的手机 {:&.rollIn}
	* 不同**分辨率**的手机


[slide]
# 一.背景
* 如今主流手机屏幕的像素点数已经远远超过了桌面显示器的像素数量，5.5英寸1920x1080P的手机与一个21英寸1920x1080P的显示器相比，同等面积下，手机的像素点更密集，可想而知，在手机屏幕上一个像素点是非常小的。 {:&.rollIn}

* 那么在CSS中设置`font-size:12px`，如果“手机屏幕物理像素：CSS像素”=“1：1”，那么PC上正常展示出来的文字在手机上你可能需要放大镜才能看清，但为什么如今的手机屏幕依然能清晰的显示？


[slide]
# 二.基本概念


[slide]
## 1.像素(Pixel)
* 中文全称 **图像元素** 。每个像素通常被视为图像的最小的完整 **取样** ，这里的图像包括显示器显示出的图片或应用程序画面、打印机输出的画面、投影仪投射的画面。 {:&.rollIn}

* 每个图像的 **像素** 通常对应于二维空间中一个特定的‘**位置**’，并且有一个或多个与那个点有关的采样值组成数值，它描述的是图像在某一点的 **颜色值** 。所以 **像素** 是抽象的，它也没有一个固定的宽高。


[slide]
## 2.物理像素(PX)
* 又称**设备像素**。显示屏就是由一个个物理像素点组成的，通过控制每个像素点的颜色，使屏幕显示出不同的图像。它是显示设备中一个最微小的物理部件，每个像素可以根据操作系统设置自己的颜色和亮度。 {:&.rollIn}


[slide]
## 3.分辨率
* **分辨率** 泛指显示系统对细节的分辨能力。能显示图像都能叫显示系统，比如显示器，投影仪，照片。 {:&.rollIn}
 
* **分辨率** 常用的单位有：**dpi**（点每英寸）、**lpi**（线每英寸）和 **ppi**（像素每英寸）。从单位来看，分辨率是一个比值，与物理单位的比值。

* 另外，**ppi** 和 **dpi** 经常都会出现混用现象。但是他们所用的领域也存在区别。从技术角度说，“像素”只存在于电脑显示领域，而“点”只出现于打印或印刷领域。


[slide]

* 日常所说的“这张图片的尺寸（或分辨率）是100x100像素”，一般都是在描述数字图片，这样的描述只是说明了图片文件包含多少个像素，或者在数字系统中的尺寸。比如图1中的七张图，我们习惯于说，第1张图的分辨率是1x1像素，第4张图的分辨率是10x10像素，其实只是说明了图片的像素数而已。

* ![不同解像度的图像的差别](/img/picture_pixel.png '不同解像度的图像的差别')


[slide]
[magic data-transition="newspaper"]
## 像素密度（PPI）
------
* **PPI** 全称是 pixel per inch，就是每英寸内有多少个像素点，当用在手机屏幕上的时候，这个像素点指的是设备像素点（物理像素）。
$$ PPI = {\sqrt{横向^2(Pixel) + 纵向^2(Pixel)} \over 屏幕尺寸(inch)} $$

========
![iphone各型号分辨率](/img/PPI-iphone.png 'iphone各型号分辨率')

[【点我】查看主流手机分辨率](http://screensiz.es/)
[/magic]


[slide]
## 4.CSS像素
* **CSS像素** 是Web编程的概念，指的是 **CSS** 样式代码中使用的逻辑像素。

* 按照 **CSS** 规范的定义，**CSS** 中的 **px** 是一个相对长度，它相对的，是viewing device的分辨率。


[slide]
## 5.设备独立像素(DIP)
> 又称**密度无关像素**，在定义 UI 布局时应使用的虚拟像素单位，用于以密度无关方式表示布局维度 或位置。    
**设备独立像素**等于 160 ppi 屏幕上的一个物理像素。在运行时，系统 根据使用中屏幕的实际密度按需要以透明方式处理 dp 单位的任何缩放 。dp 单位转换为屏幕像素很简单： px = dp * (ppi / 160)。 例如，在 240 ppi 屏幕上，1 dp 等于 1.5 物理像素。在定义应用的 UI 时应始终使用 dp 单位 ，以确保在不同密度的屏幕上正常显示 UI。

* DIP的概念是安卓提出来的，上面也是引用的安卓官方文档的定义，里面提及的*应用的 UI 应使用 dp 单位* 是指**安卓开发时**使用的长度单位应是 dp 。 {:&.rollIn}


[slide]
## 6.设备像素比(DPR)
* **设备像素比**定义了物理像素和设备独立像素的对应关系。它的值可以按下面的公式计算得到:      {:&.rollIn}

    > 设备像素比 = 设备像素 / 设备独立像素
* $$ dpr = {PX \over DIP} $$
* dpr 可以通过 `window.devicePixelRatio` 来获取


[slide]
## 思考<i class="fa fa-exclamation-triangle"></i>
<p class="text-left">通过前面的几个概念我们得到了这样两个公式：</p>
$$ dpr = {PX \over DIP} $$
$$ PX = {DIP \cdot {PPI \over 160}} $$
<p class="text-left">我们可以通过他们导出这么一个公式:</p>
$$ dpr = {PPI \over 160} $$

* 这是 **android** ，那 ios 呢？ {:&.rollIn}


[slide]
## 7.Retina工作原理
* What's **Retina** ? {:&.rollIn}
	* 是一种显示技术，可以将把更多的像素点压缩至一块屏幕里，从而达到更高的分辨率并提高屏幕显示的细腻程度，这种分辨率在正常观看距离下足以使人肉眼无法分辨其中的单独像素。
 
* <img src="/img/iPhone_3GS.jpg" class="iphone-img" title="iPhone 3GS">
<img src="/img/iPhone_4.jpg" class="iphone-img" title="iPhone 4">


[slide]

* How does **Retina** work ?
	* 以 **第三代 MacBook Pro with Retina Display** 为例，工作时显卡渲染出的 `2880x1880` 个像素每四个一组，输出原来屏幕的一个像素显示的大小区域内的图像。这样一来，用户所看到的图标与文字的大小与原来的 `1440x900` 分辨率显示屏相同，但精细度是原来的 `4` 倍。但对于特殊元素，如视频与图像，则以一个图片像素对应一个屏幕像素的方式显示。 {:&.rollIn}

	
[slide]
## 思考<i class="fa fa-exclamation-triangle"></i>
* 在windows中，我们调整了显示分辨率，比如从 800 \* 600 调整到 1024 \* 768 时，屏幕的文字图标会变小，为什么 mac 的不会？

* 答案：<span class="red3"> HiDPI <span class="red3"> {:&.rollIn}

* !["文"第一笔的渲染效果对比](/img/HiDIP.jpg '"文"第一笔的渲染效果对比') {:&.rollIn}


[slide]
## 思考<i class="fa fa-exclamation-triangle"></i>
* 为什么 iphone6 Plus dpr 为 `3 != 1080/414`？

* ![对比图](/img/iphone6plus_compare.jpg '对比图') {:&.rollIn}

* b方案：iPhone 6 Plus的逻辑pt分辨率比 iPhone 6 的低，显示内容会少 {:&.rollIn}

* c方案：所有 iOS UI 元素尺寸在屏幕上的实际物理面积一下子会变小   {:&.rollIn}

* a方案：苹果遇到了一些问题难以实现它。  {:&.rollIn}


[slide]
# 三.viewport


[slide]
## 1.视觉视窗
* 所谓的 **视觉视窗** 说白了就是设备的 **屏幕区域** ，换句话说就是用户通过屏幕所看到的页面内容。但它所对应的并不是指屏幕区域里的物理像素，而是CSS 像素。并且它所包含的 CSS 像素的数量也是随着用户缩放而有所改变。 {:&.rollIn}

* <img src="/img/meta-viewport-usage-1.jpg" class="viewport-img" title="视觉视窗">


[slide]
## 2.布局视窗
* **布局视窗** 通常比设备屏幕宽得多，一般为980px，但也不是唯一，在不同的浏览器中也会有所不同如：在Safari iPhone中布局视窗的宽为980px，在Opera中布局视窗宽为850px ，在Android WebKit 中视窗宽为800px，而在万恶的IE中布局视窗宽为974px。说了一堆，这个而已视频到底是个什么玩意呢？我们来看一个图我想你就应该明白了。 {:&.rollIn}

* <img src="/img/meta-viewport-usage-2.jpg" class="viewport-img" title="布局视窗">


[slide]
## 3.关于viewport我们聊点啥

* **布局视窗** 就是我们的页面，**视觉视窗** 就是我们的手机屏幕。 {:&.rollIn}
* 类比一下，**布局视窗** 就是墙上的一个洞，**布局视窗** 就是一张很大的报纸，我们需要透过这个洞看报纸。
* 手机默认做了一件事，就是把报纸拿的很远，这样我们正好能够一眼看见整张报纸（相当于缩放）。
* 但是这样会带来一个问题，字太小了，看不清楚，我们就需要把报纸凑近（放大），每次透过洞看报纸的一部分，要想看完整张报纸，就需要来回移动报纸（手指滑动页面）。

[slide]

* 如何设置才能让页面按照最佳方式展示以便查看？ {:&.rollIn}
* `<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">`
* [针对 *viewport* 各属性的 demo（掏出手机一起搞事情）](https://andreasbovens.github.io/understanding-viewport/)


[slide]
# 四.适配方案


[slide]
[magic data-transition="horizontal"]
## 1.高度固定，宽度自适应
* 这种方法关键在于容器元素高度使用定值，宽度去伸缩变换。容器元素内关键元素高宽和位置都不变。
* 偶尔配合一下媒体查询。
* CSS单位使用 **px** 。

========
<img src="/img/lagou_iphone4.jpeg" class="lagou-img" title="拉钩在iphone4下" width="213px" height="367px">
<p>iPhone4下</p>

========
<img src="/img/lagou_iphone6.jpeg" class="lagou-img" title="拉钩在iphone6下" width="251px" height="497px">
<p>iPhone6下</p>

========
<img src="/img/lagou_ipad.jpeg" class="lagou-img" title="拉钩在ipad下" width="490px" height="520px">
<p>iPad下</p>
[/magic]


[slide]

* 对于这类app，记住一个开发原则就好：**文字流式**，**控件弹性**，**图片等比缩放**。以图描述：

<img src="/img/lagou_dev.png" class="lagou-img" title="开发原则">


[slide]

* 优点：
	* 原理简单
* 缺点：
	* 对于小屏幕有时需要进行特殊处理
	* 应对复杂的页面稍显乏力
	* 不同屏幕去看各元素比例不一致


[slide]
[magic data-transition="horizontal"]
## 2.固定宽度，viewport缩放
* 设计图、页面宽度、viewport width使用一个宽度，浏览器帮我们完成缩放。单位使用 **px** 。

* 实现方式：`<meta name="viewport" content="width=640, user-scalable=no, target-densitydpi=device-dpi">`
* 利用 `@media only screen and (-webkit-min-device-pixel-ratio: 3)` 加载不同分辨率图片

========
<img src="/img/lizhi-4.jpeg" class="lizhi-img" title="荔枝在iphone4下" width="211px" height="368px">
<p>iPhone4下</p>

========
<img src="/img/lizhi-6.jpeg" class="lizhi-img" title="荔枝在iphone6下" width="249px" height="491px">
<p>iPhone6下</p>

========
<img src="/img/lizhi-6p.jpeg" class="lizhi-img" title="荔枝在ipad下" width="267px" height="520px">
<p> iPhone6 Plus下</p>
[/magic]


[slide]

* 优点：
	* 1:1 还原设计稿
	* 各种屏幕显示一致
	* 根据不同屏幕加载不同图片
* 缺点：
	* 1px border 问题
	* 字体渲染出来不够细致


[slide]
## 3.rem做宽度，viewport缩放
* 这也是 [淘宝](https://m.taobao.com/#index) 使用的方案，根据屏幕宽度设定 **rem** 值，需要适配的元素都使用 **rem** 为单位，不需要适配的元素还是使用 **px** 为单位。

* 实现方式：https://github.com/amfe/lib-flexible/blob/master/src/flexible.js


[slide]
### px与rem转换
<pre><code class="javascript">
$rem-baseline: 75px !default;
@function rem-convert($to, $values...) {
  $result: ();
  $separator: rem-separator($values);

  @each $value in $values {
    @if type-of($value) == "number" and unit($value) == ""{
        $value: $value * 1px;
    }
    @if type-of($value) == "number" and unit($value) == "rem" and $to == "px" {
      $result: append($result, $value / 1rem * $rem-baseline, $separator);
    } @else if type-of($value) == "number" and unit($value) == "px" and $to == "rem" {
      $result: append($result, $value / ($rem-baseline / 1rem), $separator);
    } @else if type-of($value) == "list" {
      $result: append($result, rem-convert($to, $value...), $separator);
    } @else {
      $result: append($result, $value, $separator);
    }
  }

  @return $result;
}
</code></pre>


[slide]
### px与rem转换
<pre><code class="javascript">
@function rem($values...) {
  @if $rem-px-only {
    @return rem-convert(px, $values...);
  } @else {
    @return rem-convert(rem, $values...);
  }
}

@mixin rem($properties, $values...) {
  @if type-of($properties) == "map" {
    @each $property in map-keys($properties) {
      @include rem($property, map-get($properties, $property));
    }
  } @else {
    @each $property in $properties {
      @if $rem-fallback or $rem-px-only {
        #{$property}: rem-convert(px, $values...);
      }
      @if not $rem-px-only {
        #{$property}: rem-convert(rem, $values...);
      }
    }
  }
}
</code></pre>


[slide]
### px与rem转换
<pre><code class="javascript">
@function rem-separator($list) {
    @if function-exists("list-separator")==true {
        @return list-separator($list);
    }
    $test-list: ();
    @each $item in $list {
        $test-list: append($test-list, $item, space);
    }
    @return if($test-list==$list, space, comma);
}
</code></pre>


[slide]
### 字体
* 一般来说，设计师会这样要求：<span class="red">任何手机屏幕上字体大小都要统一</span>。所以我们针对不同的 **dpr**，会做如下处理:
<pre><code class="javascript">
@mixin font-dpr($font-size) {
    font-size: $font-size / 2;
    [data-dpr="2"] & {
        font-size: $font-size;
    }
    [data-dpr="3"] & {
        font-size: $font-size * 1.5;
    }
}
</code></pre>


[slide]
### border 1px 问题
对于 `1px` 的元素我们一般不会去进行 px 到 rem 的转换，那我们设置 `border: 1px` ，设计师们还是不满意，为什么呢？

<img src="/img/line_rendering.jpg">


[slide]

* 所以，设计师想要的 **retina** 下 `border: 1px;`，其实就是 **1物理像素** 宽，对于 css 而言，可以认为是 `border: 0.5px;`，这是 **retina** 下(dpr=2下)能显示的最小单位。

* 而我们的第三个方案对整个页面会进行相应的缩放，正好实现了 `1px` 到 `1物理像素` 的展示。


[slide]
# 五.方案落地实施
