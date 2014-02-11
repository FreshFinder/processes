processes
=========

## Procfile to get processes running

Take this repo and place it in the root path of the meta-project.  For example,
your directories could look like:

```
farmsquare (this dir can be named whatever you'd like)
|\
| processes/
| frontend/
| to-the-market-api/
| reviews-api/
```

Install foreman if you don't have it already

```
gem install foreman
```

Then cd in to the processes directory (`cd processes`) run `foreman start` and
all the processes will launch

If you get an error about a port being taken already, run `lsof -i tcp:<port
that is taken>` and then go kill that process (`kill -9 <process_id>`).

Make sure to update your nginx file locally, located at: `/usr/local/etc/nginx/nginx.conf` with the following:

```
 server {
        listen       8080;
        server_name  localhost;
        location / {
          proxy_pass        http://127.0.0.1:3000;
          proxy_set_header  X-Real-IP  $remote_addr;
        }

        location /api/v1/reviews {
          proxy_pass        http://127.0.0.1:4567;
          proxy_set_header  X-Real-IP  $remote_addr;
        }

        location /api {
          proxy_pass        http://127.0.0.1:5555;
          proxy_set_header  X-Real-IP  $remote_addr;
        }


        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }

```
