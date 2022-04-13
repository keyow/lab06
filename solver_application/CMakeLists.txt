cmake_minimum_required(VERSION 3.4)
project(equation)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(CPACK_GENERATOR_DEB OFF)
option(CPACK_GENERATOR_RPM OFF)
option(CPACK_GENERATOR_MSI OFF)
option(CPACK_GENERATOR_DMG OFF)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib
        ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib
        ${CMAKE_CURRENT_BINARY_DIR}/solver)
add_executable(equation ${CMAKE_CURRENT_SOURCE_DIR}/equation.cpp)
target_link_libraries(equation formatter_ex solver)


install(TARGETS equation RUNTIME DESTINATION bin)
set(CPACK_SOURCE_GENERATOR "TGZ;ZIP")
if(CPACK_GENERATOR_RPM)
    set(CPACK_GENERATOR "RPM")
endif()

if(CPACK_GENERATOR_DEB)
    set(CPACK_DEBIAN_PACKAGE_MAINTAINER "keyow")
    set(CPACK_DEBIAN_PACKAGE_DEPENDS "libc6 (>= 2.3.1-6), libc6 (< 2.4)")
    set(CPACK_GENERATOR "DEB")
endif()

if(CPACK_GENERATOR_MSI)
    set(CPACK_GENERATOR "MSI")
endif()

if(CPACK_GENERATOR_DMG)
    set(MACOSX_BUNDLE TRUE)
    set(CPACK_GENERATOR "DragNDrop")
endif()

include(CPack)

unset(CPACK_GENERATOR_RPM CACHE)
unset(CPACK_GENERATOR_DEB CACHE)
unset(CPACK_GENERATOR_MSI CACHE)
unset(CPACK_GENERATOR_DMG CACHE)