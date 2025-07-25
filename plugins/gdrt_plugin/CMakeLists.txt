SET(PACKAGE_NAME GDRT)
SET(APP_NAME gdrt_plugin)

SET(
	GDRT_SOURCES
		main.cpp
		app.cpp
		ecef.cpp
		settings.cpp
		station.cpp
		udpclient.cpp
)

INCLUDE_DIRECTORIES(${Boost_INCLUDE_DIR})
INCLUDE_DIRECTORIES(${LIBMSEED_INCLUDE_DIR})
INCLUDE_DIRECTORIES(../../libs/plugin)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../../../common/libs)
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR}/../../../common/libs)
ADD_EXECUTABLE(gdrt_plugin ${GDRT_SOURCES})
FIND_PACKAGE(Boost REQUIRED COMPONENTS system)
TARGET_LINK_LIBRARIES(${APP_NAME} ${Boost_system_LIBRARY} mseed slplugin)
SC_LINK_LIBRARIES_INTERNAL(${APP_NAME} client)
SC_ADD_VERSION(${PACKAGE_NAME} ${APP_NAME})

INSTALL(TARGETS ${APP_NAME} RUNTIME DESTINATION ${SC3_PACKAGE_SHARE_DIR}/plugins/seedlink)

FILE(GLOB descs "${CMAKE_CURRENT_SOURCE_DIR}/descriptions/*.xml")
INSTALL(FILES ${descs} DESTINATION ${SC3_PACKAGE_APP_DESC_DIR})

FILE(GLOB cfgs "${CMAKE_CURRENT_SOURCE_DIR}/config/*.cfg")
INSTALL(FILES ${cfgs} DESTINATION ${SC3_PACKAGE_CONFIG_DIR})

