<div align="center">

# Binding of Isaac Lua API

A VSCode Extension to add support and autocomplete for The Binding of Isaac: Repentance modding API to the Lua Language Server by Sumneko.

[![Open in VSCode](https://img.shields.io/static/v1?logo=visualstudiocode&label=&message=Open%20in%20Visual%20Studio%20Code&labelColor=2c2c32&color=007acc&logoColor=007acc)](https://open.vscode.dev/Filloax/isaac-lua-api-vscode) [![Build Status](https://github.com/ManticoreGamesInc/vscode-core/workflows/CI/badge.svg)](https://github.com/Filloax/isaac-lua-api-vscode/actions?workflow=CI) [![Marketplace Version](https://img.shields.io/visual-studio-marketplace/v/Filloax.isaac-lua-api-vscode?label=Visual%20Studio%20Marketplace&logo=visual-studio-code "Current Version")](https://marketplace.visualstudio.com/items?itemName=Filloax.isaac-lua-api-vscode)

![](https://i.imgur.com/iZDP2iy.png)

</div>

This extension uses the [Lua Language Server](https://microsoft.github.io/language-server-protocol/) by [Sumneko](https://marketplace.visualstudio.com/items?itemName=sumneko.lua) to add autocomplete for The Binding of Isaac: Repentance's modding API with [EmmyLua](https://github.com/sumneko/lua-language-server/wiki/EmmyLua-Annotations) annotations.

> Tired of having to go to the [docs](https://wofsauge.github.io/IsaacDocs/rep/) every time you want to mod any small thing? Of having to run the whole game to find out if you made an error that would have been immediately visible in the editor in any other language? Or just want an autocomplete that isn't "here's every single function name I found in the mod folder"? Then this might help you.

This extension is based on the [isaac-api-autocomplete-lua](https://github.com/filloax/isaac-api-autocomplete-lua) repository.

## How to use

First off, the extension won't be active by default even if enabled for convenience (not having to manually disable-enable it in each workspace), but instead it will detect if your workspace matches an Isaac mod (contains a metadata.xml file and lua files), then will ask you for confirmation, once per workspace. It also works if metadata.xml etc are in subfolders. You can also manually enable or disable the mod with a palette command, even if you initially answered otherwise.

By default, with the extension global functions like `Game()`, `Vector(x, y)` and `Isaac.xxx` should already be recognized. To have it work for callback parameters, you'll need to add `---@param` tags, like so:

```Lua
---@param npc EntityNPC
---@param intParameter integer
---@param source EntityRef
local myCallbackFunction(_, npc, intParameter, source)
```

Autocomplete should work with the type specifications too, so it shouldn't be too annoying. You should also do this for any other function where you want the autocomplete to work on its params, also adding `---@return` for return types.

You can also use `---@type` for specific variables, more info on the [annotation documentation](https://github.com/sumneko/lua-language-server/wiki/EmmyLua-Annotations). Example:

```Lua
---@type ItemConfig_Item
local item = [etc.]
```

More examples:

![](https://i.imgur.com/1BiL3CE.png)
![](https://i.imgur.com/WnC5IFv.png)

## Extension Settings

This extension has no settings; you can configure behavior in the Lua Language Server extension settings.

## Known Issues

There are some issues on the Lua Language Server (which otherwise is very very good) side. They might be fixed when the language server is updated.

- Vector multiplication/division doesn't support number-vector operators such as

```
local a = Vector(0,1)
local b = 2 * a
```

## Release Notes

See [CHANGELOG.md](CHANGELOG.md) for full changes.

## 1.5.0

Now automatically detects if the folder is an Isaac mod, and asks the user for confirmation. See the top of the README for info.

## 1.3.0

- Use vscode-lua's 3.5.0 new features:
    - @operator: Vectors and other classes with custom operators should work, currently doesn't support number-vector operators such as

    ```
    local a = Vector(0,1)
    local b = 2 * a
    ```
    - @enum: Enums are now properly defined as enum types
- Fix EntityPlayer:UseActiveItem overloading
- Fix removing old versions of library

## 1.2.0

- Settings are now applied locally to the project, without affecting the global settings of the Lua extension, will be configurable in the future on a per-project basis
- Added "workspaceSettings" setting to disable changing base VSCode settings (ie anm2 to XML file associations)

### 1.1.0

- Added enums to the autocomplete.

### 1.0.0

- Initial release.