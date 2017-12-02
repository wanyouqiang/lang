# ServletRequest
## 获取请求行
* getServletPath()
* getContextPath()
* getMethod()
* getQueryString()
* getProtocol()
## 获取请求头
* getHeader()
* getHeaderNames()
## 获取请求体
* getParameter()
* getParameterValues()
* getParameterMap()
* getParameterNames()
## 解决请求乱码
* setCharacterEncoding("utf-8")
* new String("中文".getBytes("iso-8859-1"), "utf-8")
## 设置请求转发 getRequestDispatcher() 获取RequestDispatcher对象，然后调用forWard(request, response)方法
# ServletResponse
## 设置响应头
* setHeader(key, value)
* setContentType("text/html;charset=utf-8") 解决响应乱码
## 设置响应体
* getWriter.print()