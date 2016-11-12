cmake_minimum_required(VERSION 2.6)

# Enable C++11 support
set (CMAKE_CXX_STANDARD 11)
add_definitions(-std=c++11)

project(crts)
set (crts_version_major 2)
set (crts_version_minor 0.0)

#make sure our local CMake Modules path comes first
list(INSERT CMAKE_MODULE_PATH 0 ${CMAKE_SOURCE_DIR}/cmake)

# uninstall target
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake_uninstall.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake"
    IMMEDIATE @ONLY)

add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake)


# External dependencies
find_package(Boost COMPONENTS system)
find_package (Threads REQUIRED)
find_package (UHD REQUIRED)
find_package(Liquid REQUIRED)
find_package(Config REQUIRED)

include_directories(
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/src
    ${CMAKE_BINARY_DIR}/include
    ${CMAKE_BINARY_DIR}/src
    ${Boost_INCLUDE_DIRS}
    ${UHD_INCLUDE_DIRS}
    ${LIQUID_INCLUDES}
    ${CONFIG_INCLUDE_DIR}
)

link_directories(
    ${Boost_LIBRARY_DIRS}
)

add_subdirectory(src)
add_subdirectory(cognitive_engines)
add_subdirectory(scenario_controllers)