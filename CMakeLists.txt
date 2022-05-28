cmake_minimum_required(VERSION 3.21)
project(limetrx)

set(CMAKE_CXX_STANDARD 17)

add_executable(limetrx main.cpp)

########################################################################
# Find LimeSuite
########################################################################
MESSAGE(STATUS "Configuring LimeSuite C++ Libraries...")
find_path(LIMESUITE_INCLUDE_DIRS
        NAMES LimeSuite.h
        HINTS ${PC_LIMESUITE_INCLUDEDIR}/lime
        PATHS ${LIMESUITE_PKG_INCLUDE_DIRS}
        /usr/include/lime
        /usr/local/include/lime
        )
find_library(LIMESUITE_LIB
        NAMES LimeSuite limesuite
        HINTS ${PC_LIMESUITE_LIBDIR}
        PATHS ${LIMESDR_PKG_LIBRARY_DIRS}
        /usr/lib
        /usr/local/lib
        )

message(STATUS "Found LimeSuite: ${LIMESUITE_INCLUDE_DIRS}, ${LIMESUITE_LIB}")

include_directories(${LIMESUITE_INCLUDE_DIRS})
target_link_libraries(limetrx ${LIMESUITE_LIB})
