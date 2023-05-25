
cmake_minimum_required(VERSION 3.14)

project(uwebsockets)

add_library(
  uwebsockets
  INTERFACE
)

add_subdirectory(uSockets)
target_link_libraries(uwebsockets INTERFACE usockets)

find_package(ZLIB REQUIRED)
target_include_directories(uwebsockets INTERFACE ${ZLIB_INCLUDE_DIRS})
target_link_libraries(uwebsockets INTERFACE ${ZLIB_LIBRARIES})

target_include_directories(uwebsockets INTERFACE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

install(TARGETS uwebsockets EXPORT uwebsockets)
install(DIRECTORY uWebSockets DESTINATION include)
