cmake_minimum_required(VERSION 3.0)
include(version.cmake)
project(baseclasses VERSION ${baseclasses_VERSION})

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake-modules")
include(AddPCH)

if(CMAKE_SIZEOF_VOID_P STREQUAL 4)
  set(baseclasses_BUILD_ARCHITECTURES "x86")
  set(baseclasses_BUILD_64 OFF)
else()
  set(baseclasses_BUILD_ARCHITECTURES "x64")
  set(baseclasses_BUILD_64 ON)
endif()

set(CMAKE_CONFIGURATION_TYPES "Release;Debug" CACHE STRING "" FORCE)

# CMake finder files
configure_file(baseclasses-config.cmake.in baseclasses-config.cmake @ONLY)
configure_file(baseclasses-configVersion.cmake.in baseclasses-configVersion.cmake @ONLY)

add_subdirectory(baseclasses)

export(EXPORT BaseClassesTargets FILE BaseClassesTargets.cmake NAMESPACE BaseClasses::)
install(EXPORT BaseClassesTargets FILE BaseClassesTargets.cmake COMPONENT BaseClasses NAMESPACE BaseClasses:: DESTINATION cmake CONFIGURATIONS ${CMAKE_CONFIGURATION_TYPES})

# Install baseclasses-config.cmake and baseclasses-configVersion.cmake
install(FILES
  "${CMAKE_CURRENT_BINARY_DIR}/baseclasses-config.cmake"
  "${CMAKE_CURRENT_BINARY_DIR}/baseclasses-configVersion.cmake"
  DESTINATION "cmake"
  COMPONENT baseclasses
)

# Install public header files, source files should not be installed because they are in the lib
install(
  DIRECTORY ${PROJECT_SOURCE_DIR}/baseclasses
  DESTINATION include
  COMPONENT baseclasses
  FILES_MATCHING PATTERN "*.h"
)

SET(CPACK_PACKAGE_VERSION_MAJOR "${baseclasses_VERSION_MAJOR}")
SET(CPACK_PACKAGE_VERSION_MINOR "${baseclasses_VERSION_MINOR}")
SET(CPACK_PACKAGE_VERSION_PATCH "${baseclasses_VERSION_PATCH}")
set(CPACK_GENERATOR ZIP)
include(CPack)
