# Wiring and GPIO Usage

## Keypad Connections (4x4 Matrix)
| Keypad Pin | Pico W GPIO | Notes |
|---|---:|---|
| C1 | GP19 | Column input/output for keypad scan |
| C2 | GP18 | Column input/output for keypad scan |
| C3 | GP17 | Column input/output for keypad scan |
| C4 | GP16 | Column input/output for keypad scan |
| R1 | GP26 | Row input/output, also pulled up via 1kΩ to 3V3 |
| R2 | GP22 | Row input/output, also pulled up via 1kΩ to 3V3 |
| R3 | GP21 | Row input/output, also pulled up via 1kΩ to 3V3 |
| R4 | GP20 | Row input/output, also pulled up via 1kΩ to 3V3 |

## LED Connections
Firmware order:
`ledPins = {11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 28, 27}`

| Logical LED | Label | Pico W GPIO | Color (diagram) |
|---|---|---:|---|
| ledPins[0] | 1 | GP11 | Blue |
| ledPins[1] | 2 | GP10 | Blue |
| ledPins[2] | 3 | GP9  | Blue |
| ledPins[3] | 4 | GP8  | Blue |
| ledPins[4] | 5 | GP7  | Blue |
| ledPins[5] | 6 | GP6  | Blue |
| ledPins[6] | 7 | GP5  | Blue |
| ledPins[7] | 8 | GP4  | Blue |
| ledPins[8] | A | GP3  | Red |
| ledPins[9] | B | GP2  | Red |
| ledPins[10] | C | GP28 | Red |
| ledPins[11] | D | GP27 | Red |

All LED cathodes are tied to common GND. Each LED anode is connected through a 220Ω series resistor to the assigned GPIO.

## Power and Ground
- Keypad pull-up network: 1kΩ resistors from R1..R4 to 3V3
- Common ground: all LED cathodes return to Pico GND

## Assumptions
- Diagram uses `wokwi-pi-pico`; project target is **Pico W**, which is pin-compatible for the used GPIOs.
