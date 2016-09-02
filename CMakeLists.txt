cmake_minimum_required(VERSION 2.6)

project(twitcurl)

option(BUILD_CLIENT "Build the demo twitterClient." ON)

add_subdirectory(libtwitcurl)

if(BUILD_CLIENT)

	FIND_PACKAGE(CURL)
	IF(CURL_FOUND)
	  MESSAGE(STATUS "Curl libraries found at: ${CURL_LIBRARIES}")
	  MESSAGE(STATUS "Curl includes found at: ${CURL_INCLUDE_DIRS}")
	else(CURL_FOUND)
	  MESSAGE(SEND_ERROR "Could not find cURL on your system")
	ENDIF(CURL_FOUND)

	add_subdirectory(twitterClient)
endif(BUILD_CLIENT)