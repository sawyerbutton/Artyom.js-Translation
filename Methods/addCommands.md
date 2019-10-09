# addCommands

如果没有命令，artyom 将不会清楚如何响应你说的话。学习如何将声音命令添加到artyom中。

此方法期望以命令的数组或单个命令作为第一个参数。这些命令将会被添加到artyom的内部命令数组中（该数组保存当前artyom对象中的所有命令）。命令支持以动态的方式进行添加，artyom 还是会处理他们。

## 关于 command object

命令是文字对象，具有至少3个属性：

属性名称|类型|描述
--|:--:|--:
indexes|Array|包含所有可以触发命令的文本标识符的数组
smart|boolean|为了正确地处理命令，artyom需要知晓命令是否使用了通配符。如果确信是这种状况，则将该属性设置为true
action|Function|当被识别的文本匹配到命令数组中任意一个文本标识符后触发该函数。该函数根据命令的类型接受两个参数（第一个参数是匹配到的命令的index，第二个参数则是基于其是否是smart模式所识别到的通配符）

创建一个命令并在你说hello时展示一个警告:

```javascript
var command = {
    indexes: ["Hello"],
    action: function(){
        alert("Hello, how are you ?");
    }
};

var artyom = new Artyom();

artyom.addCommands(command);
```

## 添加一组命令

可以使用一个数组作为命令输入，将多个命令添加到 artyom。数组中的每一个元素都必须是一个命令：

```javascript
var commands = [
    {
        indexes: ["Hello"],
        action: function(){
            alert("Hello, how are you ?");
        }
    },
    {
        indexes: ["Good night"],
        action: function(){
            alert("Hello, how are you ?");
        }
    },
    {
        indexes: ["Good morning"],
        action: function(){
            alert("Hello, how are you ?");
        }
    }
];

var artyom = new Artyom();

artyom.addCommands(commands);
```

## 如何知晓哪一条命令被触发？

如果你使用了将会响应多个单词的命令，你可以在action函数中获得被读出的单词的下标：

```javascript
var artyom = new Artyom();

artyom.addCommands({
    indexes: ["Good morning","Good night", "Hello"],
    action: function(i){
        if(i == 2){
            // You said Hello
        }else if(i == 1){
            // You said Good night
        }else if(i == 0){
            // You said Good morning
        }
    }
});
```

## 使用 smart commands

smart command 是一个语音命令，其值是可以改变并长久保存的。你可以在命令中通过 * 字符获取可变的值，可变值可以从action的回调函数中获取。需要注意 `smart` 属性需要被设置为true。

比如，你可以创建一个命令，让artyom总是在你说 “repeat after me” 之后重复你说的话：

```javascript
var artyom = new Artyom();

artyom.addCommands({
    //The smart property of the command needs to be true
    smart:true,
    indexes: ["Repeat after me *"],
    action: function(i, wildcard){
        // Speak alterable value
        artyom.say(wildcard);
    }
});

// Then use the initialize function 
// ..
// And proceed to say "Repeat after me, make a sandwich"
// Then artyom should say "make me a sandwich"
```

除此之外，为了让命令更加智能，假设你已经知道如何使用它们的情况下，你可以在命令中添加正则表达式以达成更复杂的功能。添加一个正则表达式作为 indexes 数组的元素即可。

> 注意！
> 使用[测试函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test)进行测试时，正则表达式需要返回true。

```javascript
var artyom = new Artyom();

artyom.addCommands({
    //The smart property of the command needs to be true
    smart:true,
    indexes: [/Good Morning/i, new RegExp("Good Afternoon", "i")],
    action: function(i){
        artyom.say("Hey, are alright? You never say hello.");
    }
});
```
