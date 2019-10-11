# speechSupported

验证 speechSynthesis 是否被当前浏览器支持。

SpeechSynthesis接口是用于控制文本到语音输出的脚本化Web API。该函数允许你检查 Speech Synthesis API 是否在当前浏览器中使用。

```javascript
if(artyom.speechSupported()){
  // Use artyom.say("Text");
}else{
  // Unsupported :/
}
```