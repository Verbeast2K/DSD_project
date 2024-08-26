# Random number generation using Linear Feedback Shift Registers in VHDL

The advantage of hardware computing lies in its high speed and efficiëncy. Using FPGA's, it's possible to set up a digital system to execute a large amount of computations in a low amount of clock cycles thanks to parallel processing.

A good example of this strength of FPGA's can be found in their ability to quickly perform complex random number generation.

This project takes a look at Linear Feedback Shift Registers (LFSR's) and how they can be used to develop random number generators.

![alt text](/images/image.png)

https://www.youtube.com/watch?v=Ks1pw1X22y4

*^Good video explaining the LFSR^*

A linear feedback shift register is a simple shift register where the input bit is a result of a linear operation of the previous register state.

The bit that gets pushed out during the register shift can be used as a pseudo randomly generated bit.

The advantage of the LFSR lies in its simplicity and this makes it possible to generate a pseudo random bit stream at high speeds. This simplicity however comes at the cost of it being finite and predictable. The linearity of the system makes it possible to easily decipher the feedback function and original seed if enough values from the bit stream are given.

![alt text](/images/image-2.png)
*Notice how easily predictable the sequence of a simple LFSR is*

So how is it possible to make a Random Number Generater (RNG) using the LFSR without it becoming predictable?

The best way to do this is to make use of multiple LFSR's that get combined in a non-linear fashion or at least one that seems non-linear. Ultimately, it's not possible to create a true non-linear function using nothing but digital systems, but we can make it a lot harder to predict the randomness by making the encoding sequence more complicated.

We have a couple of ways to do this:

1. Combining multiple LFSR's using variable timing offsets
2. Combining LFSR's with differing lengths
3. Making more convoluted tap combinations

4. Increasing the amount of LFSR's in the previous 3 solutions

A good example of a more convoluted RNG using LFSR's is the Trivium cipher.

![
](/images/image-1.png)
*structure of Trivium*

Trivium uses three shift registers with different lengths, which are combined together into 288-bit internal states. Every clock cycle, all three registers get a bit shifted into them using a combination of taps from the own register and one other register. Each clock cycle, a single bit is produced.

Furthermore, the key and initialisation vector are written in two of the three registers where the remaining bits are written in a fixed pattern and each shift register has no taps on the first 65 bits.

Thanks to its structure, the Trivium cipher makes it impossible to easily discern a pattern in the bitstream which makes the most obvious way to crack the cipher a brute-force attack.
