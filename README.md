# jivelite

Jivelite is a visualization software for controlling the Logitech Media Server (Squeezebox Server) playback.

-----

## Why this repo?

I ceated this repo because I want to install Jivelite on fresh arm64 system like the ones for Orange Pi Zero 3 or Orange Pi 5 etc...

The fact is JiveLite requires LuaJit.

So we are facing few difficulties:
* orignal JiveLite from Ralph Irving Repo is using an old LuaJit (2.0) for arm32. This LuaJit version is not compatible with recent arm64 architectures Linux version as explainded [here](https://luajit.org/status.html). We only can install LuaJit 2.1
* few modifications are required in order to use the JiveLite code for the last LuaJit version
* some libraires are required

So I created this repo to pack everything inside and I can run a script to simplify the installation process.

-----

sudo apt install -y git build-essential libluajit-5.1-dev libsdl1.2-dev libsdl-ttf2.0-dev libsdl-gfx1.2-dev libsdl-image1.2-dev libexpat1-dev
