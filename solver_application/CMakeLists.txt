cmake_minimum_required(VERSION 3.4)
project(equation)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
option(CPACK_GENERATOR_ZIP ON)


add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib
        ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib
        ${CMAKE_CURRENT_BINARY_DIR}/solver)
add_executable(equation ${CMAKE_CURRENT_SOURCE_DIR}/equation.cpp)
target_link_libraries(equation formatter_ex solver)


install(TARGETS equation RUNTIME DESTINATION bin)
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "keyow")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "libc6 (>= 2.3.1-6), libc6 (< 2.4)")
set(CPACK_GENERATOR "DEB;RPM")
include(CPack)
