
MinecraftHDL
-------------------------------------------

This project attempts to be a basic "HDL" for minecraft redstone. As of now, it can compile all combinational logic, 
but the combinational logic must be specified with a list of equations in strictly sum-of-products form.

The output is generated in the form of a .schematic, which can be imported into any world using standard tools such as
WorldEdit.

Due to the necessarily generic nature of the script, the output is surely not as compressed as it could be, but the script
does generate fairly compact logic. 



./tests contains some sample input JSON files for the compiler:

* test1 is a test of the size and girth ability of the compiler. The equation for Y has a significantly wide input array, 
  and a significantly long set of prime implicants.

* test2 is the logic for a seven segment display. The compiled schematic can be directly hooked up to a compatible seven segment
  display and work (using the convention described in the remainder of this document)

* test3 is a trivial, simple example.



The convention used for the seven segment display outputs:

    SA  
SF       SB
    SG
SE       SC
    SD


IMPORTANT!
----------

Both the inputs and the outputs will be ordered in the same way that the 'inputs' and 'outputs' lists are ordered in the input file
Left to right in the input file corresponds to "from the inside of the logic rail" outward:

If your input file specifies:

"inputs": ["A", "B", "C"],
"outputs": ["X", "Y", "Z"],

your schematic (from the side), will appear as:


Y-axis
^
|
|
|
-------> Z-axis

 ___________
|            | ----X----Y----Z----   <== Output rail
|            |
|            |
|            |
|   LOGIC    |
|            |
|            |
|            | ----A----B----C----   <== Input rail
 -----------