# Keyboard Layers App companion

A simple python script to display the selected layer layout on screen
At the moment it only supports the default layouts of [Miryoku QMK](https://github.com/manna-harbour/miryoku_qmk)

Demonstration video:
[![Demonstration](https://img.youtube.com/vi/WpxBLXetmFg/0.jpg)](https://www.youtube.com/watch?v=WpxBLXetmFg)


It works by sending different Function keys (F13 to F19) to the host when switching between layers

It requires the following changes to your miryoku_qmk firmware:

File: keyboards/<your_keyboard>/keymaps/manna-harbour_miryoku/keymap.c

```c
// Notifies the host of the layer change
// Layers reference: users/manna-harbour_miryoku/miryoku_babel/miryoku_layer_list.h
layer_state_t layer_state_set_user(layer_state_t state) {
    switch (get_highest_layer(state)) {
        case 0:
            // send f13
            SEND_STRING(SS_TAP(X_F13));
            break;
        case 4:
            SEND_STRING(SS_TAP(X_F14));
            break;
        case 5:
            SEND_STRING(SS_TAP(X_F15));
            break;
        case 6:
            SEND_STRING(SS_TAP(X_F16));
            break;
        case 7:
            SEND_STRING(SS_TAP(X_F17));
            break;
        case 8:
            SEND_STRING(SS_TAP(X_F18));
            break;
        case 9:
            SEND_STRING(SS_TAP(X_F19));
            break;
        default:
            uprintf("Layer not mapped: %d\n", get_highest_layer(state));
            break;
    }
    return state;
}
```

## Requirements
- Python 3
- Tkinter
- Pillow
- Keyboard

## Installation

### Linux

#### Fedora
`sudo dnf install python3-tkinter`

`sudo dnf install python3-pillow-tk`

`sudo pip install pillow keyboard`

#### Debian
`sudo apt-get install python3-tk`

`sudo apt-get install python3-pil.imagetk`

`sudo pip install pillow keyboard`

## Run the script as root
`sudo python keyboard_layers.py`
