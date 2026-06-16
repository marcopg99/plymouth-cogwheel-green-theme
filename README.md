# Plymouth Cogwheel Green Theme

A boot splash (Plymouth) theme with a minimalist green look, built around an animated cogwheel and a progress bar. It also provides the unlock screen with a password prompt for systems that show Plymouth while unlocking encrypted disks.

## Preview

The theme shows:

- A full-screen custom background.
- A centered logo inside a decorative box.
- An animated cogwheel (spinner) during boot.
- A progress bar at the bottom.
- A password dialog for encrypted disks (LUKS) with a lock icon.

## Repository layout

```
.
├── install.sh                          # Installation script
└── cogwheel-green-marcopg99/
    ├── cogwheel-green-marcopg99.plymouth   # Theme metadata
    ├── cogwheel-green-marcopg99.script     # Animation logic
    ├── background.png                      # Background
    ├── logo_box.png                        # Logo box
    ├── box.png                             # Password dialog box
    ├── entry.png                           # Password entry field
    ├── lock.png                            # Lock icon
    ├── bullet.png                          # Password character
    ├── spinner.png                         # Animated cogwheel
    ├── progress_bar.png                    # Progress bar
    └── progress_box.png                    # Progress bar container
```

## Requirements

- Plymouth installed on the system.
- Root privileges (the script uses `sudo`).
- A Debian/Ubuntu-based distribution if you want to use `update-initramfs` as-is; on other distributions you will need to regenerate the initramfs with the equivalent tool (`dracut`, `mkinitcpio`, etc.).

## Installation

Clone the repository and run the install script as root:

```bash
git clone https://github.com/marcopg99/plymouth-cogwheel-green-theme.git
cd plymouth-cogwheel-green-theme
sudo ./install.sh
```

The script will:

1. Copy the `cogwheel-green-marcopg99` directory to `/usr/share/plymouth/themes`.
2. Register the theme with `update-alternatives` and let you select it as the default.
3. Regenerate the initramfs so the theme is loaded at boot time.

## Manual installation

If you prefer doing it by hand:

```bash
sudo cp -r cogwheel-green-marcopg99 /usr/share/plymouth/themes/
sudo update-alternatives --install \
    /usr/share/plymouth/themes/default.plymouth default.plymouth \
    /usr/share/plymouth/themes/cogwheel-green-marcopg99/cogwheel-green-marcopg99.plymouth 100
sudo update-alternatives --config default.plymouth
sudo update-initramfs -u
```

On Arch / Manjaro and other distributions using `mkinitcpio`:

```bash
sudo mkinitcpio -P
```

## Previewing the theme without rebooting

You can preview the theme with:

```bash
sudo plymouthd
sudo plymouth --show-splash
# ...to close the preview:
sudo plymouth --quit
```

## Uninstall

```bash
sudo update-alternatives --remove default.plymouth \
    /usr/share/plymouth/themes/cogwheel-green-marcopg99/cogwheel-green-marcopg99.plymouth
sudo rm -rf /usr/share/plymouth/themes/cogwheel-green-marcopg99
sudo update-initramfs -u
```

## Credits

Theme based on the original *COGWHEEL-A-SPINNER-PGR-2-GRAY* work by **DUKE93** (2020), adapted and customized by **marcopg99**.

## License

Distributed under the terms of the **GNU General Public License v3** or later, matching the original script. See <https://www.gnu.org/licenses/> for details.
