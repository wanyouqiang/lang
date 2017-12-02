# AJAX 页面无刷新技术

### 使用JavaScript实现AJAX

* 使用GET方式实现AJAX
    `
        // 获取 XMLHttpRequest的实例
        var xmlhttp = new XMLHttpRequest();
        // 打开
        xmlhttp.open(请求的方法, url, 是否异步);
        // 发送
        xmlhttp.send();

        xmlhttp.onreadystatechange = function() {
            if (xmlhttp.readyState == 4 && xmlhttp.status = 200) {
                // AJAX请求全部完成，获取响应数据
                var data = xmlhttp.responseText;
                console.log(data);
            }
        }

    `

* 使用POST实现AJAX
    `
        var xmlhttp = new XMLHttpRequest();
        xmlhttp.open("POST"，url, 是否异步);
        xmlhttp.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
        xmlhttp.send("name=mike&gender=male");
    `

* 同步(true)与异步(false)区别
> 设置为异步，页面直接显示，无需等待，设置为同步，必须等待服务器响应完成后，才能进行其它操作，否则一直处于等待状态


### 使用JQuery实现AJAX
* $.ajax()
    `
        $.ajax({
            type:"get/post",
            async:true,
            url:"请求URL",
            success:function() {

            }

        });

    `

* $.get()
    `
        // data是{name:"mike", addr:"nanjing"}
        $.get("请求URL", data, function(data) {
            // 回调函数
            console.log(data);
        }, "json/text");
    `

* $.post()
    `
        // 与get方式参数一致
        $.post();
    `

### Java解析成JSON格式（flexjson.jar）
