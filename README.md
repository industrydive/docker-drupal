
Symlink to the docroot and name it app. In this case `../thesite` has at least a `www` directory for the docroot and a `shared` directory with settings.local.php and files and anything else to share, like the db dump.


````
ln -s ../thesite app
docker-compose up -d
````

Import the db. Put the sql or sql.gz file in shared. Then use drush to import. Check that we can connect to the db first.

````
docker-compose run --rm shell
cd /app/www
drush status
drush sql-cli
exit;
drush sql-cli < /app/shared/db.sql
````
