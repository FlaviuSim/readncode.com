---
layout: post
title: "Problems with easy_install"
date: 2011-02-24
comments: true
categories: Programming Python
permalink: /blog/setuptools-pip-vitualenv-python-problems
---

I work on OS X 10.6, which makes package management much more of a challenge than any Linux distro. 

Sure, I've tried <a target="blank" href="http://www.macports.org/" >MacPorts</a>, <a target="blank" href="https://github.com/mxcl/homebrew">homebrew</a>, and even <a target="blank" href="http://www.finkproject.org/">fink</a>. None makes it as easy as apt-get, though I recommend homebrew.

Anyway, I joyfully start a new python project in a clean virtual environment with virtualenv and it's companion, virtualenvwrapper (not sure why these are not part of the same project). 

I specify the <strong>--no-site-packages</strong> to make sure I don't get system packages in my virtualenv (not sure why this is not the default), like so:

```bash
mkvirtualenv --no-site-packages happy_virtual_env
```

But then it turns out I still have access to system wide packages, like django. Hmm...

...insert some 20 hours of modifying the Python Path and getting errors like:

```objc
UserWarning: Module pkg_resources was already imported from 
/System/Library/Frameworks/Python.framework/Versions/2.6/Extras/lib/python/pkg_resources.py
```

or
```objc
pkg_resources.DistributionNotFound: setuptools==0.6c9
```

...saddened, I finally "sudo rm -rf" pkg_resources.py, setuptools, pip, virtualenv, virtualenvwrapper, from both /Library/Python/2.6/site-packages/ and /usr/local/bin/

Then I manually installed setuptools (see <a target="blank" href="http://pypi.python.org/pypi/setuptools">here</a>) and then "easy_install pip", "pip install virtualenv", and now it all works as expected.

So, while I wish I knew more about package management, "nuke and pave" is sometimes ok.

