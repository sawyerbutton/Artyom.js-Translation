# fatality

停止识别的命令

该方法允许用户在任何时间终止语音识别。与 initialize 方法一样实现 promises 并只会停止语音识别，而并不会停止语音合成的队列（如果想要终止发音说话，则需要使用`shutUp`函数）。

```javascript
var artyom = new Artyom();

artyom.initialize({
    lang:"en-GB",
    debug:true, //Show what recognizes in the Console
    listen:true, //Start listening after this
    speed:0.8, // Talk a little bit slow
});

/**
 * After of 5 seconds, stop artyom.
 */
setTimeout(function(){
    artyom.fatality().then(() => {
        console.log("Artyom succesfully stopped !");
    });
}, 5000);
```