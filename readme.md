![]("keymap-drawer/main layers.svg")

# Design principles

This 34 key keymap was inspired by [Callum's layout for QMK](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md) and was conceived with these principles in mind:

01. **Every key should have one way to type it**
02. **Avoid hold-taps for regular typing** to discourage holding keys and eliminate the chance of misfiring. 
	- An *excecption* was made to accomodate `GLOBE` at the `Z` key position. This allows me to trigger my window manager of choice on macOS ([Swish](https://highlyopinionated.co/swish/)) and to use iPadOS shortcuts that require this key.
    
03. **Thumbs do all the regular layer changes**. `&numword`, toggling `NAV` for extended edits/mouse usage, and toggle of gaming layers are all made by combos.

04. **Keyboard functionality** (such as `&bootloader` and bluetooth toggles) is **hidden behind combos** available from `FUN` layer. This makes them *purposelly difficult* to trigger by accident, while still being still being accessible when needed;

05. **Combos** should be *convenience only* and always preceded by `require-prior-idle` to avoid misfiring.

# My use case and layer design choices
 
Its main use is writing prose in both English and Portuguese in both macOS and iPadOS. I use in on a [Ferris Sweep](https://github.com/davidphilipbarr/Sweep) with [nice!nanos v2](https://nicekeyboards.com/nice-nano/). I find it particularly great to type on when paired with very light and silent switches, such as [LowProKB.ca's Amnbienz twilight and nocturnals](https://lowprokb.ca/products/ambients-silent-choc-switches).

## 1. QWERTY with `'`, `;` and `/` keys positions swapped

QWERTY was kept to retain muscle memory, with a few changes:

- On `DEF`, `;` was moved down and made way to `'` as this is far more useful to make accents (as dead key) and quotations
- `/` exists in the `SYM`

## 2. Long `&sk` timeouts and `&lc` macro for cancelling queued mods when triggering layers

This emulates in ZMK the `LA_NAV` and `LA_SYM` custom behaviors found in [Callum's QMK keymap](https://github.com/qmk/qmk_firmware/blob/master/users/callum/readme.md).

A crazy long timeout (1 day) was assigned to `&sk` behavior in this keymap. So there's no rush to combine mods with either keycodes from `DEF` or the active layer.

`&mo` keys were replaced by a custom layer-cancel macro (`&lc`) that sends a `&kp K_CANCEL` tap alongside the `&mo` command within a 0ms interval. This design allows for _canceling_ mods when invoking `SYM`, `NAV`, of `FUN`, while _keeping them triggered_ for typing keys that exists only on `DEF` layer.

It was built with the [parametrized macros](https://zmk.dev/docs/behaviors/macros#parameterized-macros) behavior to make the `.keymap` file easier to read and change.

## 3. `SYM` layer optimized for BR-PT prose

* I recommend pgetreuer’s post on [how to set up a symbols layer that works for you](https://getreuer.info/posts/keyboards/symbol-layer/index.html).

- ^`~ dead keys are on home row making them trivial to type accented vowels which are common in Portuguese prose
- Basic math operations and other symbols that usually follow numbers can be typed with the left hand (very useful from within `num_word`’s `&sl SYM` on the G key position);
- Parenthesis and braces are mirrored on both hands, left opens, right closes them. Slashes are also mirrored.
- Shifted punctuation symbols that exist in `DEF` and are much used in prose (`”` and `:`) from `DEF` were assigned to SYM to 
	a. make possible to trigger them single handed via `&lc SYM` 
	b. make them more convenient to type punctuated numbers from `FUN` such as when typing hours or dates or measurements (e.g. 00:00 will not require one to move the left thumb to thumb `RSHFT` and then back to the `&lc NAV` to trigger the tri-layer, same thing happens when typing 0’00”)
- Common markdown symbols (# and *) are close to home row.

## 4. Numpad for `&num_word`

* Requires [auto-layer module](https://github.com/urob/zmk-auto-layer).

`&numword` is accessible as a combo through `D` and `&lc NAV` (leftmost thumb).

Numpad layer sits at the left half of the keyboard to make it usable while holding the mouse on the right.

This behavior allows for quick entering numbers in a numpad layout and will disable it upon key press of any key than a number, math symbol or `BACKSPACE`/`DELETE`. 

This behavior was first introduced by [Jonas Hietala](https://www.jonashietala.se/blog/2022/09/06/the_current_t-34_keyboard_layout/#numword) and this ZMK implementation was made by [urob](https://github.com/urob/zmk-config#numword).

## 5. Combos for one handed use of common action keys and in combination with the mouse on the right hand

Combos where added to make it possible to use the keyboard one handed.

- There’s `&sl SYM` on a combo with both right thumbs to make it possible to enter symbols.
- One handed number entering can be done via `&num_word` combo (see #4).
- This goes well with toggling the `NAV` layer (combo with both left thumbs) for extended mouse edits while keeping these keys available with the left hand:
	- `QA` for `ESC`
	- `RF` for `ENTER`
	- `TG` for `BACKSPACE`
	- `GB` for `DELETE`

## 6. `&swapper` for swapping between apps/windows

* Requires [tri-state module](https://github.com/urob/zmk-tri-state).

This allows for `CMD+TAB` with one key from `NAV`. It will simulate holding `CMD` between `TAB` keypresses for as long as you keep the `&lc NAV` key held.

## 7. Gaming layers

I play Age of Empires II Definitive Edition and made a series of 3 layers (`AOE`, `AGS` and `ABS`) that go well with mouse usage on the right hand. They're certainly not needed, but really tucked away by a `ZXC` combo that only can be activated from within a leftmost thumb layer from either gaming (`AGS`) or default (`NAV`) modes.

# Non-upstream ZMK implementation

Some of the features used in this keymap require the implementation of non-vanilla ZMK, such as [tri-state](https://github.com/urob/zmk-tri-state) [auto-layer](https://github.com/urob/zmk-auto-layer) modules. For that, I've pointed my `west.yml` to urob's repo that already has these features merged.