# Scott Data Systems 1

A gate-level emulator of the computer from *But How Do It Know?* by John Clark Scott.
It runs at <https://scott-cpu.cs.montana.edu/>.

The page builds the circuit and the drawing from the same description, so every wire
on the screen is a net in the machine. The registers are named A, B, C and D, the way
an 8-bit machine names them.

## Use

Open `index.html` in a browser. No build step and no server are needed.

The editor is Monaco, loaded from a pinned CDN copy so the 13 MB editor is not checked
in. With no network the page falls back to a plain text box and everything else keeps
working, so a lecture survives a dead connection.

| Control | Effect |
|---|---|
| `START` / `STOP` | Start and stop the clock. `START` stops on a jump to its own address |
| `BACK TICK` | Undo the last tick |
| `TICK` | One quarter of a step |
| `SINGLE STEP` | One stepper step |
| `INSTR` | All six steps of one instruction |
| `RESET` | Clear the registers. Memory stays |
| `CLEAR MEM` | Set all 256 bytes to zero |

With the clock stopped:

- Click a register bit or a memory bit to flip it.
- Click a wire to hold it on. A second click lets it go.
- Click the clock for the next phase. Click the stepper for the next step.
- Held step wires are exclusive. A click on one releases the others.

Query parameters: `?prog=and` or `?prog=sample` loads a program. `?speed=20` sets the clock rate.

## The assembly language

```
MOV A, 10       load a number          ADD A, B        A = A + B
MOV A, [B]      read memory at B       NOT A           also SHL and SHR
MOV [B], A      write memory at B      CMP A, B        set the flags only
JMP label       jump                   JE / JG / JGE   jump on the flags
HLT             stop                   DB 1, 2, 3      data bytes
```

The registers are A, B, C and D, and each holds a byte. A number is decimal, `0x`
hex or `0b` binary. A label is written `name:` and then used as an address. A
comment starts with `;`, and a comma between operands is optional.

`CMP` sets the flags and a jump reads them, so a conditional jump must follow its
`CMP` directly. `JG` and `JGE` compare unsigned, because the comparator reports
unsigned "larger".

Press `HELP` in the page for the same guide.

## Credits

Design of the computer copyright John Clark Scott 2009, <https://buthowdoitknow.com/>.
The design may be used freely for personal and educational use while the copyright
stays visible.

This emulator is an independent implementation written for CSCI 366 at Montana State
University.

## Deployment

GitHub Pages serves the `main` branch from the root. `CNAME` holds the custom domain.
