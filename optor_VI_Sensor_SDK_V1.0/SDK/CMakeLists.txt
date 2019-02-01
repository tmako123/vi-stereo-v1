cmake_minimum_required(VERSION 2.8)

project(camtest)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")

find_package(OpenCV REQUIRED)

include_directories("${PROJECT_SOURCE_DIR}/include")

SET(SRCS 
	include/optorcam.h
	include/optorimu.h
	include/optorusb.h
        include/winsupport.h
	src/optorcam.cpp
	src/optorimu.cpp
	src/optorusb.cpp
        src/winsupport.cpp
	)
add_library(lib_optor ${SRCS})

#add_library(optorusbcam src/optorusb.cpp src/optorcam.cpp)
#target_link_libraries(optorusbcam optorimu)
#add_library(optorimu src/optorimu.cpp)

add_executable(camtest src/camtest.cpp)
#target_link_libraries(camtest optorusbcam optorimu usb-1.0 ${OpenCV_LIBS})
target_link_libraries(camtest lib_optor usb-1.0 ${OpenCV_LIBS})
