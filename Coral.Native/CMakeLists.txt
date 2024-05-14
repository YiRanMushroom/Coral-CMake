set(TARGET_NAME CoralNative)

file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/**.h
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/**.hpp
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.c
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.h
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.hpp
)

add_library(${TARGET_NAME} STATIC ${SRC_FILES})

target_precompile_headers(${TARGET_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/Source/CoralPCH.hpp)

target_compile_definitions(${TARGET_NAME} PUBLIC "_CRT_SECURE_NO_WARNINGS")


includedirs { "Source/", "Include/Coral/" }
externalincludedirs { "../NetCore/" }


target_include_directories(${TARGET_NAME} PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/Coral
  ${CMAKE_CURRENT_SOURCE_DIR}/Source
  ${CMAKE_SOURCE_DIR}/NetCore
)

target_include_directories(${TARGET_NAME} PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}/Include/Coral
  ${CMAKE_CURRENT_SOURCE_DIR}/Source
  ${CMAKE_SOURCE_DIR}/NetCore
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