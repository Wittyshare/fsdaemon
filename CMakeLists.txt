cmake_minimum_required(VERSION 2.8.3)

PROJECT(DIR_FSDAEMON)
SET(APPNAME fsdaemon)

SET(CMAKE_INSTALL_PREFIX  /usr/local/wittyshare)

SET (APPNAME_SRCS
    src/FsDaemon/WsFsDaemonLoader.cpp
    src/FsDaemon/WsFsDaemon.cpp
    src/FsDaemon/WsUserSession.cpp
)

INCLUDE(${CMAKE_ROOT}/Modules/gdcmake/Find_wscore.cmake)

IF(NOT WSCORE_FOUND)
	MESSAGE(FATAL_ERROR "** these program needs wscore libraries... Abord.")
ENDIF(NOT WSCORE_FOUND)

INCLUDE_DIRECTORIES(
    ${WSCORE_INCLUDE_DIRS}
)

SET ( APP_LIBRARIES
      ${WSCORE_LIBRARIES}
    )

ADD_EXECUTABLE(
   ${APPNAME}
   ${APPNAME_SRCS} 
)

TARGET_LINK_LIBRARIES(${APPNAME} ${APP_LIBRARIES} )

INSTALL(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/${APPNAME}
      DESTINATION bin)

 
