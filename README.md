## Contents

1. [Architecture](#architecture)
2. [Setup env var](#setup)
3. [Install ansible and dependencies](#install-ansible-and-docker)
4. [Run](#run)


We use nginx as an entrypoint to decide whether requests are routed to authorization server (oauth2_proxy) or resource (elk). If request doesn't have authorization cookies, it will be redirected to authorization server which then delegates the process to google. And base on the result of the user authentication, toke exchange or login page redirection will happen.

### reference
1. [oauth2_proxy](https://github.com/oauth2-proxy/oauth2-proxy)
2. [elk docker](https://github.com/deviantony/docker-elk)
3. [design idea](https://developers.shopware.com/blog/2015/03/02/sso-with-nginx-authrequest-module/)

## setup
Set up env var in file /etc/environment

* GOOGLE\_CLIENT\_ID: xxxxxx
* GOOGLE\_CLIENT\_SECRET: xxxxxx
* EMAIL_DOMAIN_1: xxxx
* EMAIL_DOMAIN_2: xxxx
* SERVER_NAME: xxxx (eg: elk.example.com)

## install ansible and docker
* `sudo apt install python3-pip`
* `pip3 install ansible`
* `pip3 install docker`
* `pip3 install docker-compose`

## run
This playbook will install, configure and bootstrap:
* nginx
* oauth2_proxy
* elk

`ansible-playbook elk-playbook.yml`
