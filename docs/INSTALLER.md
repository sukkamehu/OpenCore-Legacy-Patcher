# How to download and build macOS Installers

* [Downloading](#downloading)
* [Building](#building)

This doc is centered around downloading and writting the macOS installer to a USB. If you're already familair with how to do this, you can skip.

* Note: 16GB+ USB will be required for the installer

## Downloading

The simplest way to download macOS installs would be to use installinstallmacos:

```sh
mkdir ~/macOS-installer && cd ~/macOS-installer && curl -O https://raw.githubusercontent.com/munki/macadmin-scripts/main/installinstallmacos.py && sudo python installinstallmacos.py
```

![](../images/munki.png)

As you can see, we get a nice list of macOS installers. If you need a particular versions of macOS, you can select it by typing the number next to it. For this example we'll choose 10:

![](../images/munki-process.png)

This is going to take a while as we're downloading the entire 12GB+ macOS installer.

Once finished, you'll find in your `~/macOS-Installer/` folder a DMG containing the macOS Installer, called `Install_macOS_11.1-20C69.dmg` for example. Mount it and you'll find the installer application.

* Note: We recommend to move the Install macOS.app into the `/Applications` folder, as we'll be executing commands from there.
* Note 2: Running Cmd+Shift+G in Finder will allow you to easily jump to `~/macOS-installer`

![](../images/munki-done.png)

![](../images/munki-dmg.png)

## Building

Now we'll be formatting the USB to prep for both the macOS installer and OpenCore. We'll want to use macOS Extended (HFS+) with a GUID partition map(Using GUID is important for the patcher). This will create two partitions: the main `MyVolume` and a second called `EFI` which is used as a boot partition where your Mac's firmware will check for boot files.

* Note: By default, Disk Utility only shows partitions – press Cmd/Win+2 to show all devices (alternatively you can press the View button)

![Formatting the USB](../images/format-usb.png)

Next run the `createinstallmedia` command provided by [Apple](https://support.apple.com/en-us/HT201372). Note that the command is made for USB's formatted with the name `MyVolume`:

```sh
sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

* Note: You can also replace the `createinstallmedia` path with that of where your installer's located (same idea with the drive name).

* ![](../images/createinstallmedia.png)

# Once finished, [return to the README to finish up](../README.md)