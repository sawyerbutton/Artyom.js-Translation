# redirectRecognizedTextOutput

通过 artyom 以你所希望的方式重定向识别到的文字。

有时候，你希望了解artyom 在文档中理解和展示了什么，除非在初始化时设定 debug 参数为 true，否则artyom的原始输出都会被隐藏起来（此时所有信息也都是不可回溯的，因为他们都只会被展示在console里）。

```javascript
artyom.redirectRecognizedTextOutput((recognized,isFinal) => {
    if(isFinal){
        // Nothing
        $("#span-preview").text("");
    }else{
        $("#span-preview").text(recognized);
    }
});
```