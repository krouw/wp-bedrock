# Wordpress Bedrock Docker

# USE THIS ONLY FOR LOCAL DEVELOPMENT!!!

## User Permissions

Wordpress docker env uses a debian based image for the webserver and php. 
In this environment, the user used for the web server process and wordpress files is www-data. 
In debian environments, this user is commonly logged in with ID 33.
However, utility wrappers like composer and wp cli run under an alpine linux image, 
where the user www-data is logged in with ID 82.
[https://gist.github.com/zdenekdrahos/53f16cfe902ff5f820a01b79e8c76a01](https://gist.github.com/zdenekdrahos/53f16cfe902ff5f820a01b79e8c76a01)

## Install Bedrock

1. Run
`
docker-compose run --rm --user=33  composer create-project roots/bedrock .
`
for download bedrock in the latest version.
2. Change the .env file to your needs.

## Wordpress build

(php8.1-apache)[https://github.com/docker-library/wordpress/tree/master/latest/php8.1/apache]

## Run

docker-compose up -d db wordpress

## Wordpress

(wpcli docs)[https://developer.wordpress.org/cli/commands/]

### Add language

1. Run `docker-compose run --rm wpcli wp language core list` to get the language code

2. Run `docker-compose run --rm wpcli wp --allow-root language core install *LANGUAGE_ISO_CODE*` to install the language

3. Run `docker-compose run --rm wpcli wp language core activate *LANGUAGE_ISO_CODE*` to activate the language

## Add Plugin

1. Search in (wpackagist)[https://wpackagist.org/]
2. Install plugin run `docker-compose run --rm composer require wpackagist-plugin/*PLUGIN_NAME*` to add the plugin
3. Activate the plugin run  `docker compose run --rm wpcli wp plugin activate *PLUGIN_NAME*`

## Add Theme

1. Run `docker-compose run --rm composer require wpackagist-theme/*THEME_NAME*`
2. Run `docker compose run --rm wpcli wp theme activate *THEME_NAME*`


# References

(https://github.com/trenccan777/WP-Bedrock-Docker-setup)
(https://github.com/urre/wordpress-nginx-docker-compose-image)
(https://github.com/urre/wordpress-nginx-docker-compose)