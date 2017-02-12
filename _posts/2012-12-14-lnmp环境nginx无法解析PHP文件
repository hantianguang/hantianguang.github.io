lnmp环境nginx无法解析PHP文件，html正常解析。
出现nginx无法解析php显示404 Not Found
一键安装lnmp环境，内含nginx。
首先先安装php-fpm,
yum install php-fpm
service php-fpm start    #启动 php-fpm
然后修改nginx配置文件nginx.conf 识别php
 vi /usr/local/nginx/conf/nginx.conf，如下把之前的#给去掉就可以了，顺手改一下fastcgi_param
   location ~ \.php$ {
       root           html;
       fastcgi_pass   127.0.0.1:9000;
       fastcgi_index  index.php;
       fastcgi_param SCRIPT_FILENAME /usr/share/nginx/html/$fastcgi_script_name;
       include        fastcgi_params;
    }


最后重启nginx和php-fpm。
service nginx restart
service php-fpm restart
至此即可显示成功。

附件本人nginx配置文件nginx.conf

#user  nobody;
worker_processes  1;


#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;


#pid        logs/nginx.pid;




events {
    worker_connections  1024;
}




http {
    include       mime.types;
    default_type  application/octet-stream;


    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';


    #access_log  logs/access.log  main;


    sendfile        on;
    #tcp_nopush     on;


    #keepalive_timeout  0;
    keepalive_timeout  65;


    #gzip  on;
    autoindex on;
    #fastcgi_intercept_errors on;
    server {
listen 80;
index index.php index.html index.htm;
        server_name  localhost;
root /usr/share/nginx/html;
#error_page 404 = /404.html;
        #charset koi8-r;


        #access_log  logs/host.access.log  main;


        location / {
            root   /usr/share/nginx/html;
            index index.php index.html index.htm;
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
        location ~ \.php$ {
   #fastcgi_split_path_info ^(.+\.php)(/.+)$;
            root          /usr/share/nginx/html;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME /usr/share/nginx/html/$fastcgi_script_name;
            include        fastcgi_params;
#$document_root
        }


        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }




    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;


    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}




    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;


    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;


    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;


    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;


    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


}
rtmp {    
    
    server {    
    
        listen 1937;  #鐩戝惉鐨勭鍙? 
    
        chunk_size 4000;    
          
           
        application hls {  #rtmp鎺ㄦ祦璇锋眰璺緞  
            live on;    
            hls on;    
            hls_path /usr/share/nginx/html/hls;    
            hls_fragment 5s;    
        }    
    }    
}
