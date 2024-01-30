## Design principles

This keymap was heavily inspired by [Callum's layout for QMK](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md) and is guided by the following principles:

01. **Every key should have just one way to type it**, the only exception is the `SHIFT` key that is both available as a HR mod behind a layer and a thumb key;

02. **Avoid hold-taps**, as they are finnicky to tweak, could misfire or require long pauses. Same reasons pointed by Callum at [his readme](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md) apply here.
    - Excecption was made to accomodate `GLOBE` in `DEF` and `NAV` layers, at the `Z` key position. This allows me to trigger my window manager of choice ([Swish](https://highlyopinionated.co/swish/)), see #5 bellow;
    - This behavior was mirrored on `NAV` to make possible to trigger iPadOS shortcuts for multitasking (such as `fn+control+left/right arrow` to tile the app to the left or `fn+up arrow` to trigger the app switcher).
    
03. **Thumbs do all the regular layer changes**. Except for the special `AOE2` gaming layers, `&smart_mouse` and `&numword`, that are toggled by combos;

04. **Keyboard functionality** (such as `&bootloader` and bluetooth toggles) is **hidden behind combos** available only in the `FUN` layer. This makes them *purposelly difficult* to trigger by accident, while still being still being accessible when needed;

05. **Other combos** should be *convenience only*, such as 
    - NAV layer toggle for extended edits (`left thumb keys`);
    - mute (`vol up and down` on `NAV`); and
    - left hand activation of some special keys (`ENTER`, `BACKSPACE`, `SPACE` and `ESCAPE`).

06. **Tap dance** is used to make double press on thumb `shift` trigger `&caps_word` behavior and to combine `next song` and `previous song` into the same key on `NAV`.

## My use case and layer design choices

Its main uses are writing prose in both English and Portuguese as well as some light coding.

### 1. QWERTY with changes on `'` `;` and `/` keys positions

Base layout is QWERTY with a few changes to optimize for my use case.

- On `DEF`, `;` was moved down and made way to `'` as this is far more useful to make accents and quotes in these use cases. 
- `/` only exists in the `SYM` layer.

### 2. Longe `&sk` timeouts and `&lc` for cancelling queued mods when triggering other layers

A crazy long timeout (10m) was assigned to `&sk` behavior in this keymap. So there's no rush to combine mods with keycodes with keys from `DEF` or whatever the currently active layer.

Layer keys (usually `&mo`) were replaced by a custom layer-cancel (`&lc`) macro that taps a `&kp K_CANCEL` command alongside the `&mo` command. This cancels any previoulsy `&sk` queued mods on the layer key press.

This design allows for _canceling_ mods only when invoking SYM, NAV, of FUN, while still _keep them triggered_ when you move back to `DEF`.

This emulates in ZMK the `LA_NAV` and `LA_SYM` custom behaviors found in [Callum's QMK keymap](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md).

It's built with the [parametrized macros](https://zmk.dev/docs/behaviors/macros#parameterized-macros) as `&lc` to allow for easier reading of the keymap and user modification.

### 3. `&swapper` for swapping between apps/windows

Allows for `CMD+TAB` with just one key. It keeps the modal open until you release the layer toggle, just as you would hold `CMD` between `TAB` keypresses.

This is *not native to ZMK's `main` repo* and requires [PR# 1366](https://github.com/zmkfirmware/zmk/pull/1366). See ZMK.dev [documentation](https://zmk.dev/docs/features/beta-testing) for instructions on how to use PRs not yet merged into ZMK's main repo.

### 4. Numpad for `&numword``

`&numword` is accessible through the `N` key in `SYM` layer or via a right thumbkeys combo. 

This behavior allows for quick entering numbers and will disable the numpad layer upon key press of any key than a number, math symbol or `BACKSPACE`/`DELETE`. I believe this behavior was introduced to the custom mech community in QMK by [Jonas Hietala](https://www.jonashietala.se/blog/2022/09/06/the_current_t-34_keyboard_layout/#numword). This ZMK implemenation was made by [urob](https://github.com/urob/zmk-config#numword) and I've copied with a few modifications here.

### 5. Apple's `Globe` key on mod-tap `Z` and `;` keys

Recently ZMK implementted a [keycode](https://zmk.dev/docs/codes#application-controls) for emulating `GLOBE`/`fn` key on Apple's keyboards. 

It's not 100% the same behavior made by Apple's keyboards (see limitations [here](https://github.com/zmkfirmware/zmk/pull/1938#issuecomment-1744579039)), but it gets the job done for my uses – wich is mainly window manipulation on both macOS and iPadOS. So I've made it into a `&mt` replicated in `DEF`, `NAV` and `SYM` on the keys used by lower pinkies.

### 6. `&smart_mouse` copied from urob's repo

Yet another feature copied from [urob's repo](https://github.com/urob/zmk-config?tab=readme-ov-file#smart-mouse).

It is activated from the `M,.` key combo, from `DEF` layer.

Also requires [PR #1366](https://github.com/zmkfirmware/zmk/pull/1366) used in `&swapper` behavior.

### 7. Special AOE 2 gaming layers

I've maped my main Age of Empires II Definitive Edition shortcuts to a set of 3 layers on the left half of the keyboard.

- This is toggled on/off via combo with `WER` keys from `DEF` layer;
- Pause (`F3`) is also doable within this mode by comboing `XCV`.