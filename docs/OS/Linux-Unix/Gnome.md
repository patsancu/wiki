### Set monday as first day of week in Gnome
Edit the file ~/.xsessionrc (or bashrc or whatever)
to contain the line
`"export LC_TIME=en_GB.utf8"`


### Assign/unassign keyboard's sleep button
#### Assign
```
gsettings set org.gnome.settings-daemon.plugins.power button-suspend "nothing"
```
#### Unassign
```
gsettings set org.gnome.settings-daemon.plugins.power button-suspend "suspend"
```

### Custom launchers

The applications launchers Gnome knows about are .desktop files in /usr/share/applications, and `~/.local/share/applications`. You can create custom launchers for whatever is in your home folder, by either manually creating and editing a custom .desktop file, or by using Alacarte, the old Gnome menu editor.

The Gnome desktop file documentation can be of help: https://developer.gnome.org/integration-guide/stable/desktop-files.html.en

The custom launcher is just a text file, named, for example, EclipseEE.desktop, with the following content:
```
[Desktop Entry]
Name=Eclipse EE
Exec=/home/mrPeterson/path_to_executable
StartupNotify=true
Terminal=false
Type=Application
Icon=/optional/path/to/icon.png
```