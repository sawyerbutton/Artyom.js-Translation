# restart

使用上一次使用的初始化参数对象重启一个 artyom 实例。

restart方法使用最后一个提供的初始化对象重新启动Artyom使用的默认Webkit语音识别对象。

## 例子

```javascript
let artyom = new Artyom();

artyom.initialize({
    lang: "es-ES",
    debug: true,
    continuous: true,
    listen: true
}).then(() => {
    // Say Good Morning in Spanish
    artyom.say("Buenos días !"); 

    // Restart Artyom with the initial configuration after 5 seconds
    setTimeout(() => {


        artyom.restart().then(() => {
            // The default configuration is kept
            // that means spanish mode
            artyom.say("Buenas tardes !");
        });
    }, 5000);
});
```