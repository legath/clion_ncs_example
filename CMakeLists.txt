# SPDX-License-Identifier: Apache-2.0
cmake_minimum_required(VERSION 3.13.1)


if (DEFINED ENV{ZEPHYR_BASE})
    SET(ZEPHYR_BASE $ENV{ZEPHYR_BASE})
else ()
    message(FATAL_ERROR "Please set correct ZEPHYR_BASE environment variable")
endif ()

if (DEFINED ENV{GNUARMEMB_TOOLCHAIN_PATH})
    SET(GNUARMEMB_TOOLCHAIN_PATH $ENV{GNUARMEMB_TOOLCHAIN_PATH})
else ()
    message(FATAL_ERROR "Please set correct GNUARMEMB_TOOLCHAIN_PATH environment variable")
endif ()

set(ENV{BOARD} nrf52833dk_nrf52833)
set(ENV{BOARD_DIR} $ENV{ZEPHYR_BASE}/boards/arm/nrf52833dk_nrf52833)

set(ENV{ZEPHYR_TOOLCHAIN_VARIANT} gnuarmemb)

set(ENV{CMAKE_AR} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-ar)
set(ENV{CMAKE_AS} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-as)
set(ENV{CMAKE_ASM_COMPILER} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-gcc)
set(ENV{CMAKE_ASM_COMPILER_AR} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-gcc-ar)
set(ENV{CMAKE_ASM_COMPILER_RANLIB} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-gcc-ranlib)

set(ENV{CMAKE_ASM_FLAGS_DEBUG} -g)
set(ENV{CMAKE_ASM_FLAGS_MINSIZEREL} -Os -DNDEBUG)
set(ENV{CMAKE_ASM_FLAGS_RELEASE} -O3 -DNDEBUG)
set(ENV{CMAKE_ASM_FLAGS_RELWITHDEBINFO} -O2 -g -DNDEBUG)

set(ENV{CMAKE_CXX_COMPILER} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-g++)
set(ENV{CMAKE_CXX_COMPILER_AR} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-gcc-ar)
set(ENV{CMAKE_CXX_COMPILER_RANLIB} $ENV{GNUARMEMB_TOOLCHAIN_PATH}/bin/arm-none-eabi-gcc-ranlib)

find_package(Zephyr HINTS $ENV{ZEPHYR_BASE})
project(blinky)

target_sources(app PRIVATE src/main.c)
