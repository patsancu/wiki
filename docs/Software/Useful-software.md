## Dev

### Json lint
* jsonlint-py
* `sudo apt-get install python-demjson`

## Java

### jdk
`sudo apt-add-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer`

or

`sudo apt-get install oracle-java7-installer`

### [SOAP UI](https://www.soapui.org/downloads/soapui.html)

### SDK man
`curl -s get.sdkman.io | bash`

### [STS - Spring Tool Suite](https://spring.io/tools)

## CLI software
### [Newsbeuter](http://newsbeuter.org/)
rss client

### [Mutt](http://www.mutt.org/)
email client. [Config info](https://github.com/patsancu/wiki/blob/024b21f7f966e58f92c6f8625cde2b5b3faad5e4/docs/OS/mutt.md)

## DB
### [Squirrel](http://squirrel-sql.sourceforge.net/#installation)

**Steps to add Oracle Driver**

1. Open Driver list from left menu, scroll down till you find "Oracle Thin Driver", you will notice red x mark next to it denoting the driver is still not configured.
1. After selecting "Oracle Thin Driver" click "Modify the Selected Driver" denoted by pencil.
1. Click "Extra Class Path" tab.
1. Click "Add" and select 1 jar file from %Oracle_DB_CLIENT_INSTALL%\jdbc\lib\ojdbc6_g.jar
1. Click Ok, and we are done defining the driver.
1. Now create an alias for the DB using previous driver and providing URL, username, & password.

**Note:**
No need to have Oracle client for setup, all you need is just the driver jar files. You can download from this Oracle link.

If you are using JDK 5 while running Squirrel SQL, the jar file will be %Oracle_DB_CLIENT_INSTALL%\jdbc\lib\ojdbc5_g.jar

Thin url would be something like (local db): jdbc:oracle:thin:@localhost:1521:xe

### [Oracle Database 11g Express Edition](http://www.oracle.com/technetwork/database/database-technologies/express-edition/overview/index.html)

### [SQL developer](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html)

### [DBeaver](http://dbeaver.jkiss.org/)
Soporte para Oracle, MySQL, PostgreSQL,... y *Drill*

## Communications

### [Franz](http://meetfranz.com/)
Integrate several messaging apps (skype, hangouts, slack,...). Capable of managing several accounts of the same app

### [Hangouts](https://chrome.google.com/webstore/detail/google-hangouts/knipolnnllmklapflnccelgolnpehhpl)

### [Skype](https://www.skype.com/en/download-skype/skype-for-linux/)
### [Skype alpha](https://community.skype.com/t5/Linux/Skype-for-Linux-Alpha-and-calling-on-Chrome-amp-Chromebooks/td-p/4434299)

### [Slack](https://slack.com/downloads)

## Remote
### [Gnome connection manager](http://www.kuthulu.com/gcm/gnome-connection-manager_1.1.0_all.deb)

**Change** /home/patrick/.gcm/gcm.conf
- Change **log-path** option
- Change console_close = CTRL+W (e.g. console_close = CTRL + M)

## Cloud
### [Cross FTP](http://www.crossftp.com/crossftp_1.97.6.deb)
FTP and S3 browser
### [DragonDisk](http://www.s3-client.com/download-amazon-s3-client-google-cloud-storage-client)
S3 browser

Can get shareable URL via Right Click -> Properties -> Security Tab -> Add (All users) -> Check Download and Read permissions boxes

## Tex
### Install packages
Download package (e.g. [classicthesis](https://ctan.org/pkg/classicthesis) ) and extract the sty file it to a folder named as the package under ~/texmf/tex/latex/packagename (e.g. `/home/user/texmf/tex/latex/classicthesis` )

## Misc
sudo apt-get install nautilus-actions gnome-paint
