# 最低CMake版本要求
cmake_minimum_required(VERSION 3.2.0)

# 项目名称
project(ut)

# 设置C/C++标准
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 设置编译参数
set(CMAKE_CXX_FLAGS "${CMAXE_CXX_FLAGS} -Wall")
add_definitions(-g -std=c++0x)

# 单元测试GMock
link_directories(${PROJECT_SOURCE_DIR}/unittestlib/lib)
include_directories(${PROJECT_SOURCE_DIR}/unittestlib/include)

# 目标输出位置
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/libs)

if(CMAKE_SYSTEM_NAME MATCHES "Windows")
    set(GTESTLIB wingtest wingmock pthread)
else()
    set(GTESTLIB gtest gmock pthread)
endif(CMAKE_SYSTEM_NAME MATCHES "Windows")


# 常用函数
# add_subdirectory(src)
# add_subdirectory(hellolib)

# include_directories(${PROJECT_SOURCE_DIR})
# link_directories(${LIBRARY_OUTPUT_PATH})
# add_executable(main main.cpp)
# target_link_libraries(main hello)

# set(LIBSRC hello.cpp)
# add_library(hello STATIC ${LIBSRC})

aux_source_directory(. DIRSRCS)
add_executable(main main.cpp)

enable_testing()
add_executable(SoundexTest SoundexTest.cpp)
target_link_libraries(SoundexTest ${GTESTLIB})
add_test(NAME SoundexTest COMMAND SoundexTest)