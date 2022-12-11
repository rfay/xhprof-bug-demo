This is a bug demo repo for xhprof coredump on PHP 8.1 and PHP 8.2 with 
xhprof 2.3.8

It's a demo with [DDEV](https://github.com/drud/ddev).

To demonstrate:

1. Install DDEV 
2. Check out this repo
3. `ddev start`
4. `ddev xhprof on`
5. `ddev launch`

Then `ddev logs` will show a coredump having been created in /tmp.

You can get it and inspect it. 

