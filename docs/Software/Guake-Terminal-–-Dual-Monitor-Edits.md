Guake always defaults to the left monitor. It does a great job of determining the size of ‘monitor 1′. To get Guake on my right-side monitor I had to tweak the source code. Here’s how you can do the same:

Make a copy of theGuake program and put it in yourbin folder. I renamed mine toguake-dualmon but you can call it whatever you want.

* ```cp /usr/bin/guake ~/bin/guake-dualmon```
* ```vim  ~/bin/guake-dualmon```
* Find the method definition  `def get_final_window_rect(self):`
* First we will correctly position the terminal on the right monitor. Add one line at the end, between `window_rect.y = 0`  and  `return window_rect` . The window_rect.x and window_rect.y variables tell the Guake window where to be located. Set `window_rect.x` to be the width of your left monitor and `window_rect.y` will depend on how offset the monitors are. I had to play with the ‘y’ setting to get it just right or the text starts off the top of the screen.

```
window_rect.x = 1280
window_rect.y = 24
```
* Now Guake will be positioned on your right monitor, but it will still be the size of the left one. In my case it was sized at 1280, and I needed it to be 1920. Divide your right monitor’s width by the left monitor’s width (ie. 1920/1280 = 150). Still within  `get_final_window_rect(self):` you will find the line `width = 100` . This setting is a percentage of your left monitor, so set it to the answer you got by dividing one width into the other. In my case it was:
```
width = 150
```
That’s it! Just make sure to always run your copy of the program, or better yet add it to your autostart so it runs automatically!