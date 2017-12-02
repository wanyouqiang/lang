# EL&JSTL&MVC设计模式
## EL(Expression Language)表达式语言
>相对于<%=%>,el表达式是JSP中的一项技术，el表达式的出现解决了方便获取与操作WEB容器中的数据

### 分别获取四个域中的值的内置对象
* ${applicationScope.x} <=> application.getAttribute("x")
* ${requestScope.x} <=> request.getAttribute("x")
* ${pageScope.x} <=> pageContext.getAttribute("x")
* ${sessionScope.x} <=> session.getAttribute("x")
* ${x} <=> findAttribute("x")
### 分别使用EL获取基本数据类型与引用数据类型数据

### 使用EL执行运算
* 算术运算 + - 、 /
* 逻辑运算 &&(and) ||(or) !(not)
* 比较运算 >= <= > < == !=
* 判断是否为空 empty
* 三元运算 empty xx ? xx : "some string";

### 获取WEB常用对象
* applicationScope
* pageScope
* sessionScope
* requestScope
* param  <=> request.getParameter()
* paramValues <=> request.getParameterValues()
* header
* headerValues
* cookie
* pageContext
* initParam 在web.xml中配置<context-param>相当于ServletContext.getInitParameter()方法

## JSTL的核心标签库使用
### 实现分支结构(if)
* <c:if test="关系表达式" var="name" scope="域">标签内容</c:if>
    * test要根据关系表达式的值来判断是否执行标签内容
    * var指定一个变量名称，保存test中的值（true/false）
    * scope指定要保存的域（page,request,session,application）
*    `<c:choose>
         <c:when test=""></c:when>
         <c:when test=""></c:when>
         <c:otherwise>参数不正确！</c:otherwise>
    </c:choose>
`

### set与out标签
* <c:set var="name" value="${name}" scope="域" ></c:set> 
    * var:要设置的变量名称
    * value:要设置的变量值
    * scope:要存在的域（page,session,application,request）
* <c:set target="" property="" value=""></c:set> 根据已有的对象设置值
* <c:out value="${xx}" default="" escapeXml="true"></c:out>
    * escapeXml把value中的值相关字符转义HTML实体字符


### 实现循环功能(forEach)
    `
        <c:forEach>
        begin:开始位置
        end:结束位置
        step:步长
        items:要遍历的集合
        var:要将当前换代元素存入web域中变量名称
        varStatus:要存入web域中状态名称
            count:当前换代次数
            index:索引号
            first:是否是第一次迭代
            last:是否是最后一次迭代
        </c:forEach>

    `



