cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
include("cmake/HunterVersion.cmake")

project(restinio)
include(GNUInstallDirs)

hunter_add_package(asio)
find_package(asio CONFIG REQUIRED)

hunter_add_package(Boost COMPONENTS system regex)
find_package(Boost REQUIRED COMPONENTS system regex)

hunter_add_package(http-parser)
find_package(http-parser CONFIG REQUIRED)

hunter_add_package(fmt)
find_package(fmt CONFIG REQUIRED)

set(RESTINIO_MASTER_PROJECT Off)
set(RESTINIO_INSTALL On)
#set(RESTINIO_STAND_ALONE_ASIO_HEADERS asio/include )

add_subdirectory("dev")
