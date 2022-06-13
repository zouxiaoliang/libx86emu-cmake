cmake_minimum_required(VERSION 3.5)

project(x86emu LANGUAGES C)

function(x86emuMain)
    set(SRC_DIR libx86emu)

    set(SRC ${SRC_DIR}/api.c ${SRC_DIR}/decode.c ${SRC_DIR}/mem.c ${SRC_DIR}/ops.c ${SRC_DIR}/ops2.c ${SRC_DIR}/prim_ops.c)

    add_library(thirdparty_libx86emu_static ${SRC})
    target_include_directories(thirdparty_libx86emu_static SYSTEM PUBLIC ${SRC_DIR}/include)

    add_library(thirdparty_libx86emu INTERFACE)
    target_include_directories(thirdparty_libx86emu INTERFACE ${SRC_DIR}/include)
    target_link_libraries(thirdparty_libx86emu INTERFACE thirdparty_libx86emu_static)

    add_dependencies(thirdparty_libx86emu thirdparty_libx86emu_static)
endfunction()

x86emuMain()
