# 前端DOM元素转base64，提交后台

方法：

先通过插件，将需要转码的DOM元素通过插件通过canvas绘成img,然后将img转码，提交给后台。

现有插件：
##### 1.[html2canvas](http://html2canvas.hertzen.com/documentation.html)

##### 2.[dom-to-image](https://github.com/tsayen/dom-to-image/blob/master/src/dom-to-image.js)


1.使用html2canvas做转码，封装，批量转码

```
/*

 dom转base64
//传入需要转码的dom的id,如：  ['orderTrendTable','brandComplaintsTable']
返回值为：以id为key，base64码为value的对象数组集合

*/
function tableBase64(tableIdArr){
    var tableArr = [];
    var a = 0;
    for(var i = 0; i< tableIdArr.length;i++){
        var k = tableIdArr[i];
        var key = document.getElementById(k);
        html2canvas(key, {
            onrendered: function(canvas) {
                var tableUrl = canvas.toDataURL();  
                cb(tableUrl);
            },
        });
    }
    function cb(v){
        var obj = {};
        obj[tableIdArr[a]] = v;
        tableArr.push(obj)
        a++;
    }
    return tableArr; 
}
```
### echarts批量base64
```
/*
	echarts表格转base64
	传入需要转码的echarts的实例,如： [totalOrder,totalCall,totalComplaints]
*/
function echartsBase64(echartsIdArr){
    var baseArr = [];
    for(var i = 0;i<echartsIdArr.length;i++){
        var imgInfo = echartsIdArr[i].getDataURL();
        var id = echartsIdArr[i]._dom.id;
        var obj = {};
        obj[id] = imgInfo
        baseArr.push(obj);
    }
    return baseArr
}
```