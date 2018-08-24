cmake_minimum_required(VERSION 3.7)

project(bitshuffle
  VERSION 0.3.4
  #DESCRIPTION "Filter for improving compression of typed binary data."
  #HOMEPAGE_URL https://github.com/kiyo-masui/bitshuffle
  LANGUAGES C)

add_library(bitshuffle bitshuffle.c bitshuffle_core.c iochain.c)
target_compile_options(bitshuffle PRIVATE "-mtune=generic")
set_target_properties(bitshuffle PROPERTIES POSITION_INDEPENDENT_CODE ON)
