# Image of nginx
FROM jakmall/recruitment/cloud-engineer/counter/nginx

WORKDIR /var/www/html/public

# Create index.php
RUN touch /var/www/html/public/index.php
COPY ./public/favicon.ico .
COPY ./public/robots.txt .
