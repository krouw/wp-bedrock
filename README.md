# Wordpress Bedrock Docker

# USE THIS ONLY FOR LOCAL DEVELOPMENT!!!

## Install Bedrock


1. Run
`
docker-compose run composer create-project roots/bedrock .
`
for download bedrock in the latest version.

## Change src owner for www-data in host**

*src* folder is the root of the wordpress project, so we need to change the owner of the folder to www-data user in the host.
This folder is a volume in the docker-compose.yml file. For debian systems www-data has the id 33, so the USER:GROUP must be 33:33. For ubuntu/debian + Alpine see [https://gist.github.com/zdenekdrahos/53f16cfe902ff5f820a01b79e8c76a01](https://gist.github.com/zdenekdrahos/53f16cfe902ff5f820a01b79e8c76a01)

1. You can do this with docker. Run `docker-compose run composer chown -R $USER:$USER .` for change the owner of the src folder in the host.

2. Only if you are in a UNIX like system. Run `sudo chown -R $USER:$USER src` for change the owner of the src folder in the host.

## Run

docker-compose up -d db wordpress

## Wordpress

### Add language

1. Run `docker-compose run --rm wpcli wp language core list` to get the language code

2. Run `docker-compose run --rm --user=root  wpcli wp --allow-root language core install *LANGUAGE_ISO_CODE*` to install the language

3. Run `docker-compose run --rm wpcli wp language core activate *LANGUAGE_ISO_CODE*` to activate the language


## Add Plugin

1. Search in (wpackagist)[https://wpackagist.org/]
2. Install plugin run `docker-compose run --rm composer require wpackagist-plugin/*PLUGIN_NAME*` to add the plugin
3. Activate the plugin run  `docker compose run --rm wpcli wp plugin activate *PLUGIN_NAME*`

## Add Theme

1. Run `docker-compose run --rm composer require wpackagist-theme/*THEME_NAME*`
2. Run `docker compose run --rm wpcli wp theme activate *THEME_NAME*`


