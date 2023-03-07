---
layout: cheatsheet
tags: gsettings gthumb mousepad xfconf-query
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
  - name: xfconf-query
    commands:
      List all available configuration channels: xfconf-query -l
      List all available properties and their values: xfconf-query -c xfce4-panel -l -v
      Create property: xfconf-query -c test -p /test1 -n -t int -s 1
      Update property: xfconf-query -c xfce4-power-manager -p /xfce4-power-manager/brightness-step-count -s 4
---
