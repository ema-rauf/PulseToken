# PulseToken

A small, battery-powered hardware 2FA token. It shows one-time login codes on an OLED screen, and only unlocks after your fingerprint is verified.

## Images

<!-- gallery:start -->
![Screenshot From 2026-10-19 03-20-42](images/Screenshot%20From%202026-10-19%2003-20-42.png)
![Screenshot From 2026-10-19 03-20-52](images/Screenshot%20From%202026-10-19%2003-20-52.png)
![Screenshot From 2026-10-19 03-20-59](images/Screenshot%20From%202026-10-19%2003-20-59.png)
![Screenshot From 2026-10-19 03-21-08](images/Screenshot%20From%202026-10-19%2003-21-08.png)
![Screenshot From 2026-10-19 03-21-17](images/Screenshot%20From%202026-10-19%2003-21-17.png)
![Screenshot From 2026-10-19 03-21-23](images/Screenshot%20From%202026-10-19%2003-21-23.png)
![Screenshot From 2026-10-19 03-21-38](images/Screenshot%20From%202026-10-19%2003-21-38.png)
<!-- gallery:end -->

## The problem

Phone authenticator apps live on a device that also gets lost, hacked, or runs out of battery. PulseToken keeps your codes on a separate pocket device that nobody else can unlock.

## How it works

1. Press a button to wake PulseToken.
2. Place your finger on the sensor. The fingerprint module checks it on its own, so the fingerprint never leaves the sensor.
3. The real-time clock keeps accurate time, which the time-based codes (TOTP) need.
4. Use the three buttons to pick an account. The 6-digit code appears on the OLED.

## Bill of Materials (BOM)

### Electronics

| # | Qty | Component | Ref | Footprint / size | Purpose |
|---|---|---|---|---|---|
| 1 | 1 | Seeed XIAO ESP32-C3 | U1 | XIAO-ESP32-C3-SMD | Main controller, USB-C charging |
| 2 | 1 | R503 capacitive fingerprint sensor (3.3 V, UART, 6-pin) | J3 | 1×6 pin header, 2.54 mm | Unlocks the device |
| 3 | 1 | 0.96" SSD1306 OLED, 128×64, 4-pin I2C | J2 | 1×4 pin header, 2.54 mm | Shows the codes |
| 4 | 1 | I2C RTC module (e.g. DS3231) | J1 | 1×4 pin header, 2.54 mm | Keeps time for TOTP |
| 5 | 3 | Tactile push button, 6×6×5 mm, THT | SW1–SW3 | SW_PUSH_6mm | Wake and select account |
| 6 | 1 | 10 kΩ resistor, 0805 | R1 | 0805 (hand-solder pads) | Pull-up on the sensor wake line |
| 7 | 1 | JST-PH 2-pin vertical connector | J4 | JST_PH_B2B-PH-K | Battery connector |
| 8 | 1 | 402030 LiPo battery, 3.7 V, with JST-PH plug | – | 4 × 20 × 30 mm | Power |
| 9 | 3 | 1×4 / 1×6 female-to-female jumper cables | – | 2.54 mm | Module connections |
| 10 | 1 | Custom PCB, 2-layer | – | 52.4 × 37.4 mm | Main board |

### Printed parts

| # | Qty | Part | File |
|---|---|---|---|
| 1 | 1 | Bottom shell | `cad/pulsetoken_bottom.stl` |
| 2 | 1 | Lid | `cad/pulsetoken_lid.stl` |
| 3 | 3 | Button cap | `cad/pulsetoken_button_cap.stl` |

### Other

| # | Qty | Item | Purpose |
|---|---|---|---|
| 1 | – | PLA or PETG filament (about 40 g) | Case |
| 2 | – | Super glue or hot glue | Holds the OLED in its clips (and the R503 if no nut is used) |

## Enclosure

- Three printed parts: bottom shell, lid, and button cap (print 3).
- Outer size: 75.5 × 42.4 × 34.6 mm.
- The PCB sits on 4 corner supports with locating fences; 4 posts under the lid press it down.
- The LiPo sits in a frame on the floor under the board, with a wire slot up to the JST connector.
- The R503 mounts through a 25.4 mm hole in the lid (its 28 mm ring rests on top).
- The OLED sits in a bay on the left, held by 4 corner clips behind a 23 × 12 mm window.
- The lid snaps on with 4 bumps that click into grooves in the walls.
- USB-C cutout lines up with the XIAO port for charging.
- Tolerances: 0.2 mm lid fit and OLED pocket, 0.3 mm around each button cap, 0.2 mm around the sensor thread, 0.5 mm around the PCB and battery.
- Verified with `cad/fit_check.py` against the real KiCad board model: no collisions between any case part, the board, battery, XIAO, fingerprint sensor or OLED, and every cap sits over its button.

## Files

```
cad/         STEP and STL files,
            pulsetoken_assembly.step (everything in place)
pcb/        KiCad schematic and PCB
images/     Screenshots and renders
```

## Printing

- Bottom shell: print as is, no supports.
- Lid: print upside down (flat top on the bed); the posts and clips then point up, no supports needed.
- Button caps: print 3, flange down.
- PLA or PETG, 0.2 mm layers, 20% infill.

## Assembly

1. Put the LiPo in its frame and run the wires up through the slot to J4.
2. Drop the PCB onto the corner supports.
3. Push the OLED into its clips (a dot of glue keeps it in place) and fit the R503 through its hole.
4. Put the button caps into the lid from below.
5. Connect the module cables, then press the lid down until it clicks.
