# repeatLastSay

重复Artyom.js执行的最后一个合成文本

该方法将会返回上一条说出的语句或返回对象中的文字文本。
但如果 artyom.say 函数没有在之前使用，那么将不会发生任何事。

```javascript
artyom.say("Hello", {
    onEnd: function(){
        // Say Hello Again
        artyom.repeatLastSay();
    }
});
```