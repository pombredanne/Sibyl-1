Configuration
-------------

### Configuration files

The default Sibyl configuration can be overwritten with configuration file.

These files are taken in account if they are located in any of the location (and
in the same order) returned by `sibyl config` when no configuration are
available:
```
$ sibyl config
No configuration file found. Supported paths:
	/etc/sibyl.conf
	/etc/sibyl/sibyl.conf
	/usr/local/etc/sibyl.conf
	/usr/local/etc/sibyl/sibyl.conf
	/home/user/sibyl.conf
	/home/user/.sibyl.conf
...
```

The resulting configuration file can be obtain through `sibyl config -d`.

### Default configuration

The default configuration is equivalent to:

```Python
[find]
jit_engine = qemu,gcc,llvm,tcc,python

[tests]
ctype = $SIBYL/test/ctype.py
string = $SIBYL/test/string.py
stdlib = $SIBYL/test/stdlib.py
```

### Section 'find'

This section is relative to the `find` action.

The `jit_engine` parameter is a list, separated by ',', of jitter engine
preference.
If the first engine is not available, then the second is used, and so on.

To known the jitter engine elected, use `sibyl config -V jit_engine`.

### Section 'test'

This section links to available test sets. By default, only Sibyl ones are
present.

The syntax is: `name = path/to/file.py`.
The token `$SIBYL` can be used to point to Sibyl installation dir.

The list of registered tests can be obtain withe
`sibyl config -V available_tests_keys`.

For more information on tests, please refer to the corresponding documentation.

### Configuration overview

Using `sibyl config` without option, one can obtain:
* the configuration file used, if any
* available configuration file paths
* elected jit engine
* loaded Tests, associated to their names

### API

Sibyl configuration is available from `sibyl.config:config`.

This `Config` instance provides:
* `jit_engine`: Name of engine to use for jit
* `available_tests`: dictionnary mapping test group name to corresponding classes
