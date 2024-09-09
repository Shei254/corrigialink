#note: experimental
#      currently only used for generating `compile_commands.json` for clangd
#      to build this project, it's suggested to use `makefile` instead

cmake_minimum_required(VERSION 3.7)
project(corrigialink)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_CXX_STANDARD 11)

set(SOURCE_FILES
        main.cpp
        log.cpp
        common.cpp
        lib/fec.cpp
        lib/rs.cpp
        packet.cpp
        delay_manager.cpp
        fd_manager.cpp
        connection.cpp
        fec_manager.cpp
        misc.cpp
        tunnel_client.cpp
        tunnel_server.cpp
        my_ev.cpp
)
set(CMAKE_CXX_FLAGS "-Wall -Wextra -Wno-unused-variable -Wno-unused-parameter -Wno-missing-field-initializers -O2 -g -fsanitize=address,undefined")

#target_include_directories(corrigialink PRIVATE .)
#set(CMAKE_LINK_LIBRARY_FLAG "-lrt")
add_executable(corrigialink ${SOURCE_FILES})
target_link_libraries(corrigialink rt)
target_link_libraries(corrigialink pthread)
include_directories(SYSTEM "libev")
include_directories(".")
