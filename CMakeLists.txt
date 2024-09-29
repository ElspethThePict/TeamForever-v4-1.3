cmake_minimum_required(VERSION 3.7)

project(RetroEngine)

set(RETRO_SDL_VERSION 2 CACHE STRING "Select between SDL2 and SDL1, defaults to SDL2")

set(RETRO_NAME "s1fs2a")

set(RETRO_OUTPUT_NAME ${RETRO_NAME} CACHE STRING "The exported name of the executable.")

set(RETRO_FILES
    dependencies/all/tinyxml2/tinyxml2.cpp
    RSDKv4/Animation.cpp
    RSDKv4/Audio.cpp
    RSDKv4/Collision.cpp
    RSDKv4/Debug.cpp
    RSDKv4/Drawing.cpp
    RSDKv4/Ini.cpp
    RSDKv4/Input.cpp
    RSDKv4/Math.cpp
    RSDKv4/ModAPI.cpp
    RSDKv4/Networking.cpp
    RSDKv4/Object.cpp
    RSDKv4/Palette.cpp
    RSDKv4/Reader.cpp
    RSDKv4/Renderer.cpp
    RSDKv4/RetroEngine.cpp
    RSDKv4/Scene.cpp
    RSDKv4/Scene3D.cpp
    RSDKv4/Script.cpp
    RSDKv4/Sprite.cpp
    RSDKv4/String.cpp
    RSDKv4/Text.cpp
    RSDKv4/Userdata.cpp
    RSDKv4/Video.cpp
    RSDKv4/main.cpp
    RSDKv4/NativeObjects/All.cpp
    dependencies/all/theoraplay/theoraplay.c
    dependencies/all/tinyxml2/tinyxml2.cpp
)

if(NOT PLATFORM)
    if(WIN32) # THIS ASSUMES VCPKG OR SOURCES !!!!!!!
        set(PLATFORM "Windows" CACHE STRING "The platform to compile for.")
    elseif(ANDROID)
        set(PLATFORM "Android" CACHE STRING "The platform to compile for.")
    else()
        set(PLATFORM ${CMAKE_SYSTEM_NAME} CACHE STRING "The platform to compile for.")
    endif()
endif()

include(platforms/${PLATFORM}.cmake)

set_target_properties(RetroEngine PROPERTIES OUTPUT_NAME ${RETRO_OUTPUT_NAME})

if(COMPILE_OGG)
    set(OGG_DIR dependencies/${DEP_PATH}/libogg)
    add_library(
        libogg
        STATIC
        ${OGG_DIR}/src/bitwise.c
        ${OGG_DIR}/src/framing.c
    )

    target_compile_options(libogg PRIVATE ${OGG_FLAGS})

    target_include_directories(libogg PRIVATE ${OGG_DIR}/include)
    target_include_directories(RetroEngine PRIVATE ${OGG_DIR}/include)
    target_link_libraries(RetroEngine libogg)
endif()

if(COMPILE_VORBIS)
    set(VORBIS_DIR dependencies/${DEP_PATH}/libvorbis)
    set(OGG_DIR dependencies/${DEP_PATH}/libogg)
    add_library(libvorbis STATIC
        ${VORBIS_DIR}/lib/analysis.c
        ${VORBIS_DIR}/lib/barkmel.c
        ${VORBIS_DIR}/lib/bitrate.c
        ${VORBIS_DIR}/lib/block.c
        ${VORBIS_DIR}/lib/codebook.c
        ${VORBIS_DIR}/lib/envelope.c
        ${VORBIS_DIR}/lib/floor0.c
        ${VORBIS_DIR}/lib/floor1.c
        ${VORBIS_DIR}/lib/info.c
        ${VORBIS_DIR}/lib/lookup.c
        ${VORBIS_DIR}/lib/lpc.c
        ${VORBIS_DIR}/lib/lsp.c
        ${VORBIS_DIR}/lib/mapping0.c
        ${VORBIS_DIR}/lib/mdct.c
        ${VORBIS_DIR}/lib/psy.c
        ${VORBIS_DIR}/lib/registry.c
        ${VORBIS_DIR}/lib/res0.c
        ${VORBIS_DIR}/lib/sharedbook.c
        ${VORBIS_DIR}/lib/smallft.c
        ${VORBIS_DIR}/lib/synthesis.c
        ${VORBIS_DIR}/lib/tone.c
        ${VORBIS_DIR}/lib/vorbisenc.c
        ${VORBIS_DIR}/lib/vorbisfile.c
        ${VORBIS_DIR}/lib/window.c
    )

    target_compile_options(libvorbis PRIVATE ${VORBIS_FLAGS})

    target_include_directories(libvorbis
    PRIVATE
    ${VORBIS_DIR}/include
    ${VORBIS_DIR}/lib
    ${OGG_DIR}/include
    )
    target_include_directories(RetroEngine PRIVATE ${VORBIS_DIR}/include)
    target_link_libraries(RetroEngine libvorbis libogg)
endif()

target_include_directories(RetroEngine PRIVATE
    RSDKv4/
    RSDKv4/NativeObjects/
    dependencies/all/asio/asio/include/
    dependencies/all/stb-image/
    dependencies/all/tinyxml2/
    dependencies/all/theoraplay/
)

if(DEFINED DEP_PATH)
    target_include_directories(RetroEngine PRIVATE
        dependencies/${DEP_PATH}/
    )
endif()
