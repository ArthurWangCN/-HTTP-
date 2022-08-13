### 第六章 HTTP首部
HTTP协议的请求和响应报文中必定包含HTTP首部。首部内容为客户端和服务器分别处理请求和响应提供所需要的信息。

**HTTP请求报文**

在请求中，HTTP报文由方法、URI、HTTP版本、HTTP首部字段等部分构成。

示例：

```http
GET / HTTP/1.1
Host: hackr.jp
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:13.0) Gecko/=>
20100101 Firefox/13.0
Accept: text/html, application/xhtml+xml, application/xml; q=0.9, =>
*/*; q=0.8
Accept-Language: ja,en-us;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Connection: keep-alive
If-Modified-Since: Fri, 31 Aug 2007 02:02:20 GMT
If-None-Match: "45bae1-16a-46d776ac"
Cache-Control: max-age=0
```

**HTTP响应报文**

在响应中，HTTP报文由HTTP版本、状态码（数字和原因短语）、HTTP首部字段3部分构成。

示例：

```http
HTTP/1.1304 Not Modified
Date: Thu, 07 Jun 2012 07:21:36 GMT
Server: Apache
Connection: close
Etag: "45bae1-16a-46d776ac"
```

---

使用首部字段是为了给浏览器和服务器提供报文主体大小、所使用的语言、认证信息等内容。

HTTP首部字段是由首部字段名和字段值构成的，中间用冒号“:”分隔。

如：`Content-Type: text/html`。

字段值对应单个HTTP首部字段可以有多个值，如：`Keep-Alive: timeout=15, max=100`。

若HTTP首部字段重复，根据浏览器内部处理逻辑的不同，结果可能并不一致。


4种HTTP首部字段类型：

1. 通用首部字段
2. 请求首部字段
3. 响应首部字段
4. 实体首部字段

---

**通用首部字段**

通用首部字段是指，请求报文和响应报文双方都会使用的首部。

+ Cache-Control：操作缓存的工作机制；
+ Connection：控制不再转发给代理的首部字段、管理持久连接；
+ Date：表明创建HTTP报文的日期和时间；
+ Pragma：仅作为与HTTP/1.0的向后兼容而定义；
+ Trailer：事先说明在报文主体后记录了哪些首部字段；
+ Transfer-Encoding：规定了传输报文主体时采用的编码方式；
+ Upgrade：用于检测HTTP协议及其他协议是否可使用更高的版本进行通信；
+ Via：追踪客户端与服务器之间的请求和响应报文的传输路径；
+ Warning：告知用户一些与缓存相关的问题的警告。

---

**请求首部字段**

请求首部字段是从客户端往服务器端发送请求报文中所使用的字段，用于补充请求的附加信息、客户端信息、对响应内容相关的优先级等内容。

+ Accept：通知服务器用户代理能够处理的媒体类型及媒体类型的相对优先级。可使用type/subtype这种形式，一次指定多种媒体类型；
+ Accept-Charset：通知服务器用户代理支持的字符集及字符集的相对优先顺序；
+ Accept-Encoding：告知服务器用户代理支持的内容编码及内容编码的优先级顺序；
+ Accept-Language：告知服务器用户代理能够处理的自然语言集（指中文或英文等），以及自然语言集的相对优先级；
+ Authorization：用户代理的认证信息（证书值）；
+ Expect：告知服务器期望出现的某种特定行为；
+ From：告知服务器使用用户代理的用户的电子邮件地址；
+ Host：告知服务器请求的资源所处的互联网主机名和端口号（必须的首部字段）；
+ If-Match：形如If-xxx这种样式的请求首部字段，都可称为条件请求。服务器接收到附带条件的请求后，只有判断指定条件为真时，才会执行请求。服务器会比对If-Match的字段值和资源的ETag值，仅当两者一致时，才会执行请求；
+ If-Modified-Since：告知服务器若If-Modified-Since字段值早于资源的更新时间，则希望能处理该请求；
+ If-None-Match：用于指定If-None-Match字段值的实体标记（ETag）值与请求资源的ETag不一致时，它就告知服务器处理该请求；
+ If-Range：告知服务器若指定的If-Range字段值（ETag值或者时间）和请求资源的ETag值或时间相一致时，则作为范围请求处理。反之，则返回全体资源；
+ If-Unmodified-Since：指定的请求资源只有在字段值内指定的日期时间之后，未发生更新的情况下，才能处理请求；
+ Max-Forwards：通过TRACE方法或OPTIONS方法，发送包含首部字段Max-Forwards的请求时，该字段以十进制整数形式指定可经过的服务器最大数目；
+ Proxy-Authorization：认证行为发生在客户端与代理之间；
+ Range：获取部分资源的范围请求；
+ Referer：告知服务器请求的原始资源的URI；
+ TE：告知服务器客户端能够处理响应的传输编码方式及相对优先级。它和首部字段Accept-Encoding的功能很相像，但是用于传输编码；
+ User-Agent：将创建请求的浏览器和用户代理名称等信息传达给服务器。

---

**响应首部字段**

响应首部字段是由服务器端向客户端返回响应报文中所使用的字段，用于补充响应的附加信息、服务器信息，以及对客户端的附加要求等信息。

+ Accept-Ranges：告知客户端服务器是否能处理范围请求，以指定获取服务器端某个部分的资源。
+ Age：告知客户端源服务器在多久前创建了响应。字段值的单位为秒。
+ ETag：告知客户端实体标识。它是一种可将资源以字符串形式做唯一性标识的方式。服务器会为每份资源分配对应的ETag值。
+ Location：将响应接收方引导至某个与请求URI位置不同的资源。基本上，该字段会配合3xx:Redirection的响应，提供重定向的URI。
+ Proxy-Authenticate：把由代理服务器所要求的认证信息发送给客户端。
+ Retry-After：告知客户端应该在多久之后再次发送请求。主要配合状态码503 Service Unavailable响应，或3xx Redirect响应一起使用。
+ Server：告知客户端当前服务器上安装的HTTP服务器应用程序的信息。
+ Vary：对缓存进行控制。源服务器会向代理服务器传达关于本地缓存使用方法的命令。
+ WWW-Authenticate：用于HTTP访问认证。

---

**实体首部字段**

实体首部字段是包含在请求报文和响应报文中的实体部分所使用的首部，用于补充内容的更新时间等与实体相关的信息。

+ Allow：用于通知客户端能够支持Request-URI指定资源的所有HTTP方法。
+ Content-Encoding：告知客户端服务器对实体的主体部分选用的内容编码方式。内容编码是指在不丢失实体信息的前提下所进行的压缩。（gzip、compress、deflate、identity）
+ Content-Language：告知客户端实体主体使用的自然语言。
+ Content-Length：表明了实体主体部分的大小（单位是字节）。
+ Content-Location：给出与报文主体部分相对应的URI，与Location不同，表示的是报文主体返回资源对应的URI。
+ Content-MD5：是一串由MD5算法生成的值，其目的在于检查报文主体在传输过程中是否保持完整，以及确认传输到达。
+ Content-Range：针对范围请求，返回响应时使用的首部字段Content-Range，能告知客户端作为响应返回的实体的哪个部分符合范围请求。字段值以字节为单位，表示当前发送部分及整个实体大小。
+ Content-Type：说明了实体主体内对象的媒体类型。和首部字段Accept一样，字段值用type/subtype形式赋值。
+ Expires：首部字段Expires会将资源失效的日期告知客户端。
+ Last-Modified：指明资源最终修改的时间。

---

**为Cookie服务的首部字段**

Cookie的工作机制是用户识别及状态管理。Web网站为了管理用户的状态会通过Web浏览器，把一些数据临时写入用户的计算机内。接着当用户访问该Web网站时，可通过通信方式取回之前存放的Cookie。

**Set-Cookie**

```lua
Set-Cookie: status=enable; expires=Tue, 05 Jul 2011 07:26:31 GMT; =>
path=/; domain=.hackr.jp;
```

+ expires属性指定浏览器可发送Cookie的有效期。
+ path属性可用于限制指定Cookie的发送范围的文件目录。
+ domain属性指定的域名可做到与结尾匹配一致。
+ secure属性用于限制Web页面仅在HTTPS安全连接时，才可以发送Cookie。
+ HttpOnly属性是Cookie的扩展功能，它使JavaScript脚本无法获得Cookie，防止跨站脚本攻击（Cross-site scripting,XSS）对Cookie的信息窃取。

**Cookie**

```lua
Cookie: status=enable;
```

首部字段Cookie会告知服务器，当客户端想获得HTTP状态管理支持时，就会在请求中包含从服务器接收到的Cookie。接收到多个Cookie时，同样可以以多个Cookie形式发送。

---

**其他首部字段**

+ X-Frame-Options：用于控制网站内容在其他Web网站的Frame标签内的显示问题。其主要目的是为了防止点击劫持（clickjacking）攻击。
+ X-XSS-Protection：属于HTTP响应首部，它是针对跨站脚本攻击（XSS）的一种对策，用于控制浏览器XSS防护机制的开关。
+ DNT：属于HTTP请求首部，其中DNT是Do Not Track的简称，意为拒绝个人信息被收集，是表示拒绝被精准广告追踪的一种方法。
+ P3P：属于HTTP响应首部，通过利用P3P（The Platform for Privacy Preferences，在线隐私偏好平台）技术，可以让Web网站上的个人隐私变成一种仅供程序可理解的形式，以达到保护用户隐私的目的。



