# Home Assistant Solix BLE — Solarbank 2 output control (fork)

> [!NOTE]
> **This is a fork** of [flip-dots/HaSolixBLE](https://github.com/flip-dots/HaSolixBLE) for one
> purpose: controlling the output power of an Anker **Solarbank 2** over Bluetooth until this is
> available upstream. Please use the [original integration](https://github.com/flip-dots/HaSolixBLE)
> unless you need exactly this.
>
> **What it contains** (branch `sb2-control`, releases `v3.6.0-sb2ctl.N`):
> - upstream HaSolixBLE **3.6.0**
> - the output-power control from [HaSolixBLE PR #27](https://github.com/flip-dots/HaSolixBLE/pull/27)
>   by [@jul1an-s](https://github.com/jul1an-s): a number *Output Power Target* and a button *Apply Power Target*
> - the SolixBLE library **3.9.0** with [SolixBLE PR #36](https://github.com/flip-dots/SolixBLE/pull/36)
>   (also by @jul1an-s), bundled in `custom_components/solix_ble/_vendor/` (MIT, © Harvey Lelliott) so
>   that the library installed globally in Home Assistant is not replaced; one small change makes
>   it importable from there (relative imports in `prime_device.py`)
> - a brand icon
>
> **Tested on** a Solarbank 2 E1600 Pro with its internet access blocked: *Apply* changes the AC
> output within about 2 seconds, both up and down. Every *Apply* writes the device's schedule, so
> do not press it from an automation in a tight loop (seconds).
>
> **Install via HACS:** add `https://github.com/ak111pro/HaSolixBLE` as a custom repository
> (category Integration) **instead of** the original one, then restart Home Assistant. Entity ids
> are kept. When the control feature is released upstream, switch back to the original repository.
>
> All credit for the integration and the control feature goes to
> [@flip-dots](https://github.com/flip-dots) and [@jul1an-s](https://github.com/jul1an-s).
> The fork was assembled with the help of an AI assistant (Claude, by Anthropic).

Home Assistant integration for monitoring and controlling Anker devices using a Bluetooth connection.

## Features

- 🔋 Battery percentage
- ⚡ Total Power In/Out
- 🎛️ AC/DC output control
- 🔌 AC Power In/Out
- 🚗 DC Power In/Out
- ⏰ AC/DC Timer value
- ⏲️ Time remaining to full/empty
- ☀️ Solar Power In
- 💻 USB Port Power
- 📱 USB Port Status & control
- ⚙️ Firmware version
- 🩺 Battery health
- 🌡️ Battery temperature
- ↔️ Expansion batteries (Charge, Temperature, Health, Firmware)
- 💡 Light bar status
- 🖥️ Display status & control
- ✔️ More emojis than strictly necessary


## Supported devices

This lists the supported devices, more information on what features are supported can be found in the underlying libraries [documentation](https://solixble.readthedocs.io/en/latest/index.html).

- C300(X)
- C300(X) DC
- C800(X)
- C1000(X)
- C1000(X) Gen 2
- F2000
- F2600
- F3800
- Anker Prime 160w Charger
- Anker Prime 250w Charger
- Anker Prime 20k (220w) Power Bank
- Anker Prime MagGo 3-in-1
- Solarbank 2
- Potentially more!

## Installation (HACS)

1. Ensure [HACS](https://custom-components.github.io/hacs/installation/manual/) is installed.
2. Add `https://github.com/flip-dots/HaSolixBLE` as a [custom repository](https://custom-components.github.io/hacs/usage/settings/#add-custom-repositories)
3. Install integration.
4. Restart your instance.

## Setup

1. Ensure the connection light is blinking. This can be achieved by pressing the IoT button or holding it to reset Bluetooth. The device indicator on the screen should be flashing.
2. Go to the devices page in Home Assistant and click Add on the power station. It should be automatically detected.
3. Select the correct model for your power station in the drop down. If your model is not supported select unknown and follow the steps for adding support for a new device below.
4. Click confirm, the device should be added, this may take a while as a connection is negotiated.
5. Profit???

## Limitations

- It is not possible to use Bluetooth and Wi-Fi at the same time.


## Adding support for new devices

Support for new devices can be added by setting up this integration with an unsupported device and enabling debug logging, this causes the raw telemetry data and differences between values between updates to be printed to the debug log, this can be used to determine what bytes mean what by turning things on and off and finding what value change corresponds with that in the log. You are welcome to submit a PR to the underlying library [SolixBLE](https://github.com/flip-dots/SolixBLE) to add support or to raise a GitHub issue with all of the indexes of the values and what they correspond to and I am happy to add support myself. See the underlying libraries [docs](https://solixble.readthedocs.io/en/latest/new_devices.html), this [PR](https://github.com/flip-dots/SolixBLE/pull/8), and this [discussion](https://github.com/thomluther/anker-solix-api/discussions/222) for more information on how to go about decoding different properties.


## Disclaimer

Home Assistant Solix BLE is a software library designed to work with Anker Solix/Prime devices. ANKER is a registered trademark of Anker Innovations Limited. This project is not affiliated with, endorsed by, or sponsored by Anker Innovations Limited (Though I wouldn't mind being sponsored 😉). All other trademarks cited herein are the property of their respective owners.
