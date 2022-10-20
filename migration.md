# Introduction

List of migration commands for the production site. These commands should be run when the final testing is done on staging site and content migration is on final stage.

1) Download backdrop database from https://old.basecamp.com/2298168/projects/11117862/todos/269196031
2) mysqladmin -u root -proot create rosco_digital
3) mysql -u root -proot rosco_digital < ~/Downloads/roscodigital.sql
4) (rosco_digital > backdrop ( Table for importing backdrops ))
5) Paste following in sites/default/settings.local.php
  ```
   $databases['rosco_digital']['default'] = array(
   'driver' => 'mysql',
   'database' => 'rosco_digital',
   'username' => 'root',
   'password' => 'root',
   'host' => 'localhost',
   'port' => '3306',
   'prefix' => ''
   );

   $databases['roscodb']['default'] = array(
   'driver' => 'mysql',
   'database' => 'roscodb',
   'username' => 'root',
   'password' => 'root',
   'host' => 'localhost',
   'port' => '3306',
   'prefix' => ''
   );
 ```

### Commands to migrate all fields ###
1) drush pm-uninstall weplant
2) drush en field_group_migrate migrate_plus migrate_tools weplant
3) php modules/custom/weplant/rabit_keyword_fix.php
4) drush mi --update backdrop_keywords   Worked: 2225 created:  0 failed
   
5) Path : /sites/default/files/content/backdrops : Download link "http://test.rosco.com/data/rental.zip"

6) drush mi backdrop_images   Worked: 1240 created:  26 failed
   
7) drush mi backdrop_print
8) drush mi backdrop_node   Worked: 1266 created:  0 failed
9) Path : /sites/default/files/content/rabbitmovies_videos : Download link "http://test.rosco.com/data/rabbit.zip"
10) drush mi rabbitmovies_videos  Worked: 661 created:  1333 failed,( Note: There are only 662 files in folder so other failed)
11) Path : /sites/default/files/content/rabbitmovies_images : Download link "http://test.rosco.com/data/rabbit.zip"
12) drush mi rabbitmovies_images  Worked: 661 created:  1333 failed,( Note: There are only 662 files in folder so other failed)
13) drush mi rabbit_node
14) Path : /sites/default/files/content/rabbitmovies2_images : Download link "http://test.rosco.com/data/rabbit.zip"
15) drush mi rabbitmovies2_images
16) drush mi  rabbitmovies_node
17) Path : /sites/default/files/content/imagebank : Download link "http://test.rosco.com/data/imagebank.zip"
18) drush mi imagebank_images  Worked: 562 created:  0 failed
19) drush mi imagebank_print
20) drush mi imagebank_node
21) drush mi --update imagebank_node 
22) Path : /sites/default/files/content/scenicimages : Download link "http://test.rosco.com/data/ScenicImages.zip"
23) drush mi scenicgallery_images  Worked: 454 created:  14 faile
24) drush mi scenic_gallery  Worked: 147 created:  0 failed
25) Path : /sites/default/files/content/ColorImages : Download link "http://test.rosco.com/data/MugImages.zip"
26) drush mi colorgallery_images  Worked: 2080 created:  17 failed
27) drush mi color_gallery   Worked: 1034 created:  0 failed