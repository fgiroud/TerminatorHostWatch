# Fork of [GratefulTony/TerminatorHostWatch](https://github.com/GratefulTony/TerminatorHostWatch)

### What's have changed from the original plugin ?
The configuration now accept a collection of profile/pattern, wich is more convenient than to have to create a new profile for each host.   
You can simply create a "danger_zone" profile, and configure the patterns to match any hosts differents than your local host name.   

If you really need a different profile per host, add some lines in the configuration to fullfill your needs.

# Terminator HostWatch Plugin
This plugin monitors the last line (PS1) of each terminator terminal, and applies a host-specific profile if the hostname is changed. 

As of now, the plugin simply parses the PS1-evaluated last line and matches it against the regex `[^@]+@(\w+)` (e.g. to match `user@host`).


## Installation

For now, i don't provide any .deb file, you have to install the plugin manually

Put the `host_watch.py` in `/usr/share/terminator/terminatorlib/plugins/` or `~/.config/terminator/plugins/`. Then create a profile in Terminator to match your hostname. If you have a server that displays `user@myserver ~ $`, for instance, create a profile called `myserver`.

## Configuration
You have to declare profile and the associated pattern in the configuration, the plugin will iterate over the patterns and set the profile if the pattern match the last PS-evaluated last line

```
[plugins]
  [changehostplugin]]
    [[[patterns]]]
      default = (my_name@my_machine\:\~\$)
      danger_zone = [^@]+@([\w \-\.]+)\:\~\$
```
## Development
Development resources for the Python Terminator class and the 'libvte' Python bindings can be found here:

For terminal.* methods, see: 
  - http://bazaar.launchpad.net/~gnome-terminator/terminator/trunk/view/head:/terminatorlib/terminal.py
  - and: `apt-get install libvte-dev; less /usr/include/vte-0.0/vte/vte.h`

For terminal.get_vte().* methods, see:
  - https://github.com/linuxdeepin/python-vte/blob/master/python/vte.defs
  - and: `apt-get install libvte-dev; less /usr/share/pygtk/2.0/defs/vte.defs`

## Debugging
To debug the plugin, start Terminator from another terminal emulator 
like this:

```
$ terminator --debug-classes=HostWatch
```

That should give you output like this:

```
   HostWatch::check_host: switching to profile EMEA0014, because line 'pheckel@EMEA0014 ~ $ ' matches pattern '[^@]+@(\w+)'
   HostWatch::check_host: switching to profile kartoffel, because line 'root@kartoffel:~# ' matches pattern '[^@]+@(\w+)'
   ...
```

## Authors
The plugin was developed by GratefulTony (https://github.com/GratefulTony/TerminatorHostWatch), 
and extended by Philipp C. Heckel (https://github.com/binwiederhier/TerminatorHostWatch).

## License
The plugin is licensed as GPLv2 only.
