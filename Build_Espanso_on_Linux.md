### Build espanso on linux

Compiling from sources
Prerequisites
These are the basic tools required to build espanso:

A recent Rust compiler. You can install it following these instructions: https://www.rust-lang.org/tools/install

A C/C++ compiler. On Linux, you should use the default C/C++ compiler (it's usually GCC). If you run the command specified in the next step, this will be included automatically.

Install the required linux packages:

On Ubuntu/Debian run:
```
sudo apt update && sudo apt install build-essential git wl-clipboard libxkbcommon-dev libdbus-1-dev libwxgtk3.0-gtk3-dev libssl-dev
```

On Fedora run:
```
sudo dnf install @development-tools gcc-c++ wl-clipboard libxkbcommon-devel dbus-devel wxGTK-devel.x86_64
```

On Arch Linux: 
```
sudo pacman -S base-devel wxwidgets-common wxwidgets-gtk3
```

Espanso heavily relies on cargo make for the various packaging steps. You can install it by running:

```
cargo install --force cargo-make --version 0.34.0
```

### Compiling Espanso

Once you've got all the prerequisites, you can:

#### Clone the Espanso repository

```
git clone https://github.com/federico-terzi/espanso
```

```
cd espanso
```

#### Compile espanso in release mode

##### NOTE: this will take a while (~5/15 minutes)

```
cargo make --profile release --env NO_X11=true build-binary
```

At this point, you should have the espanso binary available in the target/release/ directory.

#### Installing Espanso

Once you've compiled Espanso, you can move it into the final location. A good option would be the /usr/local/bin folder:

```
sudo mv target/release/espanso /usr/local/bin/espanso
```

The process is almost complete, you just need to grant the required capabilities.

#### Adding the required Capabilities

Espanso requires access to the /dev/input/eventX and /dev/uinput interfaces to detect triggers and inject expansions respectively. Although you could run it as root to grant the necessary permissions, Espanso supports a safer alternative that consists in adding the CAP_DAC_OVERRIDE capability to the binary's set of Permitted ones. To do so, run the following command:

```
sudo setcap "cap_dac_override+p" $(which espanso)
```

SECURITY CONSIDERATIONS
In a nutshell, this capability grants Espanso the permissions to read and write to any file in the system, but only when explicitly activated by the binary itself.

To limit the attack surface, Espanso performs the following steps:

When started, the CAP_DAC_OVERRIDE capability is contained in the Permitted set. At this point, Espanso CANNOT access arbitrary files in the system, as this is only possible once the CAP_DAC_OVERRIDE is moved to the Effective set.

After a partial initialization of the various modules, Espanso moves the CAP_DAC_OVERRIDE permission to the Effective set and opens the necessary interfaces to the /dev/input/eventX and /dev/uinput files.

Immediately after, the Permitted and Effective sets are cleared, meaning Espanso cannot access privileged files anymore. Moreover, because the Permitted set was cleared as well, the process won't be able to grant the permission again.

In short, Espanso uses the CAP_DAC_OVERRIDE permission only when opening the /dev/input* interfaces, and ungrant that permission immediately after.

For more information on Linux capabilities, see: https://man7.org/linux/man-pages/man7/capabilities.7.html

Final steps
Now run `espanso --version`. If you see the version appear, it means Espanso was successfully installed!

To complete the configuration, run these commands:

#### Register espanso as a systemd service (required only once)

```
espanso service register
```

#### Start espanso

```
espanso start
```

#### Updating espanso

```
git pull
cargo make --profile release --env NO_X11=true build-binary
espanso stop
sudo mv target/release/espanso /usr/local/bin/espanso
sudo setcap "cap_dac_override+p" $(which espanso)
espanso start
```
