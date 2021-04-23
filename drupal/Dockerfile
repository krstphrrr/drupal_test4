FROM drupal:latest
#FROM drupal/recommended:8.9.14

# getting vim inside the container for development/troubleshooting
RUN apt-get update && apt-get install apt-file -y && apt-file update && apt-get install vim git -y

# installing drupal modules / themes etc
RUN composer require drupal/ds drupal/field_group drupal/bootstrap_barrio drupal/admin_toolbar drupal/entity drupal/token drupal/migrate_plus drupal/migrate_tools:4.x-dev
#RUN composer require drupal/ds drupal/field_group drupal/bootstrap4 drupal/jquery_ui_accordion

# bibliography module and dependencies
#RUN composer require drupal/bibcite:1.x-dev academicpuma/citeproc-php:~1.0 adci/full-name-parser:^0.2 technosophos/LibRIS:~2.0 audiolabs/bibtexparser:dev-master caseyamcl/php-marc21:~1.0
RUN composer require drupal/bibcite:1.x-dev seboettg/citeproc-php:~2.1 adci/full-name-parser:^0.2.4 technosophos/libris:~2.0 audiolabs/bibtexparser:dev-master caseyamcl/php-marc21:~1.0  drupal/bibcite_entity:1.x-dev drupal/bibcite_migrate:1.x-dev drupal/bibcite_crossref:1.x-dev

# backup utilities available by default
RUN composer require drupal/backup_migrate:5.0.0-rc2

# custom php.ini's
COPY ./exports/php.ini-production /usr/local/etc/php/php.ini-production
COPY ./exports/php.ini-development /usr/local/etc/php/php.ini-development

# custom apache2 and settings.php
COPY ./php_myadminexports/apache2.conf /etc/apache2/apache2.conf
COPY ./exports/settings.php /opt/drupal/web/sites/default/settings.php

# COPY ./exports/settings.local.php /opt/drupal/web/sites/default/settings.local.php

# local drush ( local with respect to the drupal install; not global)
RUN composer require drush/drush:^10.3
# making sure the drush path is available
RUN export PATH="$HOME/.composer/vendor/bin:$PATH"

# making custom scripts available
COPY ./drupal/entrypoint.sh /usr/local/bin/
