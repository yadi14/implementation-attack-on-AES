# Exhaustive Search on Plaintext and Key
### Find all the m's which satisfies s(p + k) + s(p' + k) = m, for all possible p, p', k, and p != p' under GF(2^8) and AES's S-box. Variables p, p', k, and m are polynomials under GF(2^8).

Both programs, `P1P2K_VERBOSE.cpp` and `P1P2K_SIMPLIFY.cpp`, exhaustively simulate all 256 k's under each possible combinations of p and p', with constraint p!=p'. The total possible {p,p'}'s are are 255+254+...+2+1=32640.

# Quick Start
* Create two new directories
```
mkdir p1p2_VERBOSE
mkdir p1p2_SIMPLIFY
```
* Compile c++ program
```
g++ P1P2K_VERBOSE.cpp -o p1p2k_verbose.out
g++ P1P2K_SIMPLIFY.cpp -o p1p2k_simplify.out
```
Since each program output a total of 32640 text files in each folder `p1p2_VERBOSE`, `p1p2_SIMPLIFY`, it may take several minutes to finish execution.

* Verify all text files in `p1p2_SIMPLIFY` with MATLAB
Directly run `verifyP1P2K.m` in MATLAB.

# Output Structure
For each file in folder `p1p2_VERBOSE`, the first line contains the value of `p` and `p'`, i.e.,
> p = 00, p' = 01
The subsequent content in each file record the value for k, the S-box output, `s(p^k)`, `s(p'^k)`, and result of m, `s(p^k)^s(p'^k)=m`.
For example,
> k = 00	s(p^k) = 63, s(p'^k) = 7c, s(p^k)^s(p'^k) = 1f
> k = 01	s(p^k) = 7c, s(p'^k) = 63, s(p^k)^s(p'^k) = 1f
> k = 02	s(p^k) = 77, s(p'^k) = 7b, s(p^k)^s(p'^k) = 0c
> ...
> k = ff	s(p^k) = 16, s(p'^k) = bb, s(p^k)^s(p'^k) = ad

All numeric inside .txt file are in hexadecimal format.

In folder `p1p2_SIMPLIFY`, each file has 256 lines of hexadecimal value. All the outputs in `p1p2k_simplify.out` are the abbreviated version of the files of the same name in folder `p1p2_VERBOSE`, and it only record the m value for each k.

# Software Tools
- g++ or MinGW
- MATLAB in __2020b__ or later version. `verifyP1P2K.m` calls function [readlines](https://www.mathworks.com/help/matlab/ref/readlines.html), which is introduced on __2020b__.

# Software Used
All C++ programs have tested under g++ 7.5.0. MATLAB program has been tested on both MATLAB __2020b__ and __2021a__.
