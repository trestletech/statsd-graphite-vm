# Vagrant VM for StatsD + Graphite

Vagrant VM for [StatsD](https://github.com/etsy/statsd) and [Graphite](http://graphite.readthedocs.org/) with the help of [@hectcastro's](https://github.com/hectcastro/) graphite, statsd, and node.js cookbooks.

## To get started
You need to have [Vagrant installed](http://www.vagrantup.com/).

	$ librarian-chef install
	$ vagrant up
	$ vagrant ssh

Then after provisioning I had to run this on the guest machine as root:

    pip install 'Twisted<12.0'

to get anything to work. Then I modified /opt/graphite/conf/carbon.conf to have `USER` set to `www-data` and `LINE_RECEIVER_INTERFACE` to `0.0.0.0`.

## Graphite
	$ open http://localhost:8080
Graphite's credentials default to username `root` and password `root`.

## StatsD with Python

```python
from statsd import StatsClient
statsd = StatsClient()
statsd.incr('foo')
```

## StatsD with telnet

You can use the [TCP Stats Interface](https://github.com/etsy/statsd/blob/master/docs/admin_interface.md)

    telnet 127.0.0.1 8126

or

    echo counters | nc 127.0.0.1 8126
