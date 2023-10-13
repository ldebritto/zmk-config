## Design principles

This keymap heavily inspired by [Callum's layout for QMK](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md) and is guided by the following principles:

01. **Every key should have just one way to type it**, the only exception is the `LEFT_SHIFT` keycode that is both available as a HR mod behind a layer and a thumb key;
02. **No hold-taps**, as they are finnicky to tweak, could misfire or require long pauses. Same reasons pointed by Callum at his readme apply here. Excecption was made to accomodate `CAPS` in `DEF` and `NAV` layers, since I map it on the OS level to perform as Apple's fn key and trigger my window manager of choice ([Swish](https://highlyopinionated.co/swish/));
    - ZMK will not support firmware level Apple's fn keycode (see [Issue #947](https://github.com/zmkfirmware/zmk/issues/947) on ZMK's GitHub), but the `CAPS` keycode workaround described there works just fine;
    - This behavior was mirrored on `NAV` to make possible to trigger iPadOS shortcuts for multitasking (such as `fn+control+left/right arrow` to tile the app to the left or `fn+up arrow` to trigger the app switcher).
03. **No key combination should require more than three fingers** pressed at the same time (two thumbs and one finger should be the most taxing), different mods can be combined through sticky keys (&sk behaviors), **thumbs do all the layer changing**;
04. **Keyboard functionality** (such as `&bootloader` and bluetooth toggles) are **hidden behind combos** available only in the `FUN` layer in order to make them *purposelly difficult* to trigger by accident;
05. **Other combos** should be *convenience only*, such as NAV layer toggle for extended edits (`left thumb keys`), switching default mods between macOS and windos variants, and to mute the keyboard (`vol up and down` on `NAV`);
06. **Tap dance** is used to make double press on thumb `shift` trigger `&caps_word` behavior and to combine `next song` and `previous song` into the same key on `NAV`.

## My use case and layer design choices

Its main uses are writing prose in both English and Portuguese as well as some light coding.

### QWERTY with changes on `'` `;` and `/` keys positions

Base layout is QWERTY with a few changes to optimize for my use case.

- On `DEF`, `;` was moved down and made way to `'` as this is far more useful to make accents and quotes in these use cases. 
- `/` only exists in the `SYM` layer.

### `&lc` for cancelling queued mods

A crazy long timeout (10m) was assigned to `&sk` behavior in this keymap. So there's no rush to combine mods with keycodes in other layers.

Layer keys (usually `&mo`) were replaced by a custom layer-cancel (`&lc`) macro that taps a `&kp K_CANCEL` command alongside the `&mo` command. This cancels any previoulsy `&sk` queued mods on the layer key press.

It has been rebuilt using the [parametrized macros](https://zmk.dev/docs/behaviors/macros#parameterized-macros) to allow for using the keycode `&lc` with the desired layer just

This emulates in ZMK the `LA_NAV` and `LA_SYM` custom behaviors found in [Callum's QMK keymap](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md).

### `&swapper` for swapping between apps/windows

Allows for `CMD+TAB` (`ALT+TAB` on windows layer) with just one key. It keeps the modal open until you release the layer toggle, just as you would hold `CMD` (`ALT`) between `TAB` keypresses.

On macOS, the arrow keys on `NAV` to move more deliberately between apps.

This is not native to ZMK's mainrepo and requires [PR# 1366](https://github.com/zmkfirmware/zmk/pull/1366). See ZMK.dev [documentation](https://zmk.dev/docs/features/beta-testing) for instructions on how to use PRs not yet merged into ZMK's main repo.

### Numpad for `&num_word``

A tap with right thumb key will enable `&num_word` behavior in both Apple and Windows layers. (Hold will bring the `SYM` layer with the `&lc` macro).

This behavior allows for quick entering numbers and will disable the numpad layer upon key press of any key than a number, math symbol or `BACKSPACE`/`DELETE`. 

- A second tap on the right thumb will disable `&num_word` (hold will bring `SYM`, but will not trigger the `&lc` macro).
- Mods are still accessible on `SYM`, `NAV` and `FUN` as `&sk`.

I believe this behavior was introduced to the custom mech community in QMK by [Jonas Hietala](https://www.jonashietala.se/blog/2022/09/06/the_current_t-34_keyboard_layout/#numword). This ZMK implemenation was made by [urob](https://github.com/urob/zmk-config#numword) and copied with a few modifications here.

### Apple's `Globe` key on mod-tap `Z` and `;` keys

Recently ZMK implementted a [keycode](https://zmk.dev/docs/codes#application-controls) for emulating `GLOBE`/`fn` key on Apple's keyboards. 

It's not 100% the same behavior made by Apple's keyboards (see limitations [here](https://github.com/zmkfirmware/zmk/pull/1938#issuecomment-1744579039)), but it gets the job done for my uses – wich is mainly window manipulation on both macOS and iPadOS. So I've made it into a `&mt` replicated in `DEF`, `NAV` and `SYM` on the keys used by lower pinkies.

### Apple and Windows default layers to ease the mod differences on basic shortcuts
There are two sets of the same **5 layers** for use in Apple OSs and Windows.

1. `DEF`
2. `NUM` (for `&num_word`)
3. `NAV` (left thumb key)
4. `SYM` (right thumb key)
5. `FUN` (both thumb keys)

They only differ by the position of mods on home row. MacOS layers have `CMD` on index fingers and `CONTROL` on pinkies. Windows layers will have the other way around: `WIN` on pinkies and `CONTROL` on index fingers. This makes `cmd+c` and `ctrl+c` doable with the same finger movements, easing the transition between Windows and macOS.

It uses **Apple's OSs as default**. Switching is made by a combo at the `Z` and `;` keys both on the `FUN` and `WFUN` layers.

### AOE 2 layers

I've maped my main Age of Empires II Definitive Edition shortcuts to a set of 3 layers on the left half of the keyboard.

- This is toggled on/off via combo with `WER` keys from `DEF` layer.
- Pause (`F3`) is also doable within this mode by comboing `X C V`.