project(CoralNative
  VERSION 1.0.0
  DESCRIPTION "C++/C# wrapper around the .NET CoreCLR library, the purpose of Coral is to provide a native interface similar to Mono, but in a more modern style, and using .NET Core instead of .NET Framework "
  HOMEPAGE_URL "https://github.com/StudioCherno/Coral"
  LANGUAGES CXX C
)

set(TARGET_NAME Coral.Native)

file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/**.h
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/**.hpp
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.c
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.h
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.hpp
)

add_library(${TARGET_NAME} STATIC ${SRC_FILES})
add_library(CoralNative ALIAS ${TARGET_NAME})

target_precompile_headers(${TARGET_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/Source/CoralPCH.hpp)

if(WIN32)
  set(CORAL_PLAT "CORAL_WINDOWS")
endif()

target_compile_definitions(${TARGET_NAME} PUBLIC "_CRT_SECURE_NO_WARNINGS" "${CORAL_PLAT}")

target_include_directories(${TARGET_NAME} PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/Coral
  ${CMAKE_CURRENT_SOURCE_DIR}/Include
  ${CMAKE_CURRENT_SOURCE_DIR}/Source
  ${CMAKE_CURRENT_SOURCE_DIR}/../NetCore
)

target_include_directories(${TARGET_NAME} PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/Coral
  ${CMAKE_CURRENT_SOURCE_DIR}/Include
  ${CMAKE_CURRENT_SOURCE_DIR}/Source
  ${CMAKE_CURRENT_SOURCE_DIR}/../NetCore
)

set_target_properties(
  ${TARGET_NAME} PROPERTIES
  CXX_VISIBILITY_PRESET hidden
  VISIBILITY_INLINES_HIDDEN YES
  VERSION "${PROJECT_VERSION}"
  SOVERSION "${PROJECT_VERSION_MAJOR}"
  OUTPUT_NAME ${TARGET_NAME}
  DEBUG_POSTFIX "d"
)