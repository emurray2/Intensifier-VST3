
cmake_minimum_required (VERSION 3.4.3)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../vst3sdk/cmake/modules")

include(SMTG_VST3_SDK)

project(intensifier)

smtg_setup_platform_toolset()

set(ROOT "${CMAKE_CURRENT_SOURCE_DIR}")

set(SDK_ROOT "${ROOT}/../vst3sdk")
set(public_sdk_SOURCE_DIR ${SDK_ROOT}/public.sdk)
set(pluginterfaces_SOURCE_DIR ${SDK_ROOT}/pluginterfaces)

message(STATUS "[SMTG] CMAKE_SOURCE_DIR is set to: ${CMAKE_SOURCE_DIR}")
message(STATUS "[SMTG] CMAKE_CURRENT_LIST_DIR is set to: ${CMAKE_CURRENT_LIST_DIR}")

set(SMTG_ADD_VST3_PLUGINS_SAMPLES OFF)
set(SMTG_ADD_VST3_HOSTING_SAMPLES OFF)
set(SMTG_ADD_MYPLUGINS_SRC_PATH OFF)

if(SMTG_ADD_VSTGUI)
    set(SMTG_VSTGUI_ROOT "${SDK_ROOT}")
    smtg_enable_vstgui_support()
endif(SMTG_ADD_VSTGUI)

include_directories(${ROOT} ${SDK_ROOT})

set(VST_SDK TRUE) # used for pluginterfaces and public.sdk modules which provides only a subset of them for VST-SDK
add_subdirectory(${SDK_ROOT}/pluginterfaces)
add_subdirectory(${SDK_ROOT}/base)
add_subdirectory(${SDK_ROOT}/public.sdk)
add_subdirectory(${SDK_ROOT}/public.sdk/source/vst/interappaudio)

set(SDK_IDE_HOSTING_EXAMPLES_FOLDER FOLDER "${SDK_ROOT}/HostingExamples")
add_subdirectory(${SDK_ROOT}/public.sdk/samples/vst-hosting)
