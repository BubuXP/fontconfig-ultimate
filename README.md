
### infinality-deb


#### Infinality font configuration files, patches, scripts and source packages for Debian and derivatives distros

Original project website: [infinality.net](http://www.infinality.net/blog/infinality-freetype-patches/)

New project website: [bohoomil.com](http://bohoomil.com)

#### Quick installation instructions

**I. If you are using Debian, Ubuntu or derivatives** you can try installing the precompiled packages from my [Google Drive](https://drive.google.com/open?id=0B7AdLMiZn4FzdGZNV2FpLWhPTkk) or, if the packages are incompatible, you can rebuild them for your distro version by yourself, using the deb sources you can also found there (and soon will be ported here).

**II. If you are an Arch Linux user, or if you are using one of the Arch Linux derivatives,** go to the [project website](http://bohoomil.com) or [in the original GitHub page](https://github.com/bohoomil/fontconfig-ultimate) for more informations.

**III. If you are using any other Linux distribution,** you can use all available resources you can found here or [in the original GitHub page](https://github.com/bohoomil/fontconfig-ultimate) to rebuild a modified `fontconfig` package, or try to make a new `fontconfig-infinality` package that can work without modifying your distro's original `fontconfig` package, like this Debian version does.



#### Further customization and misc options

* Many changes to the global `fontconfig-infinality` settings can be introduced on a per-user ground in a local `$HOME/.config/fontconfig` directory. Please, consult `/usr/share/doc/fontconfig-infinality/` for examples and templates you will need to start tweaking.

* At the moment, there are two font collections supported by `fontconfig-infinality` out of the box: a free one (activated by default, installed by dependencies of the `fontconfig-infinality` package), and a proprietary one (Microsoft's fonts supplied with MS Windows and MS Office). If you want to switch between them, use `fc-presets` script. There is also a `custom` preset available for highly customized font collections. Configuration files for the customizable presets are located in `/etc/fonts/infinality.avail/`.

* If you are using a desktop environment (KDE, GNOME, etc.) that lets you adjust font settings on its own, you should duplicate the base values as found in `/etc/X11/Xsession/99infinality-settings`, and they are:
   Antialias:  1 (enabled)
    Autohint:  0 (disabled)
         DPI:  96
     Hinting:  1 (enabled)
  Hint style:  hintfull (full)
  LCD filter:  lcddefault (default)
   Sub-pixel:  rgb

___

#### Differences with bohoomil's fontconfig-ultimate project (technical information):
* Cairo: not much, only applying the patches to the Debian packages with the needed adjustments.
* Freetype: not much, only applying the patches to the Debian package with the needed adjustments, and renaming `/etc/profile.d/infinality-settings.sh` to `/etc/X11/Xsession/99infinality-settings`.
* Fontconfig: completely different approach. While `fontconfig-ultimate` is the whole fontconfig's ArchLinux package patched and rebuild to include bohoomil's custom configurations, my `fontconfig-infinality` Debian package has been projected to leave untouched the fontconfig's Debian packages. How I did this? Before a little explanation of how fontconfig works.
   * The only admitted configuration file by Fontconfig is `/etc/fonts/fonts.conf`. In this file there is an option that tells Fontconfig to include also all the configuration files inside `/etc/fonts/conf.d`, and some of the files here say to Fontconfig to include further configuration files, e.g. `/etc/fonts/local.conf` and the user's configuration in `~/.config/fontconfig/fonts.conf`.
   * Instead of changing the original source code and rebuild, I simply created a new package that replaces the original `/etc/fonts/fonts.conf` with a custom one that will ignore `/etc/fonts/conf.d` (and all the files that branch out from there) and instead it will search in `/etc/fonts/infinality.d`. Inside this new directory, I put the bohoomil's configuration (with some little retouch), leaving apart the stock config (that we can always cherry-pick if we need). One of the advantages of this approach is that the original configurations, even if customized by the user, isn't touched at all, i.e. no deleting, no changes and no need to backup.
   * Thanks to `dpkg-divert` (used in the deb package maintainer scripts), the original `/etc/fonts/fonts.conf` will be backed up as `/etc/fonts/fonts.divert` and the new `fonts.conf` won't be overwrited by regular fontconfig updates from Debian (in that case the backed up copy will be updated). Only `fontconfig-infinality` package can update the new `fonts.conf`.
   * But `dpkg-divert` doesn't work well with conffiles and causes many problems, so I find a workaround: the new `fonts.conf` will be a symlink to the real file, that is found in `/usr/share/fontconfig/infinality.conf`.
   * Obviously, when `fontconfig-infinality` is removed, the `fonts.divert` will return back to his original name.
   * Debian policy says, more or less, that configuration files that should not be modified must stay under `/usr/share` while the ones that can be modified must go in `/etc`, so:
      * `fontconfig/customize/` content will be installed in `/etc/fonts/infinality.avail/`
      * `fontconfig/readonly/` content will be installed in `/usr/share/fontconfig/infinality.avail/`
   * symlinks to the needed .conf files in these directories will be created in `/etc/fonts/infinality.d/` to activate them (I check bohoomil's patches, build scripts and package for the default list of conf to activate).
      * symlink from `/usr/share/fontconfig/conf.avail/49-sansserif.conf` must be created in `/etc/fonts/infinality.d/`
      * optionally (but not used by bohoomil) a symlink could be also created from `/usr/share/fontconfig/conf.avail/10-scale-bitmap-fonts.conf`
   * modify bohoomil's `28-user.conf` to pass from `~/.config/fontconfig/conf.d/` to `~/.config/fontconfig/infinality.d` and from `~/.config/fontconfig/fonts.conf` to `~/.config/fontconfig/infinality.conf` for compliance with other new directories names and to leave apart old fontconfig settings without any need of changes or backups.
   * remove symlink from `/usr/share/fontconfig/infinality.avail/29-local.conf` to stop using `/etc/fonts/local.conf` so, if already present, we'll preserve it from being removed or modified for use with Infinality. And because we can already customize settings in `/etc/fonts/infinality.avail/` and in user's home.


#### TO DO:
* improve documentation.
* better handling of `35-repl-custom.conf` in `fc-presets` (needed?).
* making a script similar to `fc-presets` but for changing freetype's styles.
* include legacy fontconfig-infinality configs and presets, and mechanism to swap between legacy and ultimate config type.
* Use of `$FONTCONFIG_FILE` variable to skip the need of dpkg-divert and also for simpler implementing the legacy and ultimate presets.



___

### License

The MIT License (MIT) <http://opensource.org/licenses/MIT> Copyright (c) 2014 bohoomil

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
