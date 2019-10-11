# shutUp

通过该函数停止语音合成功能。

该函数立即停止实际讲话的SpeechUtterance对象，并取消所有待处理的语音对象。该函数是对 `speechSynthesis.cancel` 的封装。

```javascript
artyom.say("Hello, this is a very very long string.\n\
           I'm getting tired. Better someone silence me otherwise\n\
           i will never stop talking . No one? please someone stops me. You will never hear this.");

 /**
  * Stop talking after 2 seconds.
  */
 setTimeout(function(){

    artyom.shutUp();

 }, 2000);
```