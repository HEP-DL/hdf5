cmake_minimum_required (VERSION 2.8)

project(hdf5)

# cetbuildtools contains our cmake modules
SET ( CETBUILDTOOLS_VERSION $ENV{CETBUILDTOOLS_VERSION} )
IF (NOT CETBUILDTOOLS_VERSION)
    MESSAGE (FATAL_ERROR "ERROR: setup cetbuildtools to get the cmake modules")
ENDIF()

set(CMAKE_MODULE_PATH $ENV{ART_DIR}/Modules
		      $ENV{CETBUILDTOOLS_DIR}/Modules
		      ${CMAKE_MODULE_PATH})

include(CetCMakeEnv)
include(CetCMakeUtils)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  EXTRA_FLAGS -pedantic -Wno-unused-local-typedefs
)

cet_report_compiler_flags()

# these are minimum required versions, not the actual product versions
find_ups_product( zlib v01_02_11 )
find_ups_product( cetbuildtools v4_14_01 )

# ADD SOURCE CODE SUBDIRECTORIES HERE

set(PERL_COMMAND "perl -w")
set(HDF5_SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/hdf5)
set(HDF5_CONFIG_PATH ${CMAKE_INSTALL_PREFIX}/${flavorqual_dir}/lib/hdf5/cmake/hdf5Config.cmake)
SET(HDF5_ENABLE_Z_LIB_SUPPORT ON CACHE BOOL "Enable Zlib Filters")
SET(BUILD_TESTING OFF CACHE BOOL "Build HDF5 Unit Testing")
SET(HDF5_BUILD_EXAMPLES  OFF CACHE BOOL "Build HDF5 Library Examples")
set(HDF5_LIB_DEPENDENCIES ${zlib} )
#set(H5_ZLIB_HEADER "zlib.h")
#set(ZLIB_INCLUDE_DIRS "${ZLIB_INC}")
set(ZLIB_LIBRARIES ${zlib} )
set(HDF5_EXTERNALLY_CONFIGURED ON)
SET(HDF5_GENERATE_HEADERS ON CACHE BOOL "Regenerate HDF5 Headers")
set(HDF5_INSTALL_CMAKE_DIR ${CMAKE_INSTALL_PREFIX}/${flavorqual_dir}/lib/hdf5/cmake)
set(HDF5_INSTALL_LIB_DIR ${CMAKE_INSTALL_PREFIX}/${flavorqual_dir}/lib)
set(HDF5_INSTALL_BIN_DIR ${CMAKE_INSTALL_PREFIX}/${flavorqual_dir}/bin)
set(HDF5_INSTALL_INCLUDE_DIR ${CMAKE_INSTALL_PREFIX}/${flavorqual_dir}/include)
set(HDF5_INSTALL_DATA_DIR ${CMAKE_INSTALL_PREFIX}/${flavorqual_dir}/share)
set(HDF5_INC
  ${CMAKE_SOURCE_PREFIX}/hdf5/src
  ${CMAKE_SOURCE_PREFIX}/hdf5/c++/src
  ${CMAKE_SOURCE_PREFIX}/hdf5/hl/src
  ${CMAKE_SOURCE_PREFIX}/hdf5/hl/c++/src
FORCE PARENT_SCOPE)
add_subdirectory(hdf5)
# Hack to get this to work with mrb correctly.
cet_add_to_library_list( hdf5 )
cet_add_to_library_list( hdf5_cpp )
cet_add_to_library_list( hdf5_hl )
cet_add_to_library_list( hdf5_tools )
include_directories( ${HDF5_INC})

# tests
add_subdirectory(test)

# ups - table and config files
add_subdirectory(ups)

# packaging utility
include(UseCPack)


