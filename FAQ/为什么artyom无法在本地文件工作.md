# 为什么 artyom 无法在本地文件工作

Artyom 无法于 file:// protocol 环境下使用

Chrome 于 *file://* 协议上屏蔽了许多内容，其中就包含了 `webkitSpeechRecognition` ，所以你无法在 window 中获取到这个属性。

你最好的选择（如果你没有服务器或者github 页面）是启动一个本地 webserver 运行 artyom， 或者通过增加 Chrome 启动参数 `--allow-file-access-from-files`。

[浏览该页面获取更多可能的解决方案](https://stackoverflow.com/questions/13723699/chrome-getusermedia-not-requesting-permission-locally)
