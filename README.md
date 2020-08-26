# extra-arrow-keys-xmodmap
Moving your hands on the keyboard to the arrow keys takes a long time. With this you can move your hands less by remapping some keys.

# Why?
Usually to write code you have to use the arrow keys, but moving your hands from the regular keys to these keys takes a long time.
With this code you can combine the altGr key with another key and assign it an up, down, right, left value to move around.

# How to
With [xmodmap](https://wiki.archlinux.org/index.php/Xmodmap) you can assign each *keycode* (number of the key) with a *keysym* (value of some symbol).

For example, the output of `xmodmap -pke` shows:

```
...
keycode  26 = e E e E EuroSign cent EuroSign
...
keycode  39 = s S s S ssharp section ssharp
keycode  40 = d D d D eth ETH eth
keycode  41 = f F f F dstroke ordfeminine dstroke
...
keycode 108 = ISO_Level3_Shift NoSymbol ISO_Level3_Shift
...
```

The fifth and sixth columns are associated with the combinations `ISO_Level3_Shift+Key` and `ISO_Level3_Shift+Shift+Key`, respectively. This symbol is associated with the [AltGr](https://en.wikipedia.org/wiki/AltGr_key) key (keycode 108).

To change the value of these combinations to the Up, Down, Left and Right symbols, we apply the following commands:

```
xmodmap -e "keycode  26 = e E e E Up Up EuroSign"
xmodmap -e "keycode  39 = s S s S Left Left ssharp"
xmodmap -e "keycode  40 = d D d D Down Down eth"
xmodmap -e "keycode  41 = f F f F Right Right dstroke"
```

And now you can move using AltGr+[E, S, D, F]. Other keys can be used following a similar procedure.

This will only last until the next reboot. To make it always available, one way is to write these commands in a shell script (`map_keys.sh`) and run it when you start the system with a "Startup Applications" software like the one available in Linux Mint. **Note:** Don't forget to make the script [executable](https://askubuntu.com/questions/229589/how-to-make-a-file-e-g-a-sh-script-executable-so-it-can-be-run-from-a-termi).

# Useful commands
1. `xev` to find information about keycode and keysym of a key.
2. `setxkbmap` to restart the xmodmap configuration.
