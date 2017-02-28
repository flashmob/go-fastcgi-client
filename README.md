# go-fastcgi-client
Automatically exported from code.google.com/p/go-fastcgi-client

This repo is for archive only.

A better one, see https://github.com/tomasen/fcgi_client

# Purpose
This package is useful if you want to call some script (eg. php) from Go. Instead of invoking it via CLI, you can invoke it through FastCGI (php-fpm). 

# Example
Call a php script

```go

import (
  "github.com/flashmob/go-fastcgi-client"
   "net/url"
)

func main() {
  var email = make(map[string]string, 5)
  email["mail_id"] = "1"
  v := url.Values{}
  v.Set("mail_id", email["mail_id"])
  reqParams := v.Encode()
  env := make(map[string]string)
  env["REQUEST_METHOD"] = "GET"
  env["SCRIPT_FILENAME"] = "/path/to/scripts/example.php"
  env["SERVER_SOFTWARE"] = "go / fcgiclient "
  env["REMOTE_ADDR"] = "127.0.0.1"
  env["SERVER_PROTOCOL"] = "HTTP/1.1"
  env["QUERY_STRING"] = reqParams
  fcgi, err := fcgiclient.New("127.0.0.1", 9000)
  if err != nil {
  	fmt.Printf("err: %v", err)
  }
  //fmt.Println("%v", reqParams)
  content,  err := fcgi.Request(env, reqParams)
  if err != nil {
  	fmt.Printf("err: %v, %v", err)
  }
  fmt.Printf("content: %s", content)
}

```
