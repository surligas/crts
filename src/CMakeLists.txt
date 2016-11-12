include_directories(${Boost_INCLUDE_DIR}
    ${UHD_INCLUDE_DIRS}
    ${LIQUID_INCLUDES}
    ${CONFIG_INCLUDE_DIR}
)

link_directories(${Boost_LIBRARY_DIRS})

list(APPEND crts_core_sources
    cognitive_engine.cpp
    extensible_cognitive_radio.cpp
    crts.cpp
    interferer.cpp
    scenario_controller.cpp
    timer.cc
    tun.cpp
)



add_library(crts-core SHARED ${crts_core_sources})
target_link_libraries(crts-core 
    ${Boost_LIBRARIES}
    ${CMAKE_THREAD_LIBS_INIT}
    ${UHD_LIBRARIES}
    ${LIQUID_LIBRARIES}
    ${CONFIG_LIBRARY}
    crts-cognitive-engines
    crts-scenario-controllers 
)


########################################################################
# Install built library files
########################################################################
install(TARGETS crts-core
    LIBRARY DESTINATION lib${LIB_SUFFIX} # .so/.dylib file
    ARCHIVE DESTINATION lib${LIB_SUFFIX} # .lib file
    RUNTIME DESTINATION bin              # .dll file
)

########################################################################
# Handle the executables
########################################################################
add_executable(config_cognitive_engines config_cognitive_engines.cpp)
add_executable(config_scenario_controllers config_scenario_controllers.cpp)
add_executable(convert_logs_bin_to_octave convert_logs_bin_to_octave.cpp)
add_executable(crts_cognitive_radio crts_cognitive_radio.cpp)
add_executable(crts_controller crts_controller.cpp)
add_executable(crts_interferer crts_interferer.cpp)

set(CRTS_EXECUTABLES
    config_cognitive_engines
    config_scenario_controllers
    convert_logs_bin_to_octave
    crts_cognitive_radio
    crts_controller
    crts_interferer
)

target_link_libraries(config_cognitive_engines crts-core)
target_link_libraries(config_scenario_controllers crts-core)
target_link_libraries(convert_logs_bin_to_octave crts-core)
target_link_libraries(crts_cognitive_radio crts-core)
target_link_libraries(crts_controller crts-core)
target_link_libraries(crts_interferer crts-core)

install(TARGETS ${CRTS_EXECUTABLES} DESTINATION bin)
