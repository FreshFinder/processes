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

Make sure to update your nginx file locally, located at: `/usr/local/etc/nginx/nginx.conf` with the server configurations from the `nginx.conf` file in this repo.

