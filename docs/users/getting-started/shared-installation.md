---
layout: docs
title: Shared Installation
---

## Shared installation

(WARNING: THIS FEATURE IS EXPERIMENTAL!)

You can install ONE s9y distribution and manage multiple users on it by sharing the core files and then deploying specially crafted files in each user's directory.

Let's do this using an example. You own the domain 's9yblogs.org'. You want to have multiple virtual hosts for as many users as you like. They are going to be called 'username.s9yblogs.org'. We choose the users 'garvin', 'j' and 'tom' for example hosts. We assume that your webserver runs as user 'www', group 'www'. We also assume that all your users are called like the subdomains, and they are also in group 'www'. We further assume that PHP's safe\_mod is turned off.

Of course, for security reasons, you should set the open\_basedir directive to the user's document root, so he can't access other installations on your host.

So your Apache-Webserver should contain Virtual Hosts like this:

    -- httpd.conf
    <VirtualHost 42.42.42.42:80>
        ServerName garvin.s9yblogs.org
        DocumentRoot /home/www/garvin.s9yblogs.org/htdocs
        <Directory "/home/www/garvin.s9yblogs.org/htdocs">
            AllowOverride All
        </Directory>
        php_value include_path ".:/usr/local/lib/php:/usr/local/lib/php/s9y/:/usr/local/lib/php/s9y/bundled-libs/"
        php_admin_value open_basedir "/usr/local/lib/php/:/usr/local/lib/php/s9y/:/home/www/garvin.s9yblogs.org/"
    </VirtualHost>

    <VirtualHost 42.42.42.42:80>
        ServerName j.s9yblogs.org
        DocumentRoot /home/www/j.s9yblogs.org/htdocs
        <Directory "/home/www/j.s9yblogs.org/htdocs">
            AllowOverride All
        </Directory>
        php_value include_path ".:/usr/local/lib/php:/usr/local/lib/php/s9y/:/usr/local/lib/php/s9y/bundled-libs/"
        php_admin_value open_basedir "/usr/local/lib/php/:/usr/local/lib/php/s9y/:/home/www/j.s9yblogs.org/"
    </VirtualHost>

    <VirtualHost 42.42.42.42:80>
        ServerName tom.s9yblogs.org
        DocumentRoot /home/www/tom.s9yblogs.org/htdocs
        <Directory "/home/www/tom.s9yblogs.org/htdocs">
            AllowOverride All
        </Directory>
        php_value include_path ".:/usr/local/lib/php:/usr/local/lib/php/s9y/:/usr/local/lib/php/s9y/bundled-libs/"
        php_admin_value open_basedir "/usr/local/lib/php/:/usr/local/lib/php/s9y/:/home/www/tom.s9yblogs.org/"
    </VirtualHost>
    -- httpd.conf

You will unpack the default s9y distribution files in "/usr/local/lib/php/s9y/". Where you store the directory 's9y' is not important, as long as you adjust the include\_path setting in the Virtual Hosts. But the directory name 's9y' is significant.

Now you can either **copy** or **link** the following subcategories:

* "/usr/local/lib/php/s9y/deployment/" [core redirection files]
* "/usr/local/lib/php/s9y/templates/" [templates so that users can change them - depends on your plugin usage!]
* "/usr/local/lib/php/s9y/plugins/" [certain plugins refer to HTTP-images]
* "/usr/local/lib/php/s9y/htmlarea/" [htmlarea WYSIWYG-editor]

to each of the user's subdirectories:

    $ cp -r /usr/local/lib/php/s9y/deployment/* /home/www/garvin.s9yblogs.org/htdocs/

    /* Either COPY: */
    $ cp -r /usr/local/lib/php/s9y/templates /home/www/garvin.s9yblogs.org/htdocs/
    $ cp -r /usr/local/lib/php/s9y/plugins /home/www/garvin.s9yblogs.org/htdocs/
    $ cp -r /usr/local/lib/php/s9y/htmlarea /home/www/garvin.s9yblogs.org/htdocs/

    /* Or LINK: */
    $ ln -s -d /usr/local/lib/php/s9y/templates /home/www/garvin.s9yblogs.org/htdocs/templates
    $ ln -s -d /usr/local/lib/php/s9y/plugins /home/www/garvin.s9yblogs.org/htdocs/plugins
    $ ln -s -d /usr/local/lib/php/s9y/htmlarea /home/www/garvin.s9yblogs.org/htdocs/htmlarea

    /* Adjust permissions */
    $ chown -R garvin.www /home/www/garvin.s9yblogs.org/htdocs/*
    $ chmod ug+rwx /home/www/garvin.s9yblogs.org/htdocs
    $ chmod ug+rwx /home/www/garvin.s9yblogs.org/htdocs/uploads/

    /* See above if you only want to link the subdirectories */
    $ cp -r /usr/local/lib/php/s9y/deployment/* /home/www/j.s9yblogs.org/htdocs/
    $ cp -r /usr/local/lib/php/s9y/templates /home/www/j.s9yblogs.org/htdocs/
    $ cp -r /usr/local/lib/php/s9y/htmlarea /home/www/j.s9yblogs.org/htdocs/
    $ chown -R j.www /home/www/j.s9yblogs.org/htdocs/*
    $ chmod ug+rwx /home/www/j.s9yblogs.org/htdocs
    $ chmod ug+rwx /home/www/j.s9yblogs.org/htdocs/uploads/

    /* See above if you only want to link the subdirectories */
    $ cp -r /usr/local/lib/php/s9y/deployment/* /home/www/tom.s9yblogs.org/htdocs/
    $ cp -r /usr/local/lib/php/s9y/templates /home/www/tom.s9yblogs.org/htdocs/
    $ cp -r /usr/local/lib/php/s9y/htmlarea /home/www/tom.s9yblogs.org/htdocs/
    $ chown -R tom.www /home/www/tom.s9yblogs.org/htdocs/*
    $ chmod ug+rwx /home/www/tom.s9yblogs.org/htdocs
    $ chmod ug+rwx /home/www/tom.s9yblogs.org/htdocs/uploads/

The difference between copying or linking the **htmlarea** and **templates** folder is a maintaineance issue. Whenever you upgrade the core s9y libraries, it could happen that the distributed templates or the htmlarea code could have changed. Now you only copied those directories, you need to copy the new files inside each of the user's directories. If you only linked them, it will be instantly all the same for every user. It is recommended to link the directories, but that depends on your OS and permission structure. Of course this way a "shared library user" cannot store his own templates inside the linked directory, so this is at a loss of individualisation.

For later management access, it is advised you keep a list of all URLs for your s9y-managed blogs. We suggest to create a SQL table like 'my\_managed\_s9y\_blogs':

    sql> CREATE TABLE my_managed_s9y_blogs (url varchar(255) default null);
    sql> INSERT INTO my_managed_s9y_blogs (url) VALUES ('http://garvin.s9yblogs.org/');
    sql> INSERT INTO my_managed_s9y_blogs (url) VALUES ('http://j.s9yblogs.org/');
    sql> INSERT INTO my_managed_s9y_blogs (url) VALUES ('http://tom.s9yblogs.org/');

Now you are almost ready for take-off. We assume that every user has access to a seperate SQL database where his blog-data is later stored in. You can already see, that the steps needed above shouldn't be to hard to put into a customized script.sh file for use in your setup.

Open up your `http://garvin.s9yblogs.org/` file. You should now see s9y's installation screen. Enter the database- and username and the corresponding password. Everything else can be left to the user.

Now every user can manage his/her blog just as if it were a standalone installation.

### Special Notes

* Each blog is still a standalone blog.
* If you update the core library files from version 0.5 to 0.6 (for example) every user of your core library will get the default s9y-Upgrader script to see and needs to update his local configuration.

As a provider for s9y blogs to your users, you are advised to migrate the user's blogs on your own. To do so, it is best that you always have a "spare" testing blog installed just like your user's blogs.

Open that installation and look at the upgrader. Execute it and see that it completes without errors. If that happened, you should cycle through a list of ALL your s9y-managed blogs like this:

    <?php
    $sql = mysql_query('SELECT url FROM my_managed_s9y_blogs');
    while ($row = mysql_fetch_array($sql, MYSQL_ASSOC)) {
        $fp = fopen($row['url'] . 'serendipity_admin.php?serendipity[action]=upgrade');
    }
    ?>

So basically all you need to do is call that script for every s9y-powered blog you host.
