# SPDX-FileCopyrightText: Copyright (c) 2023 NVIDIA CORPORATION & AFFILIATES. All rights reserved.
# SPDX-License-Identifier: Apache-2.0
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
cmake_minimum_required(VERSION 3.20)
project(v4l2_plus_source)

find_package(holoscan 0.5 REQUIRED CONFIG
             PATHS "/opt/nvidia/holoscan" "/workspace/holoscan-sdk/install")

add_library(v4l2_plus_source SHARED
v4l2_plus_source.hpp
v4l2_plus_source.cpp
  )
add_library(holoscan::v4l2_plus_source ALIAS v4l2_plus_source)
target_include_directories(v4l2_plus_source INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(v4l2_plus_source holoscan::core)

if(HOLOHUB_BUILD_PYTHON)
    add_subdirectory(python)
endif()
