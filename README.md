# Custom MySQL cartridge for OpenShift

This is a custom OpenShift cartridge able to provide the latest MySQL version (starting with 5.7.7-rc as of 10th of June 2015).

## Why

Because the standard OpenShift MySQL cartridge is stuck at 5.5 and some people are keen to use the latest MySQL server features (such as improved support for spatial data).

## When to use

When you need a quick and unsofisticated solution to run your application with the latest MySQL version.

## How to

To install this cartridge in your existing OpenShift application, go to **"See the list of cartridges you can add"**, paste the URL below in **"Install your own cartridge"** textbox at the bottom of the page and click "Next".

    http://cartreflect-claytondev.rhcloud.com/github/icflorescu/openshift-cartridge-mysql

Once the cartridge is created and started, you can SSH into the gear and use `mysql` command like this:

    ${OPENSHIFT_DATA_DIR}.mysql/bin/mysql --socket=${TMP}mysql.sock -u root

For instance, here's a one-liner to set up a root password and allow remote access:

    ${OPENSHIFT_DATA_DIR}.mysql/bin/mysql --socket=${TMP}mysql.sock -u root -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'secret-password' WITH GRANT OPTION; FLUSH PRIVILEGES;"

If you're using multiple gears, here's how you can find the MySQL gear SSH url:

    rhc app show application-name --gears

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

## TODO

Update the install script when MySQL 5.7 final is released. OpenShift doesn't allow "5.7.7-rc" as version number in the cartridge manifest file, so right now I'm "manually" adding the "-rc" suffix in the install script.

## Related

Since you're here, chances are you might also be interested in this [custom Node.js cartridge](https://github.com/icflorescu/openshift-cartridge-nodejs) or this [custom MongoDB cartridge](https://github.com/icflorescu/openshift-cartridge-mongodb).

## Credits and attributions

This cartridge was inspired by [Ted Wennmark](https://se.linkedin.com/in/tedwennmark)'s [blog post](http://mysql-nordic.blogspot.ro/2015/02/creating-minimal-mysql-installation-for.html) on how to create a minimal MySQL installation for an embedded system.

## License

The [MIT License](http://github.com/icflorescu/openshift-cartridge-mysql/LICENSE).
