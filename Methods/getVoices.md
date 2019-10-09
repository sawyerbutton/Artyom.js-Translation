# getVoices

获取浏览器所有可用声音的数组。

如果你阅读了 webkitSpeechRecognition 的原始说明，会注意到在 Google Chrome 中获取可用声音的原始方法是一个异步函数。而 artyom 允许你以同步的方式获取这些信息，并将其赋给任何你希望的变量。

如果第一次该函数没有返回任何内容，可能是因为计算机反应较慢。Artyom 尽可能地优化了获取这些声音的方法以确保效率（这些声音将会在脚本被加载如文档且语音合成API可用时被自动获取），如果该方法失败，你可以跟随这些步骤尝试解决问题。

1. 在文档的header tag 中引入artyom
2. 避免将需要声音的artyom功能与DOMReady的listeners一起使用，使用 window 的 loaded listeners 进行相关操作（window.onLoad in Javascript 或者 $(window).load() in jQuery）。

## 例子

使用下述代码将会在控制台展示一个浏览器所支持的语言的数组：

```javascript
console.log(artyom.getVoices());
```

可以使用下述的代码在控制台展示语言的名称：

```javascript
var voices = artyom.getVoices();

for(var i = 0;i < voices.length;i++){
    var voice = voices[i];
    console.log(voice.name);
}
```