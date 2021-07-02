zuul-ci
=======

Ansible role to setup zuul on a single-node installation with docker-compose.


Enable logging:
Put this content into a file called log.conf next to zuul.conf:
```ini
[loggers]
keys=root,zuul

[handlers]
keys=console

[formatters]
keys=simple

[logger_root]
level=DEBUG
handlers=console

[logger_zuul]
level=DEBUG
handlers=console
qualname=zuul
propagate=0

[handler_console]
level=DEBUG
class=StreamHandler
formatter=simple
args=(sys.stdout,)

[handler_debug]
level=DEBUG
class=logging.handlers.TimedRotatingFileHandler
formatter=simple
args=('/var/log/zuul/debug.log', 'midnight', 1, 30,)

[handler_normal]
level=INFO
class=logging.handlers.TimedRotatingFileHandler
formatter=simple
args=('/var/log/zuul/zuul.log', 'midnight', 1, 30,)

[formatter_simple]
format=%(asctime)s %(levelname)s %(name)s: %(message)s
datefmt=
```

Enable this by extending your zuul.conf:
```
[gearman]
log_config=/etc/zuul/log.conf

[gearman_server]
log_config=/etc/zuul/log.conf

[zookeeper]
log_config=/etc/zuul/log.conf

[keystore]
password=secret

[scheduler]
log_config=/etc/zuul/log.conf

[connection "githubzuulapp"]
log_config=/etc/zuul/log.conf

[executor]
log_config=/etc/zuul/log.conf
```
51.9
63.164


Requirements
------------

docker.io
docker-compose

Role Variables
--------------

TBD

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: setup zuul-ci playbook
      hosts: zuul.myhost.com
      roles:
         - name: setup zuul-ci role
           role: zuul-ci

License
-------

Apache License 2.0

Author Information
------------------

Created by Tim Beermann in behalf of OSISM GmbH.
