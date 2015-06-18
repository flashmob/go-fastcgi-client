Go fastcgi client

Usage: [go ](http://www.mysqlab.net/blog/2012/06/golang-fastcgi-client/)http://www.mysqlab.net/blog/2012/06/golang-fastcgi-client/

```

func main() {
        reqParams := "name=value"

        env := make(map[string]string)
        env["REQUEST_METHOD"] = "GET"
        env["SCRIPT_FILENAME"] = "/Users/ivan/work/test/fcgi/test.php"
        env["SERVER_SOFTWARE"] = "go / fcgiclient "
        env["REMOTE_ADDR"] = "127.0.0.1"
        env["SERVER_PROTOCOL"] = "HTTP/1.1"
        env["QUERY_STRING"] = reqParams

        fcgi, err := fcgiclient.New("127.0.0.1", 9000)
        if err != nil {
                fmt.Printf("err: %v", err)
        }

        content, err := fcgi.Request(env, reqParams)
        if err != nil {
                fmt.Printf("err: %v", err)
        }

        fmt.Printf("content: %s", content)
}

```