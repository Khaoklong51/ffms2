cmake_minimum_required(VERSION 3.10)


project(ffms2 VERSION 5.1.1 LANGUAGES C CXX)
include(GNUInstallDirs)

set(CMAKE_CXX_STANDARD 11)

option(BUILD_SHARED_LIBS "Build shared libraries (DLLs)." ON)

if("${CMAKE_CURRENT_SOURCE_DIR}" STREQUAL "${CMAKE_CURRENT_BINARY_DIR}")
    message(WARNING "Building in-source is highly not recommended\n"
                    "Please use the Build folder or create your own.")
endif()

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    set(CMAKE_BUILD_TYPE Release)
endif()

option(ENABLE_AVISYNTH "Enable AviSynth+ plugin" OFF)
option(AVISYNTH_INCLUDE_DIRECTORIES "Set Avisynth include directories" "")
option(ENABLE_INDEXER "Enable building of indexer executables" OFF)

if(CMAKE_BUILD_TYPE MATCHES Debug)
    if(MSVC)
        add_compile_options(/O0)
    else()
        add_compile_options(-O0 -g)
    endif()
elseif(CMAKE_BUILD_TYPE MATCHES Debug)
    if(MSVC)
        add_compile_options(/O2)
    else()
        add_compile_options(-O3)
    endif()
endif()

if(NOT MSVC)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra")
endif()

if(CYGWIN AND BUILD_SHARED_LIBS)
    message(FATAL_ERROR "Shared build is broken on cygwin. Please use -DBUILD_SHARED_LIBS=OFF")
endif()

add_subdirectory(src)

if(UNIX AND NOT APPLE)
    target_link_libraries(ffms2 PRIVATE rt)
endif()

set_target_properties(ffms2 PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
)

if(BUILD_SHARED_LIBS AND LINUX)
    target_link_options(ffms2 PRIVATE "-Wl,-Bsymbolic")
endif()

if(UNIX OR MINGW)
    set_target_properties(ffms2 PROPERTIES LINK_FLAGS "-Wl,-no-undefined")
endif()