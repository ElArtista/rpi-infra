FROM nginx:stable-alpine
RUN set -ex \
 && sed -r -i '/location\s+\/\s+\{/a autoindex on;' /etc/nginx/conf.d/default.conf
