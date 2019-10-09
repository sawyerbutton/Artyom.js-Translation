# Device

获取使用 Artyom 的设备的相关信息

artyom 的 device 属性是一个包含两个属性的简单对象：

Property|type|Description
---|:--:|---:
isMobile|Boolean|当设备不是台式/笔记本电脑时返回true
isChrome|Boolean|当浏览器是Google Chrome时返回true

你可以使用这个方法验证浏览器是否是 Chrome，同时提示用户（比如提示在移动设备上artyom 无法指定语言）：

```javascript
let artyom = new Artyom();

// Verify if artyom is supported
window.onload = function(){
    if(artyom.Device.isChrome){
        if(!artyom.Device.isMobile){
            alert("Artyom can talk and obey commands in this browser, however the voice will be the default voice of the device. Cannot force language here.");
        }else{
            // Everything okay ! , use artyom normally here !
        }
    }else{
        alert("Artyom only works with The Google Chrome Browser !");
    }
};
```
