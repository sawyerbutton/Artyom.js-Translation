# recognizingSupported

验证浏览器是否支持 WebkitSpeechRecognition API。

WebkitSpeechRecognition 仅在Google Chrome 25及更高版本中允许对语音识别功能进行控制和调整。

可以使用`artyom.recognizingSupported`在浏览器中验证artyom 能否提供该API:

```javascript
if(artyom.recognizingSupported()){
   // Artyom can process commands
}else{
   // This browser doesn't support webkitSpeechRecognition
}
```
