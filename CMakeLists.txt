cmake_minimum_required(VERSION 3.12)
project(dist-kadabra CXX)

find_package(PkgConfig)

pkg_check_modules(NETWORKIT REQUIRED IMPORTED_TARGET networkit)
pkg_check_modules(FABRY REQUIRED IMPORTED_TARGET fabry)

find_package(OpenMP)

add_executable(dist-kadabra main.cpp DistributedKadabra.cpp)
target_include_directories(dist-kadabra PUBLIC "${PROJECT_SOURCE_DIR}/." ${NETWORKIT_INCLUDE_DIRS} ${FABRY_INCLUDE_DIRS})
target_link_libraries(dist-kadabra PUBLIC OpenMP::OpenMP_CXX PkgConfig::NETWORKIT PkgConfig::FABRY)
install(TARGETS dist-kadabra DESTINATION ${CMAKE_INSTALL_PREFIX})