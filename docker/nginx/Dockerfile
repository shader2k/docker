FROM nginx:1.17

ARG CURRENT_USER

RUN usermod -u ${CURRENT_USER? invalid argument} www-data
RUN groupmod -g ${CURRENT_USER? invalid argument} www-data

COPY ./conf.d /etc/nginx/conf.d/
