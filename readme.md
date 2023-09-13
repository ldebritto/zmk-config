This keymap heavily inspired by [Callum's layout for QMK](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md) and is guided by the following principles:

01. Every key should have one way to type, the only exception is the `LEFT_SHIFT` keycode that is both available as a HR mod behind a layer and a thumb key;
02. No hold-taps, as they are finnicky to tweak and could make misfires or require long pauses, excecption was made to accomodate `CAPS` in `DEF` and `NAV` layers, since I map on the OS level to perform as Apple's fn key and trigger my window manager (Swish);
    - ZMK will not support firmware level Apple's fn keycode (see [Issue #947](https://github.com/zmkfirmware/zmk/issues/947) on ZMK's GitHub), but the `CAPS` keycode workaround described there works just fine.
03. No key combination should require more than three fingers pressed at the same time (two thumbs and one finger should be the most taxing), different mods can be combined through sticky keys (&sk behaviours);
04. Keyboard functionality (such as &bootloader and bluetooth toggles) are hidden behind combos available only in the `FUN` layer in order to make them purposelly difficult to trigger by accident.
05. Other combos should be convenience only, such as triggering Spotlight/Winddows Start menu (`f j`), Shortcat (`d k`), NAV layer toggle (`left thumb keys`) and to mute the keyboard (`vol up and down` on `NAV`).
06. Tap dance is used to make double press on shift trigger &caps_word behaviour and to combine `next song` and `previous song` into the same key on `NAV`.

Its main uses are prose in both English and Portuguese as well as some light coding.

There are Apple OS's set of 4 layers and Windows set for the same keys. They only differ by the position of mods on home row. MacOS layers have CMD on index fingers and CONTROL on pinkies. Windows layers will have the other way around: WIN on pinkies and CONTROL on index fingers.

This keymap requires [PR# 1366](https://github.com/zmkfirmware/zmk/pull/1366) for swapper functionality on `NAV` and `WNAV`. See ZMK.dev [documentation](https://zmk.dev/docs/features/beta-testing) to instructions on how to use PRs not yet merged into ZMK's main repo.
