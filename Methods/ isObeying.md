#  isObeying

根据内部 isObeying 属性的状态，验证artyom是否可以服从命令。

该函数返回一个boolean类型的值，以判断 artyom 是否处理了的命令（如果希望暂停 obey 的状态则可以使用函数 artyom.dontObey）函数。

```javascript
if(artyom.isObeying()){
    // Artyom obey what you say, add some commands
}else{
    // Don't talk, artyom will not process what you say
}

/**
 *  Example
 */

// Don't execute any recognized command
artyom.dontObey();

// Outputs : false
console.log(artyom.isObeying());

// Obey orders again
artyom.obey();

// Outputs : true
console.log(artyom.isObeying());
```
