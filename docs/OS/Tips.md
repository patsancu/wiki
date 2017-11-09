### Convert video to mp3
From [here](https://askubuntu.com/a/84633)
```
ffmpeg -i video.mp4 -vn \
       -acodec libmp3lame -ac 2 -ab 160k -ar 48000 \
        audio.mp3
```
or if you want to use Variable Bitrate Encoding (VBR):

```
ffmpeg -i video.mp4 -vn \
       -acodec libmp3lame -ac 2 -qscale:a 4 -ar 48000 \
        audio.mp3
```

