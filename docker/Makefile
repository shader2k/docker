#!/usr/bin/make
# Makefile readme (ru): <http://linux.yaroslavl.ru/docs/prog/gnu_make_3-79_russian_manual.html>
# Makefile readme (en): <https://www.gnu.org/software/make/manual/html_node/index.html#SEC_Contents>

CURRENT_USER = $(shell id -u):$(shell id -g)
DC_BIN := $(shell command -v docker-compose 2> /dev/null)
# Включаем .env
envfile = .env
include $(envfile)
export $(shell sed 's/=.*//' $(envfile))

COMPOSE_YML = \
        -f docker-compose.yml

-include .env



up: ## Создание и запуск контейнеров приложения
	CURRENT_USER=$(CURRENT_USER) $(DC_BIN) ${COMPOSE_YML} up --detach


down: ## Stop and remove containers, networks, images, and volumes
	$(DC_BIN) ${COMPOSE_YML} down

restart: down up ## рестарт контейнеров

bash:
	@docker exec -it "${COMPOSE_PROJECT_NAME}_php_1" bash

docker-build: ## docker build
	@docker-compose ${COMPOSE_YML} build --build-arg CURRENT_USER=$$(id -u) php
	@docker-compose ${COMPOSE_YML} build --build-arg CURRENT_USER=$$(id -u) mariadb
	@docker-compose ${COMPOSE_YML} build --build-arg CURRENT_USER=$$(id -u) nginx

composer-install:
	@docker exec -it ${COMPOSE_PROJECT_NAME}_php_1 composer install

composer-install-laravel:
	@docker exec -it ${COMPOSE_PROJECT_NAME}_php_1 composer create-project laravel/laravel . --prefer-dist


