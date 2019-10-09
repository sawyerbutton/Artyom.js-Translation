# isRecognizing

判定 artyom 是否正在’听‘你的命令。

该函数将会告知你在函数执行时 artyom 是否正在识别命令 （与 artyom 是否处于 obeying 状态无关）。

```javascript
JAVASCRIPTif(artyom.isRecognizing()){
    console.log("Artyom is listening to your commands");
}else{
    console.log("Artyom is not listening to you.");
}
```

## 例子

```javascript
// initialize artyom
artyom.initialize({
    lang:"en-GB",
    debug:true,
    continuous:true,
    listen:true
});

setTimeout(function(){

    // Show the status of the recognition, most likely to be true
    console.log("Recognizing : " + artyom.isRecognizing().toString());

    setTimeout(function(){
        // Stop recognition
        artyom.fatality();

        setTimeout(function(){    
            // Most likely to be false
            console.log("Recognizing : " + artyom.isRecognizing().toString());
        },1000);
    },1000);
},1000);
```
