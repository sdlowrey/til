Here is a basic configuration for use with Graphite.  I culled all comment lines from the original file, but it contains a lot of useful info.

```
FQDNLookup true
Interval 10
LoadPlugin logfile
LoadPlugin syslog

<Plugin logfile>
        LogLevel "info"
        File "/var/log/collectd.log"
        Timestamp true
        PrintSeverity false
</Plugin>

<Plugin syslog>
        LogLevel info
</Plugin>

LoadPlugin cpu
LoadPlugin df
<Plugin df
        Device "/dev/xvda1"

        # ignore rootfs; else, the root file-system would appear twice, causing
        # one of the updates to fail and spam the log
        FSType rootfs
        # ignore the usual virtual / temporary file-systems
        FSType sysfs
        FSType proc
        FSType devtmpfs
        FSType devpts
        FSType tmpfs
        FSType fusectl
        FSType cgroup
        IgnoreSelected true
</Plugin>


LoadPlugin disk
<Plugin disk>
        Disk "/^[hs]d[a-f][0=9]?$i/"
        IgnoreSelected false
</Plugin>

LoadPlugin interface
LoadPlugin irq
LoadPlugin load
LoadPlugin memory
LoadPlugin processes
<Plugin processes>
#       Process "name"
        ProcessMatch "vars-conductor" "python3.4 /opt/fugue/bin/vars-conductor .*"
</Plugin>

LoadPlugin protocols
LoadPlugin swap
LoadPlugin users
LoadPlugin write_graphite
<Plugin write_graphite>
        <Node "example">
                Host CARBON_IP_ADDRESS_HERE
                Port "2003"
                Protocol "tcp"
                LogSendErrors true
                Prefix "collectd.fugue"
                StoreRates true
                AlwaysAppendDS false
                EscapeCharacter "_"
        </Node>
</Plugin>
```

# Notes

## General
Always set up logging and look at the logs whenever you change ```collectd.conf```.

## Debian
On 8.3 (jessie), install with ```apt-get install collectd```.  I think it brought a ton of updates in at the same time but, since testing, I didn't really care.

The service can be controlled with ```systemctl start collectd``` but it was hard to restart. Not sure if ```collectdmon``` was getting in the way so I disabled it in ```/etc/default/collectd```.

```
USE_COLLECTDMON=0
```

## AWS
The security group for the host must allow outbound traffic to TCP 2003.
