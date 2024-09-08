project(colladadom)
cmake_minimum_required(VERSION 3.17)

include(FindPkgConfig)

find_package(Boost REQUIRED CONFIG)
pkg_check_modules(LIBXML2 libxml-2.0)
pkg_check_modules(MINIZIP minizip)
pkg_check_modules(ZLIB zlib)

set(COLLADA_DOM_SOVERSION "0")
set(COLLADA_DOM_VERSION "2.3")

file(GLOB dae_files ${CMAKE_CURRENT_SOURCE_DIR}/src/dae/*.cpp)
file(GLOB libxmlplugin_files ${CMAKE_CURRENT_SOURCE_DIR}/src/modules/LIBXMLPlugin/*.cpp)
file(GLOB stddatabase_files ${CMAKE_CURRENT_SOURCE_DIR}/src/modules/STLDatabase/*.cpp)
file(GLOB stderrplugin_files ${CMAKE_CURRENT_SOURCE_DIR}/src/modules/stdErrPlugin/*.cpp)

set(COLLADA_BASE_SOURCES ${dae_files} ${libxmlplugin_files} ${stddatabase_files} ${stderrplugin_files})
set(COLLADA_LIBS ${LIBXML2_LIBRARIES} ${MINIZIP_LIBRARIES} ${ZLIB_LIBRARIES} ${Boost_FILESYSTEM_LIBRARY} ${Boost_SYSTEM_LIBRARY} ${Boost_REGEX_LIBRARY})
list(JOIN MINIZIP_CFLAGS " " VAR_MINIZIP_CFLAGS)
set(COLLADA_COMPILE_FLAGS "${EXTRA_COMPILE_FLAGS} ${VAR_MINIZIP_CFLAGS} ${Boost_CFLAGS} -DDOM_INCLUDE_LIBXML")

if( OPT_COLLADA15 )
  add_subdirectory(src/1.5)
endif()
if( OPT_COLLADA14 )
  add_subdirectory(src/1.4)
endif()

# install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/1.4 DESTINATION ${COLLADA_DOM_INCLUDE_INSTALL_DIR} PATTERN ".svn" EXCLUDE PATTERN ".~" EXCLUDE)
# install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/1.5 DESTINATION ${COLLADA_DOM_INCLUDE_INSTALL_DIR} PATTERN ".svn" EXCLUDE PATTERN ".~" EXCLUDE)
# install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/dae DESTINATION ${COLLADA_DOM_INCLUDE_INSTALL_DIR} PATTERN ".svn" EXCLUDE PATTERN ".~" EXCLUDE)
# install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/modules DESTINATION ${COLLADA_DOM_INCLUDE_INSTALL_DIR} PATTERN ".svn" EXCLUDE PATTERN ".~" EXCLUDE)
# install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/include/dae.h ${CMAKE_CURRENT_SOURCE_DIR}/include/dae.h DESTINATION ${COLLADA_DOM_INCLUDE_INSTALL_DIR})
