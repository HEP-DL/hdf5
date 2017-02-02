# hdf5

FNAL UPS Produce Source for HDF5 support


> Disclaimer: The underlying source code is a redistribution of a product of the [HDF Group](https://support.hdfgroup.org/HDF5/). It had been modified to function within the UPS framework on 2/1/2017. The source code and binary are protected by the unmodified copyright notice herein: [https://github.com/kwierman/hdf5/blob/master/hdf5/COPYING](https://github.com/kwierman/hdf5/blob/master/hdf5/COPYING).


## Usage

In the top level CMake File:

~~~ cmake
find_ups_product( hdf5 v01_00_00 )
cet_find_library( hdf5 NAMES hdf5_debug PATHS ${HDF5_SEARCH_PATH}/lib NO_DEFAULT_PATH  )
cet_find_library( hdf5_cpp NAMES hdf5_cpp_debug PATHS ${HDF5_SEARCH_PATH}/lib NO_DEFAULT_PATH  )
cet_find_library( hdf5_hl NAMES hdf5_hl_debug PATHS ${HDF5_SEARCH_PATH}/lib NO_DEFAULT_PATH  )
cet_find_library( hdf5_tools NAMES hdf5_tools_debug PATHS ${HDF5_SEARCH_PATH}/lib NO_DEFAULT_PATH  )
set(HDF5_LIBRARIES ${hdf5} ${hdf5_cpp} ${hdf5_hl} ${hdf5_tools} )
~~~

Now, in the linker list for a given target:

~~~ cmake
cet_build_plugin( my_plugin module
  ${HDF5_LIBRARIES}
)
~~~

This can be implemented in the CETBuildTools interface. However, no documenation exists and thus I'm not going to bother wasting time trying to hack Cet tools.