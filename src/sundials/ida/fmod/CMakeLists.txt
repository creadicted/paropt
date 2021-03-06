# ---------------------------------------------------------------
# Programmer(s): Cody J. Balos @ LLNL
# ---------------------------------------------------------------
# SUNDIALS Copyright Start
# Copyright (c) 2002-2020, Lawrence Livermore National Security
# and Southern Methodist University.
# All rights reserved.
#
# See the top-level LICENSE and NOTICE files for details.
#
# SPDX-License-Identifier: BSD-3-Clause
# SUNDIALS Copyright End
# ---------------------------------------------------------------
# CMakeLists.txt file for the F2003 IDA object library
# ---------------------------------------------------------------

set(ida_SOURCES fida_mod.f90 fida_mod.c)

if(BUILD_STATIC_LIBS)
  sundials_add_f2003_interface_library(sundials_fida_mod_static STATIC
    ${ida_SOURCES}
    $<TARGET_OBJECTS:sundials_fnvecserial_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunmatrixband_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunmatrixdense_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunmatrixsparse_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolband_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsoldense_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolpcg_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolspbcgs_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolspfgmr_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolspgmr_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolsptfqmr_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunnonlinsolfixedpoint_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fsunnonlinsolnewton_mod_static_obj>
    $<TARGET_OBJECTS:sundials_fgeneric_static_obj>
  )

  # include the directoy where the .mod files reside
  target_include_directories(sundials_fida_mod_static
    PUBLIC
      $<BUILD_INTERFACE:${CMAKE_Fortran_MODULE_DIRECTORY}_STATIC>
      $<INSTALL_INTERFACE:${Fortran_INSTALL_MODDIR}>
  )

  # Set the library name and make sure it is not deleted
  set_target_properties(sundials_fida_mod_static
    PROPERTIES OUTPUT_NAME sundials_fida_mod CLEAN_DIRECT_OUTPUT 1)

  # install the library
  install(TARGETS sundials_fida_mod_static DESTINATION ${CMAKE_INSTALL_LIBDIR})

  # install the ida mod file from here since it won't go into the
  # top level fortran mod file directory
  install(FILES ${CMAKE_Fortran_MODULE_DIRECTORY}_STATIC/fida_mod.mod
          DESTINATION ${Fortran_INSTALL_MODDIR})
endif()

if(BUILD_SHARED_LIBS)
  sundials_add_f2003_interface_library(sundials_fida_mod_shared SHARED
    ${ida_SOURCES}
    $<TARGET_OBJECTS:sundials_fnvecserial_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunmatrixband_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunmatrixdense_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunmatrixsparse_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolband_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsoldense_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolpcg_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolspbcgs_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolspfgmr_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolspgmr_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunlinsolsptfqmr_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunnonlinsolfixedpoint_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fsunnonlinsolnewton_mod_shared_obj>
    $<TARGET_OBJECTS:sundials_fgeneric_shared_obj>
  )

  # include the directoy where the .mod files reside
  target_include_directories(sundials_fida_mod_shared
    PUBLIC
      $<BUILD_INTERFACE:${CMAKE_Fortran_MODULE_DIRECTORY}_SHARED>
      $<INSTALL_INTERFACE:${Fortran_INSTALL_MODDIR}>
  )

  # Set the library name and make sure it is not deleted
  set_target_properties(sundials_fida_mod_shared PROPERTIES
                        OUTPUT_NAME sundials_fida_mod
                        CLEAN_DIRECT_OUTPUT 1
                        VERSION ${idalib_VERSION}
                        SOVERSION ${idalib_SOVERSION})

  # install the library
  install(TARGETS sundials_fida_mod_shared DESTINATION ${CMAKE_INSTALL_LIBDIR})

  # install the ida mod file from here since it won't go into the
  # top level fortran mod file directory
  install(FILES ${CMAKE_Fortran_MODULE_DIRECTORY}_SHARED/fida_mod.mod
          DESTINATION ${Fortran_INSTALL_MODDIR})
endif()

message(STATUS "Added IDA F2003 interface")
