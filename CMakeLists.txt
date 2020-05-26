# CMAKE version of Ubuntu 16.04 is 3.5.
cmake_minimum_required(VERSION 3.5)

project(boost_log)

set(LINKLIBS)
set(COMPILE_OPTION)
set(INCL)
set(SRC)
################################################
file(GLOB SRC_LOG
    "libs/log/src/*.h"
    "libs/log/src/*.cpp"
    "libs/log/src/posix/*.h"
    "libs/log/src/posix/*.cpp"
    "libs/log/src/windows/*.h"
    "libs/log/src/windows/*.cpp"
    "libs/log/src/setup/*.h"
    "libs/log/src/setup/*.cpp"
)

list(APPEND SRC
  ${SRC_LOG}
  main.cpp
  )
list(APPEND INCL
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  )
list(APPEND COMPILE_OPTION
  -O3
  -DBOOST_ALL_DYN_LINK
  )
list(APPEND LINKLIBS
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_atomic.so
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_chrono.so
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_date_time.so
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_filesystem.so
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_log.so
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_log_setup.so
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_regex.so
  ${CMAKE_CURRENT_SOURCE_DIR}/libs/log/libboost_thread.so
  pthread
  
  )

################################################

add_executable(${PROJECT_NAME} ${SRC})
target_include_directories(${PROJECT_NAME} PRIVATE ${INCL})
target_link_libraries(${PROJECT_NAME} ${LINKLIBS})
target_compile_options(${PROJECT_NAME} PRIVATE ${COMPILE_OPTION} )
set_target_properties(${PROJECT_NAME} PROPERTIES  CXX_STANDARD 14 )
