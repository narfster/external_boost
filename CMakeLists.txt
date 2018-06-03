cmake_minimum_required(VERSION 3.10)
project(external_boost)

set(CMAKE_CXX_STANDARD 17)


# set boost location install location and find_package
set(BOOST_INCLUDEDIR $ENV{HOME}/dev/3rdparty/boost/include)
set(BOOST_LIBRARYDIR $ENV{HOME}/dev/3rdparty/boost/lib)
find_package (Boost 1.64.0 COMPONENTS system filesystem)

# find opencv at location
find_package (OpenCV 3.4.1 PATHS $ENV{HOME}/dev/3rdparty/opencv)

if(Boost_FOUND)
    message("=== Boost found ===")
    message(Boost_LIBRARY_DIR = ${Boost_LIBRARY_DIR})
    message(Boost_LIBRARY_DIR_RELEASE = ${Boost_LIBRARY_DIR_RELEASE})
    message(Boost_INCLUDE_DIRS = ${Boost_INCLUDE_DIRS})
endif()

if(OpenCV_FOUND)
    message("=== OpenCV found ===")
    message("OpenCV  Version: " ${OpenCV_VERSION})
    message("OpenCV_INSTALL_PATH = " ${OpenCV_INSTALL_PATH})
    message("OpenCV_INCLUDE_DIRS = " ${OpenCV_INCLUDE_DIRS})
    message("Use as shared lib?  = " ${OpenCV_SHARED})
    SET(OpenCV_LIB_DIR "${OpenCV_INSTALL_PATH}/lib")
endif()

# Set relative path for application to search for shared libs.
set(CMAKE_INSTALL_RPATH ${Boost_LIBRARY_DIR_RELEASE} ${OpenCV_LIB_DIR})

add_executable(external_boost main.cpp)

target_link_libraries(external_boost Boost::filesystem ${OpenCV_LIBS} )


# install target : $make install
install(TARGETS external_boost
        DESTINATION $ENV{HOME}/dev/vision)




