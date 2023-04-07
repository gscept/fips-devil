#
# project: fips-devil
#
cmake_minimum_required(VERSION 3.21)


if (NOT FIPS_IMPORT)
# include the fips main cmake file
get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
include("${FIPS_ROOT_DIR}/cmake/fips.cmake")

    project(fips-devil) 

ADD_DEFINITIONS(-DIL_NO_EXR)
    fips_setup()
endif()

OPTION(BUILD_DEVIL_ILU "Build DevIL with ILU" OFF)
OPTION(BUILD_DEVIL_ILUT "Build DevIL with ILUT" OFF)

fips_begin_lib(DevIL)
SET(DEVIL_BUILD_SHARED_LIBS OFF)
ADD_DEFINITIONS(-DIL_STATIC_LIB -DJPEGSTATIC)
fips_deps(libpng libjpeg)
target_include_directories(DevIL PUBLIC DevIL/DevIL/src-IL/include/)

if (BUILD_DEVIL_ILU)
    target_include_directories(DevIL PUBLIC DevIL/DevIL/src-ILU/include/)
endif()
if (BUILD_DEVIL_ILUT)
    target_include_directories(DevIL PUBLIC DevIL/DevIL/src-ILUT/include/)
endif()

fips_src(DevIL/DevIL/include/IL/ NO_RECURSE)
fips_src(DevIL/DevIL/src-IL/src/ NO_RECURSE)
fips_src(DevIL/DevIL/src-IL/include/ NO_RECURSE)

if (BUILD_DEVIL_ILUT)
    fips_src(DevIL/DevIL/src-ILUT/src/ NO_RECURSE)
    fips_src(DevIL/DevIL/src-ILUT/include/ NO_RECURSE)
endif()
if (BUILD_DEVIL_ILU)
    fips_src(DevIL/DevIL/src-ILU/src/ NO_RECURSE)
    fips_src(DevIL/DevIL/src-ILU/include/ NO_RECURSE)
endif()

fips_end_lib()


