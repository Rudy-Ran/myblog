### 背景
再做某项目的登录模块的时候，有一个需求是，点击某个按钮，会弹出系统的帮助文档，当用户快速点击5下以上时，弹出修改密码的弹窗。(我也不知道为什么有这么奇怪的需求)

下面是功能开发的总结，主要是要判断用户点击的次数，定时器的使用。
### JS点击事件
JS为我们提供了对点击事件的两种判断，点击和双击（*click 和 dblclick*）
```javascript
	var oBtn = document.getElementById('clickBtn');
	oBtn.onclick = function(){
		console.log('click');
	}
	oBtn.ondblclick = function(){
		console.log('dblclick');
	}
```
所谓的双击事件，就是连续的两次单击，所以如果click和dblclick同时存在，click执行的优先级更高，因此，如果我们想在执行dlbclick时，不去执行click事件，需要借助一个定时器。
**代码如下:**
```javascript
	var timer = null;
	var oBtn = document.getElementById('clickBtn');
	oBtn.onclick = function(){
		clearTimeout(timer);
		timer = setTimeout(function(){
					console.log('click');
		},300)
	}
	oBtn.ondblclick = function(){
		clearTimeout(timer);
		console.log('dblclick');
	}
```
采用定时的原理是：**因为单击事件的优先级更高，用户的双击操作，一定会先去执行click的函数，我们设置一个定时器，让click函数内的具体执行操作延迟执行，这样如果用户是一个双击操作，会在dblclick的函数里清除掉单击事件里的定时器，从而click里面的打印不会出来**
### 如何判断用户的多次点击操作
JS里是没有判断多次点击的方法的，需要我们自己去封装一个多次点击的函数。

这里需要注意的一点是，**要判断用户是否为连续点击，所以要去记录用户点击操作的时间间隔。**

**具体代码如下:**
```javascript
    var obj = this;
    var timer = null;
	//解绑dblclick
    jQuery(".login-help-btn").unbind('dbclick',null);
    lastTime = 0;
    jQuery(".login-help-btn").on('click',function(event){
            event.preventDefault();
            var currentTime = new Date().getTime();
			//记录两次相连的点击时间间隔，大于1秒，重新记录点击次数
            count = (currentTime-lastTime) < 1000 ? count + 1 : 1;
            lastTime = new Date().getTime();
            if(count === 1){
                clearTimeout(timer);
                timer=setTimeout(function(){
                    console.log('点击一次执行这部分代码');
					/*
						function(){...}
					*/
                    },250)
            }else {
					//
                    clearTimeout(timer);
            }
            if(count>4){
				    console.log('点击4次以上执行这部分代码');
                    /*
						function(){...}
					*/
            }
        });
```