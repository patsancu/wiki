### From ape+cue to several files
convert file to flac

```
cuebreakpoints CD1.cue | shntool split -o flac "file_name".flac
```
```
cuebreakpoints sample.cue | shnsplit -o flac sample.flac;
#add metadata
cuetag *.cue split-track*.flac ;
```

