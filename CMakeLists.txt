cmake_minimum_required(VERSION 3.10)

if (${CMAKE_VERSION} VERSION_GREATER_EQUAL "3.12.0")
  #  Policy CMP0075 is not set: Include file check macros honor
  #  CMAKE_REQUIRED_LIBRARIES.  Run "cmake --help-policy CMP0075" for policy
  #  details.  Use the cmake_policy command to set the policy and suppress this
  #  warning.
  #
  #  CMAKE_REQUIRED_LIBRARIES is set to:
  #
  #    ...
  #
  #  For compatibility with CMake 3.11 and below this check is ignoring it.
  cmake_policy(SET CMP0075 NEW) # cmake >= 3.12
endif()

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
