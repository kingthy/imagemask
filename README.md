# imagemask
图片隐写工具，可用于隐写文本或者文件数据。最多隐写文本字符数或者文件大小由图片的长与高来决定。

* 在线演示
https://ipfs.io/ipfs/QmUG1TKotQYsp6bSw6pX4crFWfhJRNTnJre7buEaYYBV72

* 使用示例
```html
<script type="text/javascript" src="imagemask.js"></script>
<script type="text/javascript">
var mask = new ImageMask({
    debug: false,   //是否开启调试模式
    charSize: 16,   //字符的字节位数，默认为16，即字符最大值为0xFFFF
    mixCount: 2,    //隐写数据要混合到图片颜色值里的最低位数，值范围在1-5，默认为2，如果大于3，则图片会失真很严重
    lengthSize: 24  //数据长度值的占用字节位数，默认为24，也即数据长度最大值为16777215
});
</script>
```
  * 隐写文本
```javascript
//脚本里传入页面的canvas对象和要隐写的文本
var output = document.getElementById('output');
var canvas = document.getElementById('canvas');
mask.hideText(canvas, '要隐写的文本');
output.src = canvas.toDataURL();
```
  * 隐写文件
```javascript
//脚本里传入页面的canvas对象和要隐写的文本
var output = document.getElementById('output');
var canvas = document.getElementById('canvas');
var file = document.getElementById('file');
mask.hideFile(canvas, file.files[0], , function(result){
		if(result.success){
			output.src = canvas.toDataURL();
		}else{
			alert(result.message);
		}
});
```

* 读出图片里隐写的文本
```javascript
var canvas = document.getElementById('canvas');
var message = mask.revealText(canvas);
```

* 读出图片里隐写的文件
```javascript
var canvas = document.getElementById('canvas');
var file = mask.revealFile(canvas);       //file.name = 文件名称， file.data = 文件数据
```

>* 示例图片
>>* 包含一章小说的风景图片
  ![](https://ipfs.io/ipfs/QmQnHuGoKP3ZTyixygndWa4hXfhRKZ18ZgkipeqbUeQpWg)
  
>>* 包含一张美女图片的风景图片
  ![](https://ipfs.io/ipfs/QmNUiD81fU7ypgqkrrUrJVasmACmEQ3wbfEQte9Js78ou1)
  
