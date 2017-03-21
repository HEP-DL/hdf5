# hdf5

FNAL UPS Produce Source for HDF5 support


> Disclaimer: The underlying source code is a redistribution of a product of the [HDF Group](https://support.hdfgroup.org/HDF5/). It had been modified to function within the UPS framework on 2/1/2017. The source code and binary are protected by the unmodified copyright notice herein: [https://github.com/kwierman/hdf5/blob/master/hdf5/COPYING](https://github.com/kwierman/hdf5/blob/master/hdf5/COPYING).


## Usage

For using this product with other UPS products, first ensure that the library can be found with:

~~~ bash
ups list -aK+ hdf5
~~~

On the Fermi grid, there is an existing product called `hdf5`. This lacks the C++ binding and high level tools utilized by [kevlar](github.com/HEP-DL/kevlar). *DO NOT USE THESE TOOLS*.


In the top level CMake File:

~~~ cmake
find_ups_product( hdf5 v01_00_00 )
~~~

And in the `ups/product_deps` file:

~~~ txt
# under product version
hdf5             v01_00_00
#under dep table
qualifier uboonecode    hdf5      boost     gcc  notes
e10:debug e10:debug e10:debug e10:debug -nq-
e10:opt   e10:opt   e10:opt   e10:opt   -nq-
e10:prof  e10:prof  e10:prof  e10:prof  -nq-
~~~

Now, in the CMake File for a given target:

~~~ cmake
include_directories( $ENV{HDF5_INC} )
cet_build_plugin( my_plugin module
  ${hdf5_cpp}
)
~~~


>
