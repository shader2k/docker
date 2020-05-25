FROM mariadb:10.5

RUN apt update && apt install pv

ARG CURRENT_USER

RUN usermod -u ${CURRENT_USER? invalid argument} mysql
RUN groupmod -g ${CURRENT_USER? invalid argument} mysql
