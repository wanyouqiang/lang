# 使用Filter与自定义请求类实现乱码处理
## Filter相关内容（新建一个EncodingFilter实现Filter接口）
    `
    package com.youqiang.filter;

    import com.youqiang.servlet.MyRequest;
    import com.youqiang.servlet.MyServlet;

    import javax.servlet.*;
    import javax.servlet.annotation.WebFilter;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import java.io.IOException;

    /**
     * Created by youqiang on 2017/9/10.
     */
    @WebFilter(filterName = "CharacterEncodingFilter")
    public class CharacterEncodingFilter implements Filter {
        public void destroy() {
        }

        public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
            HttpServletRequest request = (HttpServletRequest) req;
            HttpServletResponse response = (HttpServletResponse) resp;

            // 设置响应编码类型为utf-8编码
            response.setContentType("text/html;charset=utf-8");

            MyRequest myRequest = new MyRequest(request);

            // 传递请求与响应
            chain.doFilter(myRequest, response);
        }

        public void init(FilterConfig config) throws ServletException {

        }

    }

    `
## 自定义请求类相关内容（新建一个MyRequest继承自HttpServletRequestWrapper类）
    `
    package com.youqiang.servlet;

    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletRequestWrapper;
    import java.io.UnsupportedEncodingException;
    import java.util.Map;
    import java.util.Set;

    /**
     * 自定义一个请求类继承自HttpServletRequestWrapper类
     * 分别重写requestParameter(),requestParameterMap(),requestParameterValues()实现字符编码转换
     * Created by youqiang on 2017/9/10.
     */
    public class MyRequest extends HttpServletRequestWrapper {
        private HttpServletRequest request;
        private boolean flag = false;

        public MyRequest(HttpServletRequest request) {
            super(request);
            this.request = request;
        }

        @Override
        public String getParameter(String name) {
            //return super.getParameter(name);
            // 调用本类中的getParameterMap()方法进行处理
            String res = null;
            Map<String, String[]> parameterMap = this.getParameterMap();
            for (Map.Entry<String, String[]> entry : parameterMap.entrySet()) {
                String key = entry.getKey();
                String[] values = entry.getValue();
                if (key.equals(name)) {
                    res = values[0];
                }
            }
            return res;
        }

        @Override
        public String[] getParameterValues(String name) {
            Map<String, String[]> parameterMap = this.getParameterMap();
            if (parameterMap == null) {
                return super.getParameterValues(name);
            } else {
                String[] values = parameterMap.get(name);
                return values;
            }
        }

        @Override
        public Map<String, String[]> getParameterMap() {
            String method = this.request.getMethod();
            if ("get".equalsIgnoreCase(method)) {
                // 如果是以get方式请求，进行编码转换
                Map<String, String[]> map = this.request.getParameterMap();
                if (flag) {
                    // 保证字符编码只转换一次，如果flag值为true,map中存放的是已经编码过的字符串，则不再进行编码转换
                    return map;
                }

                // 进行字符编码的转换
                Set<String> keys = map.keySet();
                for (String key : keys) {
                    String[] values = map.get(key);
                    for (int i = 0; i < values.length; i++) {
                        try {
                            String resValue = new String(values[i].getBytes("iso-8859-1"), "utf-8");
                            // 将转换后的字符串重新放回map中
                            values[i] = resValue;
                        } catch (UnsupportedEncodingException e) {
                            e.printStackTrace();
                        }
                    }
                }
                // 将flag设置为true
                flag = true;
                return map;

            } else if ("post".equalsIgnoreCase(method)) {
                // 如果是以post方式请求，进行编码转换
                try {
                    this.request.setCharacterEncoding("utf-8");
                } catch (UnsupportedEncodingException e) {
                    e.printStackTrace();
                }

                return this.request.getParameterMap();
            } else {
                // 如果请求的方法不是get与post，则使用父类的方法进行处理
                return super.getParameterMap();
            }
        }
    }

    `