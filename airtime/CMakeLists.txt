# Copyright Airtime Media 2021
project(at_zookeeper_c)
cmake_minimum_required(VERSION 3.12.0)

set(ZK_C_API_SOURCES
  # headers
  ../src/c/include/zookeeper.h
  ../src/c/include/zookeeper_version.h
  ../src/c/include/zookeeper_log.h
  ../src/c/include/proto.h
  ../src/c/include/recordio.h

  ../src/c/src/zk_adaptor.h
  ../src/c/src/zk_hashtable.h

  ../src/c/src/hashtable/hashtable_itr.h
  ../src/c/src/hashtable/hashtable_private.h
  ../src/c/src/hashtable/hashtable.h

  ../generated/zookeeper.jute.h


  # sources
  ../src/c/src/zookeeper.c
  ../src/c/src/recordio.c
  ../src/c/src/zk_log.c
  ../src/c/src/zk_hashtable.c
  ../src/c/src/mt_adaptor.c

  ../src/c/src/hashtable/hashtable_itr.c
  ../src/c/src/hashtable/hashtable.c

  ../generated/zookeeper.jute.c
)

set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O2")

add_library(at_zookeeper_c STATIC ${ZK_C_API_SOURCES})

target_compile_definitions(at_zookeeper_c PUBLIC
 THREADED
)

target_compile_options(at_zookeeper_c PUBLIC
  -Wno-asm-operand-widths
)

target_include_directories(at_zookeeper_c
  PUBLIC ${PROJECT_SOURCE_DIR}/../src/c/include
  PUBLIC ${PROJECT_SOURCE_DIR}/../generated
)

target_link_libraries(at_zookeeper_c LINK_PUBLIC
  m
)
