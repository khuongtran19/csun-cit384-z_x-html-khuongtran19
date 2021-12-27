# Laboratory Assignment: x-html
A sample client and server component to process a x-html file

## Assignment

1. Create a client-side tool called, cit384-url, the can process the MIME type  application/x-html
2. Creae a server-side content-generator that can create a HTTP response for a x-html file.  

## Specification
1. cit384-url
   * parse the URL provided on the command line -- leave this for later
     - Usage: cit384-url  hostname port URI
   * make a call to DNS to get the IP address 
   * use the socket command to make a connection to the server
   * send a HTTP request
   * read the HTTP response
   * If it detects Content-type: applicaton/x-html
     - decode the body
     - uncompress the un-decoded body
     ```
     cat HTTP response body | base64 -d | uncompress -
     ```

1. x-html
   * modify the previously discussed plain-html code generater
   * check the size of the requested file
   * If the file is > $X_SIZE.  # You can set X_SIZE to 1024
     - modify the MIMI type
      ```
      Content-type: application/x-html
      ```
     - compress and then base64 encode the requested file
       ```
       cat filename.x-html | compress - | base64
       ```

## Notes
1. Build a simple server that returns a <blah>.x-html file
   - socket -s ${PORT_NUM} -f -q -l -p 'cat my.x-html'
     -   -s: a server-side socket is created on ${PORT}
     -   -f: fork a child process for each connection
     -   -q: quit: The connection is closed when an end-of-file condition occurs on stdin
     -   -l: loop to receive the next network connection
     -   -p: execute the supporting program: 'cat my.x-html'
1. Server information
  ```
  # See the simple server setup for the information needed
  HOSTNAME=localhost
  PORT=${PORT_NUM}
  ```
  
1. Build a simple client that requests a <blah>.x-html file, e.g., test-url
  ```
  #! /bin/bash
  socket ${HOSTNAME} ${PORT} ${URI} <<EOF
  GET $URI HTTP/1.1
  host: $HOSTNAME
  
  EOF
  ```
 
  
  
  ```

