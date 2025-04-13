cmake_minimum_required(VERSION 4.0)
project(cmake_external_lib_template)

set(CMAKE_CXX_STANDARD 20)

add_executable(cmake_external_lib_template main.cpp)
configure_file(config.yaml config.yaml COPYONLY)

#find_package(yaml-cpp QUIET)
#if (NOT yaml-cpp_FOUND)
#    message("yaml-cpp not found, cloning git repository")
#    find_package(Git)
#    if (NOT Git_FOUND)
#        message(FATAL_ERROR "Git not found, can't initialize!")
#    endif()
#    execute_process(
#            COMMAND ${GIT_EXECUTABLE} clone
#            https://github.com/jbeder/yaml-cpp.git
#            WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/extern
#    )
#    add_subdirectory(extern/yaml-cpp)
#endif()
include(FetchContent)
FetchContent_Declare(external-yaml-cpp
    GIT_REPOSITORY  https://github.com/jbeder/yaml-cpp.git
    GIT_TAG         yaml-cpp-0.6.3
)
FetchContent_MakeAvailable(external-yaml-cpp)
target_link_libraries(cmake_external_lib_template PRIVATE yaml-cpp)

include(CMakePrintHelpers)
cmake_print_properties(TARGETS yaml-cpp PROPERTIES TYPE SOURCE_DIR)