# Cookie&Session
## Cookie
### 设置Cookie
    `
        Cookie cookie = new Cookie(key, value);
        // 设置Cookie的有效时间（以秒为单位）,如果不设置有效期，则在关闭浏览器时会自动删除
        cookie.setMaxAge(60*60*24);
        // 设置Cookie的有效路径
        cookie.setPath("/");
        // 把Cookie以响应头的形式发送给浏览器
        response.addCookie(cookie);

    `
### 获取Cookie
    `
        Cookie[] cookies = request.getCookies();
        for (Cookie c : cookies) {
            String name = c.getName();
            String value = c.getValue();
            System.out.println(name + ":" + value);
        }
    `

### 删除Cookie
    `
        // 把有效期设置为0即可删除Cookie
        cookie.setMaxAge(0);
        cookie.addCookie(cookie);

    `

## Session
### 创建Session
    `
        HttpSession session = request.getSession();
        session.setAttribute("name", "youqiang");
        session.setAttribute("addr", "nanjing");
    `
### 获取Session
    `
        HttpSession session = request.getSession();
        session.getAttribute("name");
        session.getAttribute("addr");
    `
### 销毁Session
    `
        HttpSession session = request.getSession();
        session.invalidate();
    `