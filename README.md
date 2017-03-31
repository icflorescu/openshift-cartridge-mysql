# Custom MySQL cartridge for OpenShift

![mysql-openshift](https://cloud.githubusercontent.com/assets/581999/13375581/503e858e-ddac-11e5-96de-b4cd718e7cc3.png)

This is a custom OpenShift cartridge providing the latest MySQL version (5.7.17 as of March 29 2017).

## Why

Because the standard OpenShift MySQL cartridge is stuck at 5.5 and some people are keen to use the latest MySQL server features (such as improved support for spatial data).

## When to use

When you need a quick and unsofisticated solution to run your application with the latest MySQL version.

## Installing

To install this cartridge in your existing OpenShift application, go to **"See the list of cartridges you can add"**, paste the URL below in **"Install your own cartridge"** textbox at the bottom of the page and click "Next".

    https://raw.githubusercontent.com/icflorescu/openshift-cartridge-mysql/master/metadata/manifest.yml

## Setting up

Once the cartridge is created and started, you can SSH into the database gear:

    ssh gear-url

...and connect to the server with `mysql` client like this:

    ${OPENSHIFT_DATA_DIR}.mysql/bin/mysql --socket=${TMP}mysql.sock -u root

If you really need it, you can enable remote access for root like this (make sure to replace `secret` with a strong password):

    ${OPENSHIFT_DATA_DIR}.mysql/bin/mysql --socket=${TMP}mysql.sock -u root -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'secret' WITH GRANT OPTION; FLUSH PRIVILEGES;"

If you're using multiple gears, here's how you can find the MySQL gear SSH url:

    rhc app show application-name --gears

Once you've enabled remote access, you can use `rhc port-forward` and MySQL Workbench or your favorite client to connect from your development machine.

Use `DB_HOST` and `DB_PORT` environment variables to connect from an application running in the main web cartridge. For instance, here's how you'd do it in a Node.js application using [Knex.js](http://knexjs.org/):

    var knex = require('knex')({
      client: 'mysql',
      connection: {
        host     : process.env.DB_HOST,
        port:    : process.env.DB_PORT,
        user     : 'your_database_user',
        password : 'your_database_password',
        database : 'myapp_test'
      }
    });

## Notes

- Can't guarantee this cartridge is production-ready. Some people use it though (on **their own responsibility**).
- This is a **lean cartridge**. A standard MySQL installation takes a huge amount of space (over 1.5GB for MySQL 5.7.5). To save space, just the necessary MySQL binaries are installed.
- In order to avoid an OpenShift configuration conflict, **the server instance is listening on 13306 instead of the standard MySQL port 3306**.
- Don't hesitate to make a pull-request with an updated version in [this file](https://github.com/icflorescu/openshift-cartridge-mysql/blob/master/metadata/manifest.yml#L4) if you notice this cartridge version is behind the latest [MySQL release](http://dev.mysql.com/downloads/mysql).
- **Don't open issues in this repository to ask questions about `rhc port-forward`**. Please refer to the [OpenShift documentation](https://developers.openshift.com/en/managing-port-forwarding.html) to learn about it. I am not an employee of RedHat / OpenShift, nor do I have any form of consultancy agreement with them and the fact that I open-sourced this cartridge doesn't mean I'm willing to offer free advice on the subject. Pull-requests and suggestions are always welcome, though.

## Related

Since you're here, chances are you might also be interested in this [custom Node.js cartridge](https://github.com/icflorescu/openshift-cartridge-nodejs) or this [custom MongoDB cartridge](https://github.com/icflorescu/openshift-cartridge-mongodb).

## Credits and attributions

This cartridge was inspired by [Ted Wennmark](https://se.linkedin.com/in/tedwennmark)'s [blog post](http://mysql-nordic.blogspot.ro/2015/02/creating-minimal-mysql-installation-for.html) on how to create a minimal MySQL installation for an embedded system.

## Credits

See contributors [here](https://github.com/icflorescu/openshift-cartridge-mysql/graphs/contributors).

If you find this repo useful, don't hesitate to give it a star and [spread the word](http://twitter.com/share?text=Checkout%20this%20custom%20MySQL%20cartridge%20for%20OpenShift!&amp;url=http%3A%2F%2Fgithub.com/icflorescu/openshift-cartridge-mysql&amp;hashtags=MySQL,database,OpenShift&amp;via=icflorescu).

## License

The [ISC License](http://github.com/icflorescu/openshift-cartridge-mysql/blob/master/LICENSE).
