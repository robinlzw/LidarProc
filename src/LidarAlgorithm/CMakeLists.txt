# find all files in the current directory
aux_source_directory(. DIR_ALGORITHM_SRCS)
find_package(GDAL REQUIRED)
include_directories(${GDAL_INCLUDE_DIR})
message("compile Lidar Algorithm")
include_directories("../../library/")


find_package(OpenCV 4.1.0 REQUIRED) # 找OpenCV 4.0安装路径
include_directories(${OpenCV_INCLUDE_DIRS}) # 加载OpenCV 4.0的头文件

if(OpenCV_FOUND)
    message(STATUS "complie with openCV")
else()
    message("compile without openCV\n")
endif()

add_library(libalgorithm ${DIR_ALGORITHM_SRCS})
target_link_libraries(libalgorithm libbase libgeometry)
target_link_libraries(libalgorithm ${GDAL_LIBRARY})
target_link_libraries(libalgorithm ${OpenCV_LIBS})

