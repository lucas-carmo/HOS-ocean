# About this fork
This fork implements the changes from “Implementation of Two New Spectral Input Options in HOS-Ocean – Part I” (available at https://apps.dtic.mil/sti/pdfs/AD1111149.pdf) regarding the use of WaveWatch III data.


# HOS-ocean 

High-Order Spectral method for oceanic simulations

[![Travis][buildstatus_image_travis]][travisci]
[![Appveyor][buildstatus_image_appveyor]][appveyorci]
[![Codecov][codecov_image]][codecovci]

This readme file describes the different cases that might be computed with the periodic HOS model
and gives instructions to set the numerical parameters `n1` to `p2`

Setting the value of integers `n1`, `n2`, `M`, `p1` and `p2` in
[`variables_3D.f90`](sources/HOS/variables_3D.f90)

## 2D simulation

For a 2D simulation, compile with `n2=1` `AND` `p2=1` to adjust the memory allocation to minimum

If partial dealiasing is used, compile with `p1` set to maximal required value
(total dealiasing is obtained with `p1=M`
but it can be reduced if `p1` is further set to a value below `M`)

## 3D simulation

For a 3D simulation, compile with `n2\=1` `AND` `p2` set to required value

If partial dealiasing is used in x-direction,
compile with `p1` set to maximal required value
(total dealiasing is obtained with `p1=M`
but it can be reduced if `p1` is further set to a value below `M`)

If partial dealiasing is used in y-direction,
compile with `p2` set to maximal required value
(total dealiasing is obtained with `p2=M`
but it can be reduced if `p2` is further set to a value below `M`)

* `input_HOS.dat` will have to be attached to run this program *

Setting the value of integer `i_case` in `input_HOS.dat`

- `i_case = 1` : starts from rest

- `i_case = 2` and `21` : starts with a natural mode

   - `2`  - progressive wave: potential on free surface accordingly to linear theory
   - `21` - stationary wave: no velocity at initial time
   The number of the mode, its amplitude and phase have to be chosen
   in the module [`initial_condition.f90`](sources/HOS/initial_condition.f90).

- `i_case = 3` and `31` and `32` : Irregular directional sea-state from spectrum specified :

    - `3`  - input file parameters
    - `31` - WAVEWATCH III® spectrum file
    - `32` - previous HOS-ocean simulation

- `i_case = 8...` : Nonlinear regular wave (from Rienecker and Fenton).
   This means that `xlen` and `ylen` are interpreted as integer and
   represent the number of wavelength in x- and y- direction
   respectively.

    - `i_case = 81` : `steepness 0.1`
    - `i_case = 82` : `steepness 0.2`
    - `i_case = 83` : `steepness 0.3`
    - `i_case = 84` : `steepness 0.4`
    - `i_case = 89` : `steepness 0.09`

Further details about input file, output of the code...
may be find at the Wiki page of
HOS-ocean project: https://github.com/LHEEA/HOS-ocean/wiki


[buildstatus_image_travis]: https://travis-ci.org/LHEEA/HOS-ocean.svg?branch=master
[travisci]: https://travis-ci.org/LHEEA/HOS-ocean

[buildstatus_image_appveyor]: https://ci.appveyor.com/api/projects/status/kgkw3p6ygj47j2oj?svg=true
[appveyorci]: https://ci.appveyor.com/project/gducrozet/hos-ocean

[codecov_image]: https://codecov.io/gh/LHEEA/HOS-ocean/branch/master/graph/badge.svg
[codecovci]: https://codecov.io/gh/LHEEA/HOS-ocean
