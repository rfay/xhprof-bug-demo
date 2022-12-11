This is a bug demo repo for xhprof coredump on PHP 8.1 and PHP 8.2 with 
xhprof 2.3.8

It's a demo with [DDEV](https://github.com/drud/ddev).

To demonstrate:

1. Install DDEV on Linux host. I used Ubuntu, [docker installation](https://ddev.readthedocs.io/en/latest/users/install/docker-installation/#linux) and [ddev installation](https://ddev.readthedocs.io/en/latest/users/install/ddev-installation/#linux)
2. Check out this repo
3. `ddev start`
4. `ddev xhprof on`
5. `ddev exec curl localhost`

Then `ddev logs` will show a coredump having been created in /tmp.

You can get it and inspect it. For example:
```
gdb /usr/sbin/php-fpm8.2 core.1670789386.php-fpm.3373
bt
```

Complexities:
* Since this happens inside a container, the coredump location has to be configured on the host Linux system. 
  * ~~On macOS host, `docker run -it --rm --privileged --pid=host justincormack/nsenter1` and then `echo '/tmp/core.%t.%e.%p' > /proc/sys/kernel/core_pattern` and `ulimit -c unlimited`~~ I haven't figured out how to capture a core on macOS.
  * On Linux (I used Ubuntu host), `echo '/tmp/core.%t.%e.%p' | sudo tee /proc/sys/kernel/core_pattern`
