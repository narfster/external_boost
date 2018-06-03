cmake_minimum_required(VERSION 3.10)
project(external_boost)

set(CMAKE_CXX_STANDARD 17)


set(BOOST_INCLUDEDIR $ENV{HOME}/CLionProjects/3rdparty/install/boost/include)
set(BOOST_LIBRARYDIR $ENV{HOME}/CLionProjects/3rdparty/install/boost/lib)


find_package (Boost 1.64.0 COMPONENTS system filesystem)
find_package( OpenCV 3.4.1 PATHS $ENV{HOME}/CLionProjects/3rdparty/install/opencv)

add_executable(external_boost main.cpp)

target_link_libraries(external_boost Boost::filesystem ${OpenCV_LIBS})








