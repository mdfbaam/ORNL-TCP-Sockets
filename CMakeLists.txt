cmake_minimum_required(VERSION 3.14)

project(
    sockets
    LANGUAGES CXX
    VERSION 0.1
)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_AUTOMOC ON)

find_package(Qt5 REQUIRED COMPONENTS Network)

file(GLOB_RECURSE SOURCES "src/**.cpp")
file(GLOB_RECURSE HEADERS "include/**.h")

add_library(${PROJECT_NAME})

target_sources(
    ${PROJECT_NAME}
    PRIVATE
    ${SOURCES}
)

target_sources(
    ${PROJECT_NAME}
    PUBLIC FILE_SET HEADERS
    BASE_DIRS ${CMAKE_CURRENT_LIST_DIR}/include
    FILES ${HEADERS}
)

target_link_libraries(
    ${PROJECT_NAME}
    Qt5::Core
    Qt5::Network
)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

install(
    TARGETS  ${PROJECT_NAME}
    EXPORT   ${PROJECT_NAME}Targets
    FILE_SET HEADERS
)
install(
    EXPORT ${PROJECT_NAME}Targets
    NAMESPACE ornl::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)

configure_package_config_file(
    config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)
install(
    FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}
)

