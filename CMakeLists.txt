cmake_minimum_required(VERSION 3.14)

project(ORNL-TCP-Sockets LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 COMPONENTS Network REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Network REQUIRED)

file(GLOB_RECURSE SOURCES "src/**.cpp")
file(GLOB_RECURSE HEADERS "include/**.h")

add_library(ORNL-TCP-Sockets STATIC
  ${SOURCES}
  ${HEADERS}
)

target_link_libraries(ORNL-TCP-Sockets Qt${QT_VERSION_MAJOR}::Core Qt${QT_VERSION_MAJOR}::Network)

target_compile_definitions(ORNL-TCP-Sockets PRIVATE ORNLTCPSOCKETS_LIBRARY)
