---
layout: post
title: "Deploying Flask with nginx"
date: 2012-04-27
comments: true
categories: Programming Python
permalink: /blog/Deploying-Flask-with-nginx-uWSGI-and-Supervisor
---

{% img http://flask.pocoo.org/docs/_images/logo-full.png %}

The [Flask docs](http://flask.pocoo.org/docs/deploying/uwsgi/) for this take you 80% of the way there.

Basically, we need **[uWSGI](http://projects.unbit.it/uwsgi/)** to create a [UNIX socket](http://en.wikipedia.org/wiki/Unix_domain_socket), which nginx can route requests to as they come in. 

First, let's make sure uWSGI runs independent of nginx.

The docs tell us to write this:

```bash
uwsgi -s /tmp/uwsgi.sock -w myapp:app
```

There's two problems with this: 

First, you may get some error that it doesn't find flask if you are using a virtual environment (which you should). 

Second, nginx may not be able to read the file later if the permissions don't let it.

So I had to adapt it to this:

```bash
uwsgi -s /tmp/uwsgi.sock -w flask_file_name:app -H /path/to/virtual/env --chmod-socket 666
```

Now, install nginx with apt-get install nginx. Change the /etc/nginx/sites-available/default to read:

```
server {
    listen       80;
    server_name  _;
    location / { try_files $uri @yourapplication; }
    location @yourapplication {
      include uwsgi_params;
      uwsgi_pass unix:/tmp/uwsgi.sock;
    }
}
```

Now symlink the file above to the enabled one, because that's how nginx works:

```
ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default
```

Start nginx with '/etc/init.x/nginx restart'

Go to a browser and try it out. Yay!

But what if you want to restart the server? nginx will restart, but your uWSGI will not. We'll use **[supervisord](http://readthedocs.org/docs/supervisord/en/latest/index.html)** for that.

```
apt-get install supervisor
```

We need to set up the /etc/supervisord.conf to tell supervisor what to do:

<script src="https://gist.github.com/2510028.js?file=gistfile1.cfg"></script>

Now, kill your supervisor, start it again, and your Flask app be running ad infinitum.

```bash
ps -A | grep supervisor
kill <id>
sudo supervisord -c /etc/supervisord.conf
```

**[Here's](https://gist.github.com/760606)** another supervisor sample config file to get you inspired.

Hope this helps.
