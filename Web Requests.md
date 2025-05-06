## Hyper Text Transfer Protocol (HTTP)
-  The term `hypertext` stands for text containing links to other resources and text that the readers can easily interpret.
## URL
Structure of a URL:
	http://admin:password@inlanefreight.com:80/dashboard.php?login=true#status

Here is what each component stands for:

|**Component**|**Example**|**Description**|
|---|---|---|
|`Scheme`|`http://` `https://`|This is used to identify the protocol being accessed by the client, and ends with a colon and a double slash (`://`)|
|`User Info`|`admin:password@`|This is an optional component that contains the credentials (separated by a colon `:`) used to authenticate to the host, and is separated from the host with an at sign (`@`)|
|`Host`|`inlanefreight.com`|The host signifies the resource location. This can be a hostname or an IP address|
|`Port`|`:80`|The `Port` is separated from the `Host` by a colon (`:`). If no port is specified, `http` schemes default to port `80` and `https` default to port `443`|
|`Path`|`/dashboard.php`|This points to the resource being accessed, which can be a file or a folder. If there is no path specified, the server returns the default index (e.g. `index.html`).|
|`Query String`|`?login=true`|The query string starts with a question mark (`?`), and consists of a parameter (e.g. `login`) and a value (e.g. `true`). Multiple parameters can be separated by an ampersand (`&`).|
|`Fragments`|`#status`|Fragments are processed by the browsers on the client-side to locate sections within the primary resource (e.g. a header or section on the page).|
## cURL
Used to send a basic HTTP request to any URL, Eg:
		curl inlanefreight.com
It doesn't render the HTML/JavaScript/CSS code but prints it as raw format.
It can be used to download a page or a file and output the content into a flag using the -O flag, if we want to specify the file name use -o, Eg:
		curl -O inlanefreight.com/index.html
In order to silent the status of a request use -s, Eg:
		curl -s -O inlanefreight.com/index.html
To skip certificate check in cURL use -k, Eg:
		curl -k https://inlanefreight.com

## HTTP Requests and Responses

![[Pasted image 20250506123215.png]]
The image above shows an HTTP GET request to the URL:

- `http://inlanefreight.com/users/login.html`

The first line of any HTTP request contains three main fields 'separated by spaces':

| **Field** | **Example**         | **Description**                                                                                                       |
| --------- | ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `Method`  | `GET`               | The HTTP method or verb, which specifies the type of action to perform.                                               |
| `Path`    | `/users/login.html` | The path to the resource being accessed. This field can also be suffixed with a query string (e.g. `?username=user`). |
| `Version` | `HTTP/1.1`          | The third and final field is used to denote the HTTP version.                                                         |
The next set of lines contain HTTP header value pairs, like `Host`, `User-Agent`, `Cookie`, and many other possible headers. These headers are used to specify various attributes of a request. The headers are terminated with a new line, which is necessary for the server to validate the request. Finally, a request may end with the request body and data.
## HTTP Response

Once the server processes our request, it sends its response. The following is an example HTTP response:

![HTTP response details: Version 'HTTP/1.1', status '200 OK'. Headers include date, server 'Apache/2.4.41', set-cookie 'PHPSESSID=m4u64rqlpfthrvvb12ai9voqgf', and content-type 'text/html; charset=UTF-8'.](https://academy.hackthebox.com/storage/modules/35/raw_response.png)
The first line of an HTTP response contains two fields separated by spaces. The first being the `HTTP version` (e.g. `HTTP/1.1`), and the second denotes the `HTTP response code` (e.g. `200 OK`).

Response codes are used to determine the request's status. After the first line, the response lists its headers, similar to an HTTP request.

Finally, the response may end with a response body, which is separated by a new line after the headers. The response body is usually defined as `HTML` code. However, it can also respond with other code types such as `JSON`, website resources such as images, style sheets or scripts, or even a document such as a PDF document hosted on the webserver.

## HTTP Headers

Headers can have one or multiple values, appended after the header name and separated by a colon. We can divide headers into the following categories:

1. `General Headers`
2. `Entity Headers`
3. `Request Headers`
4. `Response Headers`
5. `Security Headers`

`General Headers`:

[General headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec4.html) are used in both HTTP requests and responses. They are contextual and are used to `describe the message rather than its contents`.

|**Header**|**Example**|**Description**|
|---|---|---|
|`Date`|`Date: Wed, 16 Feb 2022 10:38:44 GMT`|Holds the date and time at which the message originated. It's preferred to convert the time to the standard [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) time zone.|
|`Connection`|`Connection: close`|Dictates if the current network connection should stay alive after the request finishes. Two commonly used values for this header are `close` and `keep-alive`. The `close` value from either the client or server means that they would like to terminate the connection, while the `keep-alive` header indicates that the connection should remain open to receive more data and input.|

`Entity Headers`:

Similar to general headers, [Entity Headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec7.html) can be `common to both the request and response`. These headers are used to `describe the content` (entity) transferred by a message. They are usually found in responses and POST or PUT requests.

|**Header**|**Example**|**Description**|
|---|---|---|
|`Content-Type`|`Content-Type: text/html`|Used to describe the type of resource being transferred. The value is automatically added by the browsers on the client-side and returned in the server response. The `charset` field denotes the encoding standard, such as [UTF-8](https://en.wikipedia.org/wiki/UTF-8).|
|`Media-Type`|`Media-Type: application/pdf`|The `media-type` is similar to `Content-Type`, and describes the data being transferred. This header can play a crucial role in making the server interpret our input. The `charset` field may also be used with this header.|
|`Boundary`|`boundary="b4e4fbd93540"`|Acts as a marker to separate content when there is more than one in the same message. For example, within a form data, this boundary gets used as `--b4e4fbd93540` to separate different parts of the form.|
|`Content-Length`|`Content-Length: 385`|Holds the size of the entity being passed. This header is necessary as the server uses it to read data from the message body, and is automatically generated by the browser and tools like cURL.|
|`Content-Encoding`|`Content-Encoding: gzip`|Data can undergo multiple transformations before being passed. For example, large amounts of data can be compressed to reduce the message size. The type of encoding being used should be specified using the `Content-Encoding` header.|

## Request Headers:

The client sends [Request Headers](https://tools.ietf.org/html/rfc2616) in an HTTP transaction. These headers are `used in an HTTP request and do not relate to the content` of the message. The following headers are commonly seen in HTTP requests.

|**Header**|**Example**|**Description**|
|---|---|---|
|`Host`|`Host: www.inlanefreight.com`|Used to specify the host being queried for the resource. This can be a domain name or an IP address. HTTP servers can be configured to host different websites, which are revealed based on the hostname. This makes the host header an important enumeration target, as it can indicate the existence of other hosts on the target server.|
|`User-Agent`|`User-Agent: curl/7.77.0`|The `User-Agent` header is used to describe the client requesting resources. This header can reveal a lot about the client, such as the browser, its version, and the operating system.|
|`Referer`|`Referer: http://www.inlanefreight.com/`|Denotes where the current request is coming from. For example, clicking a link from Google search results would make `https://google.com` the referer. Trusting this header can be dangerous as it can be easily manipulated, leading to unintended consequences.|
|`Accept`|`Accept: */*`|The `Accept` header describes which media types the client can understand. It can contain multiple media types separated by commas. The `*/*` value signifies that all media types are accepted.|
|`Cookie`|`Cookie: PHPSESSID=b4e4fbd93540`|Contains cookie-value pairs in the format `name=value`. A [cookie](https://en.wikipedia.org/wiki/HTTP_cookie) is a piece of data stored on the client-side and on the server, which acts as an identifier. These are passed to the server per request, thus maintaining the client's access. Cookies can also serve other purposes, such as saving user preferences or session tracking. There can be multiple cookies in a single header separated by a semi-colon.|
|`Authorization`|`Authorization: BASIC cGFzc3dvcmQK`|Another method for the server to identify clients. After successful authentication, the server returns a token unique to the client. Unlike cookies, tokens are stored only on the client-side and retrieved by the server per request. There are multiple types of authentication types based on the webserver and application type used.|

## Response Headers

[Response Headers](https://tools.ietf.org/html/rfc7231#section-7) can be `used in an HTTP response and do not relate to the content`. Certain response headers such as `Age`, `Location`, and `Server` are used to provide more context about the response. The following headers are commonly seen in HTTP responses.

|**Header**|**Example**|**Description**|
|---|---|---|
|`Server`|`Server: Apache/2.2.14 (Win32)`|Contains information about the HTTP server, which processed the request. It can be used to gain information about the server, such as its version, and enumerate it further.|
|`Set-Cookie`|`Set-Cookie: PHPSESSID=b4e4fbd93540`|Contains the cookies needed for client identification. Browsers parse the cookies and store them for future requests. This header follows the same format as the `Cookie` request header.|
|`WWW-Authenticate`|`WWW-Authenticate: BASIC realm="localhost"`|Notifies the client about the type of authentication required to access the requested resource.|
## Security Headers

Finally, we have [Security Headers](https://owasp.org/www-project-secure-headers/). With the increase in the variety of browsers and web-based attacks, defining certain headers that enhanced security was necessary. HTTP Security headers are `a class of response headers used to specify certain rules and policies` to be followed by the browser while accessing the website.

| **Header**                  | **Example**                                   | **Description**                                                                                                                                                                                                                                                                                                                             |
| --------------------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Content-Security-Policy`   | `Content-Security-Policy: script-src 'self'`  | Dictates the website's policy towards externally injected resources. This could be JavaScript code as well as script resources. This header instructs the browser to accept resources only from certain trusted domains, hence preventing attacks such as [Cross-site scripting (XSS)](https://en.wikipedia.org/wiki/Cross-site_scripting). |
| `Strict-Transport-Security` | `Strict-Transport-Security: max-age=31536000` | Prevents the browser from accessing the website over the plaintext HTTP protocol, and forces all communication to be carried over the secure HTTPS protocol. This prevents attackers from sniffing web traffic and accessing protected information such as passwords or other sensitive data.                                               |
| `Referrer-Policy`           | `Referrer-Policy: origin`                     | Dictates whether the browser should include the value specified via the `Referer` header or not. It can help in avoiding disclosing sensitive URLs and information while browsing the website.                                                                                                                                              |