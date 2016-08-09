cmake_minimum_required(VERSION 3.3)

project(example_lib)

# define the library

set(library_srcs
    example_lib/library/module0/module0.cpp
    example_lib/library/module1/module1.cpp
)

add_library(library_static STATIC ${library_srcs})
add_library(library_shared SHARED ${library_srcs})

add_library(library_iface INTERFACE)
target_compile_definitions(library_iface
    INTERFACE LIBRARY_HEADER_ONLY
)

set(installed_srcs
    include/example_lib/library/module0/module0.cpp
    include/example_lib/library/module1/module1.cpp
)
add_library(library_srcs INTERFACE)
target_sources(library_srcs INTERFACE
    $<INSTALL_INTERFACE:${installed_srcs}>
)


# install and export the library

install(DIRECTORY
    example_lib/library
  DESTINATION
    include/example_lib
)
install(FILES
    example_lib/library.hpp
    example_lib/api.hpp
  DESTINATION
    include/example_lib
)
install(TARGETS
    library_static
    library_shared
    library_iface
    library_srcs
  EXPORT library_targets
  RUNTIME DESTINATION bin
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  INCLUDES DESTINATION include
)
install(EXPORT library_targets
    NAMESPACE example_lib::
    DESTINATION lib/cmake/example_lib
)

install(FILES example_lib-config.cmake
    DESTINATION lib/cmake/example_lib
)
