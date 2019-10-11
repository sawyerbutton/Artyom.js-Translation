# newDictation

听写对象允许你通过简单几行代码创建简单的听写。

使用原始的webkitSpeechRecognition API 同样可以提供听写的功能，但是与调用原生API比较起来，使用 artyom 库则要优雅许多。

> 注意

当artyom处于活动状态时，听写对象不能处于活动状态，为了避免错误，推荐在启动一个 newDictation 对象之前使用 `artyom.fatality()` 修改 artyom 的活跃状态，当 dictation 对象的 onEnd 事件被触发时，你可以再次激活 artyom。

`newDictation` 方法接受单个参数，该参数是一个拥有下述属性的对象：

Property name|Type|Description
---|:--:|---:
continuous|Boolean|当使用https进行链接时，该属性能被设置为true，且 dictation 对象在手动停止函数触发前将不会暂停，在没有 https 链接时，dictation 对象将会在一定时间后停止。
onResult|Function|可以在此属性中处理听写的输出，请参阅示例。
OnStart|Function|于听写启动时进行操作
OnEnd|Function|于听写停止时进行操作

newDictation 的函数调用方式很简单，使用 `newDictation` 函数创建一个 Dictation 对象并将其存入一个变量中，返回的对象拥有 `start` 和 `stop` 两个属性。

## 例子

```javascript
var settings = {
    continuous:true, // Don't stop never because i have https connection
    onResult:function(text){
        // Show the Recognized text in the console
        console.log("Recognized text: ", text);
    },
    onStart:function(){
        console.log("Dictation started by the user");
    },
    onEnd:function(){
        alert("Dictation stopped by the user");
    }
};

var UserDictation = artyom.newDictation(settings);

// Link the events to buttons in the document
$("#button-start").click(function(){
    // Start the Dictation
    UserDictation.start();
});

$("#button-stop").click(function(){
    // Stop the Dictation
    UserDictation.stop();
});

```
