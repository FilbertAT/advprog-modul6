# Reflection Modul 6
 Filbert Aurelian Tjiaranata
 2306152336 / AdPro B
 ---
 ## Contents
 
 1. [Commit 1 Reflection](##commit-1-reflection)
 2. [Commit 2 Reflection](##commit-2-reflection)
 
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
 
 ### Enhancements:
 
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