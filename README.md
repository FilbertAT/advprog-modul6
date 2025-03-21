# Reflection Modul 6
 Filbert Aurelian Tjiaranata
 2306152336 / AdPro B
 ---
 ## Contents
 
 1. [Commit 1 Reflection](##commit-1-reflection)
 
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