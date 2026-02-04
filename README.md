# Duckie Plymouth Theme

A cute animated duck theme for Plymouth boot splash screen and LUKS password entry.

![Version](https://img.shields.io/badge/version-1.2-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## Preview

This theme features an adorable animated duck that plays during boot and when entering your LUKS encryption password.

- **21-frame animation** for smooth duckie movement
- **Black background** for clean, minimal look
- **LUKS-optimized** for password entry screens
- **No animation on shutdown** for faster power-off

## Features

- ✨ Smooth 21-frame duck animation
- 🖤 Minimalist black background
- 🔒 Perfect for LUKS encrypted systems
- 🚀 Lightweight and fast
- 📦 Easy to install

## Installation

### Arch Linux

```bash
# Copy theme to Plymouth themes directory
sudo cp -r duckie /usr/share/plymouth/themes/

# Set as default theme
sudo plymouth-set-default-theme -R duckie

# Rebuild initramfs
sudo mkinitcpio -P
```

### Ubuntu/Debian

```bash
# Copy theme to Plymouth themes directory
sudo cp -r duckie /usr/share/plymouth/themes/

# Set as default theme
sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/duckie/duckie.plymouth 100

# Update initramfs
sudo update-initramfs -u
```

### Generic Linux

```bash
# Copy theme to Plymouth themes directory
sudo cp -r duckie /usr/share/plymouth/themes/

# Set as default theme
sudo plymouth-set-default-theme duckie

# Rebuild initramfs (command varies by distro)
sudo dracut --force  # For RHEL/Fedora
# or
sudo mkinitcpio -P  # For Arch
# or
sudo update-initramfs -u  # For Debian/Ubuntu
```

## Customization

### Changing Animation Speed

Edit `duckie.script` and modify this line:

```javascript
flyingman_sprite.SetImage(flyingman_image[Math.Int(progress / 3) % numberofframes]);
```

- Change `/3` to a smaller number for faster animation
- Change `/3` to a larger number for slower animation

### Changing Background Color

Edit `duckie.script` and modify these lines:

```javascript
Window.SetBackgroundTopColor (0, 0, 0);    # RGB values (0-1)
Window.SetBackgroundBottomColor (0, 0, 0); # RGB values (0-1)
```

For example, for a dark blue background:
```javascript
Window.SetBackgroundTopColor (0, 0, 0.2);
Window.SetBackgroundBottomColor (0, 0, 0.2);
```

## File Structure

```
duckie/
├── duckie.plymouth      # Theme configuration file
├── duckie.script        # Animation script
├── startup-1.png        # Animation frame 1
├── startup-2.png        # Animation frame 2
├── ...
└── startup-21.png       # Animation frame 21
```

## Technical Details

- **Type**: Plymouth script-based theme
- **Resolution**: 284x276 pixels per frame
- **Format**: PNG with alpha transparency
- **Animation**: 21 frames at ~3 frames per refresh cycle
- **Memory**: ~200KB total (all frames)

## Requirements

- Plymouth (boot splash system)
- Linux kernel with LUKS support (for encrypted disks)
- Initramfs system (initramfs-tools, mkinitcpio, or dracut)

## Testing

Preview the theme without rebooting:

```bash
# Test in a window (X11)
sudo plymouthd --debug --debug-file=/tmp/plymouth-debug.log
sudo plymouth --show-splash
# Wait a few seconds to see animation
sudo plymouth --quit

# Or use the plymouth preview tool
sudo plymouthd
sudo plymouth show-splash
sleep 5
sudo plymouth quit
```

## Troubleshooting

### Theme not showing

1. Check if Plymouth is installed:
   ```bash
   plymouth --version
   ```

2. Verify theme is installed:
   ```bash
   plymouth-set-default-theme --list
   ```

3. Check if theme is set:
   ```bash
   plymouth-set-default-theme
   ```

4. Rebuild initramfs:
   ```bash
   sudo mkinitcpio -P  # Arch
   sudo update-initramfs -u  # Debian/Ubuntu
   ```

### Animation is too fast/slow

Edit the `duckie.script` file and adjust the division factor in the animation line (see Customization section above).

### Black screen on shutdown

This is intentional! The theme shows a black screen during shutdown for faster power-off. If you want animation during shutdown too, remove this section from `duckie.script`:

```javascript
if (mode == "shutdown" || mode == "reboot") {
    # Just keep the black background for shutdown/reboot
    fun refresh_callback () {
        # Do nothing, keep the black screen
    }
}
```

## Version History

- **v1.2** (2025-06-05): Modified for LUKS-only with black shutdown screen
- **v1.1**: Animation improvements
- **v1.0**: Initial release

## Credits

Created by @Quackieduckie

## License

MIT License - Feel free to modify and share!

## Contributing

Contributions welcome! Feel free to:
- Submit bug reports
- Create pull requests
- Share your customizations
- Create new frame animations

## Support

If you encounter issues:
1. Check the Troubleshooting section
2. Review Plymouth logs: `/var/log/plymouth-debug.log`
3. Open an issue on GitHub

---

**Enjoy your cute duckie boot screen!** 🦆
