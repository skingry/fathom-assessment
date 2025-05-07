FROM nginx

COPY default.conf /etc/nginx/conf.d/

ADD site /usr/share/nginx/html/
COPY probes /usr/share/nginx/probes

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
