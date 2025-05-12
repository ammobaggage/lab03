cmake_minimum_required(VERSION 3.5)
project(solver_lib)

add_library(solver_lib STATIC solver.cpp)

target_link_libraries(solver_lib PRIVATE formatter_ex)

target_include_directories(solver_lib PUBLIC
    
    /formatter_ex_lib
    /formatter_lib
)
