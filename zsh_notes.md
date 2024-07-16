### zsh notes

brew plugin:

| Alias  | Command                             | Description                                                        |
|--------|-------------------------------------|--------------------------------------------------------------------|
| bcubc  | brew upgrade --cask && brew cleanup | Update outdated casks, then run cleanup                            |
| bcubo  | brew update && brew outdated --cask | Update Homebrew data, then list outdated casks                     |
| brewp  | brew pin                            | Pin a specified formula so that it's not upgraded                  |
| brews  | brew list -1                        | List installed formulae or the installed files for a given formula |
| brewsp | brew list --pinned                  | List pinned formulae, or show the version of a given formula       |
| bubc   | brew upgrade && brew cleanup        | Upgrade outdated formulae and casks, then run cleanup              |
| bubo   | brew update && brew outdated        | Update Homebrew data, then list outdated formulae and casks        |
| bubu   | bubo && bubc                        | Do the last two operations above                                   |
| buf    | brew upgrade --formula              | Upgrade only formulas (not casks)                                  |

git plugin:

| gcl | git clone --recurse-submodules |
|-----|--------------------------------|
| ghh | git help                       |

aliases plugin:

| acs           | show all aliases by group                 |
|---------------|-------------------------------------------|
| acs <keyword> | filter aliases by <keyword> and highlight |

alias-finder plugin:

alias-finder “<command>”

archlinux plugin:

| Alias        | Command                         | Description                                                  |
|--------------|---------------------------------|--------------------------------------------------------------|
| pacin        | sudo pacman -S                  | Install packages from the repositories                       |
| pacins       | sudo pacman -U                  | Install a package from a local file                          |
| pacinsd      | sudo pacman -S --asdeps         | Install packages as dependencies of another package          |
| paclean      | sudo pacman -Sc                 | Clean out old and unused caches and packages                 |
| pacloc       | pacman -Qi                      | Display information about a package in the local database    |
| paclocs      | pacman -Qs                      | Search for packages in the local database                    |
| paclr        | sudo pacman -Scc                | Remove all files from the cache                              |
| paclsorphans | sudo pacman -Qdt                | List all orphaned packages                                   |
| pacmir       | sudo pacman -Syy                | Force refresh of all package lists after updating mirrorlist |
| pacre        | sudo pacman -R                  | Remove packages, keeping its settings and dependencies       |
| pacrem       | sudo pacman -Rns                | Remove packages, including its settings and dependencies     |
| pacrep       | pacman -Si                      | Display information about a package in the repositories      |
| pacreps      | pacman -Ss                      | Search for packages in the repositories                      |
| pacrmorphans | sudo pacman -Rs $(pacman -Qtdq) | Delete all orphaned packages                                 |
| pacupd       | sudo pacman -Sy                 | Update and refresh local package, ABS and AUR databases      |
| pacupg       | sudo pacman -Syu                | Sync with repositories before upgrading packages             |
| pacfileupg   | sudo pacman -Fy                 | Download fresh package databases from the server             |
| pacfiles     | pacman -F                       | Search package file names for matching strings               |
| pacls        | pacman -Ql                      | List files in a package                                      |
| pacown       | pacman -Qo                      | Show which package owns a file                               |

| Alias   | Command               | Description                                                       |
|---------|-----------------------|-------------------------------------------------------------------|
| yaconf  | yay -Pg               | Print current configuration                                       |
| yaclean | yay -Sc               | Clean out old and unused caches and packages                      |
| yaclr   | yay -Scc              | Remove all files from the cache                                   |
| yain    | yay -S                | Install packages from the repositories                            |
| yains   | yay -U                | Install a package from a local file                               |
| yainsd  | yay -S --asdeps       | Install packages as dependencies of another package               |
| yaloc   | yay -Qi               | Display information about a package in the local database         |
| yalocs  | yay -Qs               | Search for packages in the local database                         |
| yalst   | yay -Qe               | List installed packages including from AUR (tagged as "local")    |
| yamir   | yay -Syy              | Force refresh of all package lists after updating mirrorlist      |
| yaorph  | yay -Qtd              | Remove orphans using yay                                          |
| yare    | yay -R                | Remove packages, keeping its settings and dependencies            |
| yarem   | yay -Rns              | Remove packages, including its settings and unneeded dependencies |
| yarep   | yay -Si               | Display information about a package in the repositories           |
| yareps  | yay -Ss               | Search for packages in the repositories                           |
| yaupd   | yay -Sy               | Update and refresh local package, ABS and AUR databases           |
| yaupg   | yay -Syu              | Sync with repositories before upgrading packages                  |
| yasu    | yay -Syu --no-confirm | Same as yaupg, but without confirmation                           |

to uncompress any kind of archive or compressed file:

extract (filename)

nmap plugin:

| nmap_open_ports            | scan for open ports on target.                                                                            |
|----------------------------|-----------------------------------------------------------------------------------------------------------|
| nmap_list_interfaces       | list all network interfaces on host where the command runs.                                               |
| nmap_slow                  | slow scan that avoids to spam the targets logs.                                                           |
| nmap_fin                   | scan to see if hosts are up with TCP FIN scan.                                                            |
| nmap_full                  | aggressive full scan that scans all ports, tries to determine OS and service versions.                    |
| nmap_check_for_firewall    | TCP ACK scan to check for firewall existence.                                                             |
| nmap_ping_through_firewall | host discovery with SYN and ACK probes instead of just pings to avoid firewall restrictions.              |
| nmap_fast                  | fast scan of the top 300 popular ports.                                                                   |
| nmap_detect_versions       | detects versions of services and OS, runs on all ports.                                                   |
| nmap_check_for_vulns       | uses vulscan script to check target services for vulnerabilities.                                         |
| nmap_full_udp              | same as full but via UDP.                                                                                 |
| nmap_traceroute            | try to traceroute using the most common ports.                                                            |
| nmap_full_with_scripts     | same as nmap_full but also runs all the scripts.                                                          |
| nmap_web_safe_osscan       | little "safer" scan for OS version  as connecting to only HTTP and HTTPS ports doesn't look so attacking. |
| nmap_ping_scan             | ICMP scan for active hosts.                                                                               |

