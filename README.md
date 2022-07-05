
midi@3:14 is a home-made electronic keyboard for playing music.

This repository contains a program that shows the current state of the keyboard
on a PCD8544 (Nokia 5110) display. It uses the following crates:

* [pcd8544](https://github.com/tiliosys/pcd8544-rust)
* [midi314](https://github.com/tiliosys/midi314-lib)

`midi314-display` can typically be run on a Raspberry Pi SBC with a PCD8544 hat.
The pin numbers and the SPI device path are hard coded in `main.rs` at the moment but they are easy to change.

| Constant     | Value             | Role                                 |
|:-------------|:------------------|:-------------------------------------|
| `LCD_RST`    | 24                | Reset pin number                     |
| `LCD_DC`     | 25                | Data/Command pin number              |
| `LCD_SPI`    | `/dev/spidev0.0`  | SPI device file                      |
| `LCD_ORIENT` | `Portrait(false)` | Default orientation in portrait mode |

The display shows the following information:

* Pitch range: current min and max note names.
* Program range: current min and max program numbers.
* Current program or percussion mode.
* Tempo.
* Loop states: empty, recording, playing, muted.

If no LCD is attached, the program also prints the same information to the standard output.

Building
--------

Build the program using this command from the root of the source tree:

```
cargo build --release
```

Running
-------

We assume that you have followed the instructions from
[midi314-looper](https://github.com/tiliosys/midi314-looper/blob/main/README.md)
to start FluidSynth and the midi@3:14 looper program.

From the root of this source tree, start the display program:

```
./target/release/midi314-display
```

In another terminal, connect the MIDI input of the display program to the keyboard:

```
pw-link "Midi-Bridge:Arduino Leonardo:(capture_0) Arduino Leonardo MIDI 1" midi314-display:midi_in
```
