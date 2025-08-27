# Chip 3 Mini@sic

This is the project that was a little rushed, main purpose for this project is to verify the tool chain for UMC PDK.

## 26 Aug

I wanted to include the row based encoder for this design (**Row_encoder_5P**), other than that, I would like to include the LVDS transmitter (**FXLVTX020HA0A**) and probably the memory FIFO module (memory module not generated yet, but requested)

First of all, I will try to generate this module's layout and optimise the port (tiktok port has been designed with 45 pins, which is not necessary).

### Stuff I need to write down:

LVDS module can be simulated with the provided! Just make sure the input are correctly set!

**VBG** should be set at 1.2 V for the band gap reference.
**EN** should be set at 1, and the module will only start waking up after this has been set at 1, the wake up time is about **1 ms**
**RS** this decides if the module is working at power down mode, 0 for power down, 1 for normal working.

In the meantime, the LVDS module is an IO cell itself, so it does not require more IO cells. 

But to power the cell, it is required to have 2 pairs of independent power cells, for both Analogue 3.3 V and Digital 3.3 V and respective GND.


## 27 Aug

Finished the synthesis for the row based encoder using GII faraday standard cells, which should be compatible. But the flip-flop cells used in the implementation are the scan registers, which causes problems in innovus. Innovus tool will think the design has a scan chain, which does not exist.

Will now redo synthesis and add a scan chain in it.

I have added the scan chain inside the design, but it seems I have designed it in the wrong clock frequency....

I forgot the compression unit works at 40 MHz instead of 20 MHz...

Will have to fix this....

In the mean time, I do not know if this is the correct behaviour for the unit...