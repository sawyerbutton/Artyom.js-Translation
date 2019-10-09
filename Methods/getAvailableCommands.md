# getAvailableCommands

获取当前 artyom 中所有的命令

该函数允许你获取执行时 artyom 中已加载的全部命令。该函数不会返回完整的命令，而是会返回一个拥有下述结构的对象构成的数组：

- indexes：所有触发命令的适配符
- smart：该命令是否是smart 属性
- description：该命令所拥有的描述（if existing）

## 例子

当某命令不存在时向artyom加载其作为新的命令：

```javascript
let artyom = new Artyom();

// Some code that adds commands

var commands = artyom.getAvailableCommands();

for(var i = 0;i < commands.length;i++){
    var command = comanddos[i];

    // If NOT exists a command triggered by hello, add it . 
    if(!command.indexOf("hello")){
        artyom.addCommands([
            {
                description:"Says hello to the user",
                indexes:["hello","whats up"],
                action:function(){
                    artyom.say("Hey what's your budget");
                }
            }
        ]);

        break;//Stop search in commands
    }
}

// Now we can say hello !
```