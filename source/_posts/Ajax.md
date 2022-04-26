---
title: Ajax
category: Java
date: 2021-10-12 08:19:33
tags:
---

### Ajax

参考资料：[MDN-Ajax](https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started)

1. “异步”特性
   1. 定义：可以在不重新刷新页面的情况下与服务器通信，交换数据，或更新页面。
   2. 可以用来做什么：
      1. 在不重新加载页面的情况下发送请求给服务器。
      2. 接受并使用从服务器发来的数据。
2. 怎样发送http请求
3. 处理服务器响应
   1. 检查请求状态，如果状态的值是 `XMLHttpRequest.DONE` （对应的值是4），意味着服务器响应收到了并且是没问题的，然后就可以继续执行。
        ```javascript
        if (httpRequest.readyState === XMLHttpRequest.DONE) {
            // Everything is good, the response was received.
        } else {
            // Not ready yet.
        }
        ```
   2. 通过检查响应码 200 OK 判断AJAX有没有成功.
        ```javascript
        if (httpRequest.status === 200) {
            // Perfect!
        } else {
            // There was a problem with the request.
            // For example, the response may have a 404 (Not Found)
            // or 500 (Internal Server Error) response code.
        }
        ```
   3. 检查完请求状态 --> HTTP响应码 --> 访问使用用服务器返回的数据
      1.  `httpRequest.responseText` – 服务器以文本字符的形式返回
      2.  `httpRequest.responseXML` – 以 XMLDocument 对象方式返回，之后就可以使用JavaScript来处理
4. 例子(简单的HTTP请求,请求一个HTML文档并输出内容)
    ```html
    <!DOCTYPE html>
    <html lang="en">

    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>

    <body>
        <p>I'm a test</p>
        <button id="ajaxButton" type="button">Make a request</button>

        <script>
            (function () {
                var httpRequest;
                document.getElementById("ajaxButton").addEventListener('click', makeRequest);

                function makeRequest() {
                    httpRequest = new XMLHttpRequest();

                    if (!httpRequest) {
                        alert('Giving up :( Cannot create an XMLHTTP instance');
                        return false;
                    }
                    httpRequest.onreadystatechange = alertContents;
                    httpRequest.open('GET', 'test.html');
                    httpRequest.send();
                }

                function alertContents() {
                    try {
                        if (httpRequest.readyState === XMLHttpRequest.DONE) {
                            if (httpRequest.status === 200) {
                                alert(httpRequest.responseText);
                            } else {
                                alert('There was a problem with the request.');
                            }
                        }
                    }
                    catch (e) {
                        alert('Caught Exception: ' + e.description);
                    }
                }

            })();
        </script>

    </body>

    </html>

    ```
    在这个例子中：
    1. 用户点击 “Make a request” 按钮；
    2. 事件处理调用 `makeRequest()` 函数；
    3. 请求已通过然后（onreadystatechange）传给 `alertContents()` 执行。
    4. `alertContents()` 检查返回的响应是否OK，然后 `alert()` test.html 文件内容。
5. 