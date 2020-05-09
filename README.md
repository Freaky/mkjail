# NAME

**mkjail** - make a minimal chroot/jail environment

# SYNOPSIS

`mkjail` \[-t | --timeout DURATION] \[-a | --archive FILE] \[-d | --dir DIRECTORY] \[-l | --list \[FILE]] command \[args]

# DESCRIPTION

`mkjail` runs a given command with an optional timeout, tracing any path
lookups it performs in order to construct a list of dependent files, folders
and devices.

By default the list is printed to stdout, but the `-l` argument allows a file to
be specified.

The list can also be used to create an archive using `tar(1)` in any format its
automatic creation mode supports, and it can be used to create a directory that
should be ready to use as a `chroot(8)` or `jail(8)` environment.

# EXAMPLE

```shell
-% mkjail -d ruby-jail /usr/local/bin/ruby -e "puts 'Hello'"
 == TRACE /usr/local/bin/ruby -e puts 'Hello'
Hello
 == EXIT 0
 == DIR ruby-jail
ruby-jail/
ruby-jail/dev
...
ruby-jail/var/run
ruby-jail/var/run/ld-elf.so.hints
14073 blocks
-% sudo chroot ruby-jail /usr/local/bin/ruby -e "puts 'Hello'"
Hello
```
