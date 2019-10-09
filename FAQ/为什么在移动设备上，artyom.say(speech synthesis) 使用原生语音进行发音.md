# 为什么在移动设备上，artyom.say(speech synthesis) 使用原生语音进行发音

speech synthesis 需要使用浏览器语音的语音标识符进行初始化。但是语音标识符命名法并不存在统一标准。

> 注意
> 从 artyom v1.0.3 版本之后，可以对移动设备的 speech synthesis 语言进行修改，其默认值为 （en_US, en-US）。如果设备仍然使用原生语言，你需要在源码中修改 voice 的变量。

如果你已经在移动设备中使用了 Artyom， 你可能已经发现 Voice synthesis 在移动版 Chrome 中的表现与 桌面版 Chrome 中的表现不太一致。个中缘由十分简单，然而官方并不准备给出解决方案去修复之，并强调只有在桌面版本的 Google Chrome 中 Artyom 才能绝对正常地使用。

## 为什么桌面版和移动版的Chrome中Artyom表现并不一致？

如果你在桌面版的 Google Chrome 中使用下述代码获取 voices 属性

`console.log(artyom.getVoices());`

你会得到下述结果

`Google US English, Google Deutsch, Google español`

这些语种的名字在所有语种的桌面版Chrome 上总是一致的，然而如果你在移动设备上进行同样的操作，你会得到与上述不一样的结果，比如:

`english USA, german GERMANY, español ESPAÑA `

在其他设备中，结果则可能是

`en_US, de_DE, es_ES`

理论上来说，我们只需要所有语种的对应编码和浏览器编码记录下来，那么这就不再是一个问题（理论上）。然而，这个方案只能在英语作为当前语种的设备上生效，比如一台位于德国的设备，上述代码的可能输出是：

`englisch Vereinigte Staaten, deutsch Deutschland, Spanisch Spanien`

尝试去对各个国家地区，各种名称识别器，并对各种设备及各种语言进行统一的适配，毫无疑问会大量增加 artyom 作为一个工具包的大小，更何况可能这样的适配可能并不能一本万利。

如果你尝试对某些特别的设备进行支持（设备的所选语种已知，语种对应代码已知），那你可以fork artyom.js 的项目并使用所需设备的语种代码[*编辑源码中的`artyomLanguages variable`*](https://github.com/sdkcarlos/artyom.js/blob/master/development/artyom-source/artyom.js#L64)。

兴许未来的版本中我们会提供一个方法支持自定义语言名称识别器，而不需要你再创造一个只属于你的 artyom.js(截止到2019年第四季度并没有)

## 这样的现象对于 command recognition 也存在吗？

并不会，Speech Recognition 拥有特定的语种代码，并且其并不依赖于浏览器，相关信息将会发送给 Google 服务器进行处理，而不是浏览器本地。