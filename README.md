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

## Code changes

common.h, line 62

```
/*#include <SDL.h> RC*/
#include "/usr/include/SDL/SDL.h"
```

jive.h, line 13

```
/* #include <SDL_image.h> */
#include "/usr/include/SDL/SDL_image.h"

/*#include <SDL_ttf.h> */
#include "/usr/include/SDL/SDL_ttf.h"

/*#include <SDL_gfxPrimitives.h> */
#include "/usr/include/SDL/SDL_gfxPrimitives.h"

/*#include <SDL_rotozoom.h>*/
#include "/usr/include/SDL/SDL_rotozoom.h"
```

jive_framework.c, line 12
```
#ifndef __APPLE__
/*#include <SDL_syswm.h>*/
#include "/usr/include/SDL/SDL_syswm.h"
```

lua_cjson.c, line 1302

```
#if !defined(LUA_VERSION_NUM) || LUA_VERSION_NUM < 502
/* Compatibility for Lua 5.1.
 *
 * luaL_setfuncs() is used to create a module table where the functions have
 * json_config_t as their first upvalue. Code borrowed from Lua 5.2 source. */
/* static void luaL_setfuncs (lua_State *l, const luaL_Reg *reg, int nup) */
void luaL_setfuncs (lua_State *l, const luaL_Reg *reg, int nup)

lxplib.c, line 533

static const struct luaL_Reg lxp_funcs[] = {
  {"new", lxp_make_parser},
  {NULL, NULL}
};
```


sudo apt install -y git build-essential libluajit-5.1-dev libsdl1.2-dev libsdl-ttf2.0-dev libsdl-gfx1.2-dev libsdl-image1.2-dev libexpat1-dev
