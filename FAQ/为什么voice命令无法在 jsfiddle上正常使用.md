# 为什么 voice 命令无法在 jsfiddle 上正常使用

Artyom 无法在注入脚本中使用。

由于安全原因，Artyom.js无法在注入脚本上运行。如果没有该安全屏蔽，speech recognition 将成为不安全连接（http）的危险后门。

虽然大多是使用 Speech Recognition API 的方式都不会涉及注入脚本。JSFiddle 将脚本注入到 Iframe 中的方式进行工作，但在这种场景下，Speech Recognition 无法正常工作。你需要通过伺服于 **http** 或 **https** 链接的文件使用 webkitSpeechRecognition。
