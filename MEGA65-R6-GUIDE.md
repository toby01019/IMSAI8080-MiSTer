# IMSAI 8080 for MEGA65 R6: front-panel update

Version 0.3.0 front-panel prototype, 23 October 2026, by Toby.

The original-style front panel and green 80-column terminal now share one screen. F7 enlarges the front panel; F7 again restores the combined view. The program, terminal and RUN/STOP state are preserved. LEDs and supported switch positions reflect live machine state. STEP and POWER are display-only.

## Illustrated views

Illustrated documentation edition, 23 October 2026. The FPGA core remains version 0.3.0; its binary is unchanged.

These two views are rendered from the MEGA65 simulation, not captured from physical hardware. The R6 hardware results are documented separately below. R3 hardware remains untested.

![Combined terminal and front panel — MEGA65 simulation render](mega65-combined-simulation.png)

Combined terminal and front panel — MEGA65 simulation render.

![Enlarged front panel with F7 — MEGA65 simulation render](mega65-f7-simulation.png)

Enlarged front panel with F7 — MEGA65 simulation render.

F7 switches between the combined terminal/front-panel view and the enlarged front panel. Press F7 again to return; terminal contents and program state are preserved. STEP and POWER are display-only.

## Requirements and installation

This is the **R6 hardware build**. Use it only with the matching MEGA65 board revision. R3A is not separately verified. The R3 and R6 files are independently compiled; do not interchange them.

Keep your current working core and factory/recovery slot. This package has a distinct filename, `PANELR6.COR`. Copy it to the SD card without replacing an older core. Select an available non-factory slot in the NO SCROLL startup menu and check the target before installing. Do not interrupt a flash operation. Installation on Toby's R6 and the confirmed hardware checks are documented below.

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

The R6 short hardware test below passed. R3 hardware remains untested. Simulated previews are labelled as such. The framework and existing menu firmware are unchanged; external I/O exceptions from its timing constraints remain.

## R6 hardware test — 23 October 2026

The version 0.3.0 front-panel core was installed in slot 5 of Toby's physical MEGA65 R6. The following results were confirmed by Toby at the connected display and keyboard; they are user-observed hardware results, separate from the automated simulation results.

| Test | Observed result |
| --- | --- |
| Boot and display | Combined terminal/front-panel view and enlarged front-panel view work. |
| F7 view switching | Enlarges the panel and returns to the combined view; typed HALLO remains visible. |
| F1 RUN / STOP | Both states work. |
| Memory controls | In STOP, selected hexadecimal address 8000, prepared A5 and wrote it; after next/previous address navigation, address 8000 reads A5. |
| Program loading | Tiny BASIC starts through the existing program loader. |
| BASIC arithmetic | PRINT 6*7 returns 42. |
| Program retention across F7 | Entered 10 PRINT "HALLO", switched views twice, then RUN prints HALLO. |
| Resume after STOP | After STOP and RUN, PRINT 2+3 returns 5. |

This is a successful short hardware smoke test, not an exhaustive compatibility or endurance test. R3 hardware, complete game play, every switch/LED and external peripheral operation remain unverified. STEP and POWER remain display-only.

Only the previous IMSAI slot 5 was replaced, with Toby's explicit authorization. Its v0.2.1 rollback COR file was preserved and hash-verified. The main core and other slots were not programmed; the SD-card MEGA65.ROM and MEGA65.D81 hashes matched before and after transfer. No full readback comparison of all flash slots was performed.

## First hardware check

Check the boot text and terminal, HELP menu, BIN loading and a simple BASIC calculation. Use F1 to stop, read/edit a safe RAM address, then F7 twice; verify the same memory and terminal content return. Repeat F7 during normal execution and check the program continues. Keep the older core available as fallback.

Sources, component licenses and build reports accompany this package. The shared framework is MiSTer2MEGA65; the CPU is vm80a. See CREDITS.md and Sources/ for their original licenses. The front-panel artwork is a decorative recreation, not a claim that every physical IMSAI control is implemented.

## Measured implementation results

Setup slack: +0.387 ns; hold slack: +0.016 ns; pulse-width slack: +0.264 ns.

| Resource | Used | Available | Use |
| --- | ---: | ---: | ---: |
| Slice LUTs | 20236 | 134600 | 15.03% |
| Slice Registers | 12574 | 269200 | 4.67% |
| Block RAM Tile | 137.5 | 365 | 37.67% |
| DSPs | 58 | 740 | 7.84% |

The DRC report contains warnings, not a warning-free certification. The R3 warning summary matches the previous v0.2.1 R6 baseline (143 warnings across CHECK-3, DPIP-1, DPOP-1, DPOP-2, REQP-1580 and REQP-1839). Read the board-specific report for the actual list. Async RAM-control and framework pipelining warnings remain; the short R6 hardware test does not establish exhaustive hardware coverage.
