cmake_minimum_required(VERSION 2.8)
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../cmake)
include(GoProCommon)

SET(CMAKE_SKIP_BUILD_RPATH TRUE)
SET(CMAKE_SKIP_RPATH TRUE)
set(CMAKE_BUILD_RPATH "")
set(CMAKE_INSTALL_RPATH "")
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH FALSE)
SET(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE)

set(PROJ_NAME rtmp)
string(TOUPPER ${PROJ_NAME} PROJ_UPPER)
project(${PROJ_NAME})

if(${SYSTEM_NAME} MATCHES "linux-arm-")
    # need this so 32 bit linux builds can access >2GB files
    add_definitions(-D_FILE_OFFSET_BITS=64)
elseif(${SYSTEM_NAME} MATCHES "linux-x86")
    # need this so 32 bit linux builds can access >2GB files
    add_definitions(-D_FILE_OFFSET_BITS=64)
endif()

set(${PROJ_UPPER}_LIBRARY_TYPE SHARED)

set(${PROJ_UPPER}_INCLUDE_DIRS include)

set(${PROJ_UPPER}_PUBLIC_HEADERS include/amf.h include/rtmp.h)

set(${PROJ_UPPER}_SOURCES src/amf.c  src/hashswf.c  src/log.c  src/parseurl.c  src/rtmp.c)

add_gopro_library(${PROJ_NAME})

