cmake_minimum_required (VERSION 2.6)
project (simple_example)

add_executable(simple_example src/simple_example.cpp)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -lpthread -lrt -lsnappy -lz -lbz2 -llz4 -ltcmalloc -lrocksdb")
