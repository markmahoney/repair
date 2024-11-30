November 2024

Got the floppy drive for pretty cheap off eBay, because it was untested. You could tell just from pics on the listing that it was in pretty rough shape. When it arrived, it was indeed in rough shape.

- completely disassembled unit
- applied rustoleum and a wire brush dremel to the (aluminum?) base
- cleaned PCB and entire floppy-handling assembly
- found and installed replacement spindle and stepper motors as the old ones were totally seized
- located a seemingly servicable replacement belt for the spindle drive
  - Atari 1050-adjacent Floppy Drive rubber spindle belt from console5
  - tuned by adjusting pot at r7 to 300rpm
- replaced cap at c14 because it was leaking, plus caps c12 and c5 because they looked suspicious
  - c5: PART: 1572-1103-N from digikey; CAP ALUM 220UF 20% 16V AXIAL TH
  - c14: PART: 495-2442-N from digikey; CAP FILM 10000PF 10% 400VDC RAD
  - c12: PART: 4000PHCT-ND from digikey; CAP ALUM 470UF 20% 6.3V AXIAL TH

I also start reading through https://www.wang2200.org/docs/external/MPI_51-52_FlexibleDiskDriveProductManual.729-1114.5-82.pdf and though it's a useful point of reference for the rough shape of the underlying drive mechanisms, the PCB in the Rana Systems drive differs substantially from the design referenced in that document. But I can't find anything specific to the Elite One o its the best I can do.

At this point after reassembly, the drive powers up, spindles moves, and the read head can track back and forth. Busy light turns on when spindle is rotating and the write protect light/circuit seems to work correctly. But when I hook the drive up to an Apple II it can't read shit.

I built a small driver out of a RPi Pico 2 board and an ATX power supply so that I could power the spindle and drive the read head back and forth at will, and look up an article on how to adjust track positioning of the read head, assuming that was the problem (https://polprog.net/blog/fdalign/ is an excellent article). I also install header pins at test points 1, 2, 3 because it seems like that's where the amplified signal from the MC3470P (https://ia803001.us.archive.org/30/items/MC3470/MC3470_text.pdf) goes from pins 16/17; those test points were unpopulated for some reason.

At this point though, I don't see shit on the scope; inputs are set to AC coupling, 100mv, 1us but nothing of note to see that isn't maybe just noise. I try adjusting and then entirely replace pots R15 and R28 (3009P-1-203 on mouser, "Through Hole Trimmer Resistors - Through Hole 20Kohms 10% 3/4inch rectangular") as I think those are part of some kind of filter network, but still nothing. I also replace the MC2470P with a maybe-real new old stock part but no dice.

Is the read head solenoid just dead? Did I damage it during disassembly? It's apparently kind of sensitive.

Things I still haven't tried but would if I didn't want to move on to other projects right now:
- measure voltage going to the read head solenoids at pin 5 just to make sure there's anything there
- I bought some new darlington transistor packages for U5 just in case but that's probably not it
- pull the J175 FETs at F1/F2 to see if they're good, and maybe look at the other transistors around there at Q4/5
- see if I can track down a new read/write solenoid part for the read head

Frustrating! I need to be more patient with myself though; I still don't know shit about electronics, but whenever I spend time with this stuff, I am learning! Even when I wind up just making things worse.
