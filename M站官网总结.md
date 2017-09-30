# M站官网总结





### 1.弹窗控件抽出，单独引用


### 2.目前的浏览器对于video标签的强制劫持，生出等比大小的native控件，造成样式的不可控。


    具体表现：1）z-index层级最高
              2）iOS的qq浏览器会会将视频控件居中，对于一些需要做侧边菜单的页面影响严重
              3）网上的video控件多用svg来生成播放或暂停按钮，不使用wifi的时候会加载不出来。

### 3.移动端video标签兼容属性


    http://www.bubuko.com/infodetail-1918217.html

### 4.移动页面侧边菜单问题


    对于菜单展开，页面移出视口范围，在滑动菜单的时候会造成主页面的滑动，
    http://www.51xuediannao.com/javascript/jszzyddmrsjyjzzzhxgdsjff_1152.html
    原因分析：
        1.移动端页面内容横向超出视口会出现横向的滚动条，但这个滚动条属于浏览器，即便overflow             ：hidden，也会出现。所以会出现横向滚动。
	    ps:
		后期发现移动端页面内容横向超出，
		如果该内容不隐藏掉（即display：		         none）的话，一定会出现横向的滚		             动条，且且不受开发者控制。
        2，使用event.preventDefault()阻止冒泡，会造成页面所不可滚动，无论横向还是纵向。所以给           需要滚动的dom元素，监听touch事件，并判断touch的移动方向，在需要滚动的方向（如纵向）             不作处理，在不需要滚动的方向（如横向）阻止冒泡。

### 5.唤醒app,


   安卓可以唤醒，通过URL             Scheme协议，但是存在问题。前端无法在不和Native交互的情况下，判断是否跳转到APP，所以一般的做法是在跳转之后加一个定时器在3S之后跳下载链接。。可这样页面会到一个空白页，体验不好，待优化。网页通用的生成iframe的做法无效，应该有待研究。
	iOS的safari无法通过URL Scheme的方式唤醒APP,会判定链接无效，需要通过深层链接来做。
	微信中也无法唤起APP，无论安卓或是iOS只能跳下载。

### 6.网页无法判断用户是否关注某个公众号，也无无法跳转到公众号页面，无法判断用户网络状态，


### 7唤起电话：
   

     <a href=’tel:13400000'></a>


### 8.唤起邮箱：

    <a href=‘mailto:8234@qq.com’></a>


### 9.react 的编程模式，思想


### 10.微信分享的link:


    window.location.origin + window.location.pathname
    引用jweixin,js的时候，不要写死http头

### 11，react-slick轮播图片


### 12页面头部position：fixed的时候，页面下拉会遮住fixed的header，


    解决办法：将header写在滚动区域的div之外。

	

