# ftrimify

> See [this blog post](https://www.jamesrobinsonvfx.com/tips/2021/08/19/ftrim-function/)
> for more info on why `ftrim()` is cool.

Adds an item to the right-click menu of string parameters, as well as to the
Gear menu of any node. `ftrimify` wraps channel references like `ch()` and `chs()`
in `ftrim()`, to help round off excess precision in string parameters.


- [ftrimify](#ftrimify)
  - [Quick Overview](#quick-overview)
  - [Menu Items](#menu-items)
    - [ftrimify](#ftrimify-1)
    - [ftrimify All String Parameters](#ftrimify-all-string-parameters)
  - [Installation](#installation)
    - [Houdini Packages](#houdini-packages)
    - [Manual Installation](#manual-installation)

## Quick Overview

It's common for string parameters to add a bunch of extra digits you don't want.

Say you have a FLIP object with a particle separation of `0.1`. When
referenced in a string parameter like:

```
`chs("/obj/dopnet1/flipsolver/particlesep")`
```
it will probably come out to something like

```
0.10000000000000001
```
We can help fix it using the HScript expression [`ftrim()`](https://www.sidefx.com/docs/houdini/expressions/ftrim.html):
```
`ftrim(chs("/obj/dopnet1/flipsolver/particlesep"))`
```

## Menu Items

### ftrimify

Only string parameters will have this option added to their right-click menu.
Select it to have all `ch()` and `chs()` channel references wrapped up in
`ftrim()`.

If a channel reference is already wrapped up in `ftrim()`, it will be skipped so
that you can safely run it again if you update your node/parameter without
adding a bunch of extra `ftrim(ftrim(ftrim(ftrim(...))))`s.

### ftrimify All String Parameters

This is found in the Gear menu of any node. It runs `ftrimify` over each string
parameter on the node.

## Installation

### Houdini Packages

1. Download the latest release [here](https://github.com/jamesrobinsonvfx/ftrimify/releases/latest/download/ftrimify.zip).
   * Optionally, you can clone this repo if you'd like instead.
2. Navigate to your houdini user preferences folder and into the `packages`
   directory (if the `packages` folder does not exist, create it).
   ```
   $HOUDINI_USER_PREF_DIR/packages
   ```
3. Copy the zip archive here and extact its contents.
4. Move (or copy) the `ftrimify.json` file to the parent directory
   `$HOUDINI_USER_PREF_DIR/packages`.

5. Launch Houdini

### Manual Installation
If you prefer not to use Houdini packages for whatever reason, you can manually
copy the files to any Houdini Location (`$HSITE`, `$HOUDINI_USER_PREF_DIR`) or
anyhwere on your `$HOUDINI_PATH`.

- `ParmMenu.xml` and `ParmGearMenu.xml` should live at the root. ie. if you're moving these files into your user prefs
  folder, it should live right inside the `houdini18.5` folder.
- Copy the module `wranglegist.py` to `python2.7libs` or `python3.7libs`
  (depending on your Houdini installation version)