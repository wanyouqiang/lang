# JSP
## JSP中常见的标签
* <%=%> expression(表达式标签)
* <% JAVA语句 %> scriplet（脚本标签）
* <%! %> declaration（定义标签）
* <%@ page %> directive （指令标签）
* <%--注释内容--%> comment （注释标签）不会被解释到.java文件中
## JSP指令
### page 告诉JSP引擎，怎么将JSP转换成Servlet
* import 引入Java类包
* language 指定语言Java
* contentType text/html;charset=UTF-8
* pageEncoding 当前页面编码格式
* autoFlush 自动刷新
* buffer response缓存区大小
* session 布尔值，与request.getSession(true/false)作用一致
* errorPage="error.jsp" 指定错误跳转页面，在实际开发中一般使用web.xml中<error-page>标签
### include 在当前JSP文件中包含其它JSP文件，最终解释成一个servlet类文件
### taglib

## JSP内置对象
* out 代表JspWriter中的一个对象，与response.getWriter()不同。
* session
* request
* response
* application(代表ServletContext的一个对象)
* config(同ServletConfig,获取服务器配置信息)
* page 代表当前通过JSP页面所解释成的Servlet对象
* pageContext 代表当前JSP的上下文，能够获取其它内置对象
    * setAttribute(key, value, PageContext.域)
    * getAttribute(key)
    * findAttribute(key) 可以从四个域中进行获取
* exception 要先设置isErrorPage="true"

## JSP域对象
* request------Request
* session------request.getSession()
* pageContext
* application------ServletContext

## JSP动态包含与静态包含
* 静态包含：<%@page include file="abc.jsp"%>
* 动态包含：<jsp:include page="abc.jsp">
* 静态包含与动态包含区别
    * 请求后生成的.java源码数量不同
    * 静态包含不允许定义相同的变量