# Configuring MX Master 3S Thumb Button on Arch Linux with KDE Plasma

[https://wiki.archlinux.org/title/Logitech_MX_Master](https://wiki.archlinux.org/title/Logitech_MX_Master)

This guide outlines the steps for mapping the thumb button on the Logitech MX Master 3S mouse to perform the "Ctrl+Alt+Tab" keystroke, utilizing `xev`, `xbindkeys`, and `xdotool` on Arch Linux with KDE Plasma.

## Step 1: Identify the Button Press with `xev`

- Run `xev` from the terminal to capture and identify the system's recognition of the thumb button press.
- Press the thumb button and note the button number from the output (`button 10` in this case).

```bash
xev
```

## Step 2: Install Necessary Tools

Ensure `xbindkeys` and `xdotool` are installed on your system:

```bash
sudo pacman -S xbindkeys xdotool
```

## Step 3: Configure logid.cfg for Logitech Device Management (Optional)

This step involves configuring `/etc/logid.cfg` for your MX Master 3S. For direct button mapping with `xbindkeys``, specific changes to this file are not required. The goal is to ensure the mouse is correctly recognized.This configuration step was considered but not required for the direct button mapping approach that was ultimately successful.

```sh
devices: ({
  name: "MX Master 3S";

  // A lower threshold number makes the wheel switch to free-spin mode
  // quicker when scrolling fast.
  smartshift: { on: true; threshold: 20; };

  hiresscroll: { hires: true; invert: false; target: false; };

  // Higher numbers make the mouse more sensitive (cursor moves faster),
  // 4000 max for MX Master 3.
  dpi: 1500;

  buttons: (

    // Change the thumb button to emit "KEY_F24".
    { cid: 0x53; action = { type: "Keypress"; keys: ["KEY_F24"]; }; },

    // Standard configuration for the top button.
    { cid: 0x56; action = { type: "Keypress"; keys: ["KEY_BACK"]; }; }

  );
});
```

## Step 4: Create and Configure .xbindkeysrc

Create or modify the .xbindkeysrc file in your home directory:

```bash
nano ~/.xbindkeysrc
```

Add the following configuration to map the thumb button (button 10) to "Ctrl+Alt+Tab":

```bash
"xdotool keydown Control_L keydown Alt_L key Tab keyup Alt_L keyup Control_L"
  b:10
```

This tells xbindkeys to listen for button 10 presses and execute the xdotool command, simulating the "Ctrl+Alt+Tab" keystroke.

## Step 5: Reload xbindkeys

Reload `xbindkeys`` to apply the changes:

```bash
killall xbindkeys
 sh
```

## Step 6: Test the Configuration

Test the thumb button on your MX Master 3S to ensure it now triggers the `Ctrl+Alt+Tab`` action, confirming the setup's success.

Following these steps allows you to map any mouse button recognized by your Linux system to perform complex keyboard actions, offering a high degree of customization for your input devices.
