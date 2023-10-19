# Italian layout variant based on US Dvorak layout for Kinesis Advantage

This repository provides a _US variant_ layout for XKB that supports Italians deadkeys (i.e. vowels with diacritics) especially meant for [Kinesis Advantage keyboard](http://www.kinesis-ergo.com/shop/advantage-for-pc-mac/).

This is the original Dvorak US layout:

![Kinesis Advantage Dvorak US layout](http://drive.google.com/uc?id=0B8TPut6hfwH0ei1GS3ZkSGxpSVk)

and this is the Dvorak US layout with Italian variant:

![Kinesis Advantage Dvorak US layout Italian variant](http://drive.google.com/uc?id=0B8TPut6hfwH0WUNxZkxnV3ptVFE)

Even if everything in this repository is meant for Kinesis Advantage, I'm sure that you can learn from here everything you need to build, remap and customize your own keyboard layout for Linux.

If you need some help to understand better how all the parts are working, please have a look at [my guide on Medium.com](https://medium.com/@damko/a-simple-humble-but-comprehensive-guide-to-xkb-for-linux-6f1ad5e13450#.gnyfmp6y4)

## Install

### Before installing this repo

Run a backup of your current `/usr/share/X11/xkb` configuration directory

    su -
    cd /usr/share/X11/
    tar zcf previous-xkb.tgz xkb

So that you can roll back any time with this command:

    su -
    cd /usr/share/X11/
    rm -fR xkb
    tar zxf previous-xkb.tgz

### In case of troubles

If you have already modified your `/usr/share/X11/xkb` and you don't trust it anymore and you have lost your `previous-xkb.tgz` you can try to replace the xkb configuration directory with the xkb-original.tgz file that you can see in this repo (taken from a Debian testing - September 2017:

    su -
    cd /usr/share/X11/
    rm -fR xkb
    tar zxf {path}/xkb-original.tgz

### Now you can install

Be aware that this repository has two branches:

* master
* hack

**hack** is the branch you might be interested in and contains the modified files. **master** contains the original files, you know, in case of need and for [comparison](https://github.com/damko/xkb_kinesis_advantage_dvorak_layout/compare).

    git clone git@github.com:damko/xkb_kinesis_advantage_dvorak_layout.git
    cd xkb_kinesis_advantage_dvorak_layout
    git checkout hack
    sudo cp -fR * /usr/share/X11/xkb/

These commands will apply the changes:

    setxkbmap -model kinesis -layout us -variant kinesis_adv_dvorak_it -option
    setxkbmap -model kinesis -layout us -variant kinesis_adv_dvorak_it -option -option "lv3:rwin_switch"

You will end up with a standard American Dvorak layout with all the additional vowels with diacritics required for the Italian language.

### Kinesis Italian deadkeys

With the Kinesis Italian layout in this repo, to type a character with a grave mark (`), use
Win+R, then the vowel you want the grave over.

### mac-hip deadkeys

The standard Mac US keyboard layout is already quite hip, sporting a wide variety of
deadkeys accessed by the "Option" key, which I'll call "AltGr" from here on.  It also has
some non-deadkey productions, like AltGr+a produces å, AltGr+Shift+a produces Å.  This is
great if you type å a lot, but for most English–speaking hipsters it's a waste of a key
combination.

The "mac-hip" layout replaces all single accented letter combinations with either a deadkey
for the diacritic, if there is not a diacritical mark already, freeing up 1 combination for
something more hip, or if there is already a deadkey for that diacritic, both combinations
are freed up.

One exception is AltGr-n, which is not a deadkey for the squiggle diacritic as on standard
MacOS US layout, but but produces the _eñe_ letter directly.  Because, you know, as a US
speaker, you're typing Spanish a lot if you're hip.

#### Standard mac US deadkeys

The following deadkeys are default in MacOS already, and available with the 'mac' keyboard
variant without installing this repo; these are all shown 

* AltGr+backtick: grave (ˋ, eg è, used in French, Italian and otehrs)

* AltGr+shift+backtick: horn (eg ơ, used in Vietnamese)

* AltGr+e: acutE (´, eg é)

* AltGr+u: Umlaut (¨, eg ü) - technically called "diaeresis" in English and that's the term
  used in Unicode, but German makes the most use of this diacritic so the German term
  _umlaut_ ("OOM-lout") is generally used.

* AltGr+i: cIrcumflex, (^, eg _Ô mon Dieu!_ - OMG in French)

* AltGr+Shift+g: double acute (˝, eg ű, used in Hungarian, ӳ from various Slavic languages)

* AltGr+n: tilde/_virgulilla_ (˜, eg Spanish ñ, "eñe", described above)

* AltGr+Shift+comma: macron (¯, a long vowel, eg Māori, the people indigenous to New Zealand in the South
  Pacific)

* AltGr+Shift+period: breve (˘, a short vowel)

* AltGr+Shift+s: dead stroke (- or /, eg ɍ or Ⱦ)

#### mac-hip deadkeys

* AltGr+a: overring deadkey (˚ eg for å/Å as used in many chiefly Scandinavian languages) instead of å

* AltGr+shift+a: assigned ⃤  U+20E4 COMBINING ENCLOSING UPWARD POINTING TRIANGLE instead of Å.

* AltGr+Shift+period: caron deadkey (ˇ, used in pīnyīn, the standard Chinese romanization
  form, to denote 三声: tone 3, a falling-then-rising tone as in _pí jiǔ_, beer).  Looks
  just like a breve and the two diacritics are often confused, but the caron is more useful
  for writing Chinese using Latin/English letters.

#### mac-hip diacritic letter direct productions

mac-hip undeadens the ñ and leaves ç as it is;

* AltGr+n: enters Ñ directly (dead ˜ in 'mac' layout)

* AltGr+Shift+n: enters Ñ directly (enters ˜ in 'mac' layout)

* AltGr+C: enters ç directly (same in 'mac', and real MacOS)

* AltGr+Shift+C: enters Ç directly (same in 'mac', and real MacOS)

## mac-hip variations from 'mac' layout

* the top row is untouched, apart from the dead horn becoming the peace sign.

* key combinations above a diacritic deadkey produce the unicode combining form of that diacritic.
  These are used in the reverse way to deadkeys; i.e., you type a, then AltGr+Shift+e, to get á.

  * except AltGr+Shift+i, which produces ☝ - a finger pointing up, sometimes used for
    "Informational" blocks ("take note")

  * AltGr+Shift+p produces a capital π: Π, not the "N-ary product" symbol, ∏ (I believe this is a bug
    in the Linux 'mac' layout)

* AltGr+A does not produce å, it produces a deadkey: see the earlier section.

* AltGr+shift+a: assigned combining, enclosing triangle (   ⃤) - (eg with exclamation mark: ! ⃤)
  Not to be confused with capital delta Δ.

* AltGr+Shift+s does not produce a dead stroke, it produces Scissors: ✁

* AltGr+d: produces delta (δ), not a partial derivative (∂) as on MacOS and 'mac'.  I swear MacOS
  used to produce the Greek letter, not the mathematical symbol in the past.

* AltGr+J: produces capital delta (∆), not a increment (∆) as on MacOS and 'mac'

* **Fractions mappings**: 'mac-hip' has mappings for all fractions of eight, which reduce to
  quarters and one half when they are even.  Somehow, my hip mac layout I designed in 2015 matches
  the 'mac' Linux layout for ¼, ½ and ¾.  I'm not sure how that coincidence happened unless this was
  the standard mapping in an earlier version of Mac OS.  They are listed here in numerical order:

  * AltGr+z: produces one eighth (⅛), not a cedilla (¸) as Mac or a dead cedilla (for making ç) as on Linux 'mac'

  * AltGr+Shift+Y: enters one fourth/quarter (¼), not capital A acute (Á) as on Mac.
 
  * AltGr+Shift+D: produces three eighths (⅜), not the letter eth (ð) as on 'mac' or captial I circumflex (Î) as on Mac.

  * AltGr+Shift+J: produces one half (½), not capital O circumflex (Ô) as on Mac 

  * AltGr+Shift+F: produces five eighths (⅝), not capital I umlaut (Ï) as on Mac 

  * AltGr+Shift+M: produces three fourths/quarters (¾), not capital A circumflex (Â) as on Mac

  * AltGr+Shift+H: produces seven eighths (⅞), not capital O actute (Ó) as on Mac

* AltGr+h: does not produce an "above dot" (˙) as on Mac or dead above dot as on 'mac' but two superior/superscript: as in E = mc²

* AltGr+k: produces ₂, as in CO₂, not an abovering (˚) as on Mac or a dead abovering as on 'mac'
  (dead abovering is on AltGr+a on this layout).

* AltGr+v produces a check mark (✓), not a square root (√)

* AltGr+v produces a cross (✗), not an integral symbol (∫)

* AltGr+Shift+v produces therefore (∴), not a diamond (◊)

* AltGr+Shift+v produces because (∵), not a dotless i (ı)

## Multiple layouts

If you want to load an additional layout, let's say the Russian one providing Cyrillic, run these commands

    setxkbmap -model kinesis -layout us,us -variant kinesis_adv_dvorak_it,rus -option
    setxkbmap -model kinesis -layout us,us -variant kinesis_adv_dvorak_it,rus -option "lv3:rwin_switch,grp:alt_space_toggle"

You can switch between the Italian or the Russian layout by hitting ALT+SPACE

If you want to load the US layout and the Italian variant run these commands:

    setxkbmap -model kinesis -layout us,us -variant ,kinesis_adv_dvorak_it -option
    setxkbmap -model kinesis -layout us,us -variant ,kinesis_adv_dvorak_it -option "lv3:rwin_switch,grp:alt_space_toggle"

## Test and run

Run

    setxkbmap -print -verbose 10

to check that all the parameters where loaded correctly by XKB.

You should see something like this (depending on what you have set in the `setxkbmap` command):

    Setting verbose level to 10
    locale is C
    Trying to load rules file ./rules/evdev...
    Trying to load rules file /usr/share/X11/xkb/rules/evdev...
    Success.
    Applied rules from evdev:
    rules:      evdev
    model:      kinesis
    layout:     us,us
    variant:    kinesis_adv_dvorak_it,rus
    options:    caps:none,shift:both_capslock,lv3:rwin_switch,grp:alt_space_toggle
    Trying to build keymap using the following components:
    keycodes:   evdev+aliases(qwerty)
    types:      complete
    compat:     complete
    symbols:    pc+us(kinesis_adv_dvorak_it)+us(rus):2+inet(evdev)+group(alt_space_toggle)+level3(rwin_switch)+capslock(none)+shift(both_capslock)
    geometry:   kinesis(model100)
    xkb_keymap {
        xkb_keycodes  { include "evdev+aliases(qwerty)" };
        xkb_types     { include "complete"  };
        xkb_compat    { include "complete"  };
        xkb_symbols   { include "pc+us(kinesis_adv_dvorak_it)+us(rus):2+inet(evdev)+group(alt_space_toggle)+level3(rwin_switch)+capslock(none)+shift(both_capslock)"    };
        xkb_geometry  { include "kinesis(model100)" };
    };

Test your layout by typing some text and, if everything is working as expected, make the modifications permanent by editing the `/etc/default/keyboard` in this way:

    XKBMODEL="kinesis"
    XKBLAYOUT="us,us"
    XKBVARIANT="kinesis_adv_dvorak_it,rus"
    XKBOPTIONS="lv3:rwin_switch,grp:alt_space_toggle"

Reboot your machine, run again `setxkbmap -print -verbose 10` and test again by typing some text. Everything should work as expected.
