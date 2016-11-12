file(GLOB_RECURSE sc_controller_files
    "*.cpp"
)

add_library(crts-scenario-controllers SHARED ${sc_controller_files})
target_link_libraries(crts-scenario-controllers 
    ${Boost_LIBRARIES}
)