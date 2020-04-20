# setup-manjaro

## Create Package List:

AUR

```
  pacman -Qqe | grep -v "$(pacman -Qqm)" > pacman.lst
```

Normal Packages

```
comm -23 <(pacman -Qqett | sort) <(pacman -Qqg base -g base-devel | sort | uniq)
```

Install Packages:

```
cat pacman.lst | xargs pacman -S --needed --noconfirm
```

## 3cx

Setup [GitHub - jiahaog/nativefier: Make any web page a desktop application](https://github.com/jiahaog/nativefier)

```shell
npm install nativefier -g
```

```shell
nativefier --name "3cx" --tray --icon icon.png  "https://mirabit.3cx.ch/webclient/"
```

Flag --disable-gpu bei Problemen verwenden

### Starter erstellen

https://wiki.ubuntuusers.de/Men%C3%BCeditor/




# Notes

```
sudo pacman -Sy
sudo pacman -S wine-staging winetricks
sudo pacman -S giflib lib32-giflib libpng lib32-libpng libldap lib32-libldap gnutls lib32-gnutls mpg123 lib32-mpg123 openal lib32-openal v4l-utils lib32-v4l-utils libpulse lib32-libpulse alsa-plugins lib32-alsa-plugins alsa-lib lib32-alsa-lib libjpeg-turbo lib32-libjpeg-turbo libxcomposite lib32-libxcomposite libxinerama lib32-libxinerama ncurses lib32-ncurses opencl-icd-loader lib32-opencl-icd-loader libxslt lib32-libxslt libva lib32-libva gtk3 lib32-gtk3 gst-plugins-base-libs lib32-gst-plugins-base-libs vulkan-icd-loader lib32-vulkan-icd-loader cups samba dosbox

```

Dannach Wineprefix kopieren und einpflegen mit Daten aus Windows festplatte

Oder neu erstellen:

```
WINEPREFIX="$HOME/prefix_notes" WINEARCH=win32 winecfg
```

- Windows auf XP Umstellen
- C & D Laufwerk hinzufügen
- Navigate to HKEY_CURRENT_USER/Software/Wine/X11 Driver/
- In the right panel, right-click and create a new String Value and name it**“ClientSideGraphics”**
- Right-click on the newly created key and modify the value to **“N”**

```
winetricks vcrun2015 gdiplus ie7 
```

Datei notes.ini bearbeiten *UseBasicNotes=1* hinzufügen

Besser [Notes 10 unter Linux verwenden &ndash; assonos Blog](https://www.assono.de/blog/notes-10-unter-linux-verwenden)

Browser noch auf extern ändern

1. `wine regedit`
   - HKEY_CURRENT_USER -> Software -> Wine
   - Create **WineBrowser** key if it doesn't exist
   - Create **Browser** key if it doesn't exist under WineBrowser
   - Edit **Browser** key to read the following
     - `xdg-open,firefox,konqueror,mozilla,netscape,galeon,opera,dillo`
   - Save in `regedit`
2. `wine regedit`
   - HKEY_CLASSES_ROOT -> http -> shell -> open
   - Create/Edit **command** key to read the following
     - `C:\windows\system32\winebrowser.exe -nohome "%1"`
   - Save in `regedit`
3. Completely close out of Wine and reload Wine.
