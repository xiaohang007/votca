find_package(CLANG_FORMAT 10)
if(CLANG_FORMAT_FOUND)
  set(FORMAT_SOURCES)
  foreach(DIR ${ENABLED_VOTCA_PACKAGES})
    set(ABS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../${DIR})
    file(GLOB_RECURSE ${DIR}_SOURCES ${ABS_DIR}/*.cc ${ABS_DIR}/*.h ${ABS_DIR}/*.cpp ${ABS_DIR}/*.hpp ${ABS_DIR}/*.c)
    list(APPEND FORMAT_SOURCES ${${DIR}_SOURCES})
  endforeach()
  add_custom_target(format
    COMMAND ${CLANG_FORMAT_EXECUTABLE} -i -style=file ${FORMAT_SOURCES}
    DEPENDS ${FORMAT_SOURCES})
endif()
