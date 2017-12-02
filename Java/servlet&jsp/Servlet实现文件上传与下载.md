# Servlet实现文件下载(使用ServletContext与Commons.io包实现)
    `
    // 获取图片文件名称
        String filename = request.getParameter("filename");
        // 获取ServletContext对象
        ServletContext servletContext = getServletContext();
        // 获取Mime类型
        String mimeType = servletContext.getMimeType("filename");
        // 设置Content-type
        response.setContentType(mimeType);
        response.setHeader("Content-Disposition","attachment;filename=" + filename);
        
        InputStream inputStream = servletContext.getResourceAsStream("/WEB-INF/downloads/" + filename);

        ServletOutputStream outputStream = response.getOutputStream();
        // 转换流
        IOUtils.copy(inputStream, outputStream);
        // 关闭流
        IOUtils.closeQuietly(inputStream);
        IOUtils.closeQuietly(outputStream);
    `
# Servlet实现文件上传（使用Part类实现）
    `
        //设置form表单enctype值为multipart/form-data
        // 在servlet上方写上MultipartConfig()注解，并指定路径
        request.setCharacterEncoding("utf-8");
        Part part = request.getPart(filename);
        String header = part.getHeader("Content-Disposition");
        String fileName = header.subString(header.indexOf("filename=\"") + "filename=\"".length, header.lastIndexOf("\""));
        part.write(fileName);

    `