# detectErrors

通过artyom探查客户端中发现的错误。

该方法允许开发者探查是什么问题阻止了artyom的启动。

> 注意
> 该方法将会在下个版本移除（因为该功能只供开发者使用？？？）

```javascript
var errorObject = artyom.detectErrors();

console.log(normalError);

// Outputs for example
//{
//    code: "artyom_error_localfile",
//    message: "Fatal Error Detected : It seems you're running the artyom demo from a local file ! The SpeechRecognitionAPI Needs to be hosted someway (server as http or https). Artyom will NOT work here, Sorry."
//}
```