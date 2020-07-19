# docker-teampass
**Docker image of Teampass password manager with fixed API access**

*Teampass is a Collaborative Passwords Manager - https://teampass.net, https://github.com/nilsteampassnet/TeamPass*

Based on teampass/teampass image, but with fixed API access:

```
RUN sed -i "/^}/i \
  location /api/ {\
          try_files $uri $uri/ /api/index.php?$args;\
  }" /etc/nginx/sites-enabled/default.conf
```

changed to

```
RUN sed -E -i '/^}/i\        location /api/ {' /etc/nginx/sites-enabled/default.conf && \
  sed -E -i '/^}/i\                try_files $uri $uri/ /api/index.php?$args;' /etc/nginx/sites-enabled/default.conf && \
  sed -E -i '/^}/i\        }' /etc/nginx/sites-enabled/default.conf 
```
