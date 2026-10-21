# AetherCTR2

<table><tr><td>

### Based on SmartMTR by Dariusz Socha, SQ5X

The design of AetherCTR2's face (the S-meter, the gauges, the layout and
styling) and its meter peak and trough markers come from
**[SmartMTR](https://smartmtr.net/)**, created by **Dariusz Socha (SQ5X)**.

Used with his kind permission. All credit for the SmartMTR design is his:
**https://smartmtr.net/**

</td></tr></table>

<table><tr><td>

### For the CTR2-Max by Lynn Hansen, Lynovation

The **CTR2-Max** controller, its hardware design and its stock firmware are
the work of **Lynn Hansen** of **[Lynovation, LLC](https://lynovation.com/)**.
AetherCTR2 runs on his hardware, beside his firmware, and only on units
registered with it.

Distributed with Lynovation's kind authorization. All credit for the
CTR2-Max is his: **https://lynovation.com/**

</td></tr></table>

AetherCTR2 is firmware for the **Lynovation CTR2-Max** that makes it a front
panel for a FlexRadio, through [AetherSDR](https://github.com/aethersdr/AetherSDR)'s
CTR2 USB relay: tuning, slices, meters, CW and the radio's settings, on the
CTR2-Max's knobs and screen.

This repository holds signed release images only. AetherCTR2's source code is
not published.

## Installing

Install AetherCTR2 from AetherSDR, not by hand: open **Settings → Controllers →
CTR2...**, and in its **CTR2-Max Firmware** part pick a release and press
**Install…**. The [user guide](USER-GUIDE.md) walks through installing,
updating, switching firmware and connecting to the radio. AetherSDR checks each
release's signature, installs AetherCTR2 beside the CTR2-Max's own firmware
(which stays installed, with its settings), and updates it later over the
USB cable. The CTR2-Max Firmware window needs an AetherSDR release newer
than v26.10.2.

- **A registered CTR2-Max.** AetherCTR2 runs only on a CTR2-Max registered
  with its stock firmware. Registration keys come from Lynovation.
- **Both firmwares stay.** The CTR2-Max firmware button on AetherCTR2's
  status screen, or AetherSDR's **Restart into: Stock Firmware**, starts the
  stock firmware again. CTR2-Max firmware v1.02.00 and later can switch back
  with **Run AetherCTR2** in its Settings menu.

AetherCTR2 is distributed with the authorization of Lynovation, LLC; see the
credit above.

## What a release contains

Each release has two files: `aetherctr2-VERSION.asdr`, the package AetherSDR
installs, and `SHA256SUMS`, its checksum. (GitHub adds the "Source code"
archives to every release; here they hold only this README and the license
files.)

The `.asdr` is an uncompressed tar archive (`tar -xf` lists and unpacks it)
holding:

| File | What |
|---|---|
| `manifest.json` | The release: version, images, where each goes, and what is never written |
| `manifest.json.sig` | Ed25519 signature of `manifest.json` (base64) |
| `aetherctr2.bin` | The AetherCTR2 application, RSA-3072 signed |
| `bootloader.bin`, `partition-table.bin` | Installed with it the first time |

AetherSDR accepts a release only if `manifest.json` is signed by the
AetherCTR2 release key, whose Ed25519 public key is
`c5caf07300756c8fa37cc4f47b600a302162635cad5e8e2f85101f2308b1bb19`; the
manifest's SHA-256 values then cover every image.

## Help

For help, see [SUPPORT.md](SUPPORT.md). Report security problems privately, as
[SECURITY.md](SECURITY.md) describes. Everyone here follows the
[Code of Conduct](CODE_OF_CONDUCT.md).

## License

AetherCTR2 is proprietary: owners of a CTR2-Max may install and run these
images on it ([LICENSE](LICENSE)). The SmartMTR design credited above is
Dariusz Socha's ([NOTICE.md](NOTICE.md)). Third-party components keep their
own licenses ([THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md)). The CTR2-Max
and its stock firmware are Lynn Hansen's and Lynovation's (NOTICE.md).
