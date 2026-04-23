# TandemSDR v1.1

TandemSDR is a self-contained SDR remote control that runs entirely in a browser with no installation required. It links to SDRplay's SDRconnect software via WebSocket and provides a full receiver control interface including spectrum display, waterfall, audio output, signal metering (dBm and SNR), and signal history charting.

## Features

- **WebSocket connection to SDRconnect**

  - Connects to SDRconnect running locally or on a network.

  - Default connection: 127.0.0.1 port 5454 (both configurable).  A hostname like *labcomputer *can also be used if SDRconnect is Windows admin mode.

  - *IP addresses and names are saved in browser local storage and survive page reloads.  Accessible from dropdown menu.

  - Will connect over the WAN if router has port 5454 forwarding enabled.

  - Connection status indicator shows Connected, Connecting, or Disconnected.

  - On connect, all current device state is retrieved automatically from SDRconnect.

- **Frequency Control**

  - Separate VFO and Center frequency inputs in MHz.

  - Hold-to-repeat step buttons and mouse scroll wheel for VFO tuning. Step buttons accelerate the longer they are held.

  - Selectable step size: 10 Hz, 100 Hz, 500 Hz, 1 kHz, 2.5 kHz, 5 kHz, 10 kHz, 12.5 kHz, 25 kHz, 100 kHz.

  - Hold-to-repeat step buttons for Center frequency using the selected step size.

  - VFO → Center button to sync the center to the current VFO frequency. When sample rate is above 2 MSPS a 10 kHz offset is applied to keep the VFO out of the DC centre of the spectrum.

- **Device Controls**

  - Sample rate selector: 62.5 kSPS to 10 MSPS.

  - Device selector — populated dynamically from SDRconnect.

  - Antenna selector — populated dynamically from SDRconnect.

  - RF Gain slider with overload warning indicator.

- **Demodulation**

  - Modes: AM, SAM (Synchronous AM), USB, LSB, CW, NFM, WFM.

  - Each mode sets a default filter bandwidth on selection.

  - Filter bandwidth input with hold-to-repeat step buttons that accelerate the longer they are held. Maximum bandwidth is enforced per mode.

  - WFM mode requires a minimum sample rate of 250 kSPS; the 62.5 and 125 kSPS options are disabled when WFM is selected. If either of those rates is active when WFM is selected, the sample rate automatically jumps to 2 MSPS.

  - RDS on/off toggle with PI, PTY, and PS display (WFM mode).

  - Stereo on/off toggle with stereo indicator.

- **Audio**

  - Audio in SDRconnect is muted after TandemSDR is connected.

  - Audio streamed from SDRconnect and decoded in the browser via the Web Audio API.

  - Volume control slider with mute toggle button.

  - Noise Reduction on/off toggle with strength slider.

  - Audio AGC on/off toggle with threshold slider.

  - Squelch on/off toggle with level slider.

- **S-Meter**

  - Segmented bar display calibrated to IARU standard.

  - HF mode (below 30 MHz): S9 = −73 dBm, 6 dB per S-unit.

  - VHF mode (30 MHz and above): S9 = −93 dBm, 6 dB per S-unit.

  - Segments S1–S9 in green, +10 through +60 dB over S9 in red.

  - Automatically switches HF/VHF calibration based on current frequency.

- **Signal readouts**

  - Live Signal Power display in dBm.

  - Live Signal SNR display in dB.

  - Live Frequency display.

- **Spectrum Display**

  - FFT spectrum analyzer. (512 points)

  - Adjustable Max (reference) and Min (base) level inputs.

  - Frame averaging: None, 2, 4, 8, 16 frames.

  - Zoom: ×1, ×2, ×4 — cycled via button or keyboard.

  - Frequency snap grid: 1 kHz, 5 kHz, 9 kHz, 10 kHz, 25 kHz, 100 kHz.

  - Crosshair follows mouse with frequency readout.

  - Left-click sets VFO frequency at cursor position.

  - Right-click sets Center frequency at cursor and syncs VFO.

  - Drag on the frequency label row to pan the center frequency.

  - Scroll wheel steps the VFO frequency.

- **Waterfall Display**

  - Scrolling waterfall below the spectrum.

  - Optional frame averaging (follows spectrum averaging setting).

  - Speed selector: Slow, Medium, Fast.

  - Same mouse controls as the spectrum (left-click, right-click, scroll wheel).

- **Signal History Chart**

  - Time-series chart of Signal Power (dBm) or SNR over time.

  - Selectable capture interval: 500 ms, 1 sec, 5 sec, 10 sec, 30 sec, 60 sec.

  - Start/Stop/Clear capture control.

  - Session min and max values with timestamps displayed on the chart.

  - Scrollable history slider to review up to 10× the visible window of captured data. Automatically snaps back to live after 20 seconds of inactivity.

  - Crosshair mouseover shows exact value and timestamp when stopped or in history mode.

  - **Record** — opens a native file save dialog and streams data directly to a CSV file in real time as samples are captured.

  - **Export** — saves the current in-memory buffer to a CSV file via a native file save dialog. CSV includes frequency, mode, capture interval, and timestamped power and SNR columns.

- **Memory**

  - 10 memory slots for saving and recalling receiver settings. 

  - Each slot stores VFO frequency, center frequency, mode, filter bandwidth, sample rate, antenna, RF gain, step size, volume, and spectrum display settings (reference level, base level, zoom, averaging, snap).

  - Slots are saved in browser local storage and survive page reloads.

  - Individual slots can be cleared from the memory modal.

- **Band Selector**

  - Quick-access modal for jumping to common bands with one click.

  - Sets center frequency, sample rate, mode, snap, and step for the selected band. Also sets RF gain to maximum and turns squelch off.

  - Covers Amateur Radio (160 m through 33 cm), Shortwave Broadcast (120 m through 11 m), and Broadcast (AM and FM).

- **Keyboard Shortcuts** (hotkeys)

| Key | Action |
| - | - |
| ← → | Step VFO by selected step size |
| ↑ ↓ | Step Center by Snap value |
| PgUp PgDn | Jump Center one full span width |
| = | Copy VFO → Center |
| A | AM mode |
| S | SAM mode |
| U | USB mode |
| L | LSB mode |
| C | CW mode |
| N | NFM mode |
| W | WFM mode |
| V | Toggle audio mute |
| Q | Toggle squelch |
| D | Toggle Spectrum Display |
| F | Toggle WaterFall (enables Spectrum first if hidden) |
| Z | Cycle spectrum zoom (×1 → ×2 → ×4) |
| + | Increase sample rate |
| - | Decrease sample rate |
| M | Save memory slot |
| R | Recall memory slot |
| B | Open Band Selector |
| H or ? | Open Help |
| Esc | Close any open modal |


- **Built-in Help**

  - Help modal accessible via the ? button or H/? keyboard shortcut.

  - Covers all mouse controls for spectrum and waterfall.

  - Full keyboard shortcut reference.

## Requirements

- No installation and no internet connection required. Open the HTML file directly in your browser

- **SDRplay SDRconnect** must be running with WebSocket access enabled on port 5454

- Compatible with any SDRplay RSP device supported by SDRconnect.

- Works in any modern browser. The **Record** and **Export** features require a Chromium-based browser (Google Chrome, Microsoft Edge, Brave, or Opera) as they depend on the File System Access API, which is not supported in Firefox or Safari.

## Typical Workflow

1. Start **SDRconnect** and ensure it is running with WebSocket enabled. See image below

2. Open **TandemSDR** by double-clicking the HTML file in your browser.

3. Enter the IP address and port of the SDRconnect instance (defaults to 127.0.0.1:5454).

4. Click **Connect**. TandemSDR will retrieve all current device settings automatically.

5. Use the **VFO** input or click on the **Spectrum** to tune to a frequency.

6. Select a demodulation **Mode** and adjust **Filter BW** as needed.

7. Adjust **RF Gain**, **Volume**, **Noise Reduction**, and **Squelch** as desired.

8. Click **Show** under Spectrum Display to enable the spectrum and waterfall.

9. Use **Signal History** to capture and export signal power or SNR over time.

10.  Hotkeys (listed above) allow quick changes to features and parameters. 

## License

This program is free software: you can redistribute it and/or modify it under the terms of the **GNU General Public License** as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

You must:

- Keep the copyright and license header.

- Release any modifications or derivative works under GPLv3 (or later).

See [https://www.gnu.org/licenses/gpl-3.0.html](https://www.gnu.org/licenses/gpl-3.0.html) for the full license text.




**\*\* Enable WebSocket in SDRconnect before using program. ** 


