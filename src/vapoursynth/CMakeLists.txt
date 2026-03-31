

include_directories(${PROJECT_SOURCE_DIR}/src/vapoursynth/
    ${PROJECT_SOURCE_DIR}/include/
    ${INCLUDE_DIR})

set(all_files
    vapoursource4.cpp
    vapoursynth4.cpp)

add_library(VAPOURSYNTH OBJECT ${all_files})