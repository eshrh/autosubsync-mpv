# autosubsync-mpv
Automatic subtitle synchronization script for mpv media player,
using [ffsubsync](https://github.com/smacke/ffsubsync).
This is a fork of [autosub](https://github.com/vayan/autosub-mpv),
and it's meant to work nicely alongside `autosub`,
[trueautosub](https://github.com/fullmetalsheep/mpv-iina-scripts)
or similar scripts.

For support of [alass](https://github.com/kaegi/alass), other subtitle formats, 
synchronization using an existing subtitle, and some other things check
out [this branch](https://github.com/joaquintorres/autosubsync-mpv/tree/v0.32).
You should probably use this one if you're using an updated version of `mpv`, 
since `master` branch is intended to support older, deprecated versions such as 
the ones in official Debian/Ubuntu repos.

### Installation
1. Install [ffsubsync](https://github.com/smacke/ffsubsync).
You can simply use `pip install ffsubsync`,
assuming you already have `ffmpeg` installed.
2. Download `autosubsync.lua` or clone the repo.
3. If your `ffsubsync` path isn't the default,
create a config file at `~/.config/mpv/script-opts/autosubsync.conf` 
(GNU/Linux) or `%AppData%\mpv\script-opts\` (Windows)
and add the correct path. For example:
```
subsync_path=/usr/local/bin/ffsubsync
```
* In Windows you need to use forward slashes 
or double backslashes for your path,
like `"C:\\Users\\YourPath\\Scripts\\ffsubsync"`
or `"C:/Users/YourPath/Scripts/ffsubsync"`,
or else it won't work. 

* In GNU/Linux you can use `which ffsubsync` to find out where it is.

* If you're using an older version of `mpv`, it's possible that you
need to add your `.conf` file to `lua-settings` instead of `script-opts`. 

4. Move `autosubsync.lua` to your scripts folder.
This is typically in `~/.config/mpv/scripts` (GNU/Linux)
or `%AppData%\mpv\scripts\` (Windows).

### Usage
When you have an out of sync sub, press `n` to synchronize it.

`ffsubsync` can typically take up to about 20-30 seconds
to synchronize (I've seen it take as much as 2 minutes
with a very large file on a lower end computer), so it
would probably be faster to find another, properly
synchronized subtitle with `autosub` or `trueautosub`.
Many times this is just not possible, as all available
subs for your specific language are out of sync.
Take into account that using this script has the
same limitations as `ffsubsync`, so subtitles that have
a lot of extra text or are meant for an entirely different 
version of the video might not sync properly.

Note that the script will create a new subtitle file, in the same folder 
as the original, with the `_retimed` suffix at the end.

### Issues
If you are having trouble getting it to work, feel free to open an issue, but
try to check if [ffsubsync](https://github.com/smacke/ffsubsync) works properly
outside of `mpv` first. When `ffsubsync` isn't working, `autosubsync` will likely
fail. If you do open an issue, please try to include `mpv`'s output to the 
terminal.

### Possible improvements
* Add support for other subsync tools besides `ffsubsync`. This shouldn't be too hard,
and it might help cover some alternatives that are faster or have different edge cases.
* ~~Actually check if the srt file exists before feeding it to ffsubsync.
Pressing n without the proper file will cause ffsubsync to extract the
whole raw audio before actually raising the corresponding error flag,
and that's just incredibly slow for such basic error handling.~~
Fixed, added some messages too.
* Test if it works properly in ~~Windows~~ or MacOS, or in mpv-based
players like [mpv.net](https://github.com/stax76/mpv.net) 
or [celluloid](https://celluloid-player.github.io/).
* ~~Modify it to support multiple filenames/languages. 
Since `autosub` and `trueautosub` only use one language at a time and 
the same subtitle name as the video file, this hasn't been too much of a bother yet.~~
* Add compatibility with 
[autoload](https://github.com/mpv-player/mpv/blob/master/TOOLS/lua/autoload.lua) 
to sync all the files in a playlist.
