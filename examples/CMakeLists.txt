#  Sharedlib++
#  Copyright: (C) 2015 Ali Paikan
#  Authors: Ali Paikan <ali.paikan@gmail.com>
#
#  Copy Policy: Released under the terms of the LGPLv2.1 or later, see LGPL.TXT
#


# cmake_minimum_required(VERSION 2.6)


INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}
                    ../include)

ADD_LIBRARY(mymath SHARED MyMath.cpp MyMath.h)


IF(WIN32)
    LINK_LIBRARIES(sharedlibpp)
ELSE()
    LINK_LIBRARIES(sharedlibpp dl)
ENDIF()

ADD_EXECUTABLE(math_test math_test.cpp)

# Install the include
install(DIRECTORY .
        DESTINATION ${CMAKE_INSTALL_PREFIX}/include
        FILES_MATCHING PATTERN "*.h*")
 
# Install the library
install(TARGETS mymath
        EXPORT mymath
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib)