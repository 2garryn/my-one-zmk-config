# ZMK Firmware for Ergonaut One keyboard

This is a repository for a ZMK Firmware for Ergonaut One keyboard.

> **Dongle build**
> This config is set up for a **3-piece dongle layout**: a third XIAO BLE
> (the *dongle*) acts as the BLE central and plugs into your computer over USB,
> while both keyboard halves connect to it as wireless peripherals. The dongle
> stays connected to the host, so neither half ever talks to the computer
> directly. See [How to flash the keyboard?](#how-to-flash-the-keyboard) and
> [How to pair halves?](#how-to-pair-halves) for the dongle-specific steps.

## Default keymap

Visual representation of the default keymap in keyboard-layout-editor: [KLE](http://www.keyboard-layout-editor.com/#/gists/13d0f7ae7a8b5835efcd23d61f50336a)

Below representation was generated with [`keymap-drawer`](https://github.com/caksoylar/keymap-drawer) – check out the automatically generated layouts using the [automated Github workflow](https://github.com/caksoylar/keymap-drawer/tree/main#setting-up-an-automated-drawing-workflow) for each keyboard in the [`keymap-drawer` folder](keymap-drawer/), which is always up to date with the config.

![Keymap Representation](./keymap-drawer/ergonaut_one.svg?raw=true "Keymap Representation")

This layout is heavily inspired from [Watchman 42-key layout](https://github.com/aroum/Watchman-layouts)

## FAQ

- [FAQ](#faq)
  - [How to change the keymap?](#how-to-change-the-keymap)
  - [How to flash the keyboard?](#how-to-flash-the-keyboard)
  - [How to pair halves?](#how-to-pair-halves)
  - [Problems](#problems)
    - [I'm getting File Transfer Error after copying firmware to the keyboard](#im-getting-file-transfer-error-after-copying-firmware-to-the-keyboard)

### How to change the keymap?

1. Fork or use this repository as a template https://github.com/ergonautkb/one-zmk-config.
2. Enable Github Actions for your repository.

You have two options on how to configure your desired keymap:

#### Option 1. Keymap Editor

1. Open [Keymap Editor](https://nickcoutsos.github.io/keymap-editor/).
2. Connect it to your Github account and give an access to your repository to Keymap Editor's app.
3. Make changes to your keymap and press `Save` - it will trigger software build. Wait for it to complete.
4. Grab the `firmware.zip` archive.

#### Option 2. Manual

1. Make changes to the [ergonaut_one.keymap](config/ergonaut_one.keymap) file using your favorite text editor.
2. Commit changes to your repository.
3. Go to `Actions` tab in your Github repository, locate the latest build and wait for it to complete.
4. Grab the `firmware.zip` archive

### How to flash the keyboard?

1. Obtain `firmware.zip`
2. Unzip `firmware.zip` - you should have these files:
   - `ergonaut_one_left-xiao_ble-zmk.uf2` – left half
   - `ergonaut_one_right-xiao_ble-zmk.uf2` – right half
   - `ergonaut_one_dongle-xiao_ble-zmk.uf2` – dongle (BLE central / USB)
   - `settings_reset-xiao_ble-zmk.uf2` – clears stored Bluetooth bonds, see [How to pair halves?](#how-to-pair-halves)
3. For the device you want to flash, connect it to the PC via USB-C cable (for the halves, turn off the power first by moving the slider to `OFF`)
4. Press `RESET` button **twice** to enter DFU mode - you should see new USB device in your file manager
5. Copy the corresponding firmware to the root directory of the new USB device
6. Disconnect the device from the PC
7. Repeat steps 3-6 for the remaining devices

Flash all three pieces (`left`, `right`, and `dongle`). The dongle is the only piece you keep plugged into the computer.

### How to pair halves?

With the dongle layout, the halves bond to the dongle (not to each other). If the
pieces won't connect after flashing - or you reflash and pairing breaks - reset
the stored bonds on all three:

1. Flash `settings_reset-xiao_ble-zmk.uf2` to the dongle and to **both** halves (same DFU steps as above)
2. Reflash the normal firmware to each piece (`dongle`, `left`, `right`)
3. Power both halves on and plug the dongle into the PC - they will automatically discover and bond to the dongle

### Problems

#### I'm getting File Transfer Error after copying firmware to the keyboard

It's OK. Proof: https://zmk.dev/docs/troubleshooting#file-transfer-error
