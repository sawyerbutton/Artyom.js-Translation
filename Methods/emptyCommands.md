# emptyCommands

移除artyom中所有已加载的命令

就像你可以向artyom中添加命令一样，你也可以移除他们。使用 emptyCommands 方法所有已加载的命令：

```javascript
let artyom = new Artyom();

//Clear all the available commands of artyom
artyom.emptyCommands();

//Then retrieve 
var commands = artyom.getAvailableCommands();
console.log(commands); // Ouputs : []
```