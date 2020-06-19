set(CMAKE_VERBOSE_MAKEFILE True)
cmake_minimum_required(VERSION 3.15)
cmake_policy(VERSION 3.15)
set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake" ${CMAKE_MODULE_PATH})

set(NALL_VERSION "0.110.1")
set(NALL_VERSION_MAJOR "0")
set(NALL_ROOT ${CMAKE_CURRENT_SOURCE_DIR})
set(NALL_INCLUDE_ROOT ${NALL_ROOT}/nall)

project(nall
    LANGUAGES CXX
    VERSION ${NALL_VERSION}
    #    SOVERSION ${NALL_VERSION_MAJOR}
    DESCRIPTION "BYUU- nall Library"
)

# Only do these if this is the main project, and not if it is included through add_subdirectory
if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    # Optionally set things like CMAKE_CXX_STANDARD, CMAKE_POSITION_INDEPENDENT_CODE here
    set(CMAKE_CXX_STANDARD 17)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)
    set(CMAKE_POSITION_INDEPENDENT_CODE ON)

    # Let's ensure -std=c++xx instead of -std=g++xx
    set(CMAKE_CXX_EXTENSIONS OFF)

    # Let's nicely support folders in IDE's
    set_property(GLOBAL PROPERTY USE_FOLDERS ON)


    # Docs only available if this is the main app
    find_package(Doxygen)
    if(Doxygen_FOUND)
        add_subdirectory(docs)
    else()
        message(STATUS "Doxygen not found, not building docs")
    endif()
endif()

set(SOURCE_FILES
    ${NALL_INCLUDE_ROOT}/database/sqlite3.hpp
    ${NALL_INCLUDE_ROOT}/database/odbc.hpp
    ${NALL_INCLUDE_ROOT}/inline-if.hpp
    ${NALL_INCLUDE_ROOT}/instance.hpp
    ${NALL_INCLUDE_ROOT}/posix/service.hpp
    ${NALL_INCLUDE_ROOT}/posix/shared-memory.hpp
    ${NALL_INCLUDE_ROOT}/adaptive-array.hpp
    ${NALL_INCLUDE_ROOT}/vfs/memory/file.hpp
    ${NALL_INCLUDE_ROOT}/vfs/vfs.hpp
    ${NALL_INCLUDE_ROOT}/vfs/fs/file.hpp
    ${NALL_INCLUDE_ROOT}/vfs/fs/cdrom.hpp
    ${NALL_INCLUDE_ROOT}/file-map.hpp
    ${NALL_INCLUDE_ROOT}/serializer.hpp
    ${NALL_INCLUDE_ROOT}/hashset.hpp
    ${NALL_INCLUDE_ROOT}/array-span.hpp
    ${NALL_INCLUDE_ROOT}/suffix-array.hpp
    ${NALL_INCLUDE_ROOT}/macos/guard.hpp
    ${NALL_INCLUDE_ROOT}/utility.hpp
    ${NALL_INCLUDE_ROOT}/reed-solomon.hpp
    ${NALL_INCLUDE_ROOT}/main.hpp
    ${NALL_INCLUDE_ROOT}/vfs.hpp
    ${NALL_INCLUDE_ROOT}/nall.hpp
    ${NALL_INCLUDE_ROOT}/hash/sha384.hpp
    ${NALL_INCLUDE_ROOT}/hash/hash.hpp
    ${NALL_INCLUDE_ROOT}/hash/sha224.hpp
    ${NALL_INCLUDE_ROOT}/hash/crc64.hpp
    ${NALL_INCLUDE_ROOT}/hash/sha256.hpp
    ${NALL_INCLUDE_ROOT}/hash/crc16.hpp
    ${NALL_INCLUDE_ROOT}/hash/crc32.hpp
    ${NALL_INCLUDE_ROOT}/hash/sha512.hpp
    ${NALL_INCLUDE_ROOT}/varint.hpp
    ${NALL_INCLUDE_ROOT}/function.hpp
    ${NALL_INCLUDE_ROOT}/array.hpp
    ${NALL_INCLUDE_ROOT}/emulation/21fx.hpp
    ${NALL_INCLUDE_ROOT}/vector.hpp
    ${NALL_INCLUDE_ROOT}/traits.hpp
    ${NALL_INCLUDE_ROOT}/interpolation.hpp
    ${NALL_INCLUDE_ROOT}/map.hpp
    ${NALL_INCLUDE_ROOT}/beat/archive/container.hpp
    ${NALL_INCLUDE_ROOT}/beat/archive/extract.hpp
    ${NALL_INCLUDE_ROOT}/beat/archive/create.hpp
    ${NALL_INCLUDE_ROOT}/beat/archive/node.hpp
    ${NALL_INCLUDE_ROOT}/beat/single/apply.hpp
    ${NALL_INCLUDE_ROOT}/beat/single/create.hpp
    ${NALL_INCLUDE_ROOT}/elliptic-curve/modulo25519-optimized.hpp
    ${NALL_INCLUDE_ROOT}/elliptic-curve/curve25519.hpp
    ${NALL_INCLUDE_ROOT}/elliptic-curve/ed25519.hpp
    ${NALL_INCLUDE_ROOT}/elliptic-curve/modulo25519-reference.hpp
    ${NALL_INCLUDE_ROOT}/arithmetic.hpp
    ${NALL_INCLUDE_ROOT}/bit.hpp
    ${NALL_INCLUDE_ROOT}/file.hpp
    ${NALL_INCLUDE_ROOT}/inode.hpp
    ${NALL_INCLUDE_ROOT}/intrinsics.hpp
    ${NALL_INCLUDE_ROOT}/xorg/clipboard.hpp
    ${NALL_INCLUDE_ROOT}/xorg/xorg.hpp
    ${NALL_INCLUDE_ROOT}/xorg/guard.hpp
    ${NALL_INCLUDE_ROOT}/service.hpp
    ${NALL_INCLUDE_ROOT}/serial.hpp
    ${NALL_INCLUDE_ROOT}/terminal.hpp
    ${NALL_INCLUDE_ROOT}/cipher/chacha20.hpp
    ${NALL_INCLUDE_ROOT}/algorithm.hpp
    ${NALL_INCLUDE_ROOT}/primitives.hpp
    ${NALL_INCLUDE_ROOT}/queue.hpp
    ${NALL_INCLUDE_ROOT}/literals.hpp
    ${NALL_INCLUDE_ROOT}/variant.hpp
    ${NALL_INCLUDE_ROOT}/shared-pointer.hpp
    ${NALL_INCLUDE_ROOT}/encode/huffman.hpp
    ${NALL_INCLUDE_ROOT}/encode/zip.hpp
    ${NALL_INCLUDE_ROOT}/encode/bwt.hpp
    ${NALL_INCLUDE_ROOT}/encode/wav.hpp
    ${NALL_INCLUDE_ROOT}/encode/mtf.hpp
    ${NALL_INCLUDE_ROOT}/encode/rle.hpp
    ${NALL_INCLUDE_ROOT}/encode/url.hpp
    ${NALL_INCLUDE_ROOT}/encode/base.hpp
    ${NALL_INCLUDE_ROOT}/encode/html.hpp
    ${NALL_INCLUDE_ROOT}/encode/lzsa.hpp
    ${NALL_INCLUDE_ROOT}/encode/bmp.hpp
    ${NALL_INCLUDE_ROOT}/encode/base64.hpp
    ${NALL_INCLUDE_ROOT}/matrix.hpp
    ${NALL_INCLUDE_ROOT}/dl.hpp
    ${NALL_INCLUDE_ROOT}/path.hpp
    ${NALL_INCLUDE_ROOT}/platform.hpp
    ${NALL_INCLUDE_ROOT}/pointer.hpp
    ${NALL_INCLUDE_ROOT}/galois-field.hpp
    ${NALL_INCLUDE_ROOT}/image/load.hpp
    ${NALL_INCLUDE_ROOT}/image/static.hpp
    ${NALL_INCLUDE_ROOT}/image/scale.hpp
    ${NALL_INCLUDE_ROOT}/image/utility.hpp
    ${NALL_INCLUDE_ROOT}/image/interpolation.hpp
    ${NALL_INCLUDE_ROOT}/image/blend.hpp
    ${NALL_INCLUDE_ROOT}/image/fill.hpp
    ${NALL_INCLUDE_ROOT}/image/core.hpp
    ${NALL_INCLUDE_ROOT}/induced-sort.hpp
    ${NALL_INCLUDE_ROOT}/primitives/integer.hpp
    ${NALL_INCLUDE_ROOT}/primitives/boolean.hpp
    ${NALL_INCLUDE_ROOT}/primitives/bit-field.hpp
    ${NALL_INCLUDE_ROOT}/primitives/real.hpp
    ${NALL_INCLUDE_ROOT}/primitives/literals.hpp
    ${NALL_INCLUDE_ROOT}/primitives/natural.hpp
    ${NALL_INCLUDE_ROOT}/primitives/bit-range.hpp
    ${NALL_INCLUDE_ROOT}/primitives/types.hpp
    ${NALL_INCLUDE_ROOT}/property.hpp
    ${NALL_INCLUDE_ROOT}/array-view.hpp
    ${NALL_INCLUDE_ROOT}/random.hpp
    ${NALL_INCLUDE_ROOT}/mac/poly1305.hpp
    ${NALL_INCLUDE_ROOT}/decode/huffman.hpp
    ${NALL_INCLUDE_ROOT}/decode/zip.hpp
    ${NALL_INCLUDE_ROOT}/decode/bwt.hpp
    ${NALL_INCLUDE_ROOT}/decode/mtf.hpp
    ${NALL_INCLUDE_ROOT}/decode/rle.hpp
    ${NALL_INCLUDE_ROOT}/decode/png.hpp
    ${NALL_INCLUDE_ROOT}/decode/url.hpp
    ${NALL_INCLUDE_ROOT}/decode/base.hpp
    ${NALL_INCLUDE_ROOT}/decode/gzip.hpp
    ${NALL_INCLUDE_ROOT}/decode/html.hpp
    ${NALL_INCLUDE_ROOT}/decode/lzsa.hpp
    ${NALL_INCLUDE_ROOT}/decode/inflate.hpp
    ${NALL_INCLUDE_ROOT}/decode/bmp.hpp
    ${NALL_INCLUDE_ROOT}/decode/base64.hpp
    ${NALL_INCLUDE_ROOT}/any.hpp
    ${NALL_INCLUDE_ROOT}/endian.hpp
    ${NALL_INCLUDE_ROOT}/unique-pointer.hpp
    ${NALL_INCLUDE_ROOT}/run.hpp
    ${NALL_INCLUDE_ROOT}/set.hpp
    ${NALL_INCLUDE_ROOT}/http/server.hpp
    ${NALL_INCLUDE_ROOT}/http/response.hpp
    ${NALL_INCLUDE_ROOT}/http/role.hpp
    ${NALL_INCLUDE_ROOT}/http/request.hpp
    ${NALL_INCLUDE_ROOT}/http/client.hpp
    ${NALL_INCLUDE_ROOT}/http/message.hpp
    ${NALL_INCLUDE_ROOT}/hid.hpp
    ${NALL_INCLUDE_ROOT}/stdint.hpp
    ${NALL_INCLUDE_ROOT}/string.hpp
    ${NALL_INCLUDE_ROOT}/location.hpp
    ${NALL_INCLUDE_ROOT}/chrono.hpp
    ${NALL_INCLUDE_ROOT}/view.hpp
    ${NALL_INCLUDE_ROOT}/atoi.hpp
    ${NALL_INCLUDE_ROOT}/directory.hpp
    ${NALL_INCLUDE_ROOT}/arithmetic/barrett.hpp
    ${NALL_INCLUDE_ROOT}/arithmetic/unsigned.hpp
    ${NALL_INCLUDE_ROOT}/arithmetic/natural.hpp
    ${NALL_INCLUDE_ROOT}/file-buffer.hpp
    ${NALL_INCLUDE_ROOT}/smtp.hpp
    ${NALL_INCLUDE_ROOT}/string/cast.hpp
    ${NALL_INCLUDE_ROOT}/string/utility.hpp
    ${NALL_INCLUDE_ROOT}/string/utf8.hpp
    ${NALL_INCLUDE_ROOT}/string/vector.hpp
    ${NALL_INCLUDE_ROOT}/string/pascal.hpp
    ${NALL_INCLUDE_ROOT}/string/trim.hpp
    ${NALL_INCLUDE_ROOT}/string/replace.hpp
    ${NALL_INCLUDE_ROOT}/string/markup/bml.hpp
    ${NALL_INCLUDE_ROOT}/string/markup/xml.hpp
    ${NALL_INCLUDE_ROOT}/string/markup/node.hpp
    ${NALL_INCLUDE_ROOT}/string/markup/find.hpp
    ${NALL_INCLUDE_ROOT}/string/find.hpp
    ${NALL_INCLUDE_ROOT}/string/match.hpp
    ${NALL_INCLUDE_ROOT}/string/allocator/adaptive.hpp
    ${NALL_INCLUDE_ROOT}/string/allocator/vector.hpp
    ${NALL_INCLUDE_ROOT}/string/allocator/copy-on-write.hpp
    ${NALL_INCLUDE_ROOT}/string/allocator/small-string-optimization.hpp
    ${NALL_INCLUDE_ROOT}/string/view.hpp
    ${NALL_INCLUDE_ROOT}/string/atoi.hpp
    ${NALL_INCLUDE_ROOT}/string/eval/parser.hpp
    ${NALL_INCLUDE_ROOT}/string/eval/literal.hpp
    ${NALL_INCLUDE_ROOT}/string/eval/node.hpp
    ${NALL_INCLUDE_ROOT}/string/eval/evaluator.hpp
    ${NALL_INCLUDE_ROOT}/string/transform/dml.hpp
    ${NALL_INCLUDE_ROOT}/string/transform/cml.hpp
    ${NALL_INCLUDE_ROOT}/string/compare.hpp
    ${NALL_INCLUDE_ROOT}/string/format.hpp
    ${NALL_INCLUDE_ROOT}/string/core.hpp
    ${NALL_INCLUDE_ROOT}/string/split.hpp
    ${NALL_INCLUDE_ROOT}/string/convert.hpp
    ${NALL_INCLUDE_ROOT}/cd/edc.hpp
    ${NALL_INCLUDE_ROOT}/cd/efm.hpp
    ${NALL_INCLUDE_ROOT}/cd/scrambler.hpp
    ${NALL_INCLUDE_ROOT}/cd/session.hpp
    ${NALL_INCLUDE_ROOT}/cd/crc16.hpp
    ${NALL_INCLUDE_ROOT}/cd/rspc.hpp
    ${NALL_INCLUDE_ROOT}/cd/sync.hpp
    ${NALL_INCLUDE_ROOT}/memory.hpp
    ${NALL_INCLUDE_ROOT}/cd.hpp
    ${NALL_INCLUDE_ROOT}/maybe.hpp
    ${NALL_INCLUDE_ROOT}/windows/guid.hpp
    ${NALL_INCLUDE_ROOT}/windows/utf8.hpp
    ${NALL_INCLUDE_ROOT}/windows/launcher.hpp
    ${NALL_INCLUDE_ROOT}/windows/registry.hpp
    ${NALL_INCLUDE_ROOT}/windows/detour.hpp
    ${NALL_INCLUDE_ROOT}/windows/service.hpp
    ${NALL_INCLUDE_ROOT}/windows/guard.hpp
    ${NALL_INCLUDE_ROOT}/windows/shared-memory.hpp
    ${NALL_INCLUDE_ROOT}/thread.hpp
    ${NALL_INCLUDE_ROOT}/merge-sort.hpp
    ${NALL_INCLUDE_ROOT}/counting-sort.hpp
    ${NALL_INCLUDE_ROOT}/range.hpp
    ${NALL_INCLUDE_ROOT}/dsp/resampler/cubic.hpp
    ${NALL_INCLUDE_ROOT}/dsp/dsp.hpp
    ${NALL_INCLUDE_ROOT}/dsp/iir/one-pole.hpp
    ${NALL_INCLUDE_ROOT}/dsp/iir/biquad.hpp
    ${NALL_INCLUDE_ROOT}/dsp/iir/dc-removal.hpp
    ${NALL_INCLUDE_ROOT}/vector/specialization/uint8_t.hpp
    ${NALL_INCLUDE_ROOT}/vector/access.hpp
    ${NALL_INCLUDE_ROOT}/vector/utility.hpp
    ${NALL_INCLUDE_ROOT}/vector/modify.hpp
    ${NALL_INCLUDE_ROOT}/vector/assign.hpp
    ${NALL_INCLUDE_ROOT}/vector/memory.hpp
    ${NALL_INCLUDE_ROOT}/vector/compare.hpp
    ${NALL_INCLUDE_ROOT}/vector/iterator.hpp
    ${NALL_INCLUDE_ROOT}/vector/core.hpp
    ${NALL_INCLUDE_ROOT}/iterator.hpp
    ${NALL_INCLUDE_ROOT}/image.hpp
    ${NALL_INCLUDE_ROOT}/arguments.hpp
    ${NALL_INCLUDE_ROOT}/locale.hpp
    ${NALL_INCLUDE_ROOT}/simd.hpp
    ${NALL_INCLUDE_ROOT}/matrix-multiply.hpp
    ${NALL_INCLUDE_ROOT}/shared-memory.hpp
)

add_library(nall INTERFACE)
target_include_directories(nall INTERFACE ${NALL_INCLUDE_ROOT}/)