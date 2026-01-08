# Windows Fonts on Linux

See <https://wiki.archlinux.org/title/Microsoft_fonts>



## Source


Microsoft fonts are propietary, so the best way to get them is from an existing
Windows installation or from a fresh download.


### Existing Windows installation

From <https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=ttf-ms-win11>:

> On the installed Windows 11 system fonts are usually located in
>
>     C:\Windows\Fonts
>
> and license file is
>
>     C:\Windows\System32\Licenses\neutral\_Default\Core\license.rtf


### Recent Windows install medium

From <https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=ttf-ms-win11>:

> You can freely download retail Windows 11 from
> <https://www.microsoft.com/en-us/software-download/windows11>
>
> Fonts are located in `sources/install.wim` file on the ISO, which is a
> 'Windows Imaging Format' (WIM) archive. You can extract WIM using wimextract
> (`wimlib` package) or 7z (`p7zip`).
>
>     wimextract install.wim 1 /Windows/{Fonts/"*".{ttf,ttc},System32/Licenses/neutral/"*"/"*"/license.rtf} --dest-dir fonts



## Arch Linux


### AUR

In my experience, `ttf-ms-win11-auto` didn't work, but `ttf-ms-win11` did.

#### `ttf-ms-win11`

> **Summary**:
>
> ```sh
> yay -S ttf-ms-win11 # fail
>
> # Assuming Windows in /media/windows
> cp /media/windows/Windows/Fonts/* ~/.cache/yay/ttf-ms-win11
> cp /media/windows/Windows/System32/Licenses/neutral/_Default/Core/license.rtf .cache/yay/ttf-ms-win11
>
> # Remove missing fonts from PKGBUILD
> yay --editmenu --mflags --skipinteg -S ttf-ms-win11
> ```

You'll need to copy the files to the same dir as `PKGBUILD`. Easiest way to do
this is to start the install with `yay`, let it fail, then move the files to
the cache dir.

With a Windows installation mounted at `/media/windows` and the default `yay`
cache dir:

    $ yay -S ttf-ms-win11
    ...
    $ cp /media/windows/Windows/Fonts/* ~/.cache/yay/ttf-ms-win11
    $ cp /media/windows/Windows/System32/Licenses/neutral/_Default/Core/license.rtf .cache/yay/ttf-ms-win11

Then, retry the installation:

    yay -S ttf-ms-win11

To account for old Windows install, skip validity checks:

    yay --mflags --skipinteg ...

To skip files you don't have, remove them from the `PKGBUILD`:

    yay --editmenu ...
