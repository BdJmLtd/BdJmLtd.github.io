---
title:  "EPANET: C语言"
sequence: 004
---

## API

The procedure for working with these functions is as follows:

1. Use the `ENopen` function to open the Epanet library, which will enable the
   rest of the functions, except the ENepanet function.
2. Use the `ENsetxxx` functions to change the properties of elements or
   characteristics of the network or use the `ENgetxxx` functions to retrieve data
   from the network saved in the input file (file with `inp` extension).
3. For a complete simulation use the `ENsolveH` function  (this function
   automatically saves the results in a hydraulic-results file), or if a step-by-step
   simulation is desired use the following sequence of functions: `ENopenH`,
   `ENinitH`, `ENrunH`, `ENnextH`, `ENcloseH`, and access the results through the `ENgetxxx` function series.
4. The `ENsolveQ` function runs a complete simulation of a water quality model
   (this function automatically saves the hydraulic and water quality results in an output file),
   or if running the simulation step-by-step, use the following
   functions sequence: `ENopenQ`, `ENinitQ`, `ENrunQ`, `ENnextQ`, `ENcloseQ`,
   and access the results through the `ENgetxxx` function series.
5. If running new analyses is desired, return to step 2 or use the `ENreport`
   function to save a results report formatted in the results report file.
6. Call the `ENclose` function to close the Epanet file that was opened initially,
   this frees up the memory that was occupied on the computer.

To sum up, with the Epanet API we can do the following tasks:

1. Open and close the Toolkit
2. Retrieve and set network parameters
3. Run a hydraulic simulation
4. Run a water quality simulation
5. Retrieve results
6. Generate a results report

## Hydraulic Analysis

Call `EN_closeH` after all hydraulics analyses have been made
using `EN_initH` - `EN_runH` - `EN_nextH`.
**Do not call this function if `EN_solveH` is being used.** 

