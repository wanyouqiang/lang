# Servlet
* Servlet执行流程，init()->service()->destory()，Servlet在第一次访问时会加载类，执行init()方法，其它访问都会重新开辟一条线程，调用Service()方法，关闭web服务器会调用destroy()方法
* web.xml的使用方法，在web.xml中进行Servlet访问映射与设置参数。