# Local drupal


## Docroot

Symlink to the docroot and name it app. In this case `../thesite` has at least a `www` directory for the docroot and a `shared` directory with settings.local.php and files and anything else to share, like the db dump.


````
ln -s ../thesite app
docker-compose up -d
````

So it should look like this:

 - app
   - shared
     - settings.local.php
     - files
       - ...
   - www
     - index.php
     - ...
 - docker-compose.yml
 - ...

## Import the db.

Edit `app/shared/settings.local.php` to contain this:

````
<?php

// Database configuration.
$databases['default']['default'] = array(
  'driver' => 'mysql',
  'host' => 'db',
  'username' => 'drupal',
  'password' => 'drupal',
  'database' => 'drupal',
  'prefix' => '',
);
````


Then put the sql or sql.gz file in shared. Then use drush to import. Check that we can connect to the db first.

````
docker-compose run --rm shell
cd /app/www
drush status
drush sql-cli
exit;
drush sql-cli < /app/shared/db.sql
````

Or if you have a `.sql.gz` file replace that last line with this:

````
zcat database.sql.gz | drush sql-cli
````
