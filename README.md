# NAME

**mkjail** - make a minimal chroot/jail environment in an archive

# SYNOPSIS

`mkjail archive command [args]`

# DESCRIPTION

`mkjail` runs a given command for up to 20 seconds, tracking the filesystem name
lookups it performs.  It then creates an archive from those files using `tar(1)`.

The resulting archive can be extracted anywhere on the filesystem, and used with
`chroot(8)` or `jail(8)` to run the same command.  Probably.

# EXAMPLE

```shell
-% mkjail ruby-jail.txz /usr/local/bin/ruby -e "puts 'Hello'"
...
Hello
...
-% mkdir ruby-jail && tar xf ruby-jail.txz -C ruby-jail
-% sudo chroot ruby-jail /usr/local/bin/ruby -e "puts 'Chrooted!'"
Chrooted!
```
