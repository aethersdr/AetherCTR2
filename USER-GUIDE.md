# AetherCTR2 User Guide

AetherCTR2 is firmware for the Lynovation CTR2-Max that connects it to your
FlexRadio over the USB cable, through [AetherSDR](https://www.aethersdr.com).
It is installed **beside** the CTR2-Max's stock firmware, which stays on the
unit with its settings and registration, and the CTR2-Max can restart into
either one.

AetherCTR2 builds on the work of Dariusz Socha, SQ5X
([smartmtr.net](https://smartmtr.net)), and Lynn Hansen, Lynovation
([lynovation.com](https://lynovation.com)).

Everything below happens in AetherSDR's **CTR2** window: **Settings →
Controllers → CTR2...**. Its top part, **CTR2 Relay**, connects the CTR2-Max to
the radio; the part below it, **CTR2-Max Firmware**, installs and updates
AetherCTR2.

## Requirements

- **A registered CTR2-Max.** AetherCTR2 is installed only on a CTR2-Max
  registered with its stock firmware (your call and registration key, entered
  on the unit), and checks the registration again at every start.
  Registration keys come from Lynovation.
- **AetherSDR newer than v26.10.2**, built with USB HID support (hidapi) and
  serial-port support (Qt Serial Port).
- **A radio that accepts more than one client**, connected over the LAN or a
  VPN. The relay is unavailable on SmartLink connections.
- **Linux:**
  - **USB relay:** a udev rule for the CTR2 ships with AetherSDR. If the
    CTR2-Max cannot be opened, **Start** offers to install the rule
    (`/etc/udev/rules.d/70-aethersdr-ctr2.rules`) and asks for your
    administrator password once.
  - **Download mode:** installing uses the unit's USB serial port. If
    AetherSDR cannot open it, add yourself to the group that owns the port
    (`dialout` or `uucp`, depending on the distribution) and log in again.

## Installing AetherCTR2

The **CTR2-Max Firmware** part of the window has three steps:

1. **Firmware.** The AetherCTR2 releases AetherSDR can install, newest first,
   from the list on aethersdr.com. Pick one. An older release can be picked to
   go back to it.
2. **Device.** Connect the CTR2-Max with a USB cable. **Status** shows what
   the window found:
   - **AetherCTR2** (cyan): the unit runs AetherCTR2 and is updated over the
     USB cable.
   - **Stock firmware** (gold): the unit runs its stock firmware. Put it in
     download mode to install.
   - **Bootloader** (aqua): the unit is in download mode. Its screen stays
     dark; that is normal.
   - **No CTR2-Max**: nothing was found.
3. **Action.** The buttons that apply to that status are enabled.

### Putting the CTR2-Max in download mode

- **From the stock firmware:** hold **BOOT** (through the hole in the back),
  press and release **RESET**, then release **BOOT**. The screen goes dark.
- **From AetherCTR2:** press **Restart into → Bootloader** in the CTR2
  window. No buttons needed.
- **To leave it** without installing anything, press **RESET**: the unit
  starts the firmware it was running.

### First install

1. Put the CTR2-Max in download mode. **Status** reads **Bootloader**.
2. Pick the release and press **Install…**.
3. Choose **Back Up and Install…** (recommended) and save the backup file, or
   **Install Without Backup**. The backup is the unit's whole flash, about
   16 MB, and takes about a minute.
4. AetherSDR checks the unit (chip, flash size, partition layout and
   registration), writes AetherCTR2 and selects it, then restarts the unit
   into it.

Only the parts that change are written. The stock firmware, its settings and
its registration are never written. If anything is not as expected, nothing
is written.

### Updating

With **Status** reading **AetherCTR2**, pick the release and press
**Install…**. The relay stops for the update and starts again afterwards.
The update takes about three minutes. The CTR2-Max checks the firmware's
signature, restarts into it and keeps it only once it has connected again; if
anything goes wrong it goes back to the version it had.

## Switching between AetherCTR2 and the stock firmware

Both firmwares stay installed; switching only changes which one the CTR2-Max
starts.

**To the stock firmware**, from AetherCTR2, either:

- press **Restart into → Stock Firmware** in the CTR2 window, or
- on the CTR2-Max, tap **CTR2-Max firmware** on AetherCTR2's status screen,
  then tap it again (**Tap again to restart**) to confirm.

**Back to AetherCTR2**, from the stock firmware, either:

- with CTR2-Max firmware v1.02.00 or later, choose **Run AetherCTR2** at the
  bottom of page 1 of the CTR2-Max's **Settings** menu (it reads
  **AetherCTR2 n/a** when AetherCTR2 is not installed), or
- with any version, put the unit in download mode and press **Start** in the
  CTR2 window. Start only changes which firmware the unit starts; nothing
  else is written.

The CTR2 window notices the switch by itself: the device list and **Status**
follow within a couple of seconds, with no **Rescan** needed. With **Start
automatically** ticked, the relay starts again once the CTR2-Max is back in
AetherCTR2.

## Connecting to the radio (the relay)

The CTR2-Max's traffic travels over the USB cable, and AetherSDR forwards it
unchanged to the radio AetherSDR is connected to, over its own network route,
including a VPN or tailnet route the CTR2-Max could not reach by itself. The
CTR2-Max stays an independent radio client; the relay never passes through
AetherSDR's own command or transmit paths.

1. Connect AetherSDR to your radio.
2. In **CTR2 Relay**, set **Mode** to **USB** and pick the CTR2-Max in the
   **USB** list (it is listed as **AetherCTR2**).
3. Press **Start**.

The relay always goes to the radio AetherSDR is connected to, captured at
**Start**, and stops when AetherSDR disconnects or switches radios. Each time
it starts, its setup is saved and offered again at the next launch. Closing
the CTR2 window does not stop it.

### Starting automatically

Tick **Start automatically when AetherSDR connects to a radio** to have the
relay start by itself, with the setup it last started with, whenever AetherSDR
connects to a radio.

- If the CTR2-Max is not plugged in yet, or is running its stock firmware,
  AetherSDR keeps looking every few seconds and starts the relay when
  AetherCTR2 appears.
- Pressing **Stop** holds it off until AetherSDR next connects to a radio.
- **Linux:** if the udev rule is not installed yet, press **Start** once to
  install it.

### Status

While the relay runs, the window shows:

- **State:** Stopped, Connecting, Relaying, Closing or Error.
- The device and the radio it is relaying to.
- A table of counters, toward the radio (`↑ Radio`) and toward the CTR2-Max
  (`↓ CTR2`): **Bytes** relayed, bytes **Queued** and not yet sent, **UDP**
  datagrams relayed, and datagrams **Dropped** because the link to the
  CTR2-Max was backed up.
- The last error, if any.

Stop the relay to change its settings.

## Backing up and restoring

In download mode:

- **Back Up…** saves the whole flash to a file, with a description beside it
  (`.json`, same name). Keep the two files together.
- **Restore…** writes a backup back. A backup restores only onto the unit it
  came from (matched by its MAC address), and only if the file is unchanged
  since it was made. This puts back everything, the firmware included,
  exactly as it was.

**Cancel** stops between steps: a write already started finishes, and no new
one starts. A unit interrupted part way through a download-mode install stays
in download mode, so you can install again or restore the backup. An update
over the cable that is cancelled leaves the firmware the unit had.

## Troubleshooting

### "Register this CTR2-Max first" on the CTR2-Max

AetherCTR2 runs only on a registered unit.

1. Tap **CTR2-Max firmware** twice to start the stock firmware.
2. Enter your call and registration key on the unit.
3. Switch back to AetherCTR2.

### "This CTR2-Max is not registered" in AetherSDR

AetherSDR installs AetherCTR2 only on a registered unit.

1. Start the stock firmware (press **RESET**).
2. Enter your call and registration key on the unit.
3. Put it in download mode and install again.

### "Put it in download mode to install"

The unit runs its stock firmware, which cannot be updated over the USB cable.

1. Put the CTR2-Max in download mode (see
   [Putting the CTR2-Max in download mode](#putting-the-ctr2-max-in-download-mode)).

### The CTR2-Max's screen is dark after an install or restore failed

It is still in download mode, which is safe.

1. Install again, or restore the backup.
2. To leave without changing anything, press **RESET**: the unit starts the
   firmware it had.

### Start is unavailable: "Connect AetherSDR to a radio first"

The relay goes to the radio AetherSDR is connected to, and there is none.

1. Connect AetherSDR to your radio.
2. Press **Start**.

### "AetherSDR is connected through SmartLink"

The relay needs a direct LAN or VPN connection to the radio.

1. Disconnect from SmartLink.
2. Connect to the radio over the LAN or a VPN.
3. Press **Start**.

### The relay stopped on its own

It stops when AetherSDR disconnects or switches radios.

1. Reconnect AetherSDR to the radio.
2. Press **Start**, or tick **Start automatically** so it comes back by
   itself.

## More

- [AetherSDR's CTR2 page](https://docs.aethersdr.com/ctr2-proxy) covers the
  CTR2 window in full, including Wi-Fi (TCP) mode for a CTR2 on its stock
  firmware.
- [Releases](https://github.com/aethersdr/AetherCTR2/releases): each release
  is one `.asdr` package, which AetherSDR installs, and its `SHA256SUMS`.
