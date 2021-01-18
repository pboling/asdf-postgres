# asdf-postgres

Postgresql plugin for [asdf](https://github.com/asdf-vm/asdf) version manager

## Dependencies

_This assumes macOS or a debian flavored linux.  If you need it to work on something else, you'll likely need to modify the plugin._

### Mac

1. You will need a compiler.
    * ```gcc```
    * Hit the ok button and it will install.  If it already has it, then you are good.

### Ubuntu

1. You will need a comppiler.
    * ```sudo apt install linux-headers-$(uname -r) build-essential```
1. You will need libreadline
    * ```sudo apt-get install libreadline-dev```
1. On Ubuntu 19.04+, you will need curl and zlib
    * ```sudo apt-get install zlib1g-dev curl```

## Install

```
asdf plugin-add postgres
```

## ASDF options

Check [asdf](https://github.com/asdf-vm/asdf) readme for instructions on how to install & manage versions of Postgres.

When installing Postgres using `asdf install`, you can pass custom configure options with the following env vars:

* `POSTGRES_CONFIGURE_OPTIONS` - use only your configure options
* `POSTGRES_EXTRA_CONFIGURE_OPTIONS` - append these configure options along with ones that this plugin already uses

These options can be passed at runtime, or set in `~/.asdf-postgres-configure-options`. This file will be sourced at `asdf install` time if it exists.

For example, if you want to compile with a specific set of openssl libraries, you might do something like `POSTGRES_EXTRA_CONFIGURE_OPTIONS="--with-uuid=e2fs --with-openssl --with-libraries=/usr/local/lib:/usr/local/opt/openssl@1.1/lib --with-includes=/usr/local/include:/usr/local/opt/openssl@1.1/include" asdf install postgres`

# How to use (easier version)
## Install
1. Create your .tool-versions file in the project that needs postgres and add `postgres 9.4.7` or whatever version that you want.
2. run `asdf install`

## Run
1. Once it is done, run `pg_ctl start`
2. Once that starts, run `createdb default` _you can sub `default` with whatever you want your db name to be._
3. Then log in with `psql -d default` _if you didn't use default, make sure you use whatever you put in step 2._
4. If you need to move your data file around, move data from your install directory, which will look something like this: `~/.asdf/installs/postgres/9.4.7/data` to wherever you want it.  Once it is moved, start your db with `pg_ctl -D wherever/you/moved/it start`.  Your postgresql.conf file is in that directory if you need to change the port or anything.

## Stop
1. Just run `pg_ctl stop`  if you moved your data directory, you have to do `pg_ctl -D wherever/you/moved/it stop`
