### Raspberry Pi

<p>install nginx server, start deamon process then
 open localhost in a browser</p>

```bash
    sudo apt-get install nginx
    sudo nginx

    sudo nano test.app
```
<p>create node server as a child process for nginx then go localhost:3000</p>

```javascript
    http=require('http');
    var server  = http.createServer(function(req,res)=>{
        res.writeHead(200,{'Content-Type': 'text/html'});
        res.write('<html><body><h1>Hello Pi from Node</h1></body></html>');
        res.end();
    });
    server.listen(3000);
    console.log('Server listening port 3000');
```  
```bash
    sudo nano  /etc/nginx/nginx.conf
```
<p>at first commmnen two files  with "#" then type  configurations below</p>

```bash
    #  include  /etc /nginx/conf.d/*.conf
    #  incluse  /etc/nginx/site-enabled/*;

    upstream node{
        server 127.0.0.1:3000
    }
    server{
        listen 80;
        root /usr/share/nginx/www;
        try_files $uri @ode;
        location @node{
            proxy_redirect off;
            proxy_pass http://node;
        }
    }
```

