# require cmake 2.8.0 for findCUDA.cmake
CMAKE_MINIMUM_REQUIRED(VERSION 2.8.0 FATAL_ERROR)

##################
project("nsight_gtc2015_tuto")
# The version number.
set (nsight_gtc2015_VERSION_MAJOR 0)
set (nsight_gtc2015_VERSION_MINOR 0)
##################

###################################################
# DEBUG or RELEASE ? DEBUG is the default behavior
###################################################
if(NOT CMAKE_BUILD_TYPE)
  message(STATUS "Setting build type to 'Debug' as none was specified.")
  set(CMAKE_BUILD_TYPE "Debug")
endif()

# Set default install path to build
#if (CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
#  set (CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}" CACHE PATH "default install path" FORCE )
#endif()

######################################################
# allow cmake to use custom modules (e.g. Find???)
######################################################
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

find_package(CUDA REQUIRED)
include(FindCUDA)
# Make the include path visible to all targets
INCLUDE_DIRECTORIES (
  ${nsight_gtc2015_SOURCE_DIR}
  )

set( CMAKE_C_FLAGS "-Wall ${CMAKE_C_FLAGS}" )
set( CMAKE_CXX_FLAGS "-Wall ${CMAKE_CXX_FLAGS}" )

#############
# GPU BUILD
#############
# lineinfo is usefull for debugging
list(APPEND CUDA_NVCC_FLAGS --compiler-options -fno-strict-aliasing -lineinfo)
#list(APPEND CUDA_NVCC_FLAGS --ptxas-options=-v)
list(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_20,code=sm_20)
list(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_30,code=sm_30)
list(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_35,code=sm_35)
#list(APPEND CUDA_NVCC_FLAGS -gencode arch=compute_37,code=sm_37)

# nsight_gtc2015 targets
cuda_add_executable ( nsight-gtc2015-step-00
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x00
  )
cuda_add_executable ( nsight-gtc2015-step-1a
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x1a
  )
cuda_add_executable ( nsight-gtc2015-step-1b
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x1b
  )
cuda_add_executable ( nsight-gtc2015-step-20
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x20
  )
cuda_add_executable ( nsight-gtc2015-step-30
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x30
  )
cuda_add_executable ( nsight-gtc2015-step-40
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x40
  )
cuda_add_executable ( nsight-gtc2015-step-50
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x50
  )
cuda_add_executable ( nsight-gtc2015-step-60
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x60
  )
cuda_add_executable ( nsight-gtc2015-step-70
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x70
  )
cuda_add_executable ( nsight-gtc2015-step-80
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x80
  )
cuda_add_executable ( nsight-gtc2015-step-90
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x90
  )
cuda_add_executable ( nsight-gtc2015-step-91
  nsight-gtc2015.cu
  OPTIONS -DOPTIMIZATION_STEP=0x91 --use_fast_math
  )

