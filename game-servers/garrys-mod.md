# Garrys Mod

Autorefresh can lag the server when certain Lua files are edited. This happens when the refreshing cascades. This can be unwanted behaviour when editing the scripts of a large project on a live server.

To disable autorefresh, add `-disableluarefresh` to parms.

```text
 -disableluarefresh
```

When adding a loading screen with `sv_loadingurl`, most guides will tell you to add it in command line, server.cfg, or autoexec.cfg. Check gmodserver.cfg first, it is defined in this file by default as `sv_loadingurl ""`and this file will override everything else.

