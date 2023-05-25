
cmake_minimum_required(VERSION 3.14)

project(uwebsockets)
option(WITH_ZLIB "Enables ZLIB compression" OFF)

add_library(
  uwebsockets
  INTERFACE
)

add_subdirectory(uSockets)
target_link_libraries(uwebsockets INTERFACE usockets)

if (WITH_ZLIB)
    find_package(ZLIB REQUIRED)
    target_include_directories(uwebsockets INTERFACE ${ZLIB_INCLUDE_DIRS})
    target_link_libraries(uwebsockets INTERFACE ${ZLIB_LIBRARIES})
else()
    target_compile_definitions(uwebsockets INTERFACE UWS_NO_ZLIB)
endif()

target_include_directories(uwebsockets INTERFACE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

install(TARGETS uwebsockets EXPORT uwebsockets)
install(DIRECTORY uWebSockets DESTINATION include)
