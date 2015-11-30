刮奖用组件，使用了html5的画布(canvas) 在不支持画布的浏览器中自动使用div的形式（div的形式没有擦除效果，在“开始回调”中的第一个参数声明了是canvas还是div）:v:

```
 buildScratchMod:function(){
        var that = DomeWebController;
        var $canvas = $(
            ScratchMod({
                'container': that.getEle('$scratchModContainer'),//目标容器
                'bgImgSrc': 'static/img/doge.jpg',//背景图
                //'imgSrc': ,//蒙版图
                //'penImgSrc': ,//擦笔图
                'color': 'blue',//蒙版颜色（有imgSrc的情况下该属性无效）
                'width': 300,//宽度
                'height': 300,//高度
                'eraseRadius':30,//擦除笔的半径(有penImgSrc的情况下无效)
                'sampleStep': 1,//获取擦除百分百时的精度（数字越大精度越小）
                'sampleCD': 500,//获取擦除百分百的时间间隔
                'sampleCallback': that.sampleCallback,//获取擦除百分百的回调函数（返回true后不再回调）,回调的第一个入参为擦除百分百
                'startCallback': that.startCallback//开始刮的回调(只回调一次,回调的第一个入参为生成的元素类型 canvas或div)
            }));
        that.setEle("$scratchMod",$canvas);
        $canvas.css({'backgroundSize':'cover'});
    },
    sampleCallback:function(rate){
        var that = DomeWebController;
        that.getEle("$show2").html(rate);

    },
    startCallback:function(ele){
        var that = DomeWebController;
        that.getEle("$show1").html(ele+"开始了");

    }
```