set(TARGET_NAME Coral.Managed)

file(GLOB_RECURSE SRC_FILES CONFIGURE_DEPENDS
  ${CMAKE_CURRENT_SOURCE_DIR}/Source/**.cs
)

add_library(${TARGET_NAME} SHARED ${SRC_FILES})
add_library(CoralManaged ALIAS ${TARGET_NAME})

target_include_directories(${TARGET_NAME} PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}/Source
)

target_compile_options(${TARGET_NAME} PUBLIC "/unsafe")

set_target_properties(
  ${TARGET_NAME} PROPERTIES
  CXX_VISIBILITY_PRESET hidden
  VS_GLOBAL_RootNamespace "Coral.Managed"
  VS_GLOBAL_EnableDynamicLoading "true"
  VS_GLOBAL_ResolveNuGetPackages "true"
  VS_GLOBAL_Nullable "enable"
  VS_GLOBAL_RootNamespace "Coral.Managed"
  VS_PACKAGE_REFERENCES " " # we need this to force nuget restore before build !!!
  VISIBILITY_INLINES_HIDDEN YES
  VERSION "${PROJECT_VERSION}"
  SOVERSION "${PROJECT_VERSION_MAJOR}"
  OUTPUT_NAME ${TARGET_NAME}
  DEBUG_POSTFIX "d"
)