if (DEFINED DSN_CMAKE_INCLUDED)
else()
    
    set(DSN_ROOT "$ENV{DSN_ROOT}")
    if(NOT EXISTS "${DSN_ROOT}/")
        message(FATAL_ERROR "Please make sure that ${DSN_ROOT} exists.")
    endif()

    include("${DSN_ROOT}/bin/dsn.cmake")
endif()

add_definitions(-DDSN_IN_CORE)
set(DSN_IN_CORE "TRUE")

set(MY_PROJ_NAME dsn.core)

# Source files under CURRENT project directory will be automatically included.
# You can manually set MY_PROJ_SRC to include source files under other directories.
set(MY_PROJ_SRC "")

# Search mode for source files under CURRENT project directory?
# "GLOB_RECURSE" for recursive search
# "GLOB" for non-recursive search
set(MY_SRC_SEARCH_MODE "GLOB")

set(MY_PROJ_INC_PATH ${GTEST_INCLUDE_DIR})

set(MY_PROJ_LIBS gtest
                 dsn.dev.cpp.core.use
                 dsn.dev.utility
   )

set(MY_PROJ_LIB_PATH "${GTEST_LIB_DIR}")

# Extra files that will be installed
set(MY_BINPLACES "")

dsn_add_shared_library()

file(COPY test/ DESTINATION "${CMAKE_BINARY_DIR}/test/${MY_PROJ_NAME}")
