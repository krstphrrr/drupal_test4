FROM drupal:latest

RUN apt-get update && apt-get install apt-file -y && apt-file update && apt-get install vim -y

RUN composer global require drush/drush 

RUN export PATH="$HOME/.composer/vendor/bin:$PATH"

RUN composer global update

RUN composer require drupal/ds drupal/field_group drupal/bootstrap4 drupal/jquery_ui_accordion

# RUN apt-get install rename
 
COPY ./exports/settings.php /opt/drupal/web/sites/default/settings.php

COPY ./exports/example.settings.local.php /opt/drupal/web/sites/default/settings.local.php

# RUN mkdir /opt/drupal/web/themes/custom
