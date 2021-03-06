cmake_minimum_required(VERSION 2.8.12)

project(dpScreenOCR)

set(DPSO_UI "qt" CACHE STRING "UI to use: qt or none")
option(DPSO_ENABLE_NLS "Enable native language support" YES)
option(DPSO_GEN_HTML_MANUAL "Generate HTML manual. Requires Pandoc." YES)
option(DPSO_BUILD_EXAMPLE "Build example" NO)
option(DPSO_BUILD_TESTS "Build tests" NO)

set(APP_NAME "dpScreenOCR")
set(APP_FILE_NAME "dpscreenocr")

set(APP_VERSION_MAJOR "1")
set(APP_VERSION_MINOR "0")
set(APP_VERSION_PATCH "2")
set(APP_VERSION "${APP_VERSION_MAJOR}.${APP_VERSION_MINOR}.${APP_VERSION_PATCH}")

set(APP_AUTHOR "Daniel Plakhotich")
set(APP_COPYRIGHT_YEAR "2019-2020")
set(APP_URL "https://danpla.github.io/dpscreenocr/")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")

add_subdirectory(src/dpso)
if (DPSO_BUILD_EXAMPLE)
    add_subdirectory(src/dpso_example)
endif()

add_subdirectory(src/dpso_utils)

if (DPSO_UI STREQUAL "qt")
    add_subdirectory(src/ui/qt)
elseif (DPSO_UI STREQUAL "none")
else()
    message(FATAL_ERROR "Unknown UI \"${DPSO_UI}\"")
endif()

if (DPSO_BUILD_TESTS)
    add_subdirectory(tests)
endif()

include(install)
include(uninstall)
include(dist)
