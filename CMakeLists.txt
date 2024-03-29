cmake_minimum_required (VERSION 3.16)
cmake_policy(SET CMP0074 NEW)
set(CMAKE_CXX_STANDARD 17)

project("hakurei")

list(APPEND CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR})
list(APPEND CMAKE_PREFIX_PATH ${CMAKE_BINARY_DIR})
include(conan.cmake)
conan_cmake_configure(
    REQUIRES
        spdlog/1.9.2
        gtest/cci.20210126
        fmt/8.0.1
        date/3.0.1
        tomlplusplus/2.5.0
        fruit/3.6.0
        argon2/20190702
    GENERATORS
        cmake_find_package
)
conan_cmake_autodetect(settings)
conan_cmake_install(
    PATH_OR_REFERENCE .
    BUILD missing
    REMOTE conancenter
    SETTINGS ${settings}
)

find_package(spdlog REQUIRED)
find_package(fmt REQUIRED)
find_package(GTest REQUIRED)
find_package(date REQUIRED)
find_package(tomlplusplus REQUIRED)
find_package(fruit REQUIRED)
find_package(argon2 REQUIRED)

add_subdirectory(core)
add_subdirectory(ui)