# remoteProcessorService

创建一个自定义命令处理器。

在远程模式下启用了artyom，则此功能用于处理artyom识别的文本。每当用户说话和文本被识别时，该函数都会被触发。该方法的主要目标是自定义命令的处理方式，因此你可以通过自己希望的方式使用识别出的文字。

## 启动远程模式

如果在初始化时没有设定远程模式，那么 remoteProcessorService 将会失效。请确保在初始化时将 artyom 设定为远程模式：

```javascript
window.onload = function(){
    artyom.initialize({
        lang:"en-GB",
        debug:true,
        continuous:true,
        listen:true,
        // Important to use the custom processor
        mode:"remote"
    }).then(function(){
        console.log("Artyom has been correctly initialized");
        console.log("The following array shouldn't be empty" , artyom.getVoices());
    }).catch(function(){
        console.error("An error occurred during the initialization");
    });
};
```

此时一旦artyom被初始化，自定义处理器将会被使用（如果配置了自定义处理器）。

## 自定义服务处理器

创建一个自定义服务来处理服务器中存储在数据库中的命令（服务端配置所决定）：

```javascript
artyom.remoteProcessorService(function(data){
    // An object with information about the recognized text
    // by the speech recognition API
    console.info(data);

	
	if(data.isFinal){
		// execute an ajax to a server
		// which process the command
		// with something like SQL etc..
		
		$.ajax({
			url:"command-processor",
			dataType:"JSON",
			data:{
				recognized: data.text
			},
			success:function(dataFromServer){
				// The response should be a json object like 
				//{
				//	"name": "hello",
				//	"action":"alert('Hi, you said hello !');"
				//}
				
				console.log(dataFromServer);
				
				// Will alert
				eval(dataFromServer.action);
			}
		});
	}
});
```

## 自定义本地处理器

自定义函数本身并不一定要求远程服务，所以你可以对识别到的文字以下述方式进行处理：

```javascript
artyom.remoteProcessorService(function(data){
    var customDatabaseCommands = [
        {
            command_word: "Hello",
            execute: function(){
                alert("Hello");
            }
        }
    ];
	
	if(data.isFinal){
        customDatabaseCommands.forEach(function(item){
            // If the command_word property of my command is the same
            // that what you said then execute the command
            if((item.command_word).indexOf(data.text) != -1){
                // Execute the command, in this if you say hello, it will trigger
                item.execute();
            }
        });
	}
});
```