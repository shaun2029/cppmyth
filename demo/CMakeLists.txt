cmake_minimum_required (VERSION 2.6 FATAL_ERROR)
cmake_policy (VERSION 2.6)

project (livetvdemo)

###############################################################################
# add definitions
if (MSVC)
  add_definitions ("/D_USE_32BIT_TIME_T /D_CRT_SECURE_NO_WARNINGS")
  set (CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} /W3")
  set (CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} /W3")
  set (CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /W3 /Od /RTC1 /EHsc /nologo")
  set (CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /W3 /Od /RTC1 /EHsc /nologo")
endif ()

if (NOT WIN32 AND (CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX))
   add_definitions ("-fPIC")
endif ()

###############################################################################
# configure
include_directories (
  ${CMAKE_BINARY_DIR}/cppmyth/include/.)

###############################################################################
# add sources
file (GLOB SRC_FILES src/*.cpp)

set (LIVETVDEMO_SOURCES
  ${SRC_FILES})

###############################################################################
# add targets
add_executable (livetvdemo ${LIVETVDEMO_SOURCES})
add_dependencies (livetvdemo cppmyth)
target_link_libraries (livetvdemo cppmyth)
