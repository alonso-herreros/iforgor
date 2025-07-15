# Minecraft Server - Arch Linux

Check the wiki: <https://wiki.archlinux.org/title/Minecraft/Java_Edition_server>

## Install the server

The `minecraft-server` package is available in the Arch User Repository (AUR)
for the latest version of Minecraft server.

```sh
yay -Syu minecraft-server
```

The server is installed to `/srv/minecraft` and the `minecraft` user is created.

### Add mods

Download the forge installer to the server directory and run it with the
`--installServer` option:

```sh
cd /srv/minecraft
wget https://maven.minecraftforge.net/net/minecraftforge/forge/${minecraftver}-${forgever}/forge-${minecraftver}-${forgever}-installer.jar
java -jar forge-${minecraftver}-${forgever}-installer.jar --installServer
```

Add the mods to the `mods` directory in `/srv/minecraft` and configure the
executable to the `run.sh` script in the server directory (see the Configure
section)

## Configure the server

The EULA must be accepted after the first run of the server.

Settings can be set in the `/etc/conf.d/minecraftd` file, including a custom
executable path.

## Operate the server

```sh
minecraftd start
```

