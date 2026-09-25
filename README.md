# Scott Data Systems 1

A gate-level emulator of the computer from *But How Do It Know?* by John Clark Scott.
It runs at <https://scott-cpu.cs.montana.edu/>.

The page builds the circuit and the drawing from the same description, so every wire
on the screen is a net in the machine. The registers are named A, B, C and D, the way
an 8-bit machine names them, and it assembles x266.

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

## x266

x266 is x366 assembly for this machine. Every mnemonic is one x366 mnemonic that one
SDS-1 instruction performs, so the source reads like the x366 the course teaches later
and the bytes run on the hardware below.

```
MOV A, 10       load a number          ADD A, B        A = A + B
MOV A, [B]      read memory at B       NOT A           also SHL and SHR
MOV [B], A      write memory at B      CMP A, B        set the flags only
JMP label       jump                   JE / JG / JGE   jump on the flags
HLT             stop                   DB 1, 2, 3      data bytes
```

`CMP` sets the flags and a jump reads them, so a conditional jump must follow its `CMP`
directly. `JG` and `JGE` compare unsigned, because the comparator reports unsigned
"larger".

These are not in x266, because no single machine instruction performs them: `SUB`,
`INC`, `DEC`, `LEA`, `JNE`, `JL`, `JLE`, `LOOP`, `MOV A, B` and `MOV A, [0x20]`.
`SYSCALL` is rejected too: the instruction set has an I/O opcode, but this drawing has
no device attached to it.

This matches `X266Assembler.java` in the course repository, so a program assembles to
the same bytes in either tool. Press `HELP` in the page for the same list.

## Credits

Design of the computer copyright John Clark Scott 2009, <https://buthowdoitknow.com/>.
The design may be used freely for personal and educational use while the copyright
stays visible.

This emulator is an independent implementation written for CSCI 366 at Montana State
University.

## Deployment

GitHub Pages serves the `main` branch from the root. `CNAME` holds the custom domain.
