cmake_minimum_required(VERSION 3.23.1)

project(vdbvolume)

# OpenVDB
find_package(OpenVDB REQUIRED)

# TBB
find_package(TBB REQUIRED)

# Mitsuba & Dependencies
set (MITSUBA_DIR "/home/kr2/Misc/mitsuba_render/mitsuba/")
set(MITSUBA_INCLUDE_DIR "${MITSUBA_DIR}/include" )
set(MITSUBA_LIBRARY_DIR "${MITSUBA_DIR}/dist/" )
set(MITSUBA_DEPENDENCIES_INCLUDE_DIR "${MITSUBA_DIR}/dependencies/include" )
set(MITSUBA_DEPENDENCIES_LIBRARY_DIR "${MITSUBA_DIR}/dependencies/lib" )

include_directories(${MITSUBA_INCLUDE_DIR} ${MITSUBA_DEPENDENCIES_INCLUDE_DIR})
link_directories(${MITSUBA_LIBRARY_DIR} ${MITSUBA_DEPENDENCIES_LIBRARY_DIR})

add_definitions(-DSINGLE_PRECISION -DSPECTRUM_SAMPLES=3)
add_library(vdbvolume SHARED vdbvolume.cpp vdbvolume.h)
target_link_libraries(vdbvolume openvdb TBB::tbb mitsuba-core mitsuba-render)
