FROM drupal:latest

RUN apt-get update && apt-get install apt-file -y && apt-file update && apt-get install vim -y

RUN apt-get install wget -y

RUN composer require drupal/ds drupal/field_group drupal/bootstrap4 drupal/jquery_ui_accordion

RUN composer require drupal/backup_migrate:5.0.0-rc2

COPY ./exports/php.ini-production /usr/local/etc/php/php.ini-production
COPY ./exports/php.ini-development /usr/local/etc/php/php.ini-development

 
COPY ./exports/settings.php /opt/drupal/web/sites/default/settings.php

# COPY ./exports/settings.local.php /opt/drupal/web/sites/default/settings.local.php

RUN composer require drush/drush 

RUN export PATH="$HOME/.composer/vendor/bin:$PATH"

COPY ./drupal/entrypoint.sh /usr/local/bin/
