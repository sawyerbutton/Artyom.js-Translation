# obey

如果之前命令是被被停止了，则恢复之

如果之前artyom 通过 `artyom.dontObey` 函数中止了命令识别功能，调用该函数将恢复启命令识别的功能。

## 恢复命令执行

```javascript
/ Add here a lot of commands i.e :
// ["hello","how are you","say hello"]
 
artyom.initialize({
    lang:"en-GB",
    continuous:true,
    debug:true,
    listen:true
});

// Dont obey any order that the user gives
artyom.dontObey();

// If you trigger any command with your voice, nothing will happen
// but in 5 seconds enable the function again with obey
setTimeout(() => {
    // Enable command recognition again
    artyom.obey();
    // Try to say hello again and now the command will be recognized
}, 5000);
```

## 通过 ObeyKeyword 恢复命令执行功能

你可以使用声音和在初始化 artyom时设定 obeyKeyword 属性以实现恢复命令实行。该方式将允许你再说出给定词汇时恢复命令识别：

```javascript
artyom.initialize({
    lang:"en-GB",
    continuous:true,
    debug:true,
    listen:true,
    // if artyom is not obeying (paused) and the users says the obeyKeyword
    // it will continue with the command recognition (obey again)
    // if you say "start again" and artyom is not obeying, it will obey again.
    obeyKeyword: "start again"
});
```
