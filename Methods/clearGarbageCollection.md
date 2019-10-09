# clearGarbageCollection

清理数组中存储的语音对象的垃圾回收

clearGarbageCollection 函数清理了所有的 artyom 库中的 SpeechSynthesisUtterance 对象（使用 `artyom.say` 函数）。

> 注意

clearGarbageCollection方法甚至可以清理尚未说出的语言对象， 所以确保所有的 artyom.say 函数都被执行后再执行清理gc的函数。

直到（14.01.2017），由于SpeechSynthesis API中的错误，JavaScript的垃圾收集器在几秒钟后删除了许多仍然没有被说出SpeechSynthesisUtterance对象。[阅读相关bug的记录](https://bugs.chromium.org/p/chromium/issues/detail?id=509488)。这意味着，当artyom尝试去说出其他队列中的SynthesisUtteranceObject对象时（但因为gc的原因队列也不存在），API将会停止工作，并且你需要执行 `artyom.shutup` 方法，或 `speechSynthesis.cancel` 方法。为了解决这个问题，所有的SpeechSynthesis对象都存储在库的内部变量（一个数组）中。

## 清理GC

为了正常的清理gc，确保没有任何一个 SpeechUtterance 处于pending状态（在最后一个 `artyom.say`函数执行时执行清理gc）：

```javascript
let artyom = new Artyom();

// The clear command needs to be executed 
// always in the last artyom.say function
artyom.say("Hello , this is a long text 1 .");
artyom.say("Hello , this is a long text 2.");
artyom.say("Hello , this is a long text 3.");
artyom.say("Hello , this is a long text 4.");
artyom.say("Hello , this is a long text 5.");
artyom.say("Hello , this is a long text 6.");
artyom.say("Hello , this is a long text 7.");
artyom.say("Hello , this is a long text. Now i'll clean the garbage collection.",{
    onEnd: function(){
        var totalObjectsInCollection = artyom.getGarbageCollection().length;
        // Clear now that there are no more text to say.
        artyom.clearGarbageCollection();
        alert("The garbage collection has been cleaned. "+totalObjectsInCollection+" Items found. Now there are " + artyom.getGarbageCollection().length);
    }
});
```

## 为什么需要清理gc

如果你仅仅是使用 artyom 进行简单的操作，那么你可能并不需要这么做。然而，如果你想要合成许多文本语音（50个字符），那么这个文本将被 `artyom.say` 函数所处理，并生成一个超过 20k 的数组（大小可能会变化），而这个数组在被语言读出后就不再有用时，你可能就需要清理它了。

查看下面的代码以帮助你理解：

```javascript
// Remember that SpeechSynthesis is an experimental API
// Therefore, there are many unsolved bugs originally

// @INSTRUCTION 1
// This will add 1 item to the garbage collection
artyom.say("This is a semi long text that will be spoken",{
    onEnd: function(){
        // If it is executed here , the intruction 2 will be never executed
        // Because you just cleaned all the existent SpeechSynthesisObjects
        // This is safe only if is executed in the onEnd callback and you're
        // sure that no more artyom.say functions will be executed after this instruction
        artyom.clearGarbageCollection();
    }
});

artyom.say("What's up",{
    onEnd: function(){
        console.log("You may see this text in the console.");
    }
});

artyom.say("I'm trying to do something here. Please shut up your mouth.",{
    onEnd: function(){
        console.log("Probably this not ...");
    }
});

// More instructions ...
artyom.say("Hello, this other text that will be spoken",{
    onEnd: function(){
        console.log("You may see this text in the console but sometimes don't");
    }
});
```

> 注意！
> 当且仅当，在最后一个 `artyom.say` 函数执行的 `OnEnd` 回调函数中，进行gc的清理工作
