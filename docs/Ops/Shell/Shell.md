### [Bash wiki](http://wiki.bash-hackers.org/syntax/redirection)

### Setup a local smtpserver
```shell
$ python -m smtpd -n -c DebuggingServer localhost:1025
```


### Change shell
```
chsh -s /usr/local/bin/bash [username]
```

### Execute command without any env variable or with just a few
```bash
zsh $ P="ZZZ"; echo $P
ZZZ
zsh $ echo $PATATA

$ env -i PATATA="patatina" PAT="ata" bash
echo $ZZZ

$ echo $PATATA
patatina
```

### Super simple text file creation
#### *DON'T USE IN EXISTING FILES, IT WILL OVERWRITE THEM*
Write to file until EOF is written (in a single line)
```
$ cat <<EOF > p.c
some line
another line
EOF
$ cat p.c
some line
another line
```


### Double substution

```sh
$ foo="whatever"
$ i=foo
$ echo $echo ${!i}
whatever
```

### Execute process in background with lock
#### Executes process with nohup and flock
See [gist](https://gist.github.com/patsancu/e8cd32a81b9dcd7e6ae9ee9ebe78d779)
#### Shutdown process above
See [gist](https://gist.github.com/patsancu/14c858eaf32161cf91a7a48e3fd7a601)

#### Flock
Use flock as in [here](https://gist.github.com/patsancu/460aadad82c63e1710a71560ade4260d)

### Get url for git repo
```
xdg-open `git remote -v | grep fetch | head -1 | cut -f2 | cut -d' ' -f1 | sed -e's/git@/http:\/\//' -e's/\.git$//' | sed -E 's/(\/\/[^:]*):/\1\//'`
```
### Wget
#### Download all pdfs linked in a website
**Warning:** Even if it recreates only the pdfs, it will download _every_ file referenced by links
```
$ wget -r -A.pdf http://people.seas.harvard.edu/~minilek/cs229r/fall15/lec.html
```
#### Download all pdfs linked in a website, including linked websites (1 level)
```
$ wget -r -l1 -A.pdf http://people.seas.harvard.edu/~minilek/cs229r/fall15/lec.html
```

### Bash-erize cli any Python object
[python-fire](https://github.com/google/python-fire/blob/master/doc/using-cli.md)

### [Set bash variable default value](http://www.tldp.org/LDP/abs/html/parameter-substitution.html#PARAMSUBREF)
```${parameter=default}, ${parameter:=default}```
The **:** makes a difference only when **$parameter** has been declared and is null
```sh
$ echo $var

$ echo ${var:=abc}   # abc
abc
$ echo ${var}   # abc
abc

```

http://www.tldp.org/LDP/abs/html/parameter-substitution.html#PARAMSUBREF

### One line to pretty separate jsons
`curl -s localhost:7080/mappings  |  python -mjson.tool`

### Xargs with files with spaces on path
```ls *mp3 | xargs -d '\n' mplayer```

### Word frequency of text file
`cat ~/filename.txt | tr ' ' '\n' | sort | uniq -c | awk '{print $2"@"$1}'`
### Egrep
* Given a file with json lines having a field "parentalRating" and a number (e.g. '"parentalRating":"17"') , the following command will get the set of unique parental ratings, along with their frequencies in (frequency, key) pairs.
* The **o** option is to output only the strings matching the egrep regex
```
$ egrep "parentalRating\":\"[0-9]+" file.json -o | cut -d ':' -f 2 | tr -d '"' | sort | uniq -c
   1314 0
   6209 13
   1525 15
   4518 17
      3 18
   3564 7

```
### Diff folders
https://gist.github.com/37b660b98f6d29ecd1af87ffb426f380

### Record Your Command Line Session

* `$ script`
* Exit typing `$ exit`
* All of your typings (and their reults) will be saved to a file named **typescript**

### Globstar
To allow double "*" as a recursive filepath parameter, eg
```
ls **/*.xml
```
add
```
shopt -s globstar
```
to **.bashrc**

### Substring Removal
#### Deletes shortest match of $substring from front of $string.
```
${string#substring}
```
#### Deletes longest match of $substring from front of $string.
```
${string##substring}
```
#### Get last folder of current working directoy
```
$ pwd
/home/patrick/dev/python
$ echo ${PWD##*/}
python
```

### Basic integer sequence loop
```
#!/bin/bash
for i in `seq 1 10`;
   do
     echo $i
   done
```


### Display Output as a Table
```
cat /etc/passwd | column -t -s
```
### Repeat a Command Until It Runs Successfully
```
while true; do ping -c 1 8.8.8.8 > /dev/null 2>&1 && break; done
```

### Suspend machine
As root,
```
# pm-suspend
```

### Convert a File to Upper or Lower Case
```
cat myfile | tr a-z A-Z > output.txt
```

### Sort Processes by Memory Usage
```
ps aux | sort -rnk 4
```
### Sort Processes by CPU Usage
```
ps aux | sort -nk 3
```
### Xargs example
```
ls /etc/*.conf | xargs -i cp {} /home/likegeeks/Desktop/out
```


### dd
#### Basic syntax
```
dd bs=4M if=/dev/sdd of=from-sd-card.img
```

#### See progress of dd
```
sudo pkill -USR1 -n -x dd
```
This will show the progess **in the same terminal dd was executed**
#### Create File With a Specific Size
```
dd if=/dev/zero of=out.txt bs=1M count=10
```

### Shorten url with goo.gl
The `$GOOGLE_SHORTEN_API_KEY` variable needs to be set, and jq needs to be installed

```
shorten(){
    curl "https://www.googleapis.com/urlshortener/v1/url?key=$GOOGLE_SHORTEN_API_KEY" -H 'Content-Type: application/json' -d "{'longUrl': \"$1\"}" | jq '.id'
}
```

### Automatically press keys when condition is met
Use expect as in [here](https://gist.github.com/patsancu/4428820cd1f23fccbabd48fefa5c85fc)

### Convert windows-encoded text file to unix-encoded
```
awk 'BEGIN{RS="^$";ORS="";getline;gsub("\r","");print>ARGV[1]}' file_name
```

### Read lines from file in a for loop
```
FS=$'\n'       # make newlines the only separator
for j in "$(cat ./file_wget_med)"
do
    echo "$j"
done
```
or

```
input="/path/to/txt/file"
while IFS= read -r var
do
  echo "$var"
done < "$input"
```

### Display info about memory
```$ sudo lshw -C memory```

### Open the current repo on a specific web repo
```
my_hgweb() {
         if [ -d .hg ]; then
            xdg-open http://web-repo-address/hg/${PWD##*/} > /dev/null
         else
            echo Not mercurial directory
         fi
}
alias hgweb=my_hgweb
```


### Colors
#### With tput
##### Colors
* 0 – Black.
* 1 – Red.
* 2 – Green.
* 3 – Yellow.
* 4 – Blue.
* 5 – Magenta.
* 6 – Cyan.
* 7 – White.
Clear all options

```
tput setab clear
tput sgr0
```
Set foreground color
```
tput setaf 6; # turquoise
```
Set background color
```
tput setab 2; # green
```
Set bold
```
tput bold;
```
* More info: http://linuxcommand.org/lc3_adv_tput.php

* Show all color combinations
https://gist.github.com/patsancu/44fcdb7d7d195add5bc87e4aa5df88c6


## Useful snippets
### File management
#### Rename files in folder to sorted files
```
c=0; for i in `ls`;do echo "$i"; c=$((c+1)); mv "$i" "$c.txt"; done
```
#### Rename files, change extesion
```sh
for file in *.html
do
 mv "$file" "${file%.html}.txt"
done
```
#### Get extension of file
```
filename=$(basename "$fullfile")
extension="${filename##*.}"
filename="${filename%.*}"
```

#### Change mac address
```
sudo ifconfig eth0 down
sudo ifconfig eth0 hw ether  xx:xx:xx:xx:xx:xx
sudo ifconfig eth0 up
```

### Date
#### Format current date
```
$ date +'%Y%m%d'
```

### Add days to date
```shell
date -d +"2 days"
date -d +"3 minutes"
date -d +"4 months"
```

#### From epoch __seconds__ to date
```
$ date -d @1463234960
samedi 14 mai 2016, 16:09:20 (UTC+0200)
```
#### Combine
```
$ date -d @1463234960 +"%Y-%m-%d"
2016-05-14
$ date -d "1492/10/12 14:00:02" +"%Y-%m-%d %H:%M"
1492-10-12 14:00
```
For more info about [date input formats](https://www.gnu.org/software/coreutils/manual/html_node/Date-input-formats.html#Date-input-formats)

### Useful commands
* **pv** _show progress of command_
```
dd bs=4M if=/media/somedrive/raspbian-jessie.img | pv | dd of=/dev/mmcblk0
```
* **pgrep** _get PID by name_
* **pkill** _kill process by name_
* **timeout n command** _execute command for n seconds_

### See calendar for previous month, next month, and three months from now
```$ ncal -3 -A 2```

### Encode/decode base64 data
```
$ echo patata | base64
cGF0YXRhCg==
$ echo patata | base64 | base64 -d
```

### Exit traps
[Reference](https://web-beta.archive.org/web/20170317022944/http://redsymbol.net/articles/bash-exit-traps/)

Example:

```sh
#!/bin/bash
scratch=$(mktemp -d -t tmp.XXXXXXXXXX)
function finish {
  rm -rf "$scratch"
}
trap finish EXIT
```

### Check OS type
```
if [[ "$OSTYPE" == "linux-gnu" ]]; then
        # ...
elif [[ "$OSTYPE" == "darwin"* ]]; then
        # Mac OSX
elif [[ "$OSTYPE" == "cygwin" ]]; then
        # POSIX compatibility layer and Linux environment emulation for Windows
elif [[ "$OSTYPE" == "msys" ]]; then
        # Lightweight shell and GNU utilities compiled for Windows (part of MinGW)
elif [[ "$OSTYPE" == "win32" ]]; then
        # I'm not sure this can happen.
elif [[ "$OSTYPE" == "freebsd"* ]]; then
        # ...
else
        #
```

### Flatten directory
Moves recursively all files under folder "dir1" (at any level of depth) to the "dir1" folder.
```
find dir1 -type f -exec mv {} dir1 \;
```

### Declare variables for a command
#### Yes
```sh
FOO=bar bash -c 'echo $FOO'
```
####No
```sh
FOO=bar bash -c "echo $FOO"
```

### Get duplicate lines and count
prints duplicate lines only
```
cat some_file.csv | uniq -cd
```

### Geotag pictures
```
#!/bin/bash
lat=$(curl "http://nominatim.openstreetmap.org/search?
city=$1&country=$2&format=json" | jq '.[0] | .lat' | tr ­d '"')
lon=$(curl "http://nominatim.openstreetmap.org/search?
city=$1&country=$2&format=json" | jq '.[0] | .lon' | tr ­d '"')
exiftool ­GPSLongitude=$lon ­GPSLatitude=$lat ­ext jpg .
```

r## Prettify json
```
curl -s localhost:7080/mappings | python -mjson.tool
```
