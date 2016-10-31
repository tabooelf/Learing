## jQuery实现AJAX

### 1.GET

使用`get()`方法时，采用GET方式向服务器请求数据，并通过方法中回调函数的参数返回请求的数据，它的调用格式如下：
`$.get(url,[callback])`

```javascript
$.get("demo_test.php?id=1&name=lemoo",function(data,status){
    alert("Data: " + data + "\nStatus: " + status);
  });
```

- 参数通过URL传递
- 有缓存

### 2.POST

与`get()`方法相比，`post()`方法多用于以POST方式向服务器发送数据，服务器接收到数据之后，进行处理，并将处理结果返回页面，调用格式如下：
`$.post(url,[data],[callback])`

```javascript
$.post("demo_test.php",{
  num:1
},
function (data) {
  alert(data);
});
```

使用`serialize()`方法可以将表单中有name属性的元素值进行序列化，生成标准URL编码文本字符串，直接可用于ajax请求，它的调用格式如下：
`$(selector).serialize()`

### 3.ajax

使用`ajax()`方法是最底层、功能最强大的请求服务器数据的方法，它不仅可以获取服务器返回的数据，还能向服务器发送请求并传递数值，它的调用格式如下：
`$.ajax([settings])`
其中参数settings为发送ajax请求时的配置对象，在该对象中，url表示服务器请求的路径，data为请求时传递的数据，dataType为服务器返回的数据类型，success为请求成功的执行的回调函数，type为发送数据请求的方式，默认为get。

```javascript
$.ajax({
  type:"post",
  url:"demo_test.php",
  data: { num: 123 },
  dataType:"text",
  success: function (data) {
    alert(1);
  }
});
```

### 4.getJSON

使用`getJSON()`方法可以通过Ajax异步请求的方式，获取服务器中的数组，并对获取的数据进行解析，显示在页面中，它的调用格式为：
`$.getJSON(url,[data],[callback])`
可以与$.each搭配来遍历数据

```javascript
$.getJSON("demo_test.php",function(data){
  $.each(data, function (index, sport) {
    if(index==3)
      $("ul").append("<li>" + sport["name"] + "</li>");
  });
});
```

这样返回的数据直接就是JSON格式的就可以使用，但是要注意缓存问题。

## AJAX的调试

在运行AJAX的页面按F12(Chrome下)，进入“Network”选项卡，点击"XHR"过滤器，然后触发AJAX的事件。
![img](https://segmentfault.com/img/bVnbfw)



点击要进行调试的AJAX动作，进入详情页。

![img](https://segmentfault.com/img/bVnbfM)

- Request URL:查看请求的地址，一般在这里查看向后台请求的URL是否正确，错误404的话一般这里会有问题
- Request Method:请求的方式，查看是GET或者POST，GET请求的参数一致的话会有缓存
- Status Code:返回状态。一般是200正常；404未找到页面，一般是URL错误，或者后台没有创建相应的action；500内部服务错误，多为后台错误。
- 底下的Query String Parameters是向后台发送的数据，一般这里看参数是否有问题，格式及命名是否正确，事故多发地。

点击Response就可以查看服务器返回的数据了，一般在这里查看返回是否正常，格式是否正确，一般是JSON。

![img](https://segmentfault.com/img/bVnbf1)

基本上通过发送的数据及传回的数据就能定位问题所在了。