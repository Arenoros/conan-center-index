cmake_minimum_required(VERSION 2.8.12)
project(cmake_wrapper)

include(conanbuildinfo.cmake)
conan_basic_setup()

if(MYSQL_ROOT_DIR)
  find_package(MySQL REQUIRED)
  add_library(MySQL::client INTERFACE IMPORTED)
  target_link_libraries(MySQL::client INTERFACE MySQL::MySQL)
endif()
if(PostgreSQL_ROOT_DIR)
  find_package(PostgreSQL REQUIRED)
  add_library(PostgreSQL::client INTERFACE IMPORTED)
  target_link_libraries(PostgreSQL::client INTERFACE PostgreSQL::PostgreSQL)
endif()

# Disable automatic linking on MSVC
add_definitions(-DPOCO_NO_AUTOMATIC_LIBS)

add_subdirectory(source_subfolder)
