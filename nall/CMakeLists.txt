set(CMAKE_VERBOSE_MAKEFILE True)
cmake_minimum_required(VERSION 3.15)
cmake_policy(VERSION 3.15)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

set(NALL_VERSION "0.110.1")
set(NALL_VERSION_MAJOR "0")
set(NALL_ROOT ${CMAKE_CURRENT_SOURCE_DIR})
set(NALL_SOURCE_ROOT ${NALL_ROOT}/)
set(NALL_INCLUDE_ROOT ${NALL_ROOT}/)

project(nall
    LANGUAGES CXX
    VERSION ${NALL_VERSION}
    #    SOVERSION ${NALL_VERSION_MAJOR}
    DESCRIPTION "BYUU- nall Library"
)

# Only do these if this is the main project, and not if it is included through add_subdirectory
if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    # Optionally set things like CMAKE_CXX_STANDARD, CMAKE_POSITION_INDEPENDENT_CODE here
    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    set(CMAKE_POSITION_INDEPENDENT_CODE ON)

    # Let's ensure -std=c++xx instead of -std=g++xx
    set(CMAKE_CXX_EXTENSIONS OFF)

    # Let's nicely support folders in IDE's
    set_property(GLOBAL PROPERTY USE_FOLDERS ON)


    # Docs only available if this is the main app
    find_package(Doxygen)
    if(Doxygen_FOUND)
        add_subdirectory(docs)
    else()
        message(STATUS "Doxygen not found, not building docs")
    endif()
endif()