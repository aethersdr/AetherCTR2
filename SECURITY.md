# Security Policy

AetherCTR2 runs on owners' CTR2-Max units, installs updates into their flash,
and can key their transmitters, so a security problem in it is a problem on
someone's bench.

## Reporting a Vulnerability

Report it **privately**: email the maintainer at
[kk7gwy@aethersdr.com](mailto:kk7gwy@aethersdr.com). Please don't open a public
issue for it.

Include what you found, how to reproduce it (the AetherCTR2 and AetherSDR
versions, and the radio), and what an attacker could do with it. You'll get an
acknowledgment within 72 hours, and we'll work with you on a fix before
anything is disclosed.

## Scope

- **Installing and updating:** a way to get a CTR2-Max to accept or start
  firmware that isn't a signed AetherCTR2 release, or to change the parts of
  its flash that belong to Lynovation's firmware.
- **Registration:** a way to run AetherCTR2 on a CTR2-Max that isn't
  registered with Lynovation's firmware.
- **Transmit:** a way to key the radio without the operator's action, or to
  leave it keyed.
- **Crashes and hangs** caused by data from the computer, the radio or the
  network.

Problems in AetherSDR (its CTR2 window, relay or installer) go to AetherSDR's
[security policy](https://github.com/aethersdr/AetherSDR/blob/main/SECURITY.md).
Problems with the CTR2-Max hardware or Lynovation's firmware go to
[Lynovation](https://lynovation.com).

## Supported Versions

Only the latest release receives security fixes. Update from AetherSDR:
**Settings → Controllers → CTR2...**, on the **AetherCTR2** tab.
