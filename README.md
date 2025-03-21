# Reflection Modul 6
 Filbert Aurelian Tjiaranata
 2306152336 / AdPro B
 ---
 ## Contents
 
 1. [Commit 1 Reflection](##commit-1-reflection)
 2. [Commit 2 Reflection](##commit-2-reflection)
 3. [Commit 3 Reflection](##commit-3-reflection)
 4. [Commit 4 Reflection](##commit-4-reflection)
 
 ---

 ## Commit 1 Reflection
 For this assignment, I built a minimalistic HTTP server in Rust. I started by creating a new Rust project using `cargo new hello` and setting up GitHub for version control.
 
 The server utilizes Rust’s standard networking libraries:
 - **TcpListener**: Binds to `127.0.0.1:7878` to listen for incoming connections.
 - **TcpStream**: Handles communication with clients.
 - **BufReader**: Wraps the TCP stream for efficient I/O operations.

 The implementation consists of a main function that initializes the listener and continuously processes incoming connections. Each connection is passed to the 1 function, which reads the HTTP request headers.
 
 Inside `handle_connection`, the incoming stream is wrapped in a `BufReader` to allow efficient line-by-line reading. The function collects all request lines into a `Vec<String>`, stopping when an empty line is encountered, which signifies the end of the headers. The request data is then printed to provide insight into what the server receives from the client.
 
 TL;DR. This basic implementation helps me understand Rust’s networking capabilities.

 ## Commit 2 Reflection
 In this commit, I improved the server to serve actual HTML content instead of merely logging requests. This marks a significant step toward building a functional web server.
 
 ### Changes:
 1. **File System Integration**  
    Introduced the `fs` module to read HTML content from the file system using `fs::read_to_string()`.
   
 2. **HTTP Response Generation**  
    Constructed a valid HTTP response consisting of:
    - A status line: `HTTP/1.1 200 OK`
    - A `Content-Length` header indicating the response size
    - The actual HTML content read from `hello.html`

 3. **Content Serving**  
    Created a simple HTML file (`hello.html`) that the server serves to clients, allowing browsers to render a meaningful response.

 4. **Complete Request-Response Cycle**  
    Now, the server reads incoming HTTP requests, retrieves and formats the appropriate response, and sends it back to the client using `write_all()`.

 This update introduces the basics of serving static files and highlights the importance of correctly formatting HTTP responses for proper client compatibility. It also demonstrates how Rust’s standard library enables web server functionality without external dependencies.

 ![Commit 2 screen capture](/assets/images/commit2.png)
 
 ---

 ## Commit 3 Reflection
 In this commit, I implemented basic routing functionality, allowing the server to return different responses based on the requested URL path. This is an important improvement, making the server behave more like a real-world web server.

 ### Changes:
 1. **Request Path Handling**  
 Implemented logic to extract the request path from the HTTP request line to determine which content to serve.
 **Splitting Responses Based on the Requested Path**  
   - If the request is for the root path (`"/"`), the server serves `hello.html` with a `200 OK` status.  
   - If the request is for any other path, the server serves `404.html` with a `404 Not Found` status.  
   - This separation ensures that the server properly distinguishes between valid and invalid routes.

 2. **Error Handling for Invalid Requests**  
 Created a dedicated `404.html` file to improve the user experience when clients request non-existent resources.

 3. **Refactoring for Maintainability**  
   - Initially, response handling involved repetitive logic for determining status codes, reading files, and formatting responses.  
   - To improve this, I refactored the code using a **tuple** to store both the status line and filename before processing the response.  
   - This refactoring reduces redundancy, ensuring that response processing is handled in a single step instead of duplicating logic for different cases.  
   - By making the response handling modular, it becomes easier to extend the server to handle additional routes in the future.

 This update improves the server’s compliance with HTTP standards while maintaining clean and efficient routing logic using Rust’s pattern matching capabilities.

 ![Commit 3 screen capture](/assets/images/commit3.png)

 ---

 ## Commit 4 Reflection

 In this commit, I tested the limitations of a **single-threaded server**, revealing a significant performance bottleneck.  

 1. **Blocking Behavior**
 The server processes requests sequentially, meaning one slow request (like `/sleep`, which delays for 10 seconds) blocks all others.  
 2. **Request Queuing**
 Even a simple request to `/` gets stuck behind a long-running one, demonstrating poor scalability.  
 3. **Real-World Impact**
 In a production setting, this would degrade user experience, as one slow request could delay all others.  

 This test highlights the need for **multithreading**, which will allow the server to handle multiple requests concurrently, preventing delays caused by long-running tasks.