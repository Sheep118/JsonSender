cmake_minimum_required(VERSION 3.15)
project(Project2)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# linenoise（纯 C 库，直接编译源文件）
add_library(linenoise STATIC
    lib/linenoise/linenoise.c
)
target_include_directories(linenoise PUBLIC lib/linenoise)

# nlohmann/json（header-only，创建 INTERFACE 目标）
add_library(nlohmann_json INTERFACE)
target_include_directories(nlohmann_json INTERFACE lib/json/include)

# 主可执行文件
add_executable(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME}
    PRIVATE
        linenoise
        nlohmann_json
)

# 测试服务器
add_executable(server_test server_test.cpp)
