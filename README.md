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

  | Part | What it's for | Qty | Vendor | Link |
  |---|---|---|---|---|
  | Seeed XIAO ESP32-C3 | Main controller + USB-C LiPo charging | 1 | Seeed Studio | https://www.seeedstudio.com/Seeed-XIAO-ESP32C3-p-5431.html |
  | AS608 optical fingerprint sensor | Unlocks the device | 1 | Colgroad | https://colgroad.com/product/as608-fingerprint-reader-optical-sensor-module/ |
  | 0.96" 128×64 I2C OLED (SSD1306) | Shows the 6-digit codes | 1 | Colgroad | https://colgroad.com/product/0-96-inch-128x64-i2c-oled-display-module/ |
  | DS3231 RTC module | Keeps accurate time for TOTP | 1 | Colgroad | https://colgroad.com/product/ds3231-rtc-real-time-clock-module/ |
  | Tactile push button 6×6×5 mm | Wake and switch accounts | 3 | Colgroad | https://colgroad.com/product/tactile-push-button-switch/ |
  | JST-PH 2.0 mm 2-pin male header | Battery connector on the PCB | 1 | Colgroad | https://colgroad.com/product/jst-male-connector-2-0mm-2-pin-straight/ |
  | 3.7 V 800 mAh LiPo (803035) | Power | 1 | Colgroad | https://colgroad.com/product/3-7v-800mah-803035-2-96wh-lipo-rechargeable-battery/ |
  | 10 kΩ resistor, 1/4 W | Pull-up on the sensor wake line | 1 | Colgroad | https://colgroad.com/product/metal-film-resistors-5-1-4-watt-small-values/ |
  | Jumper wires, 20 cm (pack) | Connect OLED, RTC and sensor to the PCB | 1 | Colgroad | https://colgroad.com/product/20cm-male-to-male-pin-to-pin-jumper-wires-set-20pcs-40pcs/ |
  | Custom PCB, 2-layer, 52.4 × 37.4 mm | Main board | 1 | – | – |

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
