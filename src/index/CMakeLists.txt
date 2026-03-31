

include_directories(${PROJECT_SOURCE_DIR}/include/
    ${PROJECT_SOURCE_DIR}/src/index/
    ${INCLUDE_DIR})

set(all_files
    ffmsindex.cpp)

add_executable(ffmsindex
    ${all_files})

target_link_libraries(ffmsindex PRIVATE ffms2 "${LIBRARIES}")
target_link_directories(ffmsindex PRIVATE "${LIBRARIES_DIRS}")
target_compile_options(ffmsindex PRIVATE "${COMPILE_OPTIONS}")
target_include_directories(ffmsindex PRIVATE "${INCLUDE_DIR}")

install(TARGETS ffmsindex RUNTIME COMPONENT Runtime DESTINATION ${CMAKE_INSTALL_BINDIR})