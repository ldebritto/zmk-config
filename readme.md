This keymap heavily inspired by [Callum's layout for QMK](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md) and is guided by the following principles:

01. Every key should have just one way to type it, the only exception is the `LEFT_SHIFT` keycode that is both available as a HR mod behind a layer and a thumb key;
02. No hold-taps, as they are finnicky to tweak, could misfire or require long pauses. Same reasons pointed by Callum at his readme apply here. Excecption was made to accomodate `CAPS` in `DEF` and `NAV` layers, since I map it on the OS level to perform as Apple's fn key and trigger my window manager of choice ([Swish](https://highlyopinionated.co/swish/));
    - ZMK will not support firmware level Apple's fn keycode (see [Issue #947](https://github.com/zmkfirmware/zmk/issues/947) on ZMK's GitHub), but the `CAPS` keycode workaround described there works just fine;
    - This behaviour was mirrored on `NAV` to make possible to trigger iPadOS shortcuts for multitasking (such as `fn+control+left/right arrow` to tile the app to the left or `fn+up arrow` to trigger the app switcher).
03. No key combination should require more than three fingers pressed at the same time (two thumbs and one finger should be the most taxing), different mods can be combined through sticky keys (&sk behaviours);
04. Keyboard functionality (such as &bootloader and bluetooth toggles) are hidden behind combos available only in the `FUN` layer in order to make them purposelly difficult to trigger by accident;
05. Other combos should be convenience only, such as triggering Spotlight/Winddows Start menu (`f j`), [Shortcat](https://shortcat.app) (`d k`), NAV layer toggle (`left thumb keys`) and to mute the keyboard (`vol up and down` on `NAV`);
06. Tap dance is used to make double press on shift trigger &caps_word behaviour and to combine `next song` and `previous song` into the same key on `NAV`.

Its main uses are prose in both English and Portuguese as well as some light coding.

On `DEF`, `;` was moved down and made way to `'` as this is far more useful to make accents and quotes in these use cases. `/` only exists in the `SYM` layer.

There are Apple OS's set of 4 layers and Windows set for the same keys. They only differ by the position of mods on home row. MacOS layers have CMD on index fingers and CONTROL on pinkies. Windows layers will have the other way around: WIN on pinkies and CONTROL on index fingers.

This keymap requires [PR# 1366](https://github.com/zmkfirmware/zmk/pull/1366) for swapper functionality on `NAV` and `WNAV`. See ZMK.dev [documentation](https://zmk.dev/docs/features/beta-testing) to instructions on how to use PRs not yet merged into ZMK's main repo.
