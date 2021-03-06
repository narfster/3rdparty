cmake_minimum_required(VERSION 3.5.1)

include(ExternalProject)

set(CMAKE_CXX_STANDARD 14)

# Set location for all installation of libs
set(BASE_INSTALL_DIR /usr/local/)

set(BOOST_ROOT ${CMAKE_SOURCE_DIR}/boost)
set(BOOST_INSTALL_DIR ${BASE_INSTALL_DIR})

set(OPENCV_ROOT ${CMAKE_SOURCE_DIR}/opencv)
set(OPENCV_INSTALL_DIR ${BASE_INSTALL_DIR})

message("Install prefix = " ${CMAKE_INSTALL_PREFIX})

# --------------------------------------------------------------------------
# boost

ExternalProject_Add(
        boost
        PREFIX            ${BOOST_ROOT}
        TMP_DIR           ${BOOST_ROOT}/temp
        STAMP_DIR         ${BOOST_ROOT}/stamp
        #--Download step--------------
        DOWNLOAD_DIR      ${BOOST_ROOT}/download
        URL               https://dl.bintray.com/boostorg/release/1.66.0/source/boost_1_66_0.tar.gz
        URL_HASH          SHA256=bd0df411efd9a585e5a2212275f8762079fed8842264954675a4fddc46cfcf60
        #--Configure step-------------
        CONFIGURE_COMMAND ./bootstrap.sh --prefix=${BOOST_INSTALL_DIR}
        #--Build step-------------
        BUILD_COMMAND     ./b2 install -j8
        --with-filesystem
        --with-system
        --with-atomic
        --with-date_time
        --with-log
        --with-regex
        --with-thread
        --with-math
        BUILD_IN_SOURCE   true
        #--Install step---------------
        INSTALL_COMMAND   ""
        INSTALL_DIR       ""
)



# --------------------------------------------------------------------------
# OpenCV

ExternalProject_Add(opencv
        PREFIX            ${OPENCV_ROOT}
        TMP_DIR           ${OPENCV_ROOT}/temp
        STAMP_DIR         ${OPENCV_ROOT}/stamp
         #--Download step--------------
        DOWNLOAD_DIR      ${OPENCV_ROOT}/download
        URL https://github.com/opencv/opencv/archive/3.4.1.zip
        TIMEOUT "60"
        #SOURCE_DIR opencv
        #BINARY_DIR opencv-build
        UPDATE_COMMAND ""
        PATCH_COMMAND ""
        #--Build step-------------
        CMAKE_GENERATOR ${gen}
        CMAKE_ARGS
        -DCMAKE_BUILD_TYPE:STRING=Release
        -DBUILD_DOCS:BOOL=OFF
        -DBUILD_EXAMPLES:BOOL=OFF
        -DBUILD_NEW_PYTHON_SUPPORT:BOOL=OFF
        -DBUILD_PACKAGE:BOOL=OFF
        -DBUILD_SHARED_LIBS:BOOL=ON
        -DBUILD_TESTS:BOOL=OFF
        -DWITH_FFMPEG:BOOL=OFF
        #--Install step---------------
        -DCMAKE_INSTALL_PREFIX:PATH=${OPENCV_INSTALL_DIR}
        )



