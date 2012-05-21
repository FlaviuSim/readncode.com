---
layout: post
title: "Set up PostgreSQL on Mac OS 10.5+ Quickly"
date: 2011-03-03
comments: true
categories: Programming
permalink: /blog/set-up-postgresql-on-mac-os-quickly
---

To install PostgreSQL, use homebrew (the best package manager for Mac; get it <a target="blank" href="https://github.com/mxcl/homebrew">here</a>. Then, you can type this to install PostgreSQL:

```bash
$ brew install postgresql
```

You will need to create a new postgres user. To create the user account, first find an unused user ID. To see the IDs that are currently in use, type in the Terminal: 

```bash
$ sudo dscl . -list /Users UniqueID
```

Choose one that's not taken

Then, create the user account _postgres , like so: 

```bash
$ sudo dscl . create /Users/_postgres UniqueID [User ID you want] UserShell /bin/bash RealName "PostgreSQL Server" NFSHomeDirectory /usr/local/pgsql
```

```bash
$ sudo dscl . append /Users/_postgres RecordName postgres
```

(Leopard precedes daemon names with an underscore. The last command created an alias without the underscore, though, so that you can forget the underscore exists.)

By the way, if you need to delete a user on OS 10.5+, you can type this: 

```
$ sudo dscl . delete /Users/[username]
```

The user account is now created. It is not given a password intentionally. This prevents anyone but root from logging in as postgres. To use the postgres user account, type:

```bash 
$ sudo su postgres
```

Now, as a sudo-capable user, set permissions on the data directory (create it if it's not there, or delete it's contents if it has any).

```bash 
$ sudo chown postgres /usr/local/pgsql/data
```

Log back in as postgres (sudo su postgres), and initialize the database cluster:

```bash
$ initdb -D /usr/local/pgsql/data
```

```bash 
$ export PGDATA=/usr/local/pgsql/data # setting this saves you having to type the path to the data directory every time
$ pg_ctl start # this starts it, and you should probably add a log file argument: "-l /usr/local/pgsql/data/pg_log"
$ pg_ctl stop # this stops it
```

```bash 
$ createdb [name of your database]
$ createuser [name of your user]
Shall the new role be a superuser? (y/n) y
```

You now can integrate this database into your django (or Rails, or whatever) app.
The credentials would be (host: localhost, port:5432, DB: [name of your database], username: [name of your user], password: [none])

I realize I've covered nothing but the bare minimum needed to set up PostgreSQL 9 on a local Mac OS 10.6 development machine. I strongly invite you to look at the official documentation, <a target="blank" href="http://www.postgresql.org/docs/9.0/interactive/index.html">here</a>.

Hopefully, this saves you some time when you're just trying to get your app working quickly.

