# Copyright (c) 2020-2025 Intel Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.5.0...3.31.3)

project(fractal CXX)

include(../../common/cmake/common.cmake)

set_common_project_settings(tbb)

add_executable(fractal fractal.cpp main.cpp ) 

add_subdirectory(../../common/gui gui)

target_link_libraries(fractal PUBLIC TBB::tbb Threads::Threads UI_LIB_fractal)
target_compile_options(fractal PRIVATE ${TBB_CXX_STD_FLAG})

set(EXECUTABLE "$<TARGET_FILE:fractal>")
set(ARGS auto)
set(PERF_ARGS auto 1 1000000 silent)
set(LIGHT_ARGS auto 1 1000)

add_execution_target(run_fractal fractal ${EXECUTABLE} "${ARGS}")
add_execution_target(perf_run_fractal fractal ${EXECUTABLE} "${PERF_ARGS}")
add_execution_target(light_test_fractal fractal ${EXECUTABLE} "${LIGHT_ARGS}")
