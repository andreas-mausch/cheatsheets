---
layout: cheatsheet
tags: gsettings gthumb mousepad
section:
  - name: Query settings
    commands:
      List schemas: gsettings list-schemas | grep -i nm-applet
      List values (dconf): dconf list /org/gnome/nm-applet/
      List values (gsettings): gsettings list-recursively org.gnome.nm-applet
      Get value (dconf): dconf read /org/gnome/nm-applet/suppress-wireless-networks-available
      Get value (gsettings): gsettings get org.gnome.nm-applet suppress-wireless-networks-available
  - name: Set settings
    commands:
      Set value (dconf): dconf write /org/gnome/nm-applet/suppress-wireless-networks-available true
      Set value (gsettings): gsettings set org.gnome.nm-applet suppress-wireless-networks-available "true"
---
