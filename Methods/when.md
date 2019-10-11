# when

在 artyom 中设置所有可用的捕获器

当artyom中某个特殊的事件触发时，该函数允许执行你所期待的操作。
下述列表列出了所有本函数支持的事件:

Name|Description
---|:--:|
ERROR|Catches all the events identified with the code "error" and have subobjects. The objects have the following codes:info-blocked,info-denied,no-speech,aborted,audio-capture,network,not-allowed,service-not-allowed,bad-grammar,language-not-supported,recognition_overlap
SPEECH_SYNTHESIS_START|Global event triggered when artyom.say starts to speak some text.This event is dispatched along with the onStart event of artyom.say (2 times).
SPEECH_SYNTHESIS_END|Global event triggered when artyom.say finishes to read some text.This event is dispatched along with the onEnd event of artyom.say (2 times).
TEXT_RECOGNIZED|Global event triggered when the user speaks to the microphone and some text is recognized.
COMMAND_RECOGNITION_START|Global event triggered when artyom starts to listening to your commands.
COMMAND_RECOGNITION_END|Global event triggered when artyom doesn't listen anymore to your commands. The callback returns an object with information if the onEnd event has been triggered with continuous mode or not.
COMMAND_MATCHED|Global event triggered when one of the provided commands matches with your voice. (A commands has been found)
NOT_COMMAND_MATCHED|Global event triggered when the text spoken by the user does not match any of the loaded commands.


## 获取所有artyom中的错误

```javascript
let artyom = new Artyom();

//All catchable artyom errors will be catched with this
artyom.when("ERROR",function(error){

    if(error.code == "network"){
        alert("An error ocurred, artyom cannot work without internet connection !");
    }

    if(error.code == "audio-capture"){
        alert("An error ocurred, artyom cannot work without a microphone");
    }

    if(error.code == "not-allowed"){
        alert("An error ocurred, it seems the access to your microphone is denied");
    }

    console.log(error.message);
});
```

## 处理其他事件

```javascript
let artyom = new Artyom();

var onCommandMatched = "COMMAND_MATCHED";

artyom.when(onCommandMatched,function(){
   console.log("A command has been found and it will be executed.");
});

// Some events receives an object
artyom.when("COMMAND_RECOGNITION_END",function(status){
   if(status.code == "continuous_mode_enabled"){
     console.log("You're using continuous mode, therefore this callbacks is more likely to don't be used");
   }else if(status.code == "continuous_mode_disabled"){
     console.log("The continuous mode is disabled. Artyom will not listen anymore till the next initialization");
   }
});
```