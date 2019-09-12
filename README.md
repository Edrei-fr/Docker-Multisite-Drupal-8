# Docker-Multisite-Drupal-8

This compose file just set up a basic containers for use Drupal with a minimum customitazion, feel free to customize it adding Dockerfiles or env files as you needed.

In case you are wondering, the reason for host_config volume it's be able to customize your apache config and hosts config inside the drupal container. After few attemps setting up a Drupal multisite I just did it like https://www.drupal.org/docs/8/multisite/drupal-8-multisite says, but I realised I could take advantage of using Drush :) so let me explain you step by step:

- 1) Run the compose and go to the drupal container ip adress from your browser

- 2) Install a Drupal root site (database, user, password are defined in compose file and database host could be mysql container ip or its alias, as default mysql) *For nexts sites installations you should use 'root' user and empty password as it's declared by default in compose file

- 3) Edit your hosts file OUTSIDE container (I mean in your real or virtual machine). Just put a pretty name to point drupal container ip ;) this name will be the root domain name for your multisite installation

- 4) Use Drush from drupal container to install another site following drush si --help (make sure you are using --sites-subdir and --db-url pointing an empty database...)

- 5) After executing drush si [your options] the first time it will create the sites.php, subdir site and settings.php for you :) just ignore the error

- 6) Change sites/subdirsite/files permissions in order to continue the installation process (chmod a+w should be enough)

- 7) Execute drush si [your options] again and wait till installation completes

- 8) Edit your hosts file again (step 3) putting the same name as your /subdirsite/ pointing the same drupal container ip

- 9) Visit your new site from your browser


I'm not really sure how this works but the fact is I can set up a multisite inside a container and reach every site I've installed :D
