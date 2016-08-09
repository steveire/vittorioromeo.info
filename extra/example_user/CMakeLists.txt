cmake_minimum_required(VERSION 3.3)

project(example_user)

find_package(example_lib REQUIRED)

add_executable(myexe
    src/src0.cpp
    src/src1.cpp
    src/main.cpp
)

## uncomment only one of these!
# target_link_libraries(myexe example_lib::library_static)
# target_link_libraries(myexe example_lib::library_shared)
# target_link_libraries(myexe example_lib::library_iface)
target_link_libraries(myexe example_lib::library_srcs)
