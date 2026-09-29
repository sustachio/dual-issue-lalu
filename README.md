# Dual-Issue LALU

This is a Logisim processor implementing a custom dual-issue version of Tomasulo's algorithm. A full write up on the project and its performance can be found at http://sethmueller.page/post/dual-issue-out-of-order-superscaler-processor-using-tomasulo-s-algorithm-in-logisim. The algorithm is used to dynamically track dependencies between queued instructions recently pulled from memory and run them out-of-order to achieve efficient use of the multiple ALUs+memory unit. It implements an ISA used by the simplistic LALU processor in a course my school offers.

The processor has 4 16 bit registers, operates on 8 bit instructions, and can maintain up to 2 instructions completing per cycle with an optimized program.

Some fun hardware optimizations include:
- Store instructions do not occupy the common data bus upon completion allowing 3 instructions to complete on a single clock cycle under certain conditions
- The instruction memory contains 16 bit words so two 8 bit instructions can be fetched on each clock cycle (misalignment is also handled)
- All dependencies between the two instructions being issued on the same clock cycle are managed and reservation stations/registers are properly allocated

_Top level overview_

![Top level overview](/overview.png)

_Implemented ISA_

![LALU ISA](/laluisa.png)

Use instructions:
- Open `dual_issue.circ` in Logisim
- Toggle the `rst` pin high and tick the clock to set up the RAM blocks
- Copy the program in the text box into `Instruction Memory` or compile a new one with `assemblerdual.py` and `progdual.asm`
- Toggle the clock pin to run programs
