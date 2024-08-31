file(GLOB dom_files ${CMAKE_CURRENT_SOURCE_DIR}/dom/*.cpp)
add_library(collada14dom STATIC ${COLLADA_BASE_SOURCES} ${dom_files})
target_include_directories(collada14dom PRIVATE
	${colladadom_SOURCE_DIR}/include
	${colladadom_SOURCE_DIR}/include/1.4
	${LIBXML2_INCLUDE_DIRS}
	${MINIZIP_INCLUDE_DIRS}
	${ZLIB_INCLUDE_DIRS}
)
target_link_directories(collada14dom INTERFACE
	${LIBXML2_LIBRARY_DIRS}
	${MINIZIP_LIBRARY_DIRS}
	${ZLIB_LIBRARY_DIRS}
)
target_link_libraries(collada14dom ${COLLADA_LIBS})
set_target_properties(collada14dom PROPERTIES
  COMPILE_FLAGS "${COLLADA_COMPILE_FLAGS}"
  CLEAN_DIRECT_OUTPUT 1
  SOVERSION ${COLLADA_DOM_SOVERSION}
  VERSION ${COLLADA_DOM_VERSION})
install(TARGETS collada14dom DESTINATION ${COLLADA_DOM_LIBS_INSTALL_DIR})
