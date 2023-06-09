# Copyright (c) 2021, Technische Universität Kaiserslautern
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:
#
# 1. Redistributions of source code must retain the above copyright notice,
#    this list of conditions and the following disclaimer.
#
# 2. Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
#
# 3. Neither the name of the copyright holder nor the names of its
#    contributors may be used to endorse or promote products derived from
#    this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED
# TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
# PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER
# OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
# EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
# PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
# PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
# LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
# NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
# SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
# Authors:
#   Derek Christ

set(JSON_BuildTests OFF CACHE INTERNAL "")
set(JSON_ImplicitConversions OFF CACHE INTERNAL "")
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/../third_party/nlohmann ${CMAKE_CURRENT_BINARY_DIR}/nlohmann)

option(DRAMSYS_CONFIGURATION_TESTS "Build the unit tests for configuration." OFF)

if (DRAMSYS_CONFIGURATION_TESTS)
    add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/tests)
endif()

add_library(DRAMSysConfiguration STATIC
    DRAMSysConfiguration.cpp
    AddressMapping.cpp
    McConfig.cpp
    SimConfig.cpp
    ThermalConfig.cpp
    TraceSetup.cpp
    memspec/MemSpec.cpp
    memspec/MemArchitectureSpec.cpp
    memspec/MemPowerSpec.cpp
    memspec/MemTimingSpec.cpp
    util.cpp
)

target_compile_definitions(DRAMSysConfiguration PUBLIC DRAMSysResourceDirectory="${CMAKE_CURRENT_LIST_DIR}/../../../resources")

target_include_directories(DRAMSysConfiguration PUBLIC ${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(DRAMSysConfiguration PUBLIC nlohmann_json::nlohmann_json)
