cmake_minimum_required(VERSION 2.8.9)
project (mbpoll)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-parameter -Wno-unused-function")

set(MBPOLL_PKG_VERSION "1.3")

set(MBPOLL_SRCS src/mbpoll.c
    3rdparty/modbus/modbus.c
    3rdparty/modbus/modbus-data.c
    3rdparty/modbus/modbus-tcp.c
    3rdparty/modbus/modbus-rtu.c
    3rdparty/sysio/delay.c
    3rdparty/sysio/serial.c)

add_executable(mbpoll ${MBPOLL_SRCS})

target_include_directories(mbpoll PUBLIC .)
target_include_directories(mbpoll PUBLIC src)
target_include_directories(mbpoll PUBLIC 3rdparty)
#target_link_libraries(mbpoll ${FTDI_LIBRARIES})
install(TARGETS mbpoll RUNTIME DESTINATION bin)

### Debian Package generation
set(CPACK_GENERATOR "DEB")
set(CPACK_PACKAGE_VERSION "${MBPOLL_PKG_VERSION}")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Franz Flasch")
include(CPack)