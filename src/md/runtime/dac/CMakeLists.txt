
include(${CLR_DIR}/dac.cmake)
include(../../md_dac.cmake)

add_precompiled_header(stdafx.h ../stdafx.cpp MDRUNTIME_SOURCES)

add_library(mdruntime_dac ${MDRUNTIME_SOURCES})