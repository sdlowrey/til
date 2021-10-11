# RPM and yum

Sometimes the RPM database gets screwed up and you can't install/update/remove packages. You might see errors like this:

```shell
error: rpmdb: BDB0113 Thread/process 9388/140201120016448 failed: BDB1507 Thread died in Berkeley DB library
error: db5 error(-30973) from dbenv->failchk: BDB0087 DB_RUNRECOVERY: Fatal error, run database recovery
error: cannot open Packages index using db5 -  (-30973)
error: cannot open Packages database in /var/lib/rpm
CRITICAL:yum.main:

Error: rpmdb open failed
```

This can happen when a yum/rpm command is terminated while the RPM DB is being changed.

To fix, rebuild the RPM DB:

```shell
mkdir /var/lib/rpm/backup
cp -a /var/lib/rpm/__db* /var/lib/rpm/backup/
ls /var/lib/rpm/backup/
  __db.001  __db.002  __db.003
rm -f /var/lib/rpm/__db.00[0-9]
rpm --quiet -qa
rpm --rebuilddb
yum clean all
```

That should fix the problems. Clean up with `rm -rf /var/lib/rpm/backup`.