# iOS、移动版 Safari 和 HTML5 音频的限制与解决方案

### 1.单音频流
移动版 Safari 带来的最大的局限之一是一次只能播放一个单音频流。移动版 Safari 中的 HTML5 媒体元素都是单例的，所以一次只能播放一个 HTML5 音频（和 HTML5 视频）流。Apple 为这一局限做过解释，但我们推断这是为了减少数据费用（这也是大多数 iOS HTML5 其他局限的原因所在）。

iOS 为移动版 Safari 提供了单一 HTML5 媒体（音频和视频）容器。如果想要在播放一个音频流的同时播放另一个音频流，那么就会从容器中删除前一个音频流，新的音频流将会在前一个音频流的位置上被实例化。

有一点很重要，务必牢记，音频和视频是可以互换的。如果在视频播放的同时要播放音频文件，那么视频就会停止。一次只能播放一个音频或视频流。

**解决方案：**

单个音频流局限的一种解决方案是用所需音频置换出源文件，如清单 9 所示。这不是一种理想的解决方案，因为您需要等待加载新的音频流后才能播放它。

```
var audio = document.getElementById('audio');
audio.play();
 
// at some later point in your script (does not need to be from a touch event)
audio.src = 'newfile.m4a';
audio.play(); // there will be a slight delay while the new audio file loads
```

应对单个音频流局限性的一种更好的解决方案是使用 audio sprite。简言之，您要将所有的音频综合到一个单音频流中，然后播放此流的各个部分。

### 2，自动播放和加载音频

在移动版 Safari 中加载的页面上，不能自动播放音频文件。音频文件只能从用户触发的触摸（单击）事件加载。如果在 HTML 标记中使用了 autoplay 属性，那么移动版 Safari 将会忽略这个属性，并且不会在加载页面时播放此文件

除非由用户接触事件，比如通过 onmousedown、onmouseup、onclick 或 ontouchstart 触发事件，否则不能加载音频流

**解决方案：**

对于自动播放的局限性，没有变通方案。正如前面所提及的，音频流只能从用户触摸事件加载。当针对移动版 Safari 进行开发时，重要的一点是要在必要时调整您的工作流，以适应这个局限性。

音频流只在用户事件触发时才能加载。如清单 11 所示，onmousedown、onmouseup、onclick 和 ontouchstart 都是一些可用的事件，当在一个回调中调用它们时，可成功加载一个音频流。请注意，这种情况只适用于加载一个音频文件时，在一个已经加载的文件上调用 play() 会按预期的那样工作。即：设计主动地交互动作让用户去触发，从而播放audio

```
// run on page load
var button = document.getElementById('button');
var audio = document.getElementById('audio');
 
var onClick = function() {
    audio.play(); // audio will load and then play
};
 
button.addEventListener('click', onClick, false);

```

**在微信里，通过以下方式实现：**

##### 1.接在微信的js授权文件

```
<script src="res.wx.qq.com/open/js/jweixin-1.2.0.js"></script>
```
##### 2.监听微信WeixinJSBridgeReady事件，播放audio
```
document.addEventListener("WeixinJSBridgeReady", function () { 
	music.src = 'http://m.test.9now.net/c_market/invitation/media/music.mp3'
    music.play(); 
    music.pause(); 
}, false); 

```
##### 原因：应该是微信里面有处理这种情况。

**参考文献：**
[https://www.ibm.com/developerworks/cn/web/wa-ioshtml5/](https://www.ibm.com/developerworks/cn/web/wa-ioshtml5/)

### 补充问题

发现在andriod中不同版本和不同手机机型微信中存在差别，有的可以自动播放，有的不可以自动播放，且无法判断原因。暂未找到解决方案。