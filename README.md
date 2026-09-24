# Scott CPU

A gate-level emulator of the computer from *But How Do It Know?* by John Clark Scott.
It runs at <https://scott-cpu.cs.montana.edu/>.

The page is one file with no dependencies. It builds the circuit and the drawing from
the same description, so every wire on the screen is a net in the machine.

## Use

Open `index.html` in a browser. No build step and no server are needed.

| Control | Effect |
|---|---|
| `run` / `stop` | Start and stop the clock. `run` stops on a jump to its own address |
| `back tick` | Undo the last tick |
| `tick` | One quarter of a step |
| `step` | One stepper step |
| `instruction` | All six steps of one instruction |
| `reset` | Clear the registers. Memory stays |
| `clear memory` | Set all 256 bytes to zero |

With the clock stopped:

- Click a register bit or a memory bit to flip it.
- Click a wire to hold it on. A second click lets it go.
- Click the clock for the next phase. Click the stepper for the next step.
- Held step wires are exclusive. A click on one releases the others.

Query parameters: `?prog=and` or `?prog=sample` loads a program. `?speed=20` sets the clock rate.

## Instructions

Press `help` in the page for the full list. The assembler accepts labels, `;` comments,
and one-register ALU forms such as `SHL R0`. IN and OUT are not wired, because the
machine has no I/O devices.

## Credits

Design of the computer copyright John Clark Scott 2009, <https://buthowdoitknow.com/>.
The design may be used freely for personal and educational use while the copyright
stays visible.

This emulator is an independent implementation written for CSCI 366 at Montana State
University.

## Deployment

GitHub Pages serves the `main` branch from the root. `CNAME` holds the custom domain.
