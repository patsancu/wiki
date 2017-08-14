### Extract audio from video
* ```mplayer -dumpaudio -dumpfile clip_track.mp3 clip.avi``` or
* ```avconv -i /input-file-name-with-path output-filename.mp3```

### Merge pdfs into one
```
pdftk "space separated pdf files" cat output CanterburyTales.pdf
```