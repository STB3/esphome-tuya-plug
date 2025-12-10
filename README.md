# ESPHome Tuya Smart Plug 20A (EU) with Power Monitoring

Transform your Tuya Smart Plug into a fully local, Home Assistant compatible device using ESPHome firmware. This project enables complete control without cloud dependency while adding accurate power monitoring capabilities.

![Tuya Smart Plug 20A](Tuya_plug_EU.png)

## Features

- ✅ **Local Control**: No cloud dependency, full Home Assistant integration
- ✅ **Power Monitoring**: Real-time voltage, current, power, energy, and frequency measurements
- ✅ **BL0942 IC**: Sophisticated calibration-free energy measurement chip
- ✅ **Manual Control**: Physical button for local operation
- ✅ **Status LED**: Visual feedback with customizable behavior
- ✅ **Web Interface**: Built-in web server for standalone operation
- ✅ **OTA Updates**: Over-the-air firmware updates
- ✅ **WiFi Signal Monitoring**: Track connection quality

## Hardware Specifications

### Module Details
- **Chip**: Tuya T34 module with BK7231N processor
- **Power Monitoring IC**: BL0942 (Shanghai Belling Corp.)
- **Standard**: EU plug, 20A rated
- **Communication**: UART interface for power monitoring

### GPIO Pinout

| Pin | Function          |
| --- | ----------------- |
| P25 | BL0942(10) TX     |
| P26 | BL0942(9) RX      |
| P14 | Relay & Red LED   |
| P26 | Button (Inverted) |
| P24 | Blue LED          |

![PCB View](Tuya_PCB.png)

## Documentation & Datasheets

- [T34 Module Datasheet](https://developer.tuya.com/en/docs/iot/t34-module-datasheet?id=Ka0l4h5zvg6j8)
- [BL0942 Datasheet](https://www.belling.com.cn/media/file_object/bel_product/BL0942/datasheet/BL0942_V1.06_en.pdf)
- [BL0942 Tuya Application Note](https://support.tuya.com/en/help/_detail/Kd2fly62orx3p)
- [BL0942 ESPHome Documentation](https://esphome.io/components/sensor/bl0942/)

## Installation

### Prerequisites

1. **Hardware**:
   - USB to TTL/Serial programmer (3.3V logic level)
   - 5V DC power supply
   - Jumper wires
   - (Optional) Pin headers for easier connection

2. **Software**:
   - [ESPHome](https://esphome.io/) installed
   - Python 3.7 or newer

### Flashing Instructions

#### 1. Hardware Connection

Connect your programmer to the BL0942 power monitoring chip pins (easier access than T34 pins):

- **Programmer TX** → **BL0942 Pin 10** (TX)
- **Programmer RX** → **BL0942 Pin 9** (RX)
- **GND** → **GND**
- **5V DC Supply** → **Voltage Regulator Input**

⚠️ **Important**: You can try to use 5V from the programmer.
Sometimes they have not sufficient power.
If that is not working use a separate 5V power supply.

#### 2. Initial Flash

```bash
# Clone this repository
git clone https://github.com/STB3/esphome-tuya-plug.git
cd esphome-tuya-plug

# Copy the example configuration
cp tuya_plug.yaml my_tuya_plug.yaml

# Edit the configuration (add your WiFi credentials)
nano my_tuya_plug.yaml

# Flash with reduced upload speed (CRITICAL!)
esphome run my_tuya_plug.yaml --upload_speed 19200
```

⚠️ **Critical**: The upload speed **must be limited to 19200 baud**, otherwise programming will fail.

#### 3. Enter Programming Mode

1. Start the ESPHome flash command
2. Wait for "Connecting..."
3. Power cycle the 5V supply to enter bootloader mode
4. Flashing should begin automatically

#### 4. Subsequent Updates

After the initial flash, you can use OTA (Over-The-Air) updates:

```bash
esphome run my_tuya_plug.yaml
```

## Configuration

### Basic Setup

The default configuration in `tuya_plug.yaml` includes:

- WiFi with fallback AP mode
- Home Assistant API
- OTA updates
- Web server on port 80
- Power monitoring sensors
- Relay control
- Status LED with AP mode blinking

### WiFi Configuration

You can configure WiFi credentials directly in the YAML file or use a `secrets.yaml` file:

```yaml
# secrets.yaml
wifi_ssid: "YourSSID"
wifi_password: "YourPassword"
```

### Customization Options

#### Enable LED Control from Home Assistant

Uncomment the light section in the YAML file:

```yaml
light:
  - platform: binary
    name: "Status LED"
    id: status_light
    output: led_output
    internal: false  # Make visible in Home Assistant
```

#### Adjust Sensor Update Intervals

Modify the WiFi signal sensor update interval:

```yaml
sensor:
  - platform: wifi_signal
    name: "TuyaPlug WiFi Signal"
    update_interval: 30s  # Change from default 60s
```

#### Customize Device Name

Change the device name and add a static suffix:

```yaml
esphome:
  name: kitchen-plug  # Custom name
  name_add_mac_suffix: false  # Disable MAC suffix
```

## Home Assistant Integration

After flashing, the device will automatically appear in Home Assistant (assuming you have the ESPHome integration installed):

**Entities Created**:
- `switch.relay` - Main relay control
- `sensor.voltage` - Real-time voltage
- `sensor.current` - Real-time current
- `sensor.power` - Active power consumption
- `sensor.energy` - Cumulative energy usage
- `sensor.frequency` - Line frequency
- `sensor.tuyaplug_wifi_signal` - WiFi signal strength

## Troubleshooting

### Flashing Issues

**Problem**: Programming terminates prematurely  
**Solution**: Ensure you're using `--upload_speed 19200`

**Problem**: Cannot enter bootloader  
**Solution**: Try power cycling the device multiple times when "Connecting..." appears

**Problem**: No response from chip  
**Solution**: Verify TX/RX connections are not swapped

### Runtime Issues

**Problem**: Blue LED blinking continuously  
**Solution**: Device is in AP mode. Connect to "TuyaPlug" WiFi network and configure credentials

**Problem**: No power monitoring data  
**Solution**: Verify UART pins are correctly defined and BL0942 is properly connected

**Problem**: Device keeps rebooting  
**Solution**: Check power supply stability (ensure adequate 5V/1A supply)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## Safety Warning

⚠️ **DANGER: HIGH VOLTAGE**

This device operates with mains voltage (230V AC in EU). Improper modification or installation can result in:
- Electric shock
- Fire hazard
- Death

**Only work on this device if you are qualified and understand the risks involved with mains voltage.**

- Always disconnect from mains power before opening
- Never operate with the case open
- Ensure proper insulation after modification
- Follow local electrical codes and regulations
- Consider having modifications inspected by a qualified electrician

## License

This project is licensed under a **Custom Non-Commercial License**.

**You are free to**:
- ✅ Use this software for personal, non-commercial purposes
- ✅ Modify and adapt the code for your own use
- ✅ Share and distribute the unmodified software

**Restrictions**:
- ❌ **Commercial Use**: You may NOT sell devices with this firmware or modified versions without explicit written permission
- ❌ **Commercial Distribution**: You may NOT include this firmware in commercial products
- ❌ For commercial licensing inquiries, please contact: [your-email@example.com]

**Attribution**:
- When sharing or distributing, you must provide credit and link back to this repository

**Warranty Disclaimer**:
THIS SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY ARISING FROM THE USE OF THIS SOFTWARE.

---

## Acknowledgments

- ESPHome community for the excellent framework
- Tuya for hardware documentation
- Shanghai Belling Corp. for BL0942 documentation
- Home Assistant community

## Support

If you find this project helpful, please consider:
- ⭐ Starring this repository
- 📝 Sharing your experience and improvements
- 🐛 Reporting bugs and issues

---

**Disclaimer**: This project is not affiliated with or endorsed by Tuya Inc. All trademarks are property of their respective owners.
