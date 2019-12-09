cmake_minimum_required(VERSION 3.5 FATAL_ERROR)
include("cmake/HunterVersion.cmake")

option(RESTINIO_USE_BOOST_ASIO "whether to use Boost.ASIO (On) or standalone ASIO (Off)" Off)

project(restinio)
include(GNUInstallDirs)

if(RESTINIO_USE_BOOST_ASIO)
  hunter_add_package(Boost COMPONENTS asio system regex)
  find_package(Boost REQUIRED COMPONENTS asio system regex)
else()
  hunter_add_package(asio)
  find_package(asio CONFIG REQUIRED)
  set(RESTINIO_USE_BOOST_ASIO none)

  hunter_add_package(Boost COMPONENTS system regex)
  find_package(Boost REQUIRED COMPONENTS system regex)
endif()

hunter_add_package(http-parser)
find_package(http-parser CONFIG REQUIRED)

hunter_add_package(fmt)
find_package(fmt CONFIG REQUIRED)

set(RESTINIO_FIND_DEPS On)
set(RESTINIO_INSTALL On)

add_subdirectory("dev/restinio")

if(RESTINIO_USE_BOOST_ASIO MATCHES "none")
  target_link_libraries(restinio INTERFACE asio::asio_static)
else()
  target_link_libraries(restinio INTERFACE Boost::asio)
endif()
