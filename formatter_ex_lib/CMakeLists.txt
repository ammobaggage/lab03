cmake_minimum_required(VERSION 3.2)
project(formatter_ex)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(formatter_ex STATIC formatter_ex.cpp)
target_include_directories(formatter_ex PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
    )
cmake_policy(SET CMP0079 NEW)  
target_link_libraries(formatter_ex PRIVATE formatter)