



include_directories(${PROJECT_SOURCE_DIR}/src/core/
    ${PROJECT_SOURCE_DIR}/include/
    ${INCLUDE_DIR})

set(all_files
    audiosource.cpp
    ffms.cpp
    filehandle.cpp
    indexing.cpp
    track.cpp
    utils.cpp
    videosource.cpp
    videoutils.cpp
    zipfile.cpp)

add_library(CORE OBJECT ${all_files})