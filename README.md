Pipulate!
========

Pipulate lets you collect data straight off of the Web into Google Spreadsheets
using a bookmarklet approach, broadly applicable to SEO and Social Media tasks.
<pre>
          _____ _             _       _                              
         |  __ (_)           | |     | |                             
         | |__) | _ __  _   _| | __ _| |_ ___     ___ ___  _ __ ___  
         |  ___/ | '_ \| | | | |/ _` | __/ _ \   / __/ _ \| '_ ` _ \ 
         | |   | | |_) | |_| | | (_| | ||  __/  | (_| (_) | | | | | |
         |_|   |_| .__/ \__,_|_|\__,_|\__\___| (_)___\___/|_| |_| |_|
                 | |                                                 
                 |_|                                                 
</pre>

## What is Pipulate?
This is a lightweight, customizable and easily scheduled approach to collecting
data directly into Google Spreadsheets by using a bookmarklet that appears to
infuse it with magic data-collection powers. This is based on the premise that
it's just going to end up there anyway, so why not make the spreadsheet the
collector? The types of things it can collect are limited only by your
imagination.

> Compelling, no?

## How Does it Work?
Get it running on your Mac, Windows or Linux desktop, from a ready-made virtual
machine, a cloud server, or even a Raspberry Pi or other teensy tiny computer.
It basically runs on anything. Then, visit the site you just created from a web
browser (usually at http://localhost:8888), drag the bookmarklet to your
Bookmark Bar, open a Google Spreadsheet, click the bookmarklet and get
Pipulating! The data-collecting job that the initial job defines just starts
twinkling in as new rows.

## How Do I Define a Job?
I've set up the initial Pipulate job to collect some very common Web Social
Media metrics, like the counts of a Twitter Profile page, views and subscribers
off a YouTube channel page, and Facebook Shares, Likes and Google +1s of a URL.
You can customize this example to your own pages and profile, or read through
the built-in documentation (coming soon) on setting up your own job. Once
you're happy with it, replace the question marks with asterisks, and invite in
a special gmail address that you set up, and watch the job get processed daily
(or whatever). More documentation coming on the use of the question marks and
asterisks to test, then schedule jobs coming soon. Also, look in the Config tab
to see the RowThrottleNumber setting that keeps more than this number of rows
from processing at once (great for SERP checking), and the RunJobEvery setting
that you can set to values like 1 day, 1 week, 1 month, 3 days, 10 minutes, and
variations thereof.

## How Do I Customize It?
Not happy with the built-in functions? Write your own, and contributing them
back to the project here on Github. Not comfortable with programming Python?
Copy and paste the examples under the Scrapers tab, experimenting with he XPath
and RegEx patterns to grab anything you like off a page. 

# Installation Procedure:

Pipulate is made available ready-to-run on your desktop without an install.
Just download a copy of Levinux, the Tiny Virtual Server for Education, and
select Option #4. It'll take awhile, but it'll build into a Pipulate Server
(minus scheduling, until you give it a gmail). Also, it'll run dirt-slow... but
hey, it's free. Better-yet, install it on some real hardware:

## Debian/Ubuntu
From a Terminal:
- sudo apt-get install python-pip python-dev python-lxml
- sudo pip install requests
- sudo pip install flask_wtf
- sudo pip install gspread
- cd /var
- git clone https://github.com/miklevin/pipulate.git
- cd pipulate
- python pipulate.py
- Visit http://localhost:8888

## Mac OS X
From a Terminal:
- (Python 2.7 & Distribute usually already installed)
- lxml? Must check if Macs have that by default.
- sudo easy_install pip
- sudo pip install requests
- sudo pip install flask_wtf
- sudo pip install gspread
- cd ~/Desktop (or wherever)
- git clone https://github.com/miklevin/pipulate.git
- cd pipulate
- python pipulate.py
- Visit http://localhost:8888

## Windows
- Install CygWin with the following selected:
  - python 2.7
  - git
  - (lxml? Must check cygwin installer)
- Set Windows path to include Python (I will document better)
From a CygWin Shell (MinTTY):
- Download and run to get easy_install:
  - wget --no-check-certificate https://bootstrap.pypa.io/ez_setup.py
- easy_install pip
- pip install requests
- pip install flask_wtf
- pip install gspread
- git clone https://github.com/miklevin/pipulate.git
- cd pipulate
- python pipulate.py
- Visit http://localhost:8888

# Caveats

## OAuth2 For Your Security
Because this employs OAuth2 by default to avoid configuration files and storing
usernames and passwords, it will only work from localhost, or on machines
resolving from a registered domain. If you go the registered domain route,
you'll have to update the client_id under the getLoginlink to your own, under
Google's Developer Console: https://console.developers.google.com/project

## Username & Password For Scheduling
I don't have the web user interface built yet to query the admin for a GMail
username and password, and probably wouldn't be a good idea anyway, as I'm not
running the Web UI in https mode, to keep server configuration as simple as
possible. So that means to store a username and password on the computer (which
is not a good idea anyway) you must have a ../opt directory relative to
pipulate (a folder named opt next to pipualte) and run pipulate like this:

    python pipulate.py configure

This will prompt you for a username and password, and pickle it unencrypted
into ../opt. I recommend using a GMAil account that you set up specifically for
Pipualte, and then turn on 2-Step Verification and then use an App-specific
password, so that you can always revoke the password for that server. This is
all only an issue if you want scheduling. "Manual" pipulating works just fine
out of the box.

## Scheduling
I'm still working out the details of scheduling, specifically how to get the
scheduler to run as a background daemon the same way the Python webserver is.
There's nothing hard about it. Just haven't finished the work yet. To see it
roughly working, run pipulate like this:

    python pipulate.py scheduler

## Linux Auto-Start Daemon & Cron Job
Currently, the documentation on how to fully turn a Linux server into a
Pipulate server is contained in these files in the repository:

- pipulate
- pipuweb

The first file pipulate goes into /etc/init.d/ and then have the command:

    update-rc.d pipulate enable

...run once to set Pipulate to run in webserver mode, like Apache does, every
time the server is started up or reboots. The second file, pipuweb, gets
dropped into /etc/cron.hourly/ to ensure that the Pipulate webserver is always
running, even if some glitch made it stop. The way the daemon is written makes
it safe to keep trying to re-start the webserver. It won't create multiple
instances.

# Where Can I Learn More?

- The Levinux Virutal Server: http://levinux.com
- The Pipulate Main Website: (coming soon)

# To Do List
- Add the built-in documentation (introspect docstrings vs. simple TabInit)
- Turn Scheduler into Linux start-stop daemon
- Fill in tons of useful functions for SEO and Social Media
- Improve the Console Debugging Output when run as Scheduler
- Let Levinux show Pipulate Console Debugging Output by selecting menu option
- Optimize all over the place to reduce GData API calls
- Behind-login support (fetching & crawling AS Facebook user, etc.)
- Awesome UI & bookmarklet behavior from mobile
- Write the very deliberately controlled SEO spider
- Make the spider a general row inserter from any Web/Net iterable item:
  - Blog posts
  - RSS feeds
  - Email in-box (much to think about here)
  - YouTube videos
  - Tumblr Followers
  - Pulling pics down from galleries
  - Yadda, yadda, the fun never stops
  - User your imagination
  - Can't wait for community dynamics to kick-in

# License

The MIT License (MIT)

Copyright (c) 2015 Michael Jay Levin

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
