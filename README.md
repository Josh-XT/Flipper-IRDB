# Flipper-IRDB - IR Code Database

A database of infrared (IR) remote control codes in Flipper Zero `.ir` format.

## Folder Structure

```
TVs/           - Television IR codes
  Samsung/     - Samsung TV codes
  LG/          - LG TV codes
  Sony/        - Sony TV codes
  Vizio/       - Vizio TV codes
  ...          - Other TV brands

ACs/           - Air Conditioner IR codes
  Daikin/
  LG/
  Samsung/
  ...

Fans/          - Fan IR codes
Projectors/    - Projector IR codes
Audio/         - Audio equipment (soundbars, receivers)
DVD_Blu-ray/   - DVD and Blu-ray players
Cameras/       - Camera IR triggers
LED_Lighting/  - LED strip/bulb remotes
Miscellaneous/ - Other devices
```

## .ir File Format

Each `.ir` file contains one or more IR signals. Example:

```
Filetype: IR signals file
Version: 1
#
name: Power
type: parsed
protocol: Samsung32
address: 07 00 00 00
command: 02 00 00 00
#
name: Vol_up
type: parsed
protocol: Samsung32
address: 07 00 00 00
command: 07 00 00 00
```

**Key fields:**
- `protocol`: IR protocol (Samsung32, NEC, NECext, Sony, RC5, RC6, etc.)
- `address`: Device address in hex (little-endian, 4 bytes)
- `command`: Command code in hex (little-endian, 4 bytes)

**Converting to decimal for send_ir:**
- `address: 07 00 00 00` → address = 0x07 = 7
- `command: 02 00 00 00` → command = 0x02 = 2

## Finding IR Codes

1. Navigate to the device category folder (e.g., `TVs/`)
2. Find the brand subfolder (e.g., `Samsung/`)
3. Look for `.ir` files - often named by model or remote type
4. Read the file to get protocol, address, and command values

## Common TV Power Codes

| Brand | Protocol | Address | Command |
|-------|----------|---------|---------|
| Samsung | Samsung32 | 0x07 | 0x02 |
| LG | NEC | 0x04 | 0x08 |
| Sony | Sony | varies | varies |

## Usage with AGiXT send_ir

After finding the correct `.ir` file, extract the values and use:
- `protocol`: From the file (e.g., "Samsung32")
- `address`: First byte as decimal (e.g., 0x07 = 7)
- `command`: First byte as decimal (e.g., 0x02 = 2)
