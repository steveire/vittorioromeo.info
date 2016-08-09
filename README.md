
CMake buildsystem for 4-category libraries.

Build the library:

    cd extra/example_library
    mkdir build
    cd build
    cmake .. -DCMAKE_INSTALL_PREFIX=../../prefix
    make
    make install

Consume the library:

    cd extra/example_user
    mkdir build
    cd build
    cmake .. -DCMAKE_PREFIX_PATH=$PWD/../../prefix
    make
