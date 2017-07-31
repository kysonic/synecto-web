# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /var/run/nginx.pid;

events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    index   index.html index.htm;

    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  app.designmap.ru;
        return 301 https:/$server_name$request_uri;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        }

        # redirect server error pages to the static page /40x.html
        #
        error_page 404 /404.html;
        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
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

        server {
                    listen       443 ssl http2;
                    listen       [::]:443 ssl;
                    server_name  localhost;
                    root         /home/kysonic/synecto;
                    client_max_body_size 150m;
            #
                    ssl_certificate "/etc/letsencrypt/live/app.synecto.io/fullchain.pem";
                    ssl_certificate_key "/etc/letsencrypt/live/app.synecto.io/privkey.pem";
            #        # It is *strongly* recommended to generate unique DH parameters
            #        # Generate them with: openssl dhparam -out /etc/pki/nginx/dhparams.pem 2048
            #        #ssl_dhparam "/etc/pki/nginx/dhparams.pem";
            #        ssl_session_cache shared:SSL:1m;
            #        ssl_session_timeout  10m;
                    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
                    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!3DES:!MD5:!PSK;
            #        ssl_prefer_server_ciphers on;
            #
            #        # Load configuration files for the default server block.
            #        include /etc/nginx/default.d/*.conf;
            #
                    add_header Strict-Transport-Security max-age=15768000;
                    ssl_stapling on;
                     location / {
                            root /home/kysonic/synecto;
                            index index.html;
                            try_files $uri /index.html =404;
                     }

            #
            #        error_page 404 /404.html;
            #            location = /40x.html {
            #        }
            #
            #        error_page 500 502 503 504 /50x.html;
            #            location = /50x.html {
            #        }
                }



}