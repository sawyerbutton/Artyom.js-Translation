# getProperties

获取 artyom 对象的内部属性（配置属性）。

该函数返回 artyom 的真实配置对象。不要尝试去改变该对象的任何属性，因为不会发生任何事，该方法只是一个 getter。

该对象存储了 language,speed,volume, isRecognizing 和 mode 属性。

```javascript
console.log(artyom.getProperties());
```