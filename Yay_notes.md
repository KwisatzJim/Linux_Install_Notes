### Yay notes

install a package

yay -S packagename

get a PKGbuild

yay -G packagename

print a PKGbuild

yay -Gp packagename

remove a package

yay -R packagename

remove a package and dependancies

yay -Rns packagename

upgrade aur and official

yay

upgrade just aur

yay -Sua

remove unneeded dependancies

yay -Yc

print package statistics and health

yay -Ps

| Command                         | Description                                                                                            |
|---------------------------------|--------------------------------------------------------------------------------------------------------|
| yay                             | Alias to yay -Syu.                                                                                     |
| yay <Search Term>               | Present package-installation selection menu.                                                           |
| yay -Bi <dir>                   | Install dependencies and build a local PKGBUILD.                                                       |
| yay -G <AUR Package>            | Download PKGBUILD from ABS or AUR. (yay v12.0+)                                                        |
| yay -Gp <AUR Package>           | Print to stdout PKGBUILD from ABS or AUR.                                                              |
| yay -Ps                         | Print system statistics.                                                                               |
| yay -Syu --devel                | Perform system upgrade, but also check for development package updates.                                |
| yay -Syu --timeupdate           | Perform system upgrade and use PKGBUILD modification time (not version number) to determine update.    |
| yay -Wu <AUR Package>           | Unvote for package (Requires setting AUR_USERNAME and AUR_PASSWORD environment variables) (yay v11.3+) |
| yay -Wv <AUR Package>           | Vote for package (Requires setting AUR_USERNAME and AUR_PASSWORD environment variables). (yay v11.3+)  |
| yay -Y --combinedupgrade --save | Make combined upgrade the default mode.                                                                |
| yay -Y --gendb                  | Generate development package database used for devel update.                                           |
| yay -Yc                         | Clean unneeded dependencies.                                                                           |

