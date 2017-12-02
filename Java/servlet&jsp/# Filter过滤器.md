# Filter
> Filter作用:对请求与响应进行增强或拦截

### 创建一个Filter
* 实现Filter接口

### Filter生命周期
* 创建---第一次请求要过滤的资源
* 销毁---关闭web容器

### 常用方法
* doFilter()
* init()

### FilterConfig类
* getFilterName()
* getInitParameter(name) 在web.xml中进行配置<init-param>
* getInitParameterNames()

### web.xml配置
    `
    <filter>
        <filter-name></filter-name>
        <filter-class></filter-class>
    </filter>
    <filter-mapping>
        <filter-name></filter-name>
        <url-pattern>/*</url-pattern>或<servlet-name></servlet-name>指定过滤某个servlet
    </filter-mapping>
    `

### 应用
* struts2 中应用
* 权限校验
