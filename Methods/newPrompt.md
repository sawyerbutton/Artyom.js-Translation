# newPrompt

通过 artyom.js 创建一条语音提示信息。

newPromt 方法是一个期待第一个参数为单个对象的函数，该对象包含下述属性：

属性名称|类型|This text will be
---|:--:|---:
question|string|在提示启动时，该文本将会被合成
options|Array of Strings||提示所对应的可用回答
beforePrompt|Function|于artyom 提问前触发该操作
onStartPrompt|Function|于artyom提问时触发该操作
onEndPrompt|Function|于artyom提问结束时触发该操作
onMatch|Function|于artyom识别出某个选项时触发，引用的函数参数与 command 的函数参数一致（数组命令的数组下标）。必须返回一个函数才能最终执行，因此请在变量中声明一个函数并将其返回

## Voice Prompt 如何工作

Artyom 提供了使用语音触发动作的工具，有时候该功能将需要在该命令中执行更多操作，而 artyom.newPrompt创建了一种更具交互性的方式来执行这些操作。

## 需要知道的事情

- 当一个artyom 提示被执行时，之前被注入的命令都将不可用，只有提示中提供的选择才会触发动作。
- 提示必须有回应，否则任何之前加载的可用命令都将无法正常执行。所以，一般来说，推荐添加"exit","quit"或者"cancel"选项帮助程序正常运行。

## 例子

下述代码描述了一个非常简单的问题提示：

```javascript
artyom.newPrompt({
    question:"We have no cheese, you want it without cheese anyway ?",
    options:["Yes","No","Buy some cheese"],
    beforePrompt: () => {
        console.log("Before ask");
    },
    onStartPrompt: () => {
        console.log("The prompt is being executed");
    },
    onEndPrompt: () => {
        console.log("The prompt has been executed succesfully");
    },
    onMatch: (i) => { // i returns the index of the given options
        var action;

        if(i == 0){ 
            action =  () => {
                artyom.say("Your sandwich will be ready in a minute");
            }
        }

        if(i == 1){ 
            action =  () => {
                artyom.say("You may consider to order some cheese later");
            }
        }

        if(i == 2){
            action = () => {
                artyom.say("I'll order some cheese via eBay");
            }
        }

        // A function needs to be returned in onMatch event
        // in order to accomplish what you want to execute
        return action; 
    }
});
```

## Smart 例子

提示同样支持 smart 命令：

```javascript
artyom.newPrompt({
    question:"How many centimeters should I cut?",
    //We set the smart property to true to accept wildcards
    smart:true,
    options:["Cut * centimeters","Remove * centimeters"],
    beforePrompt: () => {
        console.log("Before ask");
    },
    onStartPrompt:  () => {
        console.log("The prompt is being executed");
    },
    onEndPrompt: () => {
        console.log("The prompt has been executed succesfully");
    },
    onMatch: (i,wildcard) => {// i returns the index of the given options
        var action;

        var totalCentimeters = parseInt(wildcard);

        action = () => {
            alert(wildcard + " centimeters will be removed of your sandwich!");
        };

        // A function needs to be returned in onMatch event
        // in order to accomplish what you want to execute
        return action;                       
    }
});
```
