# on

以简单的方式添加一条命令。

artyom.on 方法是 artyom.addCommands的等价代替，其仅仅是作为语法糖存在。对于只有几个命令将会被使用的 artyom 项目中，该方法将会更加便利。

该方法并不是基于Promise的实现，其仅仅是对 artyom.addCommands 函数的二次封装。作为第一个参数，需要提供commands的indexs属性，它将返回一个对象，该对象的then属性是一个函数。触发该函数并提供一个函数作为第一个参数，函数接受下标信息（数组中与命令匹配的项的索引）和通配信息。

## 普通的command

```javascript
let artyom = new Artyom();

artyom.on(['Good morning','Good afternoon']).then(function(i){
    switch (i) {
        case 0:
            artyom.say("Good morning, how are you?");
        break;
        case 1:
            artyom.say("Good afternoon, how are you?");
        break;            
    }
});
```

## smart command

如果你希望创建一个smart command，需要将on 函数接受的第二个参数设定为true：

```javascript
artyom.on(['Repeat after me *'] , true).then(function(i,wildcard){
    artyom.say("You've said : " + wildcard);
});
```

