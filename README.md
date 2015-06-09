# Custom MySQL application cartridge for OpenShift

**WARNING! Do not use yet! WIP!!!**

This is a custom MySQL cartridge.

## Why

Because the standard OpenShift MySQL cartridge is stuck at 5.5.

## When to use

When you need a quick and unsofisticated solution to run your application with the latest MySQL version.

## How to

To install this cartridge in your existing OpenShift application, go to **"See the list of cartridges you can add"**, paste the URL below in **"Install your own cartridge"** textbox at the bottom of the page and click "Next".

    http://cartreflect-claytondev.rhcloud.com/github/icflorescu/openshift-cartridge-mysql

Then you can use `DB_HOST` and `DB_PORT` environment variables to connect from an application running in the main web cartridge.

## Notes

- Can't guarantee this cartridge is production-ready. Some people use it though (on **their own responsibility**).
- This is a lean cartridge. To save space, just the necessary MySQL binaries are installed.
- Don't hesitate to make a pull-request with an updated version in [this file](https://github.com/icflorescu/openshift-cartridge-mysql/blob/master/metadata/manifest.yml#L4) if you notice this cartridge version is behind the latest [MySQL release](http://dev.mysql.com/downloads/mysql).

## Related

Since you're here, chances are you might also be interested in this [custom Node.js cartridge](https://github.com/icflorescu/openshift-cartridge-nodejs) or this [custom MongoDB cartridge](https://github.com/icflorescu/openshift-cartridge-nodejs).

## License

The [MIT License](http://github.com/icflorescu/openshift-cartridge-mysql/LICENSE).
