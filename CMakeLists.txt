cmake_minimum_required(VERSION 3.8)

project(iodine)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_REQUIRED_LIBRARIES ${CMAKE_REQUIRED_LIBRARIES} -static-libgcc -static-libstdc++)

##########################################
# Basic properties
##########################################

set(I_BASE_VERSION_MAJOR 0)
set(I_BASE_VERSION_MINOR 1)
set(I_BASE_VERSION_PATCH 0)
set(I_BASE_VERSION "${AL_BASE_VERSION_MAJOR}.${AL_BASE_VERSION_MINOR}.${AL_BASE_VERSION_PATCH}")

set(I_BASE_SOURCE_DIR ${PROJECT_SOURCE_DIR}/src)
set(I_BASE_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include)

set(I_BASE_SOURCE_FILES 
    #${I_BASE_SOURCE_DIR}/ActivityLogger.cpp
    #${I_BASE_SOURCE_DIR}/database/Database.cpp
    #${I_BASE_SOURCE_DIR}/worker/Worker.cpp
)

set(I_BASE_PUBLIC_HEADER_FILES
    #${I_BASE_INCLUDE_DIR}/al/ActivityLogger.h
    #${I_BASE_INCLUDE_DIR}/al/Config.hpp
)

set(I_BASE_PRIVATE_HEADER_FILES
    #${I_BASE_SOURCE_DIR}/entities/Model.hpp
    #${I_BASE_SOURCE_DIR}/entities/Action.hpp
    #${I_BASE_SOURCE_DIR}/entities/BrowserTabSwitchAction.hpp
    #${I_BASE_SOURCE_DIR}/entities/WindowSwitchAction.hpp
    #${I_BASE_SOURCE_DIR}/entities/ActionType.hpp
    #${I_BASE_SOURCE_DIR}/entities/Activity.hpp
    #${I_BASE_SOURCE_DIR}/database/Database.h
    #${I_BASE_SOURCE_DIR}/logger/Logger.hpp
    #${I_BASE_SOURCE_DIR}/worker/Worker.h
)

set(I_BASE_HEADER_FILES
    ${I_BASE_PUBLIC_HEADER_FILES}
    ${I_BASE_PRIVATE_HEADER_FILES}
)

##########################################
# Library iodine
##########################################

add_library(iodine ${I_BASE_SOURCE_FILES} ${I_BASE_HEADER_FILES})
target_include_directories(iodine PUBLIC $<BUILD_INTERFACE:${I_BASE_INCLUDE_DIR}>)

target_include_directories(iodine PRIVATE $<BUILD_INTERFACE:${I_BASE_INCLUDE_DIR}/al>)
target_include_directories(iodine PRIVATE $<BUILD_INTERFACE:${I_BASE_SOURCE_DIR}>)

include(GenerateExportHeader)
generate_export_header(iodine
    EXPORT_FILE_NAME ${PROJECT_BINARY_DIR}/generated/i_Export.h
    PREFIX_NAME I_LIBRARY_
)

set(I_BASE_GENERATE_HEADER_FILES ${PROJECT_BINARY_DIR}/generated/i_Export.h)
target_include_directories(iodine PUBLIC $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}/generated>)

set_property(TARGET iodine PROPERTY VERSION ${AL_BASE_VERSION})
set_property(TARGET iodine PROPERTY SOVERSION ${AL_BASE_VERSION_MAJOR})
set_property(TARGET iodine PROPERTY DEBUG_POSTFIX d)

##########################################
# Packaging iodine
##########################################

# do nothing at this time

