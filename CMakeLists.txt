cmake_minimum_required(VERSION 2.6.2)

project(stun-msg)

add_subdirectory(gtest)

include_directories(include)

add_library(stunmsg STATIC
  src/crc32.c src/crc32.h
  src/hmac_sha1.c src/hmac_sha1.h
  src/sha1.c src/sha1.h
  src/md5.c src/md5.h
  src/stun_msg.c include/stun/msg.h
)

include_directories(gtest/include src)

add_executable(stunmsg_tests
  tests/stunmsg_unittest.cc
  tests/stunmsgpp_unittest.cc
  tests/sha1_unittest.cc
  tests/hmac_sha1_unittest.cc
  tests/md5_unittest.cc
  tests/crc32_unittest.cc
  include/stun++/message.h
)

add_dependencies(stunmsg_tests stunmsg gtest gtest_main)
target_link_libraries(stunmsg_tests stunmsg gtest gtest_main)

if(WIN32)
  target_link_libraries(stunmsg_tests Ws2_32)
endif()
