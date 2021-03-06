cmake_minimum_required (VERSION 2.8.4)
project (p4benchmark)

include_directories(include)

set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wno-unused-parameter -ggdb -g")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

find_package(PCAP REQUIRED)
find_package(Threads REQUIRED)

message (STATUS "This is CMAKE_CXX_FLAGS " ${CMAKE_CXX_FLAGS})

set (SRC src/capture.c src/parser.c src/main.c)

add_executable (p4benchmark ${SRC})
target_link_libraries (p4benchmark ${PCAP_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
set_target_properties (p4benchmark PROPERTIES COMPILE_FLAGS ${CMAKE_CXX_FLAGS})


add_executable (sendb2b src/capture.c src/parser.c src/close_loop.c)
target_link_libraries (sendb2b ${PCAP_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
set_target_properties (sendb2b PROPERTIES COMPILE_FLAGS ${CMAKE_CXX_FLAGS})
