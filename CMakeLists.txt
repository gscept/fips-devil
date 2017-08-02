#
# project: fips-devil
#
cmake_minimum_required(VERSION 2.8)

# include the fips main cmake file
get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
include("${FIPS_ROOT_DIR}/cmake/fips.cmake")

fips_setup()
fips_project(fips-devil)
fips_begin_lib(DevIL)
fips_include_directories(DevIL/DevIL/src-IL/include/)
fips_include_directories(DevIL/DevIL/src-ILU/include/)
fips_include_directories(DevIL/DevIL/src-ILUT/include/)
fips_src(DevIL/DevIL/src-IL/src/ NO_RECURSE)
fips_src(DevIL/DevIL/src-ILUT/src/ NO_RECURSE)
fips_src(DevIL/DevIL/src-ILU/src/ NO_RECURSE)
fips_end_lib()
#fips_add_subdirectory(DevIL/DevIL)
fips_finish()


