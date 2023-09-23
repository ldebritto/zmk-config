## Design principles

This keymap heavily inspired by [Callum's layout for QMK](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md) and is guided by the following principles:

01. Every key should have just one way to type it, the only exception is the `LEFT_SHIFT` keycode that is both available as a HR mod behind a layer and a thumb key;
02. No hold-taps, as they are finnicky to tweak, could misfire or require long pauses. Same reasons pointed by Callum at his readme apply here. Excecption was made to accomodate `CAPS` in `DEF` and `NAV` layers, since I map it on the OS level to perform as Apple's fn key and trigger my window manager of choice ([Swish](https://highlyopinionated.co/swish/));
    - ZMK will not support firmware level Apple's fn keycode (see [Issue #947](https://github.com/zmkfirmware/zmk/issues/947) on ZMK's GitHub), but the `CAPS` keycode workaround described there works just fine;
    - This behavior was mirrored on `NAV` to make possible to trigger iPadOS shortcuts for multitasking (such as `fn+control+left/right arrow` to tile the app to the left or `fn+up arrow` to trigger the app switcher).
03. No key combination should require more than three fingers pressed at the same time (two thumbs and one finger should be the most taxing), different mods can be combined through sticky keys (&sk behaviors);
04. Keyboard functionality (such as `&bootloader` and bluetooth toggles) are hidden behind combos available only in the `FUN` layer in order to make them purposelly difficult to trigger by accident;
05. Other combos should be convenience only, such as NAV layer toggle for extended edits (`left thumb keys`), switching default mods between macOS and windos variants, and to mute the keyboard (`vol up and down` on `NAV`);
06. Tap dance is used to make double press on thumb `shift` trigger `&caps_word` behavior and to combine `next song` and `previous song` into the same key on `NAV`.

## Use case and layer design choices

Its main uses are prose in both English and Portuguese as well as some light coding.

### Apple and Windows default layers to make it kinda OS agnostic
There are Apple OS's set of 5 layers and Windows set for the same keys. They only differ by the position of mods on home row. MacOS layers have `CMD` on index fingers and `CONTROL` on pinkies. Windows layers will have the other way around: `WIN` on pinkies and `CONTROL` on index fingers.

It uses Apple's OSs as default. Switching is made by a combo at the `A` and ` keys both on the `FUN` and `WFUN` layers.

### QWERTY with changes on `'` `;` and `/` keys positions

Base layout is QWERTY with a few changes to optimize for my use case.

On `DEF`, `;` was moved down and made way to `'` as this is far more useful to make accents and quotes in these use cases. 

`/` only exists in the `SYM` layer.

### Layer macros for cancelling queued mods

An really long timeout (10s) was assigned to `&sk` behavior in this keymap. So there's no rush to combine mods with keycodes and trigger them on the desired layer.

Layer keys (usually `&mo`) were replaced by macros that insert a `&kp K_CANCEL` command between the `&mo` press and release. This will cancel any previoulsy `&sk` queued mods on pressing any layer key, even before their timeout. 

It uses macro behavior found in ZMK's main repo.

This emulates in ZMK the `LA_NAV` and `LA_SYM` custom behaviors found in [Callum's QMK keymap](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md).

### Swapper functionality

Allows for `CMD+TAB` (`ALT+TAB` on windows layer) with just one key. It keeps the modal open until you release the layer toggle, just as you would hold `CMD` (`ALT`) between `TAB` keypresses.

On macOS, you can even use the arrow keys on `NAV` to move more deliberately between apps.

This is not native to ZMK's mainrepo and requires [PR# 1366](https://github.com/zmkfirmware/zmk/pull/1366). See ZMK.dev [documentation](https://zmk.dev/docs/features/beta-testing) for instructions on how to use PRs not yet merged into ZMK's main repo.

### Numpad

A combo with both right thumbs keys will enable `&num_word` behavior in both Apple and Windows layers. 

This behavior allows for quick entering numbers and will disable the numpad layer upon key press of any key than a number, math symbol or `ENTER` `DELETE` and `BACKSPACE`. 

This behavior was introduced to the community by [Jonas Hietala](https://www.jonashietala.se/blog/2022/09/06/the_current_t-34_keyboard_layout/#numword). It's ZMK implemenation was made by [urob](https://github.com/urob/zmk-config#numword).