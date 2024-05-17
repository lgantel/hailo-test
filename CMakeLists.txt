cmake_minimum_required(VERSION 3.0.0)

# Set firmware version
add_definitions( -DFIRMWARE_VERSION_MAJOR=0 )
add_definitions( -DFIRMWARE_VERSION_MINOR=1 )
add_definitions( -DFIRMWARE_VERSION_REVISION=0 )
if(HAILO_BUILD_SERVICE)
    add_definitions( -DHAILO_SUPPORT_MULTI_PROCESS )
endif()

set(HAILO_TEST_CPP_FILES
    hailo-test.cpp
)

add_executable(hailo-test
    ${HAILO_TEST_CPP_FILES}
)

set_property(TARGET hailo-test PROPERTY CXX_STANDARD 14)

target_link_libraries(hailortcli
    libhailort
)

target_include_directories(hailo-test
    PRIVATE
    ${CMAKE_CURRENT_BINARY_DIR}
)

install(TARGETS hailo-test
   RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
   CONFIGURATIONS Release
)

