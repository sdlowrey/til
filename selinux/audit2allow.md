Scenario:
- CentOS 7
- Python (Django) web app served by nginx via uwsgi

When attempting to connect to HTTP, nginx reported a 502 (bad gateway) error:

```
2016/02/13 15:52:40 [crit] 1435#0: *1 connect() to 127.0.0.1:3031 failed (13: Permission denied)
 while connecting to upstream, client: 69.244.68.72, server: , request: "GET / HTTP/1.1",
 upstream: "uwsgi://127.0.0.1:3031", host: "ec2-54-175-194-239.compute-1.amazonaws.com"
```

Changing process uid/gid in nginx and uwsgi configs didn't help.

SELinux audit log showed the problem:

```
sudo cat /var/log/audit/audit.log|grep AVC

type=AVC msg=audit(1455385051.562:1648): avc:  denied  { name_connect }
 for  pid=15465 comm="nginx" dest=3031 scontext=system_u:system_r:httpd_t:s0
  tcontext=system_u:object_r:unreserved_port_t:s0 tclass=tcp_socket
```

The nginx process (type ```httpd_t```) is not being allowed to connect to the uWSGI process listening on port 3031. So find out what policy changes are needed.

```
sudo audit2allow -w -a

type=AVC msg=audit(1455378760.227:1551): avc:  denied  { name_connect } for
 pid=1435 comm="nginx" dest=3031
 scontext=system_u:system_r:httpd_t:s0
 tcontext=system_u:object_r:unreserved_port_t:s0 tclass=tcp_socket

	Was caused by:
	One of the following booleans was set incorrectly.

	Description:
	Allow nis to enabled

	Allow access by executing:
	# setsebool -P nis_enabled 1

	Description:
	Allow httpd to can network connect

	Allow access by executing:
	# setsebool -P httpd_can_network_connect 1
  ```

This is an HTTP problem (not NIS), so just run the command on the last line and the problem is fixed.

```
sudo setsebool -P httpd_can_network_connect 1
```
