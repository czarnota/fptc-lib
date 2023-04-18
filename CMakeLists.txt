cmake_minimum_required(VERSION 3.13)

project(fptc-lib LANGUAGES C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -pedantic -Wextra -Werror=return-type")

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -Wextra -Werror=return-type")

add_library(fptc-lib INTERFACE)
target_include_directories(fptc-lib INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/src)

add_executable(fixtest tests/test.c)
target_link_libraries(fixtest PRIVATE fptc-lib m)
target_include_directories(fixtest PRIVATE ${CMAKE_SOURCE_DIR})

add_executable(verify_32 tests/verify.c)
target_link_libraries(verify_32 PRIVATE fptc-lib m)
target_compile_definitions(verify_32 PRIVATE FIXED_BITS=64)
target_include_directories(verify_32 PRIVATE ${CMAKE_SOURCE_DIR})

add_executable(verify_64 tests/verify.c)
target_link_libraries(verify_64 PRIVATE fptc-lib m)
target_compile_definitions(verify_64 PRIVATE FIXED_BITS=64)
target_include_directories(verify_64 PRIVATE ${CMAKE_SOURCE_DIR})
