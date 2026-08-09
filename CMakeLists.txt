cmake_minimum_required(VERSION 3.20)
project(playdia C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_FLAGS_RELEASE "/O2")

set(VCPKG_TARGET_TRIPLET "x64-windows-static")

find_package(SDL2 CONFIG REQUIRED)
find_package(FFMPEG REQUIRED)
find_package(libzip REQUIRED)

add_executable(playdia
    src/main.c
    src/cpu_tlcs870.c
    src/cpu_nec78k.c
    src/cdrom.c
    src/ak8000.c
    src/zip_stream.c
    src/interconnect.c
    src/pipeline.c
    src/bios_hle.c
    src/playdia_sys.c
    src/sdl_frontend.c
)

target_include_directories(playdia PRIVATE src)

target_link_libraries(playdia PRIVATE
    SDL2::SDL2
    SDL2::SDL2main
    FFMPEG::avcodec
    FFMPEG::avutil
    FFMPEG::swscale
    libzip::zip
)
