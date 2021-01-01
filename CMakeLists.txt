cmake_minimum_required(VERSION 3.12)
project(libev C)
include(cmake/configure.cmake)

configure_file(config.h.cmake config.h)

set(EV_SRC 
  ev.c
  event.c
)

if (WIN32) 
  list(APPEND EV_LIBS Ws2_32)
endif ()

add_library(ev STATIC ${EV_SRC})
target_include_directories(ev PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries (ev ${EV_LIBS})
