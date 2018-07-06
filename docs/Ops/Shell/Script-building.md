### Simple stop
```
echo "Press enter to continue"; read noing
```

### Colorize cat output of source files

`$ pip install Pygments`

http://pygments.org/

with pygmentize -g filename

### Yes no answer
```shell
testFile=/home/patrick/dev/master.properties
sampleService='iris-cms-metadata-management-service'
if [ ! -f $testFile ]; then
  tput setaf 2
  echo "test properties file $testFile is missing"
  tput sgr0else  tput setaf 1;
  echo "Will delete all data from the CMS db.";
  tput sgr0  ;
  read -r -p "Are you sure? [y/N] " response
  case $response in      [yY][eE][sS]|[yY])
    cd $sampleService;
    gradle dropDatabase -Parchaius.url=file:$testFile ;
    cd -;
    ;;
    *)
    echo "OK, no harm done";
    ;;
  esac
fi
```

### Argument parsing

```shell
vflag=off
filename=
while getopts vf: opt
do
    case "$opt" in
      v)  vflag=on;;
      f)  filename="$OPTARG";;
      \?)		# unknown flag
      	  echo >&2 \
	  "usage: $0 [-v] [-f filename] [file ...]"
	  exit 1;;
    esac
done
shift `expr $OPTIND - 1`
```

### Arrays
```sh
distro=("redhat" "debian" "gentoo")
echo ${distro[2]} # will print gentoo
echo ${#distro[@]} # will print array length: 3
```

### Get parent folder from script
```
DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )
```

### Split colon delimited value
From [here](https://stackoverflow.com/a/918931/2769307)
```sh
### this sets the internal field separator variable
IFS=":"
```
```sh
s='Strings:With:Four:Words'
IFS=":" read -r var1 var2 var3 var4 <<< "$s"
echo "[$var1] [$var2] [$var3 [$var4]"
[Strings] [With] [Four [Words]
```

### Select specific lines with sed
#### select line 10 up to line 33
```sh
sed -n '10,33p' < file.txt
```
#### select 1st line and 3rd line
```sh
sed -n '1p;3p' < file.txt
```
