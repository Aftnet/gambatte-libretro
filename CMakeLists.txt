cmake_minimum_required(VERSION 3.19)

project(gambatte-libretro)

option(GAMBATTE_STATIC_BUILD "Build as static" OFF)
option(GAMBATTE_NETWORK_SUPPORT "Enable network support for core" ON)
option(GAMBATTE_USE_RGB565 "Set core to output in RGB565 vs XRGB8888" ON)

set(TARGETNAME ${PROJECT_NAME})

if(${GAMBATTE_STATIC_BUILD})
    add_library(${TARGETNAME} STATIC "")
else()
    add_library(${TARGETNAME} SHARED "")
    target_compile_definitions(${TARGETNAME} INTERFACE RETRO_IMPORT_SYMBOLS)
endif()

target_sources(${TARGETNAME}
PUBLIC
    libgambatte/libretro-common/include/libretro.h

PRIVATE
    common/gambatte-array.h
    common/uncopyable.h
    libgambatte/include/gambatte.h
    libgambatte/include/gbint.h
    libgambatte/include/inputgetter.h
    libgambatte/libretro/blipper.h
    libgambatte/libretro/cc_resampler.h
    libgambatte/libretro/gbcpalettes.h
    libgambatte/libretro/libretro_core_options_intl.h
    libgambatte/libretro/libretro_core_options.h
    libgambatte/libretro/net_serial.h
    libgambatte/libretro-common/include/array/rhmap.h
    libgambatte/libretro-common/include/compat/msvc/stdint.h
    libgambatte/libretro-common/include/compat/fopen_utf8.h
    libgambatte/libretro-common/include/compat/msvc.h
    libgambatte/libretro-common/include/compat/posix_string.h
    libgambatte/libretro-common/include/compat/strcasestr.h
    libgambatte/libretro-common/include/compat/strl.h
    libgambatte/libretro-common/include/encodings/utf.h
    libgambatte/libretro-common/include/file/file_path.h
    libgambatte/libretro-common/include/streams/file_stream.h
    libgambatte/libretro-common/include/string/stdstring.h
    libgambatte/libretro-common/include/time/rtime.h
    libgambatte/libretro-common/include/vfs/vfs_implementation.h
    libgambatte/libretro-common/include/vfs/vfs.h
    libgambatte/libretro-common/include/boolean.h
    libgambatte/libretro-common/include/libretro.h
    libgambatte/libretro-common/include/memmap.h
    libgambatte/libretro-common/include/retro_assert.h
    libgambatte/libretro-common/include/retro_common_api.h
    libgambatte/libretro-common/include/retro_environment.h
    libgambatte/libretro-common/include/retro_inline.h
    libgambatte/libretro-common/include/retro_miscellaneous.h
    libgambatte/src/mem/cartridge.h
    libgambatte/src/mem/huc3.h
    libgambatte/src/mem/memptrs.h
    libgambatte/src/mem/rtc.h
    libgambatte/src/sound/channel1.h
    libgambatte/src/sound/channel2.h
    libgambatte/src/sound/channel3.h
    libgambatte/src/sound/channel4.h
    libgambatte/src/sound/duty_unit.h
    libgambatte/src/sound/envelope_unit.h
    libgambatte/src/sound/length_counter.h
    libgambatte/src/sound/master_disabler.h
    libgambatte/src/sound/sound_unit.h
    libgambatte/src/sound/static_output_tester.h
    libgambatte/src/video/lcddef.h
    libgambatte/src/video/ly_counter.h
    libgambatte/src/video/lyc_irq.h
    libgambatte/src/video/m0_irq.h
    libgambatte/src/video/next_m0_time.h
    libgambatte/src/video/ppu.h
    libgambatte/src/video/sprite_mapper.h
    libgambatte/src/bootloader.h
    libgambatte/src/counterdef.h
    libgambatte/src/cpu.h
    libgambatte/src/gambatte-memory.h
    libgambatte/src/initstate.h
    libgambatte/src/insertion_sort.h
    libgambatte/src/interrupter.h
    libgambatte/src/interruptrequester.h
    libgambatte/src/minkeeper.h
    libgambatte/src/savestate.h
    libgambatte/src/serial_io.h
    libgambatte/src/sound.h
    libgambatte/src/statesaver.h
    libgambatte/src/tima.h
    libgambatte/src/video.h

    libgambatte/src/bootloader.cpp
    libgambatte/src/cpu.cpp
    libgambatte/src/gambatte.cpp
    libgambatte/src/initstate.cpp
    libgambatte/src/interrupter.cpp
    libgambatte/src/interruptrequester.cpp
    libgambatte/src/gambatte-memory.cpp
    libgambatte/src/sound.cpp
    libgambatte/src/statesaver.cpp
    libgambatte/src/tima.cpp
    libgambatte/src/video.cpp
    libgambatte/src/video_libretro.cpp
    libgambatte/src/mem/cartridge.cpp
    libgambatte/src/mem/cartridge_libretro.cpp
    libgambatte/src/mem/huc3.cpp
    libgambatte/src/mem/memptrs.cpp
    libgambatte/src/mem/rtc.cpp
    libgambatte/src/sound/channel1.cpp
    libgambatte/src/sound/channel2.cpp
    libgambatte/src/sound/channel3.cpp
    libgambatte/src/sound/channel4.cpp
    libgambatte/src/sound/duty_unit.cpp
    libgambatte/src/sound/envelope_unit.cpp
    libgambatte/src/sound/length_counter.cpp
    libgambatte/src/video/ly_counter.cpp
    libgambatte/src/video/lyc_irq.cpp
    libgambatte/src/video/next_m0_time.cpp
    libgambatte/src/video/ppu.cpp
    libgambatte/src/video/sprite_mapper.cpp
    libgambatte/libretro/libretro.cpp
    libgambatte/libretro/blipper.c
    libgambatte/libretro-common/streams/file_stream.c
    libgambatte/libretro-common/compat/fopen_utf8.c
    libgambatte/libretro-common/compat/compat_strl.c
    libgambatte/libretro-common/compat/compat_snprintf.c
    libgambatte/libretro-common/compat/compat_posix_string.c
    libgambatte/libretro-common/compat/compat_strcasestr.c
    libgambatte/libretro-common/file/file_path.c
    libgambatte/libretro-common/time/rtime.c
    libgambatte/libretro-common/string/stdstring.c
    libgambatte/libretro-common/encodings/encoding_utf.c
    libgambatte/libretro-common/vfs/vfs_implementation.c
)

target_include_directories(${TARGETNAME}
PUBLIC
    libgambatte/libretro-common/include/
PRIVATE
    common
    libgambatte/include
    libgambatte/libretro
    libgambatte/src
)

target_compile_definitions(${TARGETNAME}
PRIVATE
    __LIBRETRO__ 
    HAVE_STDINT_H
    HAVE_INTTYPES_H
)

if(${GAMBATTE_USE_RGB565})
    target_compile_definitions(${TARGETNAME} PRIVATE VIDEO_RGB565)
endif()

if(${GAMBATTE_NETWORK_SUPPORT})
    target_sources(${TARGETNAME} PRIVATE libgambatte/libretro/net_serial.cpp)
    target_compile_definitions(${TARGETNAME} PRIVATE HAVE_NETWORK)
    if(${CMAKE_SYSTEM_NAME} STREQUAL Windows)
        target_link_libraries(${TARGETNAME} PRIVATE Ws2_32.lib)
    endif()
endif()

if(MSVC)
    target_compile_definitions(${TARGETNAME} PRIVATE _CRT_SECURE_NO_WARNINGS)
    target_compile_options(${TARGETNAME} PRIVATE /sdl-)
endif()
