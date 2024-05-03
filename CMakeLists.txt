# SPDX-License-Identifier: GPL-3.0-only
# Copyright (c) 2023 CERN
#
# Please retain this header in all redistributions and modifications of the code.

cmake_minimum_required(VERSION 3.25)
project(simjtag NONE)

add_ip(simjtag
    VENDOR pulp_platform
    LIBRARY dpi
    VERSION 7.0.0
    )

ip_include_directories(${IP} SYSTEMVERILOG
    ${PROJECT_SOURCE_DIR}/src
    ${PROJECT_SOURCE_DIR}/rtl/tb/remote_bitbang
)

ip_sources(${IP} SYSTEMVERILOG
    ${PROJECT_SOURCE_DIR}/rtl/tb/SimJTAG.sv
    ${PROJECT_SOURCE_DIR}/rtl/tb/remote_bitbang/sim_jtag.c
    ${PROJECT_SOURCE_DIR}/rtl/tb/remote_bitbang/remote_bitbang.c
)

# How to include them properly?
# ${PROJECT_SOURCE_DIR}/rtl/tb/remote_bitbang/sim_jtag.c
# ${PROJECT_SOURCE_DIR}/rtl/tb/remote_bitbang/sim_jtag.h
# ${PROJECT_SOURCE_DIR}/rtl/tb/remote_bitbang/remote_bitbang.c
# ${PROJECT_SOURCE_DIR}/rtl/tb/remote_bitbang/remote_bitbang.h

if(NOT PROJECT_IS_TOP_LEVEL)
    set(RTL_LIB_NAME ${IP} PARENT_SCOPE)
endif()
