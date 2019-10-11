# sayRandom

说出给定数组的随机字符串。

此函数使可以随机地说出数组的随机引用。

Parameters|type|Description
---|:--:|---
quotes|Array of Strings|The quotes that can be spoken when this function is triggered
Returns|Object|Description
quote|Object|Returns an object with the following structure(text : the spoken text ,index : the index of the chosen quote of the given array)

```javascript
/**
 * Say something random of what is in the array when this function is triggered.
 */
artyom.sayRandom([
    "Good Morning",
    "Hey, good to see you again",
    "I don't have anything to say today",
    "Did you remember that I didn't say nothing yesterday? Well, today I dont want neither."
]);
```