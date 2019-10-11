# initialize

artyom 的 initialization 函数是在web项目中创建语音助手的关键。

初始化方法接受一个拥有不同配置属性的对象作为参数。该方法返回一个 Promise，其于初始化过程成功执行时返回fulfilled状态。

## 重要

一旦加载窗口，就需要初始化artyom。

```javascript
window.onload = function(){
    var artyom = new Artyom();

    artyom.initialize({
        lang:"en-GB",
        debug:true,
        continuous:true,
        listen:true
    }).then(function(){
        console.log("Artyom has been correctly initialized");
        console.log("The following array shouldn't be empty" , artyom.getVoices());
    }).catch(function(){
        console.error("An error occurred during the initialization");
    });
};
```

一旦脚本加载到文档中，Artyom就需要加载声音，如果在加载窗口之前初始化文档，则不会选择声音，而会导致一系列的错误。这项检查机制是一个确保artyom于window中正常工作的保险。

## 初始化对象（I put the original table here, avoid misunderstanding）

初始化对象是必须的且支持所有下述属性：

Name|Allowed type|Default value|what does
---|:--:|---:|---:
listen|Boolean|false|if listen is equal to true the voice recognition will be started otherwise this property can be ignored.
speed|Float|moderates the speed with which Artyom talks (0 ~ 1)
continuous|Boolean|false|Choose if you want Google Now mode (false) that only listen 1 command and then stops, or a Jarvis (true), that will listen forever (Recognizing all the commands that you give)
debug|Boolean|false|This property allows the developer to be aware of what happens with the recognition of Artyom. Displays all the grammars recognized in the console
volume|Float|1|Adjust the volume of the voice of artyom
lang|String|"en-GB"|Set the default language of artyom with this property
mode|String|"normal"|normal,quick,remote, read original API for more info
executionKeyword|String|null|Set a keyword that allows your command to be executed immediately when you say this word (Useful in noisy environments)
obeyKeyword|String|null|Set a keyword that allows to enable the command recognition automatically if this word (or words) is recognized while artyom is paused by artyom.dontObey.
soundex|Boolean|false|Enable the soundex algorithm for the command recognition. Sometimes the speech recognition is not 100% accurate, therefore you may want to enable to match a command even when the speech recognition API recognizes something wrong.For example, if you have a command that reacts to "Open Wallmart" and artyom recognizes "Open Willmar" the command will be not triggered. However, if the soundex option is enabled and artyom recognizes "Open Willmar" the command that reacts to "Open Wallmart" will be executed because the soundex index of these words is the same (O154).
name|String|null|Provide a name to your assistant. In this way, the assistant will reacts to the commands only when you start a phrase with this name e.g "Jarvis Good Morning".

## 以持续模式启动artyom

在初始化流程中，将`continuous` 属性设置为true，即可启动 artyom 的持续模式。在持续模式下，可以向 artyom 说无数量限制的命令，而 artyom 将会持续响应你的命令。但是在持续模式下，项目需要保持https 链接，否则在 artyom 重启自身时，浏览器将会无休止地向用户请求麦克风权限。

> 注意
> 如果没有命令，artyom虽然会启动但是不会响应用户说的任何内容，因此确保在启动前（或者动态地）向artyom 发送命令。

```javascript
var artyom = new Artyom();

artyom.initialize({
    lang:"en-GB",
    //Listen Forever
    continuous:true,
    // Log everything in the console
    debug:true,
    // Initialize artyom !
    listen:true
});
```

## 以单条命令的模式启动 artyom

单条模式特别适合于”用户点击按钮，触发一条命令“的场景，在命令执行完后，artyom将会自动停止。

```javascript
var artyom = new Artyom();

artyom.initialize({
    lang:"en-GB",
    // Process 1 command, if nothing recognized then it will stop
    continuous:false,
    // Log everything in the console
    debug:true,
    // Initialize artyom !
    listen:true
});
```

## 检查初始化流程的结果

你可以通过 初始化函数返回的Promise对象的 `then` 和 `catch` 属性验证 artyom 的初始化过程结果。用于只想在artyom侦听成功后才执行一些代码的场景。

```javascript
var artyom = new Artyom();

artyom.initialize({
    lang:"en-GB",
    continuous:true,
    debug:true,
    listen:true
}).then(() => {
    artyom.say("Artyom succesfully initialized");
}).catch((err) => {
    artyom.say("Artyom couldn't be initialized, please check the console for errors");
    console.log(err);
});
```

## 使用 obeyKeyword

`obeyKeyword` 属性用于激活artyom 的命令处理机制（如果artyom已通过 `artyom.dontObey` 方法暂停）。虽然 Google Chrome 的 Speech Recognition API 并不支持暂停，但是 artyom 支持了该功能：当内部的 obey 属性设置为false时，虽然语音识别功保持激活状态，但是没有任何内部命令将被处理。

obeyKeyword 属性是控制工作流的神器工具，比如："don't process anything" 命令出发了 artyom 的 `artyom.dontObey` 函数，此时即使 artyom 处于激活状态，也不会再执行任何命令，但如果你说出初始化时提供的 obeyKeyword 属性的文本 "listen to me again"， artyom 就可以继续处理命令了：

```javascript
var artyom = new Artyom();

artyom.addCommands([
    {
        indexes:["Stop listening"],
        action:function(i){
            artyom.dontObey();
            console.log("Artyom isn't obeying anymore");
        }
    },
    {
        indexes:["Say hello"],
        action:function(i){
            artyom.say("Hello");
        }
    }
]);

artyom.initialize({
    lang:"en-GB",
    obeyKeyword: "listen to me again",
    debug:true, //Show what recognizes in the Console
    listen:true //Start listening after this 
});

// Then you say : "stop listening"
// Then try to say : "Say hello" and that should be not executed :(
// Then say : "listen to me again"
// And finally say again: "Say hello" and artyom should say hello !
```