# CBF02V2 Finger Robot evidence

Product: `bo25vaxy`, category `szjqr`, model CBF02V2; sold to the owner as a KKmoon Fingerbot. Similar seller photos are not proof of equivalent hardware.

These files accompany the CBF02V2 support PR. They live on a separate evidence branch so screenshots and test artifacts do not enter the integration's code diff.

## Screenshots

All eight images are byte-for-byte copies of the owner's original captures. No pixels, labels or enum values were edited.

| File | Evidence |
| --- | --- |
| smartlife-home.jpg | Main actuator, Timer switch and Setting |
| smartlife-settings.jpg | Upper/Bottom 0-30, Auto and Switching display status |
| smartlife-modes.jpg | Exactly Button and Switch modes |
| smartlife-hold-time.jpg | Hold time, 0.5 seconds in this capture |
| smartlife-schedule.jpg | Schedule page; no undocumented timer mapping inferred |
| cloud-standard-instructions.jpg | Standardized instruction schema, showing only click |
| cloud-standard-status.jpg | Standardized status schema, showing only click |
| cloud-instruction-mode.png | Original DP mapping includes unmapped start/set_switch_state |

## Structured evidence

- `things-data-model.json`: full decoded model from [the original PR evidence comment](https://github.com/pascalgoedeke/ha_tuya_ble/pull/19#issuecomment-4637611431). The original response embeds this object as a JSON string in result.model; only the string wrapper was decoded.
- `standard-specifications.json`: the result object from the same comment's specifications response, without request metadata. Its restricted standardized enum is not the full native model enum.
- `historical-properties.json`: dp_id, code, type and value from that comment's properties response; timestamps and custom names omitted. These are historical cloud values, not fresh BLE observations or proof of readable state for write-only DPs.
- `ha-verification.json`: allowlisted readback after installing and restarting commit `3453ecddd44b462e124c986da43001a06710b00a` on HA Core 2026.10.1. Credentials, addresses, device/config-entry/entity IDs and unrelated HA state are excluded. This is structured readback, not a fabricated UI screenshot or packet capture.

## Owner-observed results

The owner reports the live controls work, explicitly confirming Click and Switch modes. Both temporary DP102 Boolean commands (`true` and `false`) flip the switch on/off indication without moving the arm. The final build exposes one Invert switch status configuration button using fixed `true`.

The early prose in the old PR confused DP101 and DP102. The authoritative model identifies DP101 start as auto adjustment and DP102 set_switch_state as switching display state. DP101 is not exposed. DP102 is an action, not a readable persistent inversion flag.

The existing tested DP1 inversion is retained for continuity with the owner's previous setup, not asserted as a hardware invariant. The switch remains usable in Click mode, where both on/off transitions produce a complete press/release. No Program/Toggle or guessed DP6 reverse control is added.

DP7 charge status exists in the schema but was not reported during the latest BLE session; charging capability is not claimed for the owner's CR2-powered unit. Power-cycle persistence, exhaustive range limits and BLE packet capture are not claimed. No additional physical commands were sent by Codex during packaging.

Implementation and evidence preparation are AI-assisted using Codex. Physical observations and screenshots are supplied by the device owner.
