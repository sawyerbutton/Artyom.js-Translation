# isSpeaking

判断 artyom 是否正在说话

该函数将会告知你 artyom 是否于当前时刻正在合成文本

## 使用方式

```javascript
if(artyom.isSpeaking()){
    console.log("Artyom is speaking something");
}else{
    console.log("Artyom is not speaking anything");
}
```

## 例子

```javascript
artyom.say("Hey, a test text that i will read. Probably it doesn't make sense, therefore i will say the same twice.Hey, a test text that i will read. Probably it doesn't make sense, therefore i will say the same twice.",{
    onStart:function(){
        setTimeout(function(){
            // Most likely to be true
            console.log("Speaking : "+ artyom.isSpeaking().toString());
        },500);
    },
    onEnd: function(){
        setTimeout(function(){
            // Most likely to be false
            console.log("Speaking : "+ artyom.isSpeaking().toString());
        },500);
    }
});
```