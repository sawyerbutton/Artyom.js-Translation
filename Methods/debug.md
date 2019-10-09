# debug

当 Artyom 的debug模式启动时，在控制台展示相关信息。

当 Artyom 的debug模式启动时，该函数将会在控制展示格式化的信息提示。

参数顺序|参数名称|类型|描述
---|:--:|---:|---:|
1|message|string|string
2|type|string|normal(default value)/error/info/warn

当debug属性被设置为true时，Artyom 才在内部使用该方法向外提供库的进度或相关信息提示。可以通过初始化的方式设置 debug 属性，也可以通过 `artyom.setDebug` 方法动态地设置该属性。

```javascript
var artyom = new Artyom();

// The debug mode needs to be enabled, otherwise nothing will happen
artyom.initialize({debug:true});
// Or set the debug mode dinamically
artyom.setDebug(true);
```

在控制台中展示任意类型的信息：

```javascript
var artyom = new Artyom();

// Normal message
artyom.debug("This is a normal debug message");
// Information message
artyom.debug("This is an info debug message","info");
// Warning message
artyom.debug("This is a warning debug message","warn");
// Error message
artyom.debug("This is an error debug message","error");
```
