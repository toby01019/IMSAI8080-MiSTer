# IMSAI 8080 for MEGA65 R3: front-panel update

Version 0.3.0 front-panel prototype, 23 October 2026, by Toby.

The original-style front panel and green 80-column terminal now share one screen. F7 enlarges the front panel; F7 again restores the combined view. The program, terminal and RUN/STOP state are preserved. LEDs and supported switch positions reflect live machine state. STEP and POWER are display-only.

## Requirements and installation

This is the **R3 hardware build**. Use it only with the matching MEGA65 board revision. R3A is not separately verified. The R3 and R6 files are independently compiled; do not interchange them.

Keep your current working core and factory/recovery slot. This package has a distinct filename, `PANELR3.COR`. Copy it to the SD card without replacing an older core. Select an available non-factory slot in the NO SCROLL startup menu and check the target before installing. Do not interrupt a flash operation. No core has been installed automatically by this build task.

Keep your existing `/IMSAI` program directory and BIN files from the previous release. Historical BASIC and game binaries are not duplicated in this update. Open **HELP → Programs → BIN** to load a program. HELP closes the menu.

## Controls on the MEGA65 keyboard

| Key | Function |
| --- | --- |
| F1 | Toggle RUN / STOP |
| Shift+F1 (F2) | Enter hexadecimal memory address while stopped |
| F3 | Prepare a hexadecimal byte while stopped |
| Shift+F3 (F4) | Write the prepared byte to memory while stopped |
| F5 | Next memory address while stopped |
| Shift+F5 (F6) | Previous memory address while stopped |
| F7 | Toggle combined terminal/front panel and enlarged front panel |
| Return | Finish the current edit |
| HELP | Open / close the core menu |

For Kill the Lights, keys 1–8 operate the input switches as in the previous version. The on-screen labels F2/F4/F6 refer to the shifted physical keys listed above. STEP is not an instruction-step feature.

## Validation and limits

The integrated MEGA65 simulation checks boot, typed echo, LEDs, stopped-memory deposit, F7 in STOP and RUN, preserved terminal and RAM, visible RGB and blanking alignment, and panel scaling. Separate regression tests exercise the BIN loader and Tiny BASIC `PRINT 6*7 = 42`. The board-specific FPGA build, timing and core header/CRC have been checked; reports are included.

**This new release has not been tested on real R3 or R6 hardware.** Older release hardware results do not validate this update. Simulated previews are labelled as such. Complete game play and physical HDMI/keyboard/SD operation remain to be verified. The framework and existing menu firmware are unchanged; external I/O exceptions from its timing constraints remain.

## First hardware check

Check the boot text and terminal, HELP menu, BIN loading and a simple BASIC calculation. Use F1 to stop, read/edit a safe RAM address, then F7 twice; verify the same memory and terminal content return. Repeat F7 during normal execution and check the program continues. Keep the older core available as fallback.

Sources, component licenses and build reports accompany this package. The shared framework is MiSTer2MEGA65; the CPU is vm80a. See CREDITS.md and Sources/ for their original licenses. The front-panel artwork is a decorative recreation, not a claim that every physical IMSAI control is implemented.

## Measured implementation results

Setup slack: +0.344 ns; hold slack: +0.049 ns; pulse-width slack: +0.264 ns.

| Resource | Used | Available | Use |
| --- | ---: | ---: | ---: |
| Slice LUTs | 20318 | 134600 | 15.10% |
| Slice Registers | 12730 | 269200 | 4.73% |
| Block RAM Tile | 137.5 | 365 | 37.67% |
| DSPs | 58 | 740 | 7.84% |

The DRC report contains warnings, not a warning-free certification. The R3 warning summary matches the previous v0.2.1 R6 baseline (143 warnings across CHECK-3, DPIP-1, DPOP-1, DPOP-2, REQP-1580 and REQP-1839). Read the board-specific report for the actual list. Async RAM-control and framework pipelining warnings remain; physical testing is still required.
