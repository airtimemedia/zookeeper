# Copyright Airtime Media 2015

set(ZK_C_API_SOURCES
  # headers
  zookeeper/src/c/include/zookeeper.h
  zookeeper/src/c/include/zookeeper_version.h
  zookeeper/src/c/include/zookeeper_log.h
  zookeeper/src/c/include/proto.h
  zookeeper/src/c/include/recordio.h

  zookeeper/src/c/src/zk_adaptor.h
  zookeeper/src/c/src/zk_hashtable.h

  zookeeper/src/c/src/hashtable/hashtable_itr.h
  zookeeper/src/c/src/hashtable/hashtable_private.h
  zookeeper/src/c/src/hashtable/hashtable.h

  generated/zookeeper.jute.h


  # sources
  zookeeper/src/c/src/zookeeper.c
  zookeeper/src/c/src/recordio.c
  zookeeper/src/c/src/zk_log.c
  zookeeper/src/c/src/zk_hashtable.c
  zookeeper/src/c/src/mt_adaptor.c

  zookeeper/src/c/src/hashtable/hashtable_itr.c
  zookeeper/src/c/src/hashtable/hashtable.c

  generated/zookeeper.jute.c
)

set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O2")

add_library(at_zookeeper_c STATIC ${ZK_C_API_SOURCES})

target_compile_definitions(at_zookeeper_c PUBLIC
 THREADED
)

target_include_directories(at_zookeeper_c
  PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/zookeeper/src/c/include
  PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/generated
)

target_link_libraries(at_zookeeper_c LINK_PUBLIC
  m
)
