cmake_minimum_required(VERSION 2.6)


project(libtwitcurl)

set(twitSrcs base64.cpp HMAC_SHA1.cpp oauthlib.cpp SHA1.cpp urlencode.cpp twitcurl.cpp)
FIND_PACKAGE(PkgConfig)
include_directories (${PKGS_INCLUDE_DIRS}) 


add_library(twitcurl SHARED ${twitSrcs})
#add_library(twitcurl STATIC ${twitSrcs})

set(LIB_HINTS )
set(LIB_PATHS ./lib ../lib)

find_library(CURL_LIBRARY curl HINTS ${LIB_HINTS} PATHS ${LIB_PATHS})
find_library(RTMP_LIBRARY rtmp HINTS ${LIB_HINTS} PATHS ${LIB_PATHS})
find_library(SSH2_LIBRARY ssh2 HINTS ${LIB_HINTS} PATHS ${LIB_PATHS})
find_library(LIBZ_LIBRARY NAMES libz z HINTS ${LIB_HINTS} PATHS ${LIB_PATHS})
find_library(IDN_LIBRARY idn HINTS ${LIB_HINTS} PATHS ${LIB_PATHS})
find_library(SSL_LIBRARY ssl HINTS ${LIB_HINTS} PATHS ${LIB_PATHS})
find_library(CRYPTO_LIBRARY crypto HINTS ${LIB_HINTS} PATHS ${LIB_PATHS})


set(TWITCURL_DEPENDENCIES ${CURL_LIBRARY} ${RTMP_LIBRARY} ${SSH2_LIBRARY} ${LIBZ_LIBRARY} ${IDN_LIBRARY} ${SSL_LIBRARY} ${CRYPTO_LIBRARY})

if(WIN32)
    set(TWITCURL_DEPENDENCIES ${TWITCURL_DEPENDENCIES} ws2_32 wldap32)
endif(WIN32)

link_directories(./lib ../lib ../libtwitcurl/lib)
target_link_libraries (twitcurl ${TWITCURL_DEPENDENCIES})