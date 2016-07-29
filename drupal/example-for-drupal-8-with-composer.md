# `.amazeeio.yml` Example for Drupal 8 with Composer

If Drupal 8 is installed via composer, composer is in charge of downloading Drupal Core, Drupal Contrib and external libraries. See the `composer install` command as a first command for `development` and `production` sites in order to make sure that everything is correctly installed.

Additionally the Drupal directory is usually installed within a subfolder of the Git repository. Therefore Drush and other Drupal related bash commands need to executed within that subfolder. 

In this example, composer installs Drupal within a folder called `web`. See the `cd web` prefix for each command to ensure that drush is called in the right folder.

```
sitegroup: mysitegroup
deploy_tasks:
  development:
    before_deploy:
      - composer install
    after_deploy:
      - cd web && drush -y updb --cache-clear=0
      - cd web && drush -y cr
  production:
    before_deploy:
      - composer install
  after_deploy:
      - cd web && drush -y updb --cache-clear=0
      - cd web && drush -y cr
shared:
 production:
   - src: files
     dst: web/sites/default/files
```