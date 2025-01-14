
# Donut accelerator for IceBreaker

The 'donut demo' software can be linked in with any project 
by adding this line in the Makefile:

```
DEFINES += DONUT_DEMO
```

This project has created a simple CFU that provides two custom instructions:
* single-cycle multiplication for the low 32b only
* single-cycle multiplication for the low 32b only followed by a 10-bit 
arithmetic right shift.


The unaccelerated donut code is in `$CFUROOT/third_party/litex_donut/donut.c`.
It was adapted from the LiteX "bare metal demo".
The accelerated donut code for this project is in ./src/donut.c.
It was modified by hand from the unaccelerated version.
The only changes were replacing instances of "a*b" and "(a*b)>>10" with CFU instructions.

In the demo we target the "icebreaker" board and use the "breaker+cfu"
VexRiscv variant.  In this variant, the CPU 'mul' instruction is implemented 
with an iterative multiplier unit that is slower than the CFU version.
Yes, this is a contrived example; 
it exists simply to illustrate the mechanics of adding new instructions 
using a CFU and then invoking those instructions from C code.

To run the accelerated donut demo in this project, 
plug in an iCEBreaker board and run:
```
make TARGET=icebreaker EXTRA_LITEX_ARGS="--cpu-variant=breaker+cfu" prog
make TARGET=icebreaker EXTRA_LITEX_ARGS="--cpu-variant=breaker+cfu" load
```


If all goes well, you will be connected to the CFU Playgroud menu running
on the board.   You will probably need to hit SPACE for the menu to appear.
Then just hid 'd' for the donut demo.


To compare against the unaccelerated version, cd over to the `proj_template_no_tflm`
directory and run the same `make` commands listed above.


