# say

通过该函数，artyom 可以在 Google Chrome 中说话。

该函数允许用户将任何文本字串合成为声音。该函数接受两个参数，第一个参数是需要合成为声音的文本字串，而第二个参数则是回调函数的对象，第二个参数是可选的。

Parameters|type|Description
---|:--:|---:
text|String|The string that's meant to be spoken
configuration|Object|An object with the 2 available callbacks for this function and the code language if you don't want to use the same language providen in the initialization.(onStart: a function triggered when artyom starts to speak|onEnd: a function triggered when artyom stops speaking|lang: force the language for a single utterance object.)

`artyom.say`函数使用了Google Chrome 的原生 speechSynthesis API，同时内置了许多适配方法，以提供一种不受任何字符限制的干净实用的文本转语音方法。

- Artyom消除了原始API功能中的字符限制。
- Artyom保障了回调函数的执行（原生API中，这些时间有时候不会被触发）。
- Artyom简化了API的调用方式，使其更容易使用。

```javascript
let artyom = new Artyom();

/**
 * Speak a short string and indicate its callbacks in the console.
 */
artyom.say("A simple demonstration of what i can do.",{
    onStart:function(){
        console.log("The text has been started.");
    },
    onEnd:function(){
        console.log("The text has been finished.");
    }
});

/**
 * Say something
 */
artyom.say("Welcome again");
```

## 在单词说话时强制使用某语种

默认情况下，`say`函数使用初始化方法中提供的语种。但是也可以指定自定义语种说单条语言，通过函数的第二个参数进行设置即可。

> 重要！
> 在指定单句说话的语种之前需要提供一个初始化语种，否则可能会出现错误。

```javascript
let artyom = new Artyom();

// Important, set your default language to prevent any error

artyom.initialize({lang:"en-GB"});


artyom.say("Hello World in English",{
    lang:"en-US",
    onEnd:function(){
        console.log("The text has been finished.");
    }
});

artyom.say("Hola Mundo en español",{
    lang:"es-ES",
    onEnd:function(){
        console.log("El texto ha sido leido");
    }
});

artyom.say("Bonjour tout le monde en français",{
    lang:"fr-FR",
    onEnd:function(){
        console.log("Le texte a été lu");
    }
});

artyom.say("Olá mundo em Português",{
    lang:"pt-PT",
    onEnd:function(){
        console.log("O texto foi lido");
    }
});

artyom.say("Ciao mondo in italiano",{
    lang:"it-IT",
    onEnd:function(){
        console.log("Il testo è stato letto");
    }
});

artyom.say("Using the initialization language here, that means english great britain");
```

## 对于大型文本的推荐

如果你经常需要处理巨量的文本（超过20000个字符），那最好优化业务代码。记住在合适的时间点使用`artyom.clearGarbageCollection`方法清理gc对象。阅读[理解并学会清理artyom的gc](https://docs.ourcodeworld.com/projects/artyom-js/documentation/methods/cleargarbagecollection)以了解更多信息