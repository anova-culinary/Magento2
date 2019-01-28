![Magento 2](https://cdn.rawgit.com/rafaelstz/magento2-snippets-visualstudio/master/images/icon.png)

#  Magento 2 Docker to Development

### Apache 2.4 + PHP 7.2 + OPCache + MariaDB + N98 Magerun 2 + XDebug + Redis + Varnish

### Requirements

**MacOS:**

Install [Docker](https://docs.docker.com/docker-for-mac/install/), [Docker-compose](https://docs.docker.com/compose/install/#install-compose)

**Windows:**

Install [Docker](https://docs.docker.com/docker-for-windows/install/), [Docker-compose](https://docs.docker.com/compose/install/#install-compose)

**Linux:**

Install [Docker](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/) and [Docker-compose](https://docs.docker.com/compose/install/#install-compose)

### Install Magento 2 as new project

Follow official Magento 2 installation documentation. In env.sample.php file you can find 
server' names for `redis`, `redis-session` or `db`

Basically, it's a couple of next commands:
1) `git clone https://github.com/anova-culinary/monorepo.git src`
2) `./composer install`
3) probably you will receive `vertex` issue, just run `./composer update vertex/module-tax`, it's Magento 2.+ internal issue
4) `./magento setup:install --base-url=http://anova.lc/ \
    --admin-user='admin' --admin-firstname='First' \
    --admin-lastname='Last' --admin-password='qwertyQWE123' --language=en_US \
    --currency=USD --timezone=America/Los_Angeles --cleanup-database \
    --admin-email='admin-magento@anovaculinary.com' --use-rewrites=1 --session-save=db \
    --db-host=db --db-name="magento" --db-user="magento"  --db-password="magento" \
    --backend-frontname="admin"`

### Setup Magento 2 from already existed DB dump and magento configuration

If you want to setup your Magento2 from DB dump and configuration, you need just couple of files:
1) `./web_server/setup/anova.sql`, be sure that you have a right dump with `SET sql_mode='NO_AUTO_VALUE_ON_ZERO';` inside.
2) `./web_server/setup/config.php.sample` - with enabled or disabled modules
3) `./web_server/setup/env.php.sample` - you can find sample server config in root folder

#####Execute in your terminal `bash bin/setup`

Add anova.lc and jp.anova.lc to your `/etc/hosts` file

After installation be sure that DB installed. If DB is empty, you can execute next command
```docker-compose exec apache importdb```
This command will import anova.sql database from magento root dir (local is ./src/magento, docker is apache container /var/www/html)  

### Tools
You can copy tools to check environment: `cp -r ./stools ./src/magento/stools`
+ OPCache status checker: http://anova.lc/stools/opcache.php
+ Reset OPCache: http://anova.lc/stools/opcache-reset.php
+ phpinfo(): http://anova.lc/stools/phpinfo.php
+ Check Magento2 required extensions and mods: http://anova.lc/stools/magento-check.php

### Panels

Enjoy your new panels!

**Web server:** http://anova.lc/ or http://localhost

**PHPMyAdmin:** http://localhost:8080

**Local emails:** http://localhost:8025

### Features commands

| Commands  | Description  | Options & Examples |
|---|---|---|
| `./bin/setup ` | If you want to setup Anovaculinary project on your local machine with ./env/anova.sql DB data | |
| `./start`  | If you continuing not using the CURL you can start your container manually  | |
| `./stop`  | Stop your project containers  | |
| `./kill`  | Stops containers and removes containers, networks, volumes, and images created to the specific project  | |
| `./shell`  | Access your container  | `./shell root` | |
| `./magento`  | Use the power of the Magento CLI  | |
| `./n98`  | Use the Magerun commands as you want | |
| `./grunt-init`  | Prepare to use Grunt  | |
| `./grunt`  | Use Grunt specifically in your theme or completely, it'll do the deploy and the watcher.  | `./grunt luma` |
| `./xdebug`  |  Enable / Disable the XDebug | |
| `./composer`  |  Use Composer commands | `./composer update` |

### License

MIT © 2018 [Rafael Corrêa Gomes](https://github.com/rafaelstz/) and [contributors](https://github.com/clean-docker/Magento2/graphs/contributors).
