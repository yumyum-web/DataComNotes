# The Web and HTTP

## Structure of the Web

- **Resources**: Anything that can be named and accessed on the web.
- **URL**: Uniform Resource Locator. Identifies a resource on the web.
- **Web clients**: Retrieve resources from the web.
- **Web servers**: Store and provide resources to clients.
- **Web pages**: A resource that can be displayed in a client type called **web browsers**.
- **Hyperlinks**: Links between web pages. They are used to navigate the web.

## HTTP (Hypertext Transfer Protocol)

- Many versions, but HTTP/1.1 is the one discussed here.
- Webs application layer protocol is defined here. (Requires a reliable transport layer protocol.)
- Uses a client-server model.
  - **Client**: Requests resources.
  - **Server**: Respond with resources.
- Resoureces may reference other resources.

> E.g. A web page may reference images, stylesheets, scripts, etc.
> The client (browser) will make further requests to retrieve them.
> A webpage is rendered (displayed) by the browser when all resources are retrieved.

## HTTP Overview

- **Uses TCP** as the transport layer protocol.
  1. Client opens a TCP connection (a socket) to the server.
  2. Server accepts the connection.
  3. Data is exchanged, as HTTP messages (TCP does not concern with the content/structure of the data).
  4. Connection is closed.
- **Stateless**:
  - Each request is independent of the others inside the protocol.
  - The server does not maintain any state between requests.
  - State may be maintained at a higher level.

## HTTP Operation

1. Client sends a **request** to the server.
   1. Client initiates a TCP connection to the server.
   2. Server **accepts** the connection.
   3. Client sends a HTTP request message.
2. Server processes the request and sends a **response**.
   1. Server receives the request.
   2. Server sends a HTTP response message and closes the connection.
   3. Client receives the response.

> E.g. user visits a webpage using URL:
>
> 1. Browser sends a request (with URL) to the server for the webpage.
> 2. Server processes the request and sends the webpage as a response.
> 3. Browser sees other resources in the webpage and retrieves them.
> 4. Browser renders the webpage.

## HTTP Messages

- These are in plain text ASCII format (human-readable).

### Request

```http
POST /path/to/resource HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept-language: en-US
Content-Type: text/html

Hello, server!
```

| Part         | Description                        | Example                          |
| ------------ | ---------------------------------- | -------------------------------- |
| Request line | Method, URL, and HTTP version      | `GET /path/to/resource HTTP/1.1` |
| Header lines | Additional info as key-value pairs | `Host: www.example.com`          |
| Empty line   | Separates headers from body        |                                  |
| Body         | Optional data                      | `Hello, server!`                 |

#### Method Types

- **GET**: Retrieve a resource.
- **POST**: Send data to the server.
- **PUT**: Store a resource on the server.
- **DELETE**: Remove a resource from the server.
- **HEAD**: Retrieve only the headers of a resource.

### Response

```http
HTTP/1.1 200 OK
Connection: close
Date: Mon, 23 May 2005 22:38:34 GMT
Server: Apache/1.3.0 (Unix)
Content-Type: text/html
Content-Length: 35

<!DOCTYPE html><html>Hello, client!</html>
```

| Part         | Description                        | Example                                      |
| ------------ | ---------------------------------- | -------------------------------------------- |
| Status line  | HTTP version, status code, reason  | `HTTP/1.1 200 OK`                            |
| Header lines | Additional info as key-value pairs | `Server: Apache/1.3.0 (Unix)`                |
| Empty line   | Separates headers from body        |                                              |
| Body         | Optional data                      | `<!DOCTYPE html><html>Hello, client!</html>` |

#### Status Codes

- **200 OK**: Request succeeded.
- **301 Moved Permanently**: Resource has been moved permanently.
- **400 Bad Request**: Request is invalid.
- **404 Not Found**: Resource not found.
- **505 HTTP Version Not Supported**: Server does not support the HTTP version.

## Client-Server Communication Techniques/Patterns

### Sending Data to the Server

- **Post technique**: Send data in the body of the request.
- **URL technique**:
  - Send data with the URL as query parameters.
  - E.g. `GET /path/to/resource?data1=hello&data2=server HTTP/1.1`.

### Cookies

- Cookies are key-value pairs which are stored in the client's browser.
- They are **sent with each request** to the server.
  ```http
  Cookie: key1=value1; key2=value2
  ```
- Server can set cookies in the response. May include additional info like expiration date, domain, etc.
  ```http
  Set-Cookie: sessionId=abc123; Path=/; Secure; HttpOnly
  Set-Cookie: userId=xyz456; Expires=Wed, 09 Jun 2024 10:18:14 GMT; Path=/
  ```
- Browser stores them in a file known as a cookie jar.
- Servers use cookies and backend databases to maintain session state (e.g. user login).

#### Use Cases

- Authentication/Authorization.
- Shopping carts.
- Personalization.
- Tracking: Cookies can be used to track user activity across websites (privacy concerns).
- Recommendations.

### Web Caching

- **Caching**: Storing a copy of a resource to serve again without fetching from the server.
  - **Browser cache**: Stores resources on the client side.
  - **Proxy cache**: Stores resources on the server side.
- **Client-side caching**:
  - Client sends the `If-Modified-Since` header, so the server may respond with a `304 Not Modified` status code.
  ```http
  If-Modified-Since: Mon, 23 May 2005 22:38:34 GMT
  ```
- Benefits:
  - Shorter response times.
  - Reduced bandwidth usage.
  - Reduced load on the server.
  - Access control and logging.

### Natural Language Preferences

- **Accept-Language** header: Sent by the client to indicate the preferred languages.
  ```http
  Accept-Language: si-LK
  ```

## HTTPS (Hypertext Transfer Protocol Secure)

- In HTTP, requests/responses are sent in plain text, which is insecure (can be intercepted and **understood**).
- Benefits of HTTPS:
  - **Confidentiality**: Data is encrypted. (Prevents eavesdropping.)
  - **Integrity**: Data is not tampered with. (Prevents unauthorized modification.)
  - **Authentication**: Server is authenticated. Client may also be authenticated. (Prevents impersonation of a party.)

## Web Applications

- Associated with **Web 2.0**.
- Web site vs Web application:
  - **Web site**: Static content. No user interaction.
  - **Web application**: Dynamic content. User interaction.

## Search Engines

- A web application that helps users find information on the web.
- Examples: Google, Bing, Yahoo.
