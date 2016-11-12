file(GLOB_RECURSE ce_sources
    "*.cpp"
)

add_library(crts-cognitive-engines SHARED ${ce_sources})
target_link_libraries(crts-cognitive-engines 
    ${Boost_LIBRARIES}
)