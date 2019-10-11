# setDebug

立刻调整 artyom 的debug 模式。

不通过初始化函数的方式动态修改 artyom 的 debug 模式状态。注意artyom 的debug模式已经被禁用了，将无法展示 debug 控制台信息，使用 `artyom.setDebug` 函数修改之。

```javascript
// Enable debug
artyom.setDebug(true);

// Disable debug
artyom.setDebug();
// or
artyom.setDebug(false);
```