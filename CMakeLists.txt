cmake_minimum_required(VERSION 3.12)

# Project
project(computer_vision)
set(CMAKE_CXX_STANDARD 17)

# Dependencies
if(EXISTS ${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
    conan_basic_setup()
else()
    message(WARNING "The file conanbuildinfo.cmake doesn't exist, you have to run conan install first")
endif()

enable_testing()

find_package(OpenCV REQUIRED)


# Library
#set(LIBRARY_HEADERS
#        include/beastmode/handlers/route_handler.hpp
#        include/beastmode/handlers/header_handler.hpp
#        include/beastmode/handlers/string_handler.hpp
#        include/beastmode/route.hpp
#        include/beastmode/send_lambda.hpp
#        include/beastmode/internal/namespace.hpp
#        include/beastmode/server.hpp
#        include/beastmode/internal/error.hpp
#        include/beastmode/internal/macro.h
#        include/beastmode/internal/unmacro.h)
#set(LIBRARY_SOURCES
#        src/server.cpp
#        src/route.cpp
#        src/handlers/route_handler.cpp
#        src/error.cpp)
#
#add_library(beastmode STATIC ${LIBRARY_HEADERS} ${LIBRARY_SOURCES})
#target_include_directories(beastmode PUBLIC include)
#target_compile_definitions(beastmode PUBLIC BOOST_COROUTINES_NO_DEPRECATION_WARNING=1 BOOST_BEAST_USE_STD_STRING_VIEW=1)
#target_link_libraries(beastmode PUBLIC ${CONAN_LIBS})

# Executable
set(EXE_HEADERS
        include/tracked_object.h include/recorder.h)
set(EXE_SOURCES
        src/tracked_object.cpp src/recorder.cpp)

add_executable(computer_vision src/main.cpp ${EXE_HEADERS} ${EXE_SOURCES})
target_include_directories(computer_vision PRIVATE include)
target_link_libraries(computer_vision PUBLIC
        ${CONAN_LIBS}
        ${OpenCV_LIBS})

# Test Exectuable
#set(TEST_HEADERS
#        test/tools/client.hpp)
set(TEST_SOURCES
        test/testmain.cpp
        test/test.cpp)

add_executable(test_computer_vision ${TEST_HEADERS} ${TEST_SOURCES} ${EXE_HEADERS} ${EXE_SOURCES})
target_include_directories(test_computer_vision PRIVATE include)
target_link_libraries(test_computer_vision PUBLIC
        ${CONAN_LIBS}
        ${OpenCV_LIBS})
