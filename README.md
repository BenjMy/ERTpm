# ERT Project Manager #

## Description ##

This package provides some convenient functions for handling ERT processing, inversion and visualization with particular focus on the project and time-lapse datasets.

*Manager* organizes the datasets and ERT parameters, it calls calls *process*, *invert*, and *plot*.
Default values for the parameters (arguments) of each module are described and stored through argparse.
This also allows each module to be called directly from the command-line, bypassing the ert *manager* module.
When called from the ert *manager* the argparse arguments are updated based on the ert manager inputs.
This way generic-default values are given in each module (also as example) but each project can store modified values and call the modules with a simple *manager* API.
In practice, each module follows these same steps:
    1. check cmd-line args and possibly update argparse default values.
    2. update arguments in case the module is called from the manager with new arguments.
    3. check consistency and agreement of the updated parameters.

## Installation ##

1. Clone the repository into a local directory. Choose a convenient directory as you may want to edit the package.
2. Make sure you have install the dependencies:
    1. pyvista (it automatically installs pandas, numpy, other needed libraries)
    2. pybert (ert library, it automatically installs pygimli). Note that this is included in the setup dependencies.
    3. pip, re, os, arparse, setuptools, and others are commonly already installed
    4. optional but suggested is numba, which is use to optimize some numerical functions.
3. go to the clone repository, in the root folder (where setup.py is)
4. pip install the package with editable option: `pip install -e .`

The editable installation keeps the code in the current directory, rather than default python directories (i.e., site-package).
The advantage is that any change to the package will simply available without bringing the changes in site-package by removing and reinstalling.
Alternatively, add the repository to the pythonpath variable (in .bashrc).
However editable installation has several advantages as pip and python take care of the package (e.g., dependencies, autocomplete, etc.).

## Usage ##

There is an example in ./tests.
In general, package objects can be imported as rfor standard python packages (e.g., from ERTpm.process import process).


Some of possible output formats:
AppRes and FreqDom
! ID      A      B     M      N      Appres  Amplitude,  Phase   Real-Cor, Imag-Cor  Real-Raw, Real-Std  Imag-Raw, Imag-Std  |Current| Cur.-Real, Cur. Imag   ContctR      SP    Date_And_Time Channel Gains   Tx_V
! num   Ca El  Ca El  Ca El  Ca El   (Ohm-m)   (Ohms)      (mr)    (Ohms)    (Ohms)      (V)       (V)        (V)      (V)       (ma)     (ma)       (ma)      (Ohms)     (mv)
000001 001,01 001,04 001,02 001,05 +9.336484 +3.714867 -1.291627 +3.714864 -.0047982 +2.159077 +.0034526 +.0174144 +.0031993 +581.2180  +581.1925 +5.438460 +117.0000 +138.0016 20190427_121334 CH 01 GN 1 2    62
0                               8                         11                         14         15                            18                             21                 21 + SP
NoAppRes and FreqDom
! ID      A      B     M      N    Amplitude,  Phase   Real-Cor, Imag-Cor  Real-Raw, Real-Std  Imag-Raw, Imag-Std  |Current| Cur.-Real, Cur. Imag   ContctR      SP    Date_And_Time Channel Gains   Tx_V
! num   Ca El  Ca El  Ca El  Ca El   (Ohms)      (mr)    (Ohms)    (Ohms)      (V)       (V)        (V)      (V)       (ma)     (ma)       (ma)      (Ohms)     (mv)
000001 001,01 001,04 001,02 001,05 +206.1568 -3.404595 +206.1557 -.7018794 +4.340335 +.0075644 +.0044347 +.0080165 +21.05357  +21.05337 +.0931900 +9828.000 -23.92758 20190727_121132 CH 01 GN 1 4    199
0                               8  9 r        10 ip                        13 v                                    17 curr                        20 ctc              21 + SP
NoAppRes but TW
! ID      A      B      M      N        V/I,      Std.     Amp.,     Std.  IP Window 01,  Std.      SP     Current     ContactR  Date_And_Time    Gains     Tx_V
! num   Ca El  Ca El  Ca El  Ca El     (Ohms)    (Ohms)   (Volts)   (Volts)    (mV/V)    (mV/V)    (mV)      (ma)        (Ohms)
000001 001,01 001,04 001,02 001,05 +3.85274577 +.0035838 +1.583665 +.0014731 +6.090041 +.0331004 +21.71237 +411.048590 +352.0000 20191218_112710 CH 01 GN 1   124
0                               8                         11                                              13+SP+2*TW 14+SP+2*TW    15+SP+2*TW
NoAppRes and TimeDom
! ID      A      B      M      N        V/I,      Std.     Amp.,     Std.       SP     Current     ContactR  Date_And_Time    Gains     Tx_V
! num   Ca El  Ca El  Ca El  Ca El     (Ohms)    (Ohms)   (Volts)   (Volts)    (mV)      (ma)        (Ohms)
000001 001,01 001,13 001,02 001,05 +1.77738516 +.0023832 +1.423995 +.0019094 +764.9011 +801.174400 +185.0000 20200326_122716 CH 01 GN 1   138
0                               8                         11                            13 + SP    14 + SP    15 + SP
"""
