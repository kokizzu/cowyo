![Logo](https://i.imgur.com/ixnBYOl.png)

# AwwKoala
## A Websocket Wiki and Kind Of A List Application
[![Version 1.0](https://img.shields.io/badge/version-1.0-brightgreen.svg)]()
[![Go Report Card](https://goreportcard.com/badge/github.com/schollz/AwwKoala)](https://goreportcard.com/report/github.com/schollz/AwwKoala)
[![Join the chat at https://gitter.im/schollz/AwwKoala](https://badges.gitter.im/schollz/AwwKoala.svg)](https://gitter.im/schollz/AwwKoala?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This is a self-contained wiki webserver that makes sharing easy and *fast*. You can make any page you want, and any page is editable by anyone. Pages load instantly for editing, and have special rendering for whether you want to view as a web page or view as list.

#### Basics

To jot a note, simply load the page at [`/`](http://AwwKoala.com/) and just start typing. No need to press edit, the browser will already be focused on the text. No need to press save - it will automatically save when you stop writing. The URL at [`/`](http://AwwKoala.com/) will redirect to an easy-to-remember name that you can use to reload the page at anytime, anywhere. But, you can also use any URL you want, e.g. [`/AnythingYouWant`](http://AwwKoala.com/AnythingYouWant).

#### Views and Lists

All pages can be rendered into HTML by adding `/view`. For example, the page [`/AnythingYouWant`](http://AwwKoala.com/AnythingYouWant) is rendered at [`/AnythingYouWant/view`](http://AwwKoala.com/AnythingYouWant/view). You can write in HTML or [Markdown](https://daringfireball.net/projects/markdown/) for page rendering. Math is supported with [Katex](https://github.com/Khan/KaTeX) using `$\frac{1}{2}$` for inline equations and `$$\frac{1}{2}$$` for regular equations.

If you are writing a list and you want to tick off things really easily, just add `/list`. For example, after editing [`/grocery`](http://AwwKoala.com/grocery), goto [`/grocery/list`](http://AwwKoala.com/grocery/list). In this page, whatever you click on will be striked through and moved to the end. This is helpful if you write a grocery list and then want to easily delete things from it.

#### Versioning

All previous versions of all notes are stored and can be accessed by adding `?version=X` onto `/view` or `/edit`. If you are on the `/view` or `/edit` pages the menu below will show the most substantial changes in the history. Note, only the *current* version can be edited (no branching allowed, yet).

#### Disclaimer

Be cautious about writing sensitive information in the notes as anyone with the URL has access to it. For more information, or if you'd like to edit the code, [use the github](https://github.com/schollz/AwwKoala).

### Contact

If you'd like help or find a bug, please submit [an issue](https://github.com/schollz/AwwKoala/issues). Any other comments, quetions or anything at all, just <a href="https://twitter.com/intent/tweet?screen_name=zack_118" class="twitter-mention-button" data-related="zack_118">tweet me @zack_118</a>

# Install
To get started on your local network just do:

```
git clone https://github.com/schollz/awwkoala.git
cd awwkoala
make
./awwkoala -p :8001 LOCALIPADDRESS
```

and then goto the address `http://LOCALIPADDRESS:8001/`

## Production server
I recommend using `NGINX` as middleware, as it will do caching of the static files for you. There is an example `NGINX` block in `install/`. To automatically install, on Raspberry Pi / Ubuntu / Debian system use:

```
git clone https://github.com/schollz/awwkoala.git
cd awwkoala
nano Makefile <--- EDIT Makefile to include YOUR EXTERNAL ADDRESS
make && sudo make install
```

Now the program starts and stops with

```
sudo /etc/init.d/AwwKoala start|stop|restart
```

Edit your crontab (`sudo crontab -e`) to start on boot:

```
@reboot /etc/init.d/AwwKoala start
```

# Usage

```
$ awwkoala --help
awwkoala: A Websocket Wiki and Kind Of A List Application
run this to start the server and then visit localhost at the port you specify
(see parameters).
Example: 'awwkoala localhost'
Example: 'awwkoala -p :8080 localhost'
Example: 'awwkoala -db /var/lib/awwkoala/db.bolt localhost'
Example: 'awwkoala -p :8080 -crt ssl/server.crt -key ssl/server.key localhost'
Options:
  -a string
        key to access admin priveleges (default no admin priveleges)
  -crt string
        location of ssl crt
  -db string
        location of database file (default "/home/mu/awwkoala/data.db")
  -httptest.serve string
        if non-empty, httptest.NewServer serves on this address and blocks
  -key string
        location of ssl key
  -p string
        port to bind (default ":12312")
```

```

If you set the admin flag, `-a` you can access a list of all the current files by going to `/ls/WhateverYouSetTheFlagTo`.
