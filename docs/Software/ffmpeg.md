### Rotate video 90 degrees
```
ffmpeg -i input.mp4 -filter:v transpose=2 -c:v libx264 -preset veryfast -crf 22 -c:a copy -metadata:s:v rotate="" input_rotated.mp4
```