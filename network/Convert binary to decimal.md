	128 | 64 | 32 | 16 | 8 | 4 | 2 | 1

## to convert decimal to binary we subtract the num by the values going left to right, if it is bigger or equal.

ex: 191
191 - 128 = 63 -> we put a I in the first bit
63 is smaller the 64 -> we put a 0 in the next bit;
 63 - 32 = 30 -> we put a I in the next bit;
 30 - 16 = 14 -> we put a I in the next bit;
 14 - 8 = 6 -> we put a I in the next bit;
 6 - 4 = 2 -> we put a I in the next bit;
 2 - 1 = 1 -> we put a I in the next bit;
 1 - 1 = 0 -> we put a I in the next bit; 
1 0 1 1 1 1 1 1

to convert bin to decimal we add the corresponding bits to the power of two table

ex:  0 1 1 0 0  1 0 1

64 + 32 + 4 + 1 = 101;