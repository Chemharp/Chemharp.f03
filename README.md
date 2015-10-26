# Fortran binding for the chemfiles library

[![Build Status](https://travis-ci.org/chemfiles/chemfiles.f03.svg?branch=master)](https://travis-ci.org/chemfiles/chemfiles.f03)
[![codecov.io](http://codecov.io/github/chemfiles/chemfiles.f03/coverage.svg?branch=master)](http://codecov.io/github/chemfiles/chemfiles.f03?branch=master)
[![Documentation Status](https://readthedocs.org/projects/chemfiles-fortran/badge/?version=latest)](http://chemfiles.readthedocs.org/projects/fortran/en/latest/)

This repository contains the fortran 2003 binding to the
[chemfiles](https://github.com/chemfiles/chemfiles) library. The
[documentation](http://chemfiles.readthedocs.org/projects/fortran/en/latest/) contains
the installation instructions.

## Usage example

Here is a simple example of how the usage feels in Fortran:

```fortran
program example
    use chemfiles
    use iso_fortran_env, only: int64, real32

    implicit none
    type(chfl_trajectory) :: trajectory
    type(chfl_frame) :: frame
    integer(int64) :: natoms
    real(real32), dimension(:, :), allocatable :: positions
    integer :: status

    call trajectory%open("filename.xyz", "r", status=status)
    if status /= 0 stop "Error while opening file"
    call frame%init(0)

    call file%read(frame, status=status)
    if status /= 0 stop "Error while reading file"

    call frame%atoms_count(natoms)
    write(*, *) "There are ", natoms, "atoms in the frame"

    allocate(positions(3, natoms))

    call frame%positions(positions, natoms)

    ! Do awesome things with the positions here !

    call frame%free()
    call trajectory%close()
    deallocate(positions)
}
```

You can find more examples in the `examples` directory.

## Bug reports, feature requests

Please report any bug you find and any feature you may want as a [github issue](https://github.com/chemfiles/chemfiles.f03/issues/new).
