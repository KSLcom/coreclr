# Require at least version 2.8.12 of CMake
cmake_minimum_required(VERSION 2.8.12)

set(INC_PLATFORM_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src/Common/Platform)
if (WIN32)
    add_definitions(-DWINDOWS=1)
endif()

# Compile options

if (WIN32)
    add_compile_options(-wd4820)
endif()

MACRO(SUBDIRLIST result curdir)
  FILE(GLOB children RELATIVE ${curdir} ${curdir}/*)
  SET(dirlist "")
  FOREACH(child ${children})
    IF(IS_DIRECTORY ${curdir}/${child})
        LIST(APPEND dirlist ${child})
    ENDIF()
  ENDFOREACH()
  SET(${result} ${dirlist})
ENDMACRO()

MACRO(ADDSUBDIR_REC  curdir)
    SUBDIRLIST(SUB_DIRS ${curdir})
    FOREACH(subdir ${SUB_DIRS})
        if(EXISTS "${curdir}/${subdir}/CMakeLists.txt")
           ADD_SUBDIRECTORY(${curdir}/${subdir})
        else()
           ADDSUBDIR_REC(${curdir}/${subdir})
        endif(EXISTS "${curdir}/${subdir}/CMakeLists.txt")
    ENDFOREACH()
ENDMACRO()

ADDSUBDIR_REC(${CMAKE_CURRENT_SOURCE_DIR})

