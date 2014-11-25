Readme file for the Ansible Drupal VM project
---------------------------------------------

Template to create flexible and ready to go vagrant box with L(A|N)MP inside.

Right now such features are available:

- Apache 2.x
- Mysql
- PHP 5.(4|5)
  - Xdebug
  - APC
  - Packages for mysql, uploadprogress, memcache, etc
- Memcache
- Varnish
- Git
- Apache Solr (3|4).x (based on java and tomcat6)
- Composer
- Drush
- Ruby
  - With small workaround it's possible to install any set of gems
  
TODO
 - Fix gems installation for given user
 - Configurable solr config sync
 - Nginx
 - Xhprof
 - PHPCS  & CSSlist & JSlint
 - Behat with silenium
 - Windows integration
 - Performance improvements
   - Enable swap
   - Everything into the memory
   - Something else?
 - Monitor everything (logs, performance, memory usage, etc)
 
 
Installation
1) Clone project somewhere to your machine
2) Modify Vagrantfile
  a) Modify synced_folder settings to your project root
  b) Modify memory usage (Default is 4048 MB)
  c) Modify domain name in ./ansible/vars/geerlingguy-apache.yml
  d) Modify database name in ./ansible/vars/geerlingguy-mysql.yml (credentials are root/root)
  e) Modify private VM network IP in Vagrantfile and ./ansible/inventories/dev
3) Vagrant up
4) Vagrant ssh
5) Change /etc/hosts on your machine to use private VM network IP for your domain.