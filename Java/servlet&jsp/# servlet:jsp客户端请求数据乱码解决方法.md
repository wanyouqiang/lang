# servlet/jsp客户端请求数据乱码解决方法
## 第一种方法
* 使用Urlencoder.encode()方法对请求信息进行iso-8859-1编码
* 使用Urldecoder.decode()方法对请求信息进行utf-8解码
## 第二种方法
* 使用字符串的getBytes("iso-8859-1")进行编码，然后使用new String(,"utf-8")进行解码
## 第三种方法
* 使用request.characterEncoding("utf-8")对post指定编码。
