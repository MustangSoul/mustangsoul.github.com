---
layout:     post
title:      "黑板"
subtitle:   "工具"
date:       2015-09-24 19:00:00
author:     "ZhouYan"
header-img: "img/post-bg-05.jpg"
---

    upstream yanzhourd1.rdlab_partner.mlservice {
        server 127.0.0.1:9981;
    }
    server {
        charset utf-8;
        index index.php;
        listen    80;
        server_name  partner.mlservice.yanzhourd1.rdlab.meilishuo.com;
        client_header_buffer_size 4096;
        root   /home/work/mlservice/partner/public;
        if ( $http_cookie ~* "(.*)$")
        {
            set $meilishuo_cookie $1;
        }
        access_log logs/yanzhourd1.rdlab/partner.mlservice-access.log mainweb;
        error_log  logs/yanzhourd1.rdlab/partner.mlservice-err.log  crit;

        location / {
         if (!-e $request_filename) {
                  rewrite ^(.*)$ /index.php last;
            }
            fastcgi_pass  yanzhourd1.rdlab_partner.mlservice;
            fastcgi_next_upstream error timeout invalid_header http_500;
            fastcgi_index index.php;
            include        fastcgi.conf;
        }
        location /index.php {
            fastcgi_pass  yanzhourd1.rdlab_partner.mlservice;
            fastcgi_next_upstream error timeout invalid_header http_500;
            fastcgi_index index.php;
            include        fastcgi.conf;
       }

        error_page   500 502 503 504  /404;
    }
