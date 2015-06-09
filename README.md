# Custom MySQL application cartridge for OpenShift

**WARNING! Do not use yet! This cartridge is still WIP!!!**

This is a custom MySQL cartridge.

## Why

Because the standard OpenShift MySQL cartridge is stuck at 5.5.

## When to use

When you need a quick and unsofisticated solution to run your application with the latest MySQL version.

## How to

To install this cartridge in your existing OpenShift application, go to **"See the list of cartridges you can add"**, paste the URL below in **"Install your own cartridge"** textbox at the bottom of the page and click "Next".

    http://cartreflect-claytondev.rhcloud.com/github/icflorescu/openshift-cartridge-mysql

Then you can use `DB_HOST` and `DB_PORT` environment variables to connect from an application running in the main web cartridge.

For instance, here's how you'd do it in a Node.js application using [Knex.js](http://knexjs.org/):

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

You can also use `rhc port-forward` to connect from a client / tool such as MySQL Workbench running on your development machine. See the note below if `rhc port-forward` sounds new to you.

## Notes

- Can't guarantee this cartridge is production-ready. Some people use it though (on **their own responsibility**).
- This is a **lean cartridge**. A standard MySQL installation takes a huge amount of space (over 1.5GB for MySQL 5.7.5). To save space, just the necessary MySQL binaries are installed.
- Don't hesitate to make a pull-request with an updated version in [this file](https://github.com/icflorescu/openshift-cartridge-mysql/blob/master/metadata/manifest.yml#L4) if you notice this cartridge version is behind the latest [MySQL release](http://dev.mysql.com/downloads/mysql).
- Please refer to the [OpenShift documentation](https://developers.openshift.com/en/managing-port-forwarding.html) to learn about `rhc port-forward` instead of opening issues in this GitHub repository. I am not an employee of RedHat / OpenShift, nor do I have any form of consultancy agreement with them. The fact that I open-sourced this cartridge doesn't mean I'm willing to offer free advice on the subject. Pull-requests and suggestions are always welcome, though.

## Related

Since you're here, chances are you might also be interested in this [custom Node.js cartridge](https://github.com/icflorescu/openshift-cartridge-nodejs) or this [custom MongoDB cartridge](https://github.com/icflorescu/openshift-cartridge-nodejs).

## Credits and attributions

This cartridge was inspired by [Ted Wennmark](https://se.linkedin.com/in/tedwennmark)'s [blog post](http://mysql-nordic.blogspot.ro/2015/02/creating-minimal-mysql-installation-for.html) on how to create a minimal MySQL installation for an embedded system.

## License

The [MIT License](http://github.com/icflorescu/openshift-cartridge-mysql/LICENSE).
