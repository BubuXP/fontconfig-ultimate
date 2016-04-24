
### infinality-deb


#### Font configuration files, patches, scripts and source packages for Debian and derived distros (Infinality & friends)

Project website: [bohoomil.com](http://bohoomil.com "bohoomil.com")

#### Quick installation instructions

**I. If you are using Debian, Ubuntu, or derivatives,** you can try installing the precompiled packages from my [Google Drive](https://drive.google.com/open?id=0B7AdLMiZn4FzdGZNV2FpLWhPTkk) or, if the packages are incompatible, you can rebuild them for your distro version by yourself, using the deb sources you can also found there (and soon will be ported here).

**II. If you are an Arch Linux user, or if you are using one of the Arch Linux derivatives,** go to the [project website](http://bohoomil.com) or [in the original GitHub page](https://github.com/bohoomil/fontconfig-ultimate) for more informations.

**III. If you are using any other Linux distribution,** you can use all available resources you can found here or [in the original GitHub page](https://github.com/bohoomil/fontconfig-ultimate) to rebuild a modified `fontconfig` package, or making a new `fontconfig-infinality` that could work without modifying your distro's original `fontconfig` package.



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
