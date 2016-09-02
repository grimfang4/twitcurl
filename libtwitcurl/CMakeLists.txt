cmake_minimum_required(VERSION 2.6)


project(libtwitcurl)

set(twitSrcs base64.cpp HMAC_SHA1.cpp oauthlib.cpp SHA1.cpp urlencode.cpp twitcurl.cpp)
FIND_PACKAGE(PkgConfig)
include_directories (${PKGS_INCLUDE_DIRS}) 


add_library(twitcurl SHARED ${twitSrcs})
#add_library(twitcurl STATIC ${twitSrcs})

find_library(CURL_LIBRARY curl HINTS ./lib ../lib PATHS ./lib ../lib )
find_library(RTMP_LIBRARY rtmp HINTS ./lib)
find_library(SSH2_LIBRARY ssh2 HINTS ./lib)
find_library(LIBZ_LIBRARY libz HINTS ./lib)
find_library(IDN_LIBRARY idn HINTS ./lib)
find_library(SSL_LIBRARY ssl HINTS ./lib)
find_library(CRYPTO_LIBRARY crypto HINTS ./lib)

set(TWITCURL_DEPENDENCIES ${CURL_LIBRARY} ${RTMP_LIBRARY} ws2_32 wldap32 ${SSH2_LIBRARY} ${LIBZ_LIBRARY} ${IDN_LIBRARY} ${SSL_LIBRARY} ${CRYPTO_LIBRARY})

link_directories(./lib ../lib ../libtwitcurl/lib)
target_link_libraries (twitcurl ${TWITCURL_DEPENDENCIES})