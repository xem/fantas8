Fantas8
=======

Introduction
------------

Fantas8 is a 8-bit-ish fantasy console.
<br>It displays a 128\*128px screen with a 60fps framerate.
<br>8 palettes of 4 colors can be set from a list of 64 colors (4 palettes for the background and 4 for the foreground).
<br>128 4-color graphic tiles can be set, measuring 8\*8px (or 32 measuring 16\*16px). They can contain custom pixel-art or text.
<br>An unique 256*256px tiled background image is available, made of 32\*32 tiles, each tile associated to a background palette. 
<br>A background color can also be set, as well as a global lighting (progressive fade to black or white).
<br>Up to 64 foreground sprites can be set (64 of size 8\*8px or 16 of size 16\*16px),
<br>each sprite can be placed on the screen, associated to a foreground palette, or removed.
<br>The background and the sprites can be edited, moved, scaled, mirrored and rotated at any moment, even mid-frame.
<br>The screen's viewport can be placed anywhere on a 256\*256px global area, with horizontal and vertical wrapping.
<br>Audio can be performed using 4 channels: wave 1, wave 2 (for melodies), triangle (for bass) and noise (for sound fx).
<br>127 global 8-bit variables can be set, modified and read. 1024 bytes of RAM are also available to store and compute arrays.
<br>Controls are bound to the keyboard's arrow keys (or ZQSD or WASD), X, C and Enter. Gamepads are also supported.
<br>The game's code is written using a specific language (see below). An editor/debugger is included in the project.
<br>Code, graphics and sound are exported as compressed text, so mini-games can be shared in a tweet, message or URL.

Syntax
------

The code editor allows one instruction per line.
<br>The number of lines is limited to 32768.
<br>The execution starts at line 0.
<br>Inline comments are allowed (`// comment`).

1) Variables

```js
  // Set or modify a global variable.
  // Variable names must start with a letter and can contain letters, numbers and "_".
  // 127 variables are available (a 128th variable is reserved for immediate Math operands).
  // These variables can either be 8-bit signed integers, or arrays of 8-bit signed integers.
  // Arrays can contain up to 128 items, and are zeroed by default.
  
  a = 2;
  b = 4;
  c = -20;
  d = c;
  
  e = [];
  f = [1, 2, 3];
  f[3] = 4;
  e[1] = f[2];
```
  
2) Functions
  
```js
  // Declare a function.
  // Function names must start with a letter and can contain letters, numbers and "_".
  // Functions have no local variables or parameters, everything is global.
  draw = function {
    ...
  }
  
  // When a function is called, its code is executed then the program continues just after the function call.
  draw();
```
  
3) Maths

```js
  // All operations are performed on a variable (like here, "a") or an array index (a[i]).
  // The second operand (like here, "b") can be either a variable, an array index, or an explicit number.
  // All fractional results are rounded.
  // All the numbers are signed 8-bit integers, ranging from -128 to 127.
  // Overflows result in a wrap: for example, 127 + 1 = -128; -128 - 1 = 127. 

  // Addition
  a += b; // a = 6
  
  // Subtraction
  a -= b; // a = 2
  
  // Multiplication
  a *= b; // a = 8
  
  // Floored division
  a /= b; // a = 2
  
  // Modulo
  a %= b; // a = 2
  
  // Power
  a **= b; // a = 4
  
  // Root
  a = sqrt(16); // a = 4 
  
  // Shift
  a >>= 1; // a = 3;
  a <<= 3; // a = 32;
  
  // And
  a &= b;  // a = 0;
  
  // Or
  a |= b;  // a = 36
  
  // Xor
  a ^= b;  // a = 36;
  
  // Trigonometry
  // All the angles are measured in 256ths of a turn (-128 = -180° ; 0 = 0° ; 127 = 180°).
  // The result of cos/sin is multiplied by 127 (-127 = -1 ; 0 = 0 ; 127 = 1).
  // The result of tan is rounded and capped to +/- 127.
  a = cos(angle);
  a = sin(angle);
  a = tan(angle);
  a = acos(b);
  a = asin(b);
  a = atan(b);
  a = atan2(b,c);
  
  // Hypotenuse (root of sum of squares)
  a = hypot(b, c);
  
  // Random (integer between 0 and 127)
  a = random();
  
  // Min/max
  a = min(b, c);
  a = max(b, c);
```

4) Tests
  
```js
  // Tests are used to check or compare the value of a variable with another variable or a number.
  // Tests can be nested too.
  
  if(a){
    ...
  }
  
  if(a == b){
    ...
  }
  
  if(a != b){
    ...
  }
  
  if(a < b){
    ...
  }
  
  if(a > b){
    ...
  }
  
  // Optional: a "else" block can follow a test.
  else {
    ...
  }
```
  
5) Loops

```js
  // For-loops involve a single variable that is incremented or decremented, and tested.
  for(i = 0; i < 127; i++){
    ...
  }
```

API
---

1) Graphics

a) palette

```js
  // palette() is used to set or modify a palette.
  // param i: 0-3 for a background palette, 4-7 for a foreground palette.
  // params color1-4 (array): indexes of the 4 colors picked in the global palette (0-63).
  // when it's modified, every subsequent tile using it will be drawn with the new colors.
  // The global palette is similar to the NES, with transparent on the last column (see [palette.png](palette.png)).
  palette(i, [color1, color2, color3, color4]);
```

b) graphic tiles

```js

  // Raw tiles are stored in a 64*2 cells grid, each cell measuring 8*8px.
   ___ ___ ___ ___ ___       ___ ___ ___ ___ 
  | 0 | 1 | 2 | 3 | 4 | ... |60 |61 |62 |63 |
  |___|___|___|___|___| ... |___|___|___|___|
  |64 |65 |66 |67 |68 | ... |124|125|126|127|
  |___|___|___|___|___| ... |___|___|___|___|
  
  // tile_8() is used to set or modify any 8*8px graphic tile.
  // The tile's content can be either a bitmap (pixel art) or text (one Unicode character).
  // For bitmap, each pixel can have 4 possible values (0, 1, 2, 3), corresponding to the 4 colors of a palette.
  // A tile_8 can overwrite a quarter of a tile_16.
  // If no value is set, the tile is reset.
  // param i: 0-128.
  // param value (optional): tile content (array or char).
  tile_8(i, [bitmap]);
  tile_8(i, "char");
  tile_8(i); // reset
  
  // tile_16() is used to set or modify 4 tiles at once, in order to make a single 16*16px tile.
  // The param i can only be a multiple of 2 between 0 and 62.
  // A tile_16 can overwrite one or many tile_8.
  tile_16(i, [bitmap]);
  tile_16(i, "char");
  tile_16(i); // reset
```

c) background

All the following functions can be called between two scanlines or between two pixels of a scanline to produce interesting effects.

```js
  // bg_color() is used to set or modify the default background color.
  // param c: color picked in the global palette (0-63).
  background_color(c);
  
  // bg_tile_8() is used to place a 8*8px tile in the 256*256px tiled background.
  // It's possible to use a quarter of a 16*16px tile set with tile_16().
  // Background tiles are transparent by default.
  // param tile_x: 0-31.
  // param tile_y: 0-31.
  // param tile_index: 0-128.
  // param palette: 0-3.
  // param h_mirror: mirrors the tile horizontally if set.
  // param v_mirror: mirrors the tile vertically if set.
  bg_tile_8(tile_x, tile_y, tile_index, palette, h_mirror, v_mirror);
  
  // bg_tile_16() places 4 tiles at once in the tiled background.
  // It's possible to call this function even if the 4 tiles have been set with tile_8().
  bg_tile_16(tile_x, tile_y, tile_index, palette, h_mirror, v_mirror);
  
  // bg_reset() removes one or all tiles from the background.
  // param tile_x (optional): 0-31.
  // param tile_y (optional): 0-31.
  bg_reset(tile_x, tile_y); // remove one tile
  bg_reset()                // remove all tiles
  
  // bg_center() is used to set the transformation center of the background.
  // param x: -128 - 127.
  // param y: -128 - 127.
  // default value: 0, 0 (the center).
  bg_center(x, y);
  
  // bg_translate() is used to offset the background inside the global area (no wrap if it overflows in any direction).
  // param tx:: -128 - 127.
  // param ty:: -128 - 127.
  // default value: 0, 0.
  bg_translate(tx, ty);
  
  // bg_scale() is used to stretch the background horizontally and/or vertically around the point set in bg_center().
  // param sx:: -128 - 127 (in %).
  // param sy:: -128 - 127 (in %).
  // default value: 100, 100.
  bg_scale(sx, sy);

  // bg_rotate() is used to rotate the background around the point set in bg_center().
  // param a:: -128 - 127.
  // default value: 0.
  bg_rotate(a);
  
  // bg_reset_transform() is used to reset the background's translations, scales and rotations to their default values.
  // NB: these transformations can be done in any order, and multiple times if necessary (ex: rotate, then translate, then scale twice).
  bg_reset_transform();
```

d) sprites

```js
  // sprite_8() is used to set or modify a 8*8px foreground item.
  // A total of 64 sprites (which can be any size) is available.
  // param sprite: 0-63.
  // param tile: 0-127.
  // param palette: 4-7.
  sprite_8(sprite, tile, palette);
  
  // sprite_16() is used to set or modify a 16*16px foreground item.
  // param sprite: 0-62 (only multiples of 2 are allowed).
  // param tile: 0-62.
  // param palette: 4-7.
  sprite_16(sprite, tile, palette);
  
  // move_sprite() is used to place or move a foreground item in the global area
  // param sprite: 0-63.
  // param x: -128 - 127.
  // param y: -128 - 127.
  // param h_mirror: mirrors the tile horizontally if set.
  // param v_mirror: mirrors the tile vertically if set.
  move_sprite(i, x, y, h_mirror, v_mirror);
  
  // remove_sprite() is used to stop drawing a given sprite.
  remove_sprite(i);
```

(todo? scale/rotate sprites too)

3) Audio

```js
  // sound() emits a sound instantly in one of the four channels.
  // If a note was already playing in this channel, it is stopped.
  // param c: channel (0 = wave1, 1 = wave2, 2 = triangle, 3 = noise).
  // param note: 0-87 (similar to piano keys: 0 = A0 = 27.5Hz; 87 = C8 = 4186.01Hz).
  // param duration: 0-127 (in 1/10ths of a second, 0 = infinite).
  // List of frequencies: [frequencies.png](frequencies.png).
  sound(c, note, duration);
  
  // melody() plays a list of notes with a given duration and offset between each note.
  // The melody will play in loop until it is stopped with sound_off().
  melody(c, duration, offset, [notes]);
  
  // sound_off() stops the sound emitted by a channel.
  sound_off(c);
```

4) Controls

At any moment, the program can check if one or many buttons are pressed.

```js
  // key() tells if a given key is currently pressed (0 = no, 1 = yes).
  // param n: key index.
  a = key(0); // left 
  a = key(1); // up
  a = key(2); // right
  a = key(3); // down
  a = key(4); // x
  a = key(5); // c
  a = key(6); // start
```

3) System

a) wait

```js
  // Wait for next frame.
  // The current frame rendering will be completed.
  wait_frame();
  
  // Wait for a specific scanline in the current frame.
  // All the screen's lines will be rendered up to that one.
  // param n: 1 - 127.
  wait_line(l);
  
  // Wait for a specific pixel in the current scanline.
  // All the current line's pixels will be rendered up to that one.
  // param p: 1 - 127.
  wait_pixel(p);
```

b) scroll screen (move viewport inside global area)

```js
  // [-128:-128]                [127:-128]
  //       ________________________
  //      | ----------             |
  //      ||          |    global  |
  //      || viewport |    area    |
  //      ||          |            |
  //      ||__________|            |
  //      |            x           |
  //      |             [0,0]      |
  //      |                        |
  //      |                        |
  //      |                        |
  //      |________________________|
  // [-128: 127]                [127:127]
  //
  // scroll() moves the 128*128px viewport inside the 256*256px global area.
  // default position is top left ([-128:127]).
  // param x: -128 - 127.
  // param y: -128 - 127.
  scroll(x, y);
```

c) global lighting

```js
  // light() fades all the screen to black or white.
  // param n: -128 = black, 127 = white.
  // default value: 127.
  light(n);
```

d) loop

```js
  // you can declare one special loop() function in your program.
  // It will be called at the beginning of each frame.
  loop = function (){
    
    // compute stuff
    
    // render stuff
    
    wait_frame();
  }  
```

e) time

```js
  // get_frame(), get_minute() and get_second() return the elapsed time since startup or last reset.
  // Current frame, second and minute are between 0 and 59, and increase automatically.
  // pause() and resume() stops and resume the time counters.
  // reset_time() resets the current minute, second and frame to 0.
  get_minute(); // 2
  get_second(); // 36
  get_frame();   // 11  => 2 min 36 sec 11 frames
  pause();
  resume();
  reset_time(); // => 0 min 0 sec 0 frame
```