# AJAX 基础及原生

##1.定义

**`AJAX=Asynchronous JavaScript and XML`**

同过 `Js` 实现与后端数据异步交互。使用 `get` 和 `post` 的方式向后端发送请求数据，之后根据返回的请求数据控制DOM。



## 2.XHR 创建对象

所有现代浏览器（IE7+、Firefox、Chrome、Safari及Opera）均内建XMLHttpRequest对象

老版本的IE5 和IE6 使用ActiveX对象

```javascript
var xmlhttp;
if (window.XMLHttpRequest)
  {// code for IE7+,Firefox,chrome,Opera,Safari
    xmlhttp = new XMLHttpRuquest();
  }
else
  {// code for IE6,IE5
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
  }
```

##　3.常用方法和代码示例

| 方法                                     | 描述                              |
| -------------------------------------- | ------------------------------- |
| **open(*method*,*url*,*async*)**       | **规定请求的类型、URL 以及是否异步处理请求。**     |
|                                        | ● *method*：请求的类型；GET 或 POST     |
|                                        | ● *url*：文件在服务器上的位置              |
|                                        | ● * *async*：true（异步）或 false（同步） |
| **send(*string*)**                     | **将请求发送到服务器。**                  |
|                                        | ● *string*：仅用于 POST 请求          |
| **setRequestHeader(*header*,*value*)** | **向请求添加 HTTP 头。**               |
|                                        | ● *header*: 规定头的名称              |
|                                        | ● value: 规定头的值                  |

### onreadystatechange 事件

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

每当 readyState 改变时，就会触发 onreadystatechange 事件。

readyState 属性存有 XMLHttpRequest 的状态信息。

下面是 XMLHttpRequest 对象的三个重要的属性：

| 属性                     | 描述                                       |
| ---------------------- | ---------------------------------------- |
| **onreadystatechange** | **存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。** |
| **readyState**         | **存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。**  |
|                        | **0:** 请求未初始化                            |
|                        | **1:** 服务器连接已建立                          |
|                        | **2:** 请求已接收                             |
|                        | **3:** 请求处理中                             |
|                        | **4:** 请求已完成，且响应已就绪                      |
| **status**             | ● 200: "OK"                              |
|                        | ● 404: 未找到页面                             |

### GET

```javascript
xmlhttp.onreadystatechange = function()
  {
    if (xmlhttp.readyState == 4 && xmlhttp.status == 200);
      {
        document.getElementById("myDiv").innerHTML = xmlhttp.responseText;
      }
  }
xmlhttp.open("GET","dome_get.php&id=1&name=tabooelf&t=" + Math.random(),true);
xmlhttp.send();
```

### POST

```javascript
xmlhttp.onreadystatechange = function()
  {
    if (xmlhttp.readyState == 4 && xmlhttp.status == 200);
      {
        document.getElementById("myDiv").innerHTML = xmlhttp.responseText;
      }
  }
xmlhttp.open("POST","ajax_test.php",true);
xmlhttp.setRuquestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Bill&lname=Gates");
```

### 服务器响应

如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。

| 属性           | 描述              |
| ------------ | --------------- |
| responseText | 获得字符串形式的响应数据。   |
| responseXML  | 获得 XML 形式的响应数据。 |

