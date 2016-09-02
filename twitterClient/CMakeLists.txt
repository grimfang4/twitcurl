cmake_minimum_required(VERSION 2.6)

project(twitterClient)

#find_package(CURL REQUIRED)

#find_path(CURL_INCLUDE_DIR NAMES curl.h 
#	PATH_SUFFIXES include/curl include
#          DOC "The CURL include directory"
#)

#find_library(CURL_LIBRARY NAMES CURL curl
#          DOC "The CURL library"
#)


#if ( NOT CURL_LIBRARY )
#   message ( FATAL_ERROR "CURL_LIBRARY not found!" )
#endif ( NOT CURL_LIBRARY )

IF(NOT CURL_FOUND)

FIND_PACKAGE(CURL)
IF(CURL_FOUND)
  MESSAGE(STATUS "Curl libraries found at: ${CURL_LIBRARIES}")
  MESSAGE(STATUS "Curl includes found at: ${CURL_INCLUDE_DIRS}")
else(CURL_FOUND)
  MESSAGE(SEND_ERROR "Could not find cURL on your system")
ENDIF(CURL_FOUND)

ENDIF(NOT CURL_FOUND)



set(clientSrcs twitterClient.cpp)
set(clientLibs twitcurl ${CURL_LIBRARY} ${CURL_LIBRARIES})
#set(clientLibs twitcurl ${CURL_LIBRARIES})

include_directories("include" "include/curl" ${CURL_INCLUDE_DIRS})
link_directories("C:/Users/Dearborn/Programming/Builds/curl-7.40.0-devel-mingw32/lib/")

add_executable(twitterClient ${clientSrcs})
target_link_libraries (twitterClient ${clientLibs} curl idn rtmp ssh2 ssl libz)