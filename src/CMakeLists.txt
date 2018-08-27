cmake_minimum_required(VERSION 3.7)

project(bitshuffle
  VERSION 0.3.4
  #DESCRIPTION "Filter for improving compression of typed binary data."
  #HOMEPAGE_URL https://github.com/kiyo-masui/bitshuffle
  LANGUAGES C)

find_package(OpenMP REQUIRED)

add_library(bitshuffle_core bitshuffle_core.c iochain.c)
target_include_directories(bitshuffle_core PRIVATE ${CMAKE_SOURCE_DIR}/)
set_target_properties(bitshuffle_core PROPERTIES PUBLIC_HEADER ${PROJECT_SOURCE_DIR}/bitshuffle_core.h)
target_compile_options(bitshuffle_core PUBLIC "${OpenMP_C_FLAGS}")

install(TARGETS ${PROJECT_NAME}_core
  EXPORT ${PROJECT_NAME}_coreTargets
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
  PUBLIC_HEADER DESTINATION include)

install(EXPORT ${PROJECT_NAME}_coreTargets
  FILE ${PROJECT_NAME}_coreTargets.cmake
  NAMESPACE ${PROJECT_NAME}::core::
  DESTINATION lib/cmake/${PROJECT_NAME})
