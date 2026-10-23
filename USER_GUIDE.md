# User guide -- 23 October 2026

## Kurz erklärt: F1 bis F7

| Taste | Funktion |
|---|---|
| **F1** | Programm anhalten (STOP) oder weiterlaufen lassen (RUN). |
| **F2** | Speicheradresse auswählen und ihren Inhalt ansehen. |
| **F3** | Neuen Wert zum Schreiben vorbereiten - ändert noch nichts. |
| **F4** | Den vorbereiteten Wert an die ausgewählte Adresse schreiben. |
| **F5** | Nächste Speicheradresse ansehen. |
| **F6** | Vorherige Speicheradresse ansehen. |
| **F7** | Zwischen gemeinsamer Terminal-/Frontplattenansicht und großer Frontplatte wechseln. |

**F2 bis F6 funktionieren im STOP-Zustand. Nur F4 verändert den Speicher. F7 wechselt nur die Ansicht: Ein laufendes Programm läuft weiter, ein angehaltenes bleibt angehalten.**

The default screen combines the 80 x 16 terminal and smaller panel. F7 enlarges
the panel and returns without resetting the program. STEP and POWER are display-only.

## Starting a program

The installed entries appear in MiSTer's Computer menu:

| Entry | Purpose |

| --- | --- |

| IMSAI8080 Update - Terminal | Terminal demonstration with keyboard echo |

| IMSAI8080 Update - Switch test | Simple input/output test |

| IMSAI8080 Update - Complement test | Complementary output test |

| IMSAI8080 Update - Kill the Lights | Historical LED game |

| IMSAI8080 Update - Tiny BASIC | Palo Alto Tiny BASIC V3.0 |

| IMSAI8080 Update - BASIC 4.0 | Altair 8K BASIC 4.0 |

| IMSAI8080 Update - Super Star Trek | BASIC 4.0 with automatically loaded Star Trek |

For Star Trek, wait for the listing to finish and COMMAND? to appear. Restarting its menu entry starts a new game.

## Front-panel controls

| Key | Function |

| --- | --- |

| F1 | Toggle RUN/STOP; wait for STOP before modifying memory |

| F2 | EXAMINE: enter a hexadecimal address |

| F3 | Enter a hexadecimal byte to write |

| F4 | DEPOSIT: write the prepared byte at the selected address while stopped |

| F5 | Examine the next address |

| F6 | Examine the previous address |

| Enter or Escape | Finish address or byte entry |

| F7 | Toggle combined terminal/panel and enlarged front panel |
| F12 | Open the MiSTer menu |

Addresses use four hexadecimal digits; bytes use two, entered with 0-9 and A-F. New digits shift older digits left; extra digits displace the oldest. The highlighted field identifies active input.

When stopped, ADDRESS identifies the selected location, DATA and MEM show its contents, and WRITE shows the prepared value. During RUN, address and data display the CPU bus. Input goes to the terminal while running and to the panel field while stopped.

EXAMINE does not change the program counter. RUN resumes the suspended program. These are monitor-style controls rather than a complete replica of the historical CP-A circuitry.

## First memory test

Use the Terminal demonstration:

1. Press F1 until STOP appears.

2. Press F2 and enter 8000.

3. Press F3 and enter A5.

4. Press F4; MEM should show 8000 = A5.

5. Press F5, then F6; A5 should still be present.

6. Press F1 to resume; terminal input should work again.

8000 is unused by this demonstration. It is not generally safe to modify that address in other programs; Star Trek's loader uses upper memory for its script.

## Input limitations

The keyboard supports uppercase letters, digits, space, Enter, backspace and some punctuation. Shift combinations for plus, asterisk and quotation marks, and Ctrl-C, remain incomplete. The font can display symbols that the keyboard cannot yet enter.

F1 pauses the CPU; it does not replace BASIC's Ctrl-C break function. Restarting an entry reloads the image and discards unsaved changes.

![Front-panel memory examination and deposit](front-panel-memory-check.png)

