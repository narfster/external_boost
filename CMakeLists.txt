cmake_minimum_required(VERSION 3.10)
project(external_boost)

set(CMAKE_CXX_STANDARD 17)


set(BOOST_ROOT ${CMAKE_SOURCE_DIR}/boost)
set(BOOST_INCLUDEDIR ${BOOST_ROOT}/include)
set(BOOST_LIBRARYDIR ${BOOST_ROOT}/lib)


find_package (Boost 1.64.0 COMPONENTS system filesystem)



if (NOT boost_FOUND)

    message("BOOST WAS NOT FOUND 1")

endif()

if (NOT Boost_FOUND)

message("BOOST WAS NOT FOUND 2")


include(ExternalProject)
ExternalProject_Add(
        boost
        PREFIX            ${BOOST_ROOT}
        TMP_DIR           ${BOOST_ROOT}/temp
        STAMP_DIR         ${BOOST_ROOT}/stamp
        #--Download step--------------
        DOWNLOAD_DIR      ${BOOST_ROOT}/download
        URL               https://dl.bintray.com/boostorg/release/1.64.0/source/boost_1_64_0.tar.gz
        URL_HASH          SHA256=0445c22a5ef3bd69f5dfb48354978421a85ab395254a26b1ffb0aa1bfd63a108
        #--Configure step-------------
        CONFIGURE_COMMAND ./bootstrap.sh --prefix=${BOOST_ROOT}
        #--Build step-------------
        BUILD_COMMAND     ./b2 install -j8 --with-filesystem
        BUILD_IN_SOURCE   true
        #--Install step---------------
        INSTALL_COMMAND   ""
        INSTALL_DIR       ${BOOST_ROOT}
)

else()

    message("BOOST FOUND!!")

    add_executable(external_boost main.cpp)

    target_link_libraries(external_boost Boost::filesystem)

endif()


