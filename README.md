# Artyom.js-Translation
EN to CN Translation for Artyom.js Package

## Artyom.js 包中文翻译

[Orginal Document](https://docs.ourcodeworld.com/projects/artyom-js)

[Orginal Github Repository](https://github.com/sdkcarlos/artyom.js)

Artyom 是对 Google Chrome SpeechSynthesis 和 SpeechRecognition 的强健封装工具包，通过调用其API可以帮助开发者构建属于自己的虚拟援助。通过使用 Artyom， 你有机会在你的应用中创造出属于自己的 Siri， Google Now， Cortana。

需要注意，SpeechSynthesis 和 SpeechRecognition 的官方API 只支持 Google Chrome 浏览器（因为使用了 Google Recognition 和 Synthesis 服务）。Artyom 同时也支持 Android Chrome。

使用 Artyom 需要 `HTTP` 或者 `HTTPS`, 其无法与本地文件中使用（`file://`）。如果你需要一个持续不断的虚拟支持，考虑到某些安全因素，你必须将你的项目部署于一个拥有 https 认证的站点。如果你只需要单次的虚拟支持（以 `非持续运行` 的模式使用 artyom），则不要求 https 链接。

[通过这个视频学习如何在项目中使用Artyom](https://ourcodeworld.com/articles/read/44/how-to-add-voice-commands-to-your-webpage-with-javascript)

## 主要内容

1. FAQ
   1. 为什么 artyom 无法在本地文件工作
   2. 为什么在移动设备上，artyom.say(speech synthesis) 使用原生语音进行发音
   3. 为什么 voice 命令无法在 jsfiddle 上正常使用。

2. 从这开始
   1. 简介
   2. 官方 Changelog(Todo)
   3. 必要条件

3. API 方法库
   1. addCommands
   2. clearGarbageCollection
   3. debug
   4. detectErrors
   5. Device
   6. emptyCommands
   7. fatality
   8. getAvailableCommands
   9. getLanguage
   10. getProperties
   11. getVoice
   12. initialize
   13. isObeying
   14. isRecognizing
   15. isSpeaking
   16. newDIctation
   17. newPrompt
   18. obey
   19. on
   20. recognizingSuppoerted
   21. redirectRecognizedTextOutput
   22. remoteProcessorService
   23. removeCommands
   24. repeatLastSay
   25. restart
   26. say
   27. sayRandom
   28. setDebug
   29. shutUp
   30. simulateInstruction
   31. speechSupported
   32. when
