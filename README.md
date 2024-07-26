# Simple File Server Nginx
## Step by step Guide
### Step-1 Make a Directory 
- ``mkdir fileserver``
  
### Step-2 Go to that Directory
- ``cd fileserver``
  
### Step-3 Make a file
- ``nano default.config``


## Step-4 Copy paste this section

````
server {
    listen       80;  
    listen  [::]:80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        autoindex on;

    }

    #error_page  404              /404.html;
    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}
    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}
    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
````
### Step-5 Create a Docker Compose File
- ````nano docker-compose.yml````

## Step-6 copy paste this section
````
version: '3'
services:
  nginx:
    image: nginx:stable-alpine-slim
    volumes:
      - ./default.conf:/etc/nginx/conf.d/default.conf:ro
      - ./data/:/usr/share/nginx/html:ro 
    ports:
      - 80:80
````
### Step-7 Create a Directory named data 
- ``mkdir data``

### Step-8 Use this cmd to pull img
- ``docker-compose pull``

### Step-9 Use this cmd to create a container
- ``docker-compose up -d``

##you can upoload ,download ,create folder ,delete folder files using filezilla
