# simulateInstruction

通过字符串的方式模拟语音命令的执行。

simulateInstruction 函数用于模拟命令的执行。该函数设计的初衷是为了测试功能（比如无麦克风测试）。函数接受的第一参数为字符串类型，函数会将其识别为“说出的文本”，而artyom会将该文本与命令进行匹配。

Parameters|type
instruction|String
Returns|type
if the instruction exists or matches with an existing comand, will return true otherwise false. Includes messages in the console|boolean

如果模拟指令与任何已知的命令达成匹配，则会返回true，否则则会返回false，本方法允许用户仅适用文本模拟声音命令。

## 例子

```javascript
let artyom = new Artyom();

/**
 * Add a command that reacts to "Hello"
 */
artyom.addCommands([
    {
        indexes:["Hello"],
        action:function(){
            alert("Hey, how are you");
        }
    }
]);


artyom.simulateInstruction("Hello"); //Simulate a voice  command with voice "hello".
```